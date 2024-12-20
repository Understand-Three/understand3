---
AIP编号: 29
标题: 29-对等监控服务
作者: joshlind
讨论地址（可选）: https://github.com/aptos-foundation/AIPs/issues/118
状态: 已接受
最后呼叫截止日期（可选）: <mm/dd/yyyy 最后留下反馈和评论的日期>
类型: 信息性
创建日期: 5/3/2023
更新日期（可选）: 5/3/2023
---
# 一、概述

本AIP提议了一项新的“对等监控”服务，该服务在 Aptos 节点上运行，允许节点跟踪、共享和监控对等的信息和行为。该服务旨在：

1. 通过允许组件在传播和接收数据时做出更智能的决策，从而降低节点的延迟和提高性能；

2. 通过允许节点动态绕过故障和不稳定的对等节点，提高运行质量和可靠性；

3. 通过建立节点引导和信息传播（gossip）机制的基础，来提高节点发现和选择的效率。

4. 通过允许节点更好地检测和应对恶意节点和不良行为，提高安全性；

5. 通过收集和导出重要的网络信息，提高网络可观察性。

   

# 二、动机

Aptos区块链由一个去中心化的节点对等网络（例如，验证者和全节点）组成。网络中的对等节点共同工作，以分发信息和复制状态，例如，新交易通过内存池分发给其他对等节点，并且通过状态同步共享新的区块链状态。因此，一个节点的性能和运行质量直接与其对等节点的质量和稳定性相关联。具有慢速、不稳定或行为不端的对等节点的 Aptos 节点将难以提供高质量的服务。 

为了克服这一问题，有必要跟踪和监控对等节点的行为和元数据，以便组件在运行时做出智能决策，并适当地对协议偏差做出反应。例如，当一个节点需要大量数据进行状态同步时，它应该优先考虑那些在发送数据请求时具有最小网络延迟和最高吞吐量的对等节点（以提高性能）。同样，当用户向节点提交交易时，节点应该通过最短路径将交易转发给验证者集（以减少延迟）。

为了实现这一目标，我们提出了一项新的对等监控服务，该服务在所有节点上运行，并持续收集有关对等节点和节点运行的网络上下文的重要信息。这些信息（称为“对等元数据”）可以被节点内的各种组件利用，以做出更智能的决策，更好地容忍故障，响应恶意对等节点的行为，并提高网络可见性。



# 三、对等体监控元数据

在高层次上，对等监控服务收集的元数据可以分为几个不同的类别。我们列出了最初将由本 AIP 针对的类别，但请注意，如果这些被认为有用，未来可能会支持额外的类别：

1. **对等和拓扑元数据**：这包括每个对等节点及其在网络拓扑中的角色的基本信息，例如：
   1. 每个对等节点之间的原始网络延迟；
   2. 对等节点距离验证者的深度；
   3. 对等节点的节点类型和构建信息（例如，git 哈希和版本）；
   4. 每个对等节点之间的峰值和平均吞吐量（由现有流量观察到）；
2. **网络和对等发现元数据**：这包括网络中发现的对等节点及其属性的信息，例如：
   1. 可以被任何人连接的新发现的对等节点；
   2. 提供播种服务的种子式节点，例如，引导服务；
   3. 包含大段区块链数据的归档节点；
   4. 提供高可用性和低延迟数据访问给其他人的配置良好的节点。
3. **系统和组件元数据**：这包括每个对等节点的关键系统和组件信息，例如：
   1. 资源和负载信息（例如，节点可能的工作强度以及它的剩余容量，如CPU、RAM、带宽、网络连接等）；
   2. 存储特定信息，例如最新的同步版本和纪元（帮助组件识别最新的对等节点）；
   3. 网络协议和服务信息，例如对等节点支持的协议和服务，以及对等节点是否能够处理不同的服务请求。



# 四、性能、可靠性和安全性改进

通过在每个节点内持续跟踪和监控对等体元数据，内部组件可以在运行时做出更加智能的决策，从而提高性能、可靠性和安全性。为了清晰起见，我们列举了可以使用上述识别的元数据进行的几项即时改进。我们注意到，这个列表并不完整。

1. **延迟和拓扑感知的状态同步**: 为了提高状态同步的延迟和吞吐量，可以使对等体选择算法更加智能化。例如，Aptos节点可以优先选择以下对等体：(i) 接近的（即，最小的ping时间）；(ii) 距离验证人集最近（因为它们更有可能拥有最新的数据）；(iii) 负载最少的（以帮助减少瓶颈并改善负载均衡）。
2. **存储和拓扑感知的内存池**: 为了改善内存池的延迟和吞吐量，也可以使事务转发逻辑更加智能化。例如，事务可以转发到以下对等体：(i) 到达验证人集的最短路径（以减少传输延迟）；(ii) 拥有最新存储（以确保事务不会被滞后节点错误丢弃）；(iii) 正在进行的负载最少的（以帮助负载均衡）。
3. **智能对等体发现和选择**: 当连接到网络中的其他节点时，网络堆栈可以利用新的元数据做出更加智能的决策，从而改善对等体发现和对等体选择。例如，网络堆栈：(i) 不再需要依赖创世块中的静态对等体信息（这可能已经过时）；(ii) 可以连接到连接良好、靠近验证人集且运行最新代码的对等体，以确保良好的连接性和性能。
4. **故障和恶意对等体管理**: 现在已经有了一个动态对等体发现机制，每个节点内的组件可以自动断开与故障、恶意或无用的对等体的连接，并通知网络堆栈搜索更好、更有帮助的对等体。例如，状态同步可以通知网络堆栈：(i) 一些对等体没有所需的数据，因此应该用具有适当数据的新对等体替换它们；(ii) 与恶意或不良对等体断开连接，并主动阻止一段时间内的重新连接（以避免不良行为）。

通过在每个节点内持续跟踪和监控对等元数据，内部组件可以在运行时做出更智能的决策，从而提高性能、可靠性和安全性。为了清晰起见，我们列出了几个可以立即使用上述识别的元数据进行改进的事项。我们注意到这个列表并不完整。

1. **延迟和拓扑感知的状态同步**：为了提高状态同步的延迟和吞吐量，对等选择算法可以变得更智能。例如，不是使用随机选择，Aptos节点可以优先考虑那些：
   1. 距离近（即最小ping时间）；
   2. 位于验证者集合附近（因为它们更有可能拥有最新的数据）；
   3. 负载最少（以帮助减少瓶颈并改善负载均衡）的对等节点。
2. **存储和拓扑感知的内存池**：为了提高内存池的延迟和吞吐量，交易转发逻辑也可以变得更智能。例如，交易可以转发给对等节点：
   1. 通过到验证者集合的最短路径（以减少传输延迟）；
   2. 拥有最新存储的对等节点（以帮助确保交易不会被滞后的节点错误地丢弃）；
   3. 负载最少的对等节点（以帮助负载均衡）。
3. **智能对等发现和选择**：为了在连接到网络中的其他节点时改进对等发现和对等选择，网络堆栈可以利用新的元数据来做出更智能的决策。例如，网络堆栈：
   1. 不再需要依赖创世区块中的静态对等信息（这可能已经过时）；
   2. 可以连接到连接良好的、更接近验证者集合的、运行最新代码版本的对等节点，以帮助确保良好的连接性和性能。
4. **故障和恶意对等节点管理**：现在有了动态对等发现机制，每个节点内的组件可以自动断开与故障、恶意或无帮助的对等节点的连接，并通知网络堆栈寻找更好、更有帮助的对等节点。例如，状态同步可以通知网络堆栈：
   1. 一些对等节点没有所需的数据，因此应该用拥有适当数据以满足请求的新对等节点来替换它们；
   2. 断开与恶意或不良对等节点的连接，并在一段时间内积极阻止重新连接（以阻止不良行为）。


# 五、参考实现

在 `aptos-core` 代码库中存在一个简单的参考实现。注意：当前的实现只跟踪对等体和拓扑信息。将来将扩展以处理其他类别的信息：

- **对等体监控客户端**: [https://github.com/aptos-labs/aptos-core/tree/main/network/peer-monitoring-service/client](https://github.com/aptos-labs/aptos-core/tree/main/network/peer-monitoring-service/client)
- **对等体监控服务器**: [https://github.com/aptos-labs/aptos-core/tree/main/network/peer-monitoring-service/server](https://github.com/aptos-labs/aptos-core/tree/main/network/peer-monitoring-service/server)
- **对等体监控类型**: [https://github.com/aptos-labs/aptos-core/tree/main/network/peer-monitoring-service/types](https://github.com/aptos-labs/aptos-core/tree/main/network/peer-monitoring-service/types)

# 六、风险和缺点

引入对等监控服务存在一些风险和缺点：

- **隐私问题**：对等监控服务将收集网络中每个节点的更高级别元数据。因此，确保这些元数据不包含可能影响每个节点环境或节点操作员隐私的敏感和/或机密信息，这非常重要。
- **容忍恶意响应**：鉴于去中心化节点对节点网络的无信任性质，对等监控服务能够抵御来自其他对等节点的恶意和/或误导性响应很重要。无法容忍这些响应可能导致多种攻击，例如拒绝服务攻击（DOS）、流量整形和性能攻击。
- **增加的复杂性和资源使用**：与所有优化一样，重要的是理解由于修改而产生的系统复杂性和资源使用增加的权衡。在这种情况下，应该考虑采取措施来管理这种复杂性，并减少任何此类影响。



# 七、未来潜力

对等监控服务提供了许多未来的扩展和改进。例如：

- **额外的元数据类型**：对等监控服务可以扩展以收集节点元数据的其他类别，例如：
  1. 对等声誉和评分，以帮助确保节点积极寻找性能良好和健康的对等节点；
  2. 网络追踪元数据，以帮助工程师和操作员更好地观察和调试端到端行为。
- **性能基准测试**：对等监控服务可以扩展为在我们的测试环境中充当基准测试工具。例如，该服务可以配置为在网络中发送和接收消息（具有可配置的消息大小和频率），以帮助基准测试和监控网络堆栈的性能。
- **实现整合**：对监控服务有各种实现扩展，可以帮助清理和整合Aptos核心代码。例如：
  1. 可以移除专用的节点健康检查器，并由监控服务替换；
  2. 网络堆栈和每个组件之间的应用程序接口可以进一步标准化。



# 八、建议的实施时间表

- (完成) **里程碑1**：实现基本的监控客户端和服务器框架。
- (完成) **里程碑2**：扩展框架以支持对等体和拓扑信息。
- **里程碑3**：更新各种应用程序（例如，状态同步和内存池），以利用对等体和拓扑信息，并公开此信息以供调试使用。
- **里程碑4**：扩展框架以支持对等体发现，并将此信息直接集成到网络堆栈中（例如，在节点连接拨号和启动期间）。
- **里程碑5**：扩展框架以支持系统和组件信息，并将此元数据集成到各种应用程序中。

# 九、建议的部署时间表

- (进行中) **部署步骤1**：实现里程碑1和2，并将它们切入到发布版本 v1.5 中。
- (进行中) **部署步骤2**：实现里程碑3，并将其切入到发布版本 v1.6 中。
- **部署步骤3**：实现并发布里程碑4（待定）。
- **部署步骤4**：实现并发布里程碑5（待定）。

# 十、利益相关者影响

对等体监控服务将影响 Aptos 生态系统中的各种利益相关者。例如：

- **节点操作者**：节点操作者将看到节点性能、可靠性和运营质量的改善。例如：(i) 在状态同步和处理事务时，延迟更低、吞吐量更高；(ii) 在周围网络中直接（或间接）对等体失败时，性能影响较小；(iii) 改进的节点连接性和网络发现；以及 (iv) 改进的网络和对等体可见性。
- **应用程序和客户端**：应用程序和客户端将看到更低的端到端事务延迟，从而有助于改善用户体验。例如：(i) 端到端事务延迟不太受对等体或网络故障的影响；和 (ii) 事务的尾延迟总体较低，从而有助于为提交事务的应用程序和客户端提供更可预测和稳定的体验。

对等监控服务将影响 Aptos 生态系统中的各种利益相关者。例如：

- **节点操作员**：节点操作员将看到改进的节点性能、可靠性和运行质量。例如：
  1. 在状态同步和处理交易时具有更低的延迟和更高的吞吐量；
  2.  当直接（或间接）对等节点在网络周围失败时，性能影响较小；
  3. 改善的节点连通性和网络发现；
  4. 改进的网络和对等可见性。
- **应用程序和客户端**：应用程序和客户端将看到更低的端到端交易延迟，从而帮助改善用户体验。例如：
  1. 端到端交易延迟将受到对等或网络故障的影响较小；
  2. 交易的尾部延迟总体上将更低，从而帮助为提交交易的应用程序和客户端提供更可预测和稳定的经验。
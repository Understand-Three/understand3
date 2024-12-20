---
title: 构建一个 dapp 的方法
draft: true
---
过期
# 前言

接下来这部分是官方代码描述，实际操作可以从 “现在开始”部分跟着写一个 DApp

官方的描述:https://aptos.dev/tutorials/build-e2e-dapp/create-a-smart-contract

## 使用 Create React App 开始

该项目使用 [Create React App](https://github.com/facebook/create-react-app) 启动。

```shell
npx create-react-app my-app
cd my-app
npm start
```

## 可用的脚本

在项目目录中，您可以运行：

### `npm start`

在开发模式下运行应用。
在浏览器中打开 [http://localhost:3000](http://localhost:3000) 查看应用。
如果您进行编辑，页面将会重新加载。
您还可以在控制台看到任何代码纠错（lint）错误。

### `npm test`

以交互式监听模式启动测试运行器。
有关运行测试的更多信息，请参阅 [运行测试](https://facebook.github.io/create-react-app/docs/running-tests) 部分。

### `npm run build`

将应用构建为生产版本，并存放到 `build` 文件夹中。\
它正确地为 React 生产环境打包，并优化构建以获得最佳性能。
构建结果已经压缩，并且文件名中包含哈希值。\
您的应用现在可以部署了！
有关部署的更多信息，请参阅 [部署](https://facebook.github.io/create-react-app/docs/deployment) 部分。

### `npm run eject`

**注意：这是一个单向操作。一旦执行 `eject`，就无法回滚！**
如果您对构建工具和配置选择不满意，您可以随时执行 `eject`。此命令将移除项目中的单一构建依赖。
相反，它会将所有配置文件和传递依赖（webpack，Babel，ESLint 等）直接复制到您的项目中，以便您能够完全控制它们。除了 `eject` 以外的所有命令仍然有效，但它们将指向复制的脚本，以便您可以进行调整。在此阶段，您需要自力更生。
您不必使用 `eject`。精选的功能集适合小型和中等规模的部署，并且您不应该感到有必要使用这个功能。然而我们理解，如果不能在准备好的时候自定义这个工具，这个工具将没有用处。

## 了解更多

您可以在 [Create React App 文档](https://facebook.github.io/create-react-app/docs/getting-started) 中了解更多。
要学习 React，请参阅 [React 文档](https://reactjs.org/)。




# 现在开始

官方的 `todolist` 示例
https://aptos.dev/tutorials/build-e2e-dapp/e2e-dapp-index

我写的是一个 随机抽奖的代码，但是很多部分都不完善
- move 代码基本也是抄的
- 前端的代码有一部分是 GPT 写的

## 少废话，先看效果

存在的问题：主要是 Move 代码处理抽奖的逻辑问题，这部分我暂时没有去写，因为不会，能力有限。

![image-20240323184804872](https://mielgo-markdown.oss-cn-chengdu.aliyuncs.com/image-20240323184804872.png)



## 一、初始化一个 DApp 模版

这里的 `client` 就是根目录的名称

```shell
npx create-react-app client --template typescript
```

> 建议你把我的代码复制到你的文件里，确保可以运行后，再修改一下我代码里的文字或其他的元素，等程序确实出了错之后，去想想为什么会出错。
>
> 祝你好运！

## 二、安装 antd 组件库

```shell
npm i antd@5.1.4
```

更改 `App.tsx` 如下
```tsx
import { Layout, Row, Col } from "antd"; // 顶部导入
return (
  <>
    <Layout>
      <Row align="middle">
        <Col span={10} offset={2}>
          <h1>Our todolist</h1>
        </Col>
        <Col span={12} style={{ textAlign: "right", paddingRight: "200px" }}>
          <h1>Connect Wallet</h1>
        </Col>
      </Row>
    </Layout>
  </>
);
```

## 三、添加 aptos 的钱包适配器支持

### 安装

```shell
# 钱包适配器
npm i @aptos-labs/wallet-adapter-react
# 钱包适配器 antd 组件
npm i @aptos-labs/wallet-adapter-ant-design
```


## 四、安装 petra 的钱包插件

```shell
# petra 钱包适配器插件
npm i petra-plugin-wallet-adapter
```

## 五、在 index.tsx 中添加钱包适配器

```ts
import { PetraWallet } from "petra-plugin-wallet-adapter";  // petra 钱包适配器插件
import { AptosWalletAdapterProvider } from "@aptos-labs/wallet-adapter-react";  // aptos 的钱包适配器 react 组件
```

## 六、添加一个钱包数组

```ts
const wallets = [new PetraWallet()];
```
## 七、添加钱包到 index.tsx 的渲染界面

```tsx
const root = ReactDOM.createRoot(
  document.getElementById('root') as HTMLElement
);
root.render(
  <React.StrictMode>
    <AptosWalletAdapterProvider plugins={wallets} autoConnect={true}>
  		<App />
	</AptosWalletAdapterProvider>
  </React.StrictMode>
);
```




## 八、打开 App.tsx 并添加连接钱包的 UI 组件和 css

```ts
import { WalletSelector } from "@aptos-labs/wallet-adapter-ant-design";
import "@aptos-labs/wallet-adapter-ant-design/dist/index.css";
```



## 九、在 return 中添加钱包选择器

```html
<Col span={12} style={{ textAlign: "right", paddingRight: "200px" }}>
  <WalletSelector />
</Col>
```

> 如果你现在没有 Move 合约，那么现在需要开始写 move 合约，以支持接下来的操作，示例Move合约可以在后面 “Move完整代码” 部分复制。



## 十、与链交互

> 这部分没有 `indexer` 因为我也不会。如果你发现其他的也没有，那是因为我不知道。

### 配置 petra 和aptos



```tsx
import {WalletSelector} from "@aptos-labs/wallet-adapter-ant-design";
import "@aptos-labs/wallet-adapter-ant-design/dist/index.css";
import {Content, Footer} from "antd/es/layout/layout";
import {Aptos,AptosConfig, Network,APTOS_COIN,AccountAddressInput} from "@aptos-labs/ts-sdk"
import {InputTransactionData, useWallet} from "@aptos-labs/wallet-adapter-react";
import { AccountInfo } from '@aptos-labs/wallet-adapter-core';
// 基础配置
    //----------------------
    // 在钱包内获取需要的信息 
		// account 能够获取到账户的信息
		// signAndSubmitTransaction 能够签名和提交交易
    const {account, signAndSubmitTransaction} = useWallet()
    // 实例化 aptos
    const aptosConfig = new AptosConfig({network: Network.DEVNET}); // 开发网
    const aptos = new Aptos(aptosConfig)// 实例化
    //
    // -------------------------
    // 模块地址
    const moduleAddress = "0xd9a2ded3fa92dc9062d381c51530e936376dfddd37611af6aa27e44a7978dda7"
    // const [nowAcount,setNowAccount] = useState()
```



### 从链上获取数据

```tsx
// 获取随机数的方法
const getRandomNum = async () => {
   			// 打印日志
        console.log("获取一个随机数");
   			// 判断用户是否登陆，如果没有登陆后返回一个空的数组
        if(!account) return []; 
   			// 一个交易的数据信息
        const transaction:InputTransactionData = {
            data: {
              	// 方法的地址
                function: `${moduleAddress}::randoom::random_u8`,
              	// 方法的参数
                functionArguments:[]
            }
        }
        try{
          	// 提交这笔交易（执行方法） 
            const response = await signAndSubmitTransaction(transaction);
          	// 我抄的，应该是等交易的 hash，确保执行成功
            await aptos.waitForTransaction({transactionHash:response.hash}); 
          	// 输出随机数的值
            console.log(response.events[1].data.value)
        }catch(error:any){
            console.log(error);
        }
    }

// 抽奖的方法
const handleDraw = async () => {
        console.log("开始抽奖");
        if(!account) return [];
        const transaction:InputTransactionData = {
            data: {
                function: `${moduleAddress}::randoom::pick_winner`, // 这是方法名称
                functionArguments:[]
            }
        }
        try{
            const response = await signAndSubmitTransaction(transaction);
            await aptos.waitForTransaction({transactionHash:response.hash});
            console.log(response)

            if (response.events[3].data.value === account?.address) {
                const winnerName = "您中奖了";
                setWinner(winnerName);
                // setRemainingParticipants(prevParticipants => prevParticipants.filter(name => name !== winnerName));
            } else {
                setWinner("您未中奖");
            }

        }catch(error:any){
            console.log(error);
        }
    }
```



# Move部分

## 一、初始化

> 命令解析详见：https://www.caoyang2002.top/index.php/archives/350/

初始化一个 move 文件夹

```shell
aptos move init --name randoom  
```

初始化一个 devnet 下的 aptos 账户

```shell
aptos init --network devnet
```

# move.toml

```toml
[package]
name = "randoom"
version = "1.0.0"
authors = []

[addresses]
//你自定自定义的名称 = "账户地址"
cccy = "d9a2ded3fa92dc9062d381c51530e936376dfddd37611af6aa27e44a7978dda7"

[dev-addresses]

[dependencies.AptosFramework]
git = "https://github.com/aptos-labs/aptos-core.git"
rev = "devnet" 
subdir = "aptos-move/framework/aptos-framework"

[dev-dependencies]

```

模块源码解析

```move
module <account-address>::<module-name> {

}
```


创建一个返回随机数的模块
```move
module cccy::randoom {

	// event，你可以把他理解成一个监听器，它会监听结构体的变化，并捕获这种变化发送给调用（实例化）它的方法
    #[event]
    struct Event<T> has drop,store{
        value: T
    }

    #[event]
    struct Winner has drop,store{ // 关于能力的解释：https://www.caoyang2002.top/index.php/archives/244/
        value: address
    }

    entry fun random_u8(){
        event::emit(
            Event{
            // randomness 是一个随机（数）的模块，返回一个随机（数），由于它是一个内置的模块，所以它默认具备有 drop/store/copy 能力
            // 正是因为这些默认的 drop 能力，所以它在程序结束的时候就被销毁了，
            // 导致任何希望返回这个值的方法，最终都无法获取到这个随机的值
            // 解决方案就是如上的 #[event]
                value:randomness::u8_integer()
            }
        );
    }
}
```

> 在本地测试`随机模块`的方法：https://www.caoyang2002.top/index.php/archives/383



# 完整代码展示

> 没有使用路由，如果想看路由可以搜“路由”，我记得我写过

# App.tsx

>  里面有很多垃圾代码，秉承着能跑就行的思想，所以我没有改

```tsx
import React, {useEffect, useState} from 'react';
import './App.css';
import {Button, Col, Layout, Row} from 'antd';
import {WalletSelector} from "@aptos-labs/wallet-adapter-ant-design";
import "@aptos-labs/wallet-adapter-ant-design/dist/index.css";
import {Content, Footer} from "antd/es/layout/layout";
import {Aptos,AptosConfig, Network,APTOS_COIN,AccountAddressInput} from "@aptos-labs/ts-sdk"
import {InputTransactionData, useWallet} from "@aptos-labs/wallet-adapter-react";
import { AccountInfo } from '@aptos-labs/wallet-adapter-core';

function App() {
    // 基础配置
    //----------------------
    // 在钱包内获取需要的信息
    const {account, signAndSubmitTransaction} = useWallet()
    // 实例化 aptos
    const aptosConfig = new AptosConfig({network: Network.DEVNET});
    const aptos = new Aptos(aptosConfig)
    //
    // -------------------------
    // 模块地址
    const moduleAddress = "0xd9a2ded3fa92dc9062d381c51530e936376dfddd37611af6aa27e44a7978dda7"
    // const [nowAcount,setNowAccount] = useState()

    // -------------------------

    const [prizes, setPrizes] = useState([]);
    const [selectedPrize, setSelectedPrize] = useState(null);

    const handleAddPrize = () => {
        const newPrize = prompt("请输入奖品名称:");
        if (newPrize) {
            // @ts-ignore
            setPrizes([...prizes, newPrize]);
        }
    };

    const handleSelectPrize = () => {
        const randomIndex = Math.floor(Math.random() * prizes.length);
        setSelectedPrize(prizes[randomIndex]);
    };

    //----------------------------------
    const [nowBalance, setNowBalance] = useState()
    //
    const participants = ["Alice", "Bob", "Charlie", "David", "Eve"];
    const [winner, setWinner] = useState<string | null>(null);
    const [remainingParticipants, setRemainingParticipants] = useState<string[]>([...participants]);
    
    // -----------------
    // 买票
    const  buy_ticket = async () =>{
        console.log("获取一个随机数")
        if(!account) return [];
        const transaction:InputTransactionData = {
            data: {
                function: `${moduleAddress}::randoom::buy_ticket`,
                functionArguments:[]
            }
        }
        try{
            const response = await signAndSubmitTransaction(transaction);
            await aptos.waitForTransaction({transactionHash:response.hash});
        }catch(error:any){
            console.log(error);
        }
    }

    // 获取一个随机数
    const getRandomNum = async () => {
        console.log("获取一个随机数");
        if(!account) return [];
        const transaction:InputTransactionData = {
            data: {
                function: `${moduleAddress}::randoom::random_u8`,
                functionArguments:[]
            }
        }
        try{
            const response = await signAndSubmitTransaction(transaction);
            await aptos.waitForTransaction({transactionHash:response.hash});
            console.log(response.events[1].data.value)
        }catch(error:any){
            console.log(error);
        }
    }
    // 开始抽奖
    const handleDraw = async () => {
        console.log("开始抽奖");
        if(!account) return [];
        const transaction:InputTransactionData = {
            data: {
                function: `${moduleAddress}::randoom::pick_winner`,
                functionArguments:[]
            }
        }
        try{
            const response = await signAndSubmitTransaction(transaction);
            await aptos.waitForTransaction({transactionHash:response.hash});
            console.log(response)

            if (response.events[3].data.value === account?.address) {
                const winnerName = "您中奖了";
                setWinner(winnerName);
                // setRemainingParticipants(prevParticipants => prevParticipants.filter(name => name !== winnerName));
            } else {
                setWinner("您未中奖");
            }

        }catch(error:any){
            console.log(error);
        }


    }
// 获取余额
        const refreshBalance = async () => {
            await fetchBalance(account);
        };

    // 获取余额的方法
    const fetchBalance = async (account: AccountInfo | null) => {
        if(!account)return[];
        console.log("当前的账户地址是：", account?.address)
        try {
            // @ts-ignore
            const resource = await aptos.getAccountCoinAmount({
                accountAddress: account?.address as AccountAddressInput,
                coinType: APTOS_COIN
            })
            const coin = resource / 100000000;
            setNowBalance( coin as any);
            console.log("余额：",coin)
        } catch (error) {
            console.log(error)
        }
    }

    // ----------------
    // 用户地址更新的时候重新渲染
    useEffect(()=>{
        fetchBalance(account);
        // const intervalId = setInterval(() => {
        //     fetchBalance(account);
        // }, 5000); // 每2秒执行一次 fetchBalance
        // 组件卸载时清除定时器
        // return () => clearInterval(intervalId);
    },[account?.address])

    //-------------------------------
  // 一个更改 const 的 hook， 
    const [initialBalance, setInitialBalance] = useState(null);
    const [currentBalance, setCurrentBalance] = useState(null);

  // 这是一个检测变量变化的 hook，后面的 [] 内放你想检测的变量，如果变量变化就会执行 {} 里面的代码
    useEffect(() => {
      // 获取初始余额
        const fetchInitialBalance = async () => {
            try {
                const resource = await aptos.getAccountCoinAmount({
                    accountAddress: account?.address as AccountAddressInput,
                    coinType: APTOS_COIN // 你的币种类型
                });
                const coin = resource / 100000000;
                setInitialBalance(coin as any); // 假设资源单位为 Satoshi
            } catch (error) {
                console.error('获取初始余额失败:', error);
            }
        };

        fetchInitialBalance();
    }, [account?.address]);

    useEffect(() => {
      // 下面部分知识我不清楚怎么实时更新余额的无奈之举，你可能有更好的方法
        const fetchCurrentBalance = async () => {
            try {
                const resource = await aptos.getAccountCoinAmount({
                    accountAddress: account?.address as AccountAddressInput,
                    coinType: APTOS_COIN // 你的币种类型
                });
                const coin = resource / 100000000;
                setCurrentBalance(coin as any); // 假设资源单位为 Satoshi
            } catch (error) {
                console.error('获取当前余额失败:', error);
            }
        };
        const intervalId = setInterval(fetchCurrentBalance, 2000); // 每隔2秒获取一次当前余额
        return () => clearInterval(intervalId);
    }, [account?.address]);

    useEffect(() => {
        if (initialBalance !== null && currentBalance !== null) {
            if (currentBalance > initialBalance) {
              // 这里应该使用 bignumber 库，但是我还有其他作业要做，就没写（好吧，这是借口。）
                console.log('余额增加了: ',currentBalance - initialBalance);
            } else if (currentBalance < initialBalance) {
                console.log('余额减少了: ',currentBalance - initialBalance);
            } else {
                console.log('余额未变化: ',currentBalance - initialBalance);
            }
        }
    }, [initialBalance, currentBalance]);

  return (
    <>
      <Layout>
        <Row align="middle">
          <Col span={10} offset={2}>
            <h1>Random Number</h1>
              {/*<span>*/}
              {/*    <p>当前余额：{nowBalance} APT</p>*/}
              {/*  <Button onClick={refreshBalance}>刷新余额</Button>*/}
              {/*</span>*/}
          </Col>
          <Col span={12} style={{ textAlign: "right", paddingRight: "200px" }}>
            <WalletSelector />
          </Col>
        </Row>
        <Content>
            <Row>
                <Col span={8} offset={2}>
                    <Button
                        onClick={buy_ticket}
                        block
                        type="primary"
                        style={{textAlign:"center"}}
                    >先买票</Button>
                </Col>
                <Col span={4}>
                    <></>
                </Col>
                <Col span={8}>
                    <Button
                        onClick={handleDraw}
                        block
                        type="primary"
                        style={{textAlign:"center"}}
                    >后抽奖</Button>
                </Col>
                {/*<p>aip-41 Move Aips for randomneww generation</p>*/}
            </Row>
            <Row>
                <Col span={8} offset={10}>
                    <h1>
                        {winner && <p>恭喜: {winner}</p>}
                        {!winner && <p>暂无获奖者</p>}
                    </h1>
                </Col>
            </Row>
        </Content>
        <Footer>
            <Col span={8} offset={10}>
            <p>初始余额: {initialBalance}</p>
            <p>当前余额: {currentBalance}</p>
            </Col>
        </Footer>
      </Layout>
    </>
  );
}

export default App;

```





## index.tsx

```tsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import { PetraWallet } from "petra-plugin-wallet-adapter";  // petra 钱包适配器插件
import { AptosWalletAdapterProvider } from "@aptos-labs/wallet-adapter-react";  // aptos 的钱包适配器 react 组件

const wallets = [new PetraWallet()];


const root = ReactDOM.createRoot(

  document.getElementById('root') as HTMLElement
);
root.render(
  <React.StrictMode>
    <AptosWalletAdapterProvider plugins={wallets} autoConnect={true}>
      <App />
    </AptosWalletAdapterProvider>
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();

```



## App.css

```css
.App {
  text-align: center;
}

.prizes {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

.prize {
  border: 1px solid #000;
  padding: 10px;
  margin: 0 5px;
  cursor: pointer;
  transition: border-color 0.3s ease;
}

.prize.selected {
  border-color: red;
}

.App-logo {
  height: 40vmin;
  pointer-events: none;
}

@media (prefers-reduced-motion: no-preference) {
  .App-logo {
    animation: App-logo-spin infinite 20s linear;
  }
}

.App-header {
  background-color: #282c34;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}

.App-link {
  color: #61dafb;
}

@keyframes App-logo-spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

```



## Move 完整代码

> 注：标注中的“函数”和“方法”，意思都是 function

```move
module cccy::randoom{
    use std::signer;
    use std::vector;
    use aptos_std::smart_vector;
    use aptos_std::smart_vector::SmartVector;
    use aptos_framework::aptos_coin::AptosCoin;
    use aptos_framework::coin;
    use aptos_framework::coin::Coin;
    use aptos_framework::event;
    use aptos_framework::randomness;
		// event，你可以把他理解成一个监听器，它会监听结构体的变化，并捕获这种变化发送给调用（实例化）它的方法
    #[event]
    struct Event<T> has drop,store{
        value: T
    }

    #[event]
    struct Winner has drop,store{ // 关于能力的解释：https://www.caoyang2002.top/index.php/archives/244/
        value: address
    }

    entry fun random_u8(){
        event::emit(
            Event{
            // randomness 是一个随机（数）的模块，返回一个随机（数），由于它是一个内置的模块，所以它默认具备有 drop/store/copy 能力
            // 正是因为这些默认的 drop 能力，所以它在程序结束的时候就被销毁了，
            // 导致任何希望返回这个值的方法，最终都无法获取到这个随机的值
            // 解决方案就是如上的 #[event]
                value:randomness::u8_integer()
            }
        );
    }


    // 1. 初始化奖池
    // init_module 是一个特殊的方法名它会在模块第一次被调用的时候执行
    // 在这里，我需要程序真正执行的时候创建一个奖池，但是我不希望每个人来执行我这个合约的时候都创建一个奖池，
    // 所以需要使用 init_module 在最开始的时候创建一个奖池，之后其他人来使用的时候就不必创建奖池了
    fun init_module(caller:&signer){
        move_to(caller,Pools{
        		// 存用户的抽奖票
            titckets_user: smart_vector::empty(),
            // 初始 coin 为零
            coins:coin::zero(),
            // 奖池为关闭
            is_closed:false
        })
    }

    // 定义一个名为“奖池”的结构体，
    
    struct Pools has key {
    		// 保存每个买了抽奖票的用户的地址
    		// SmartVector 的作用就是让插入和查询变得简单高效，还能省钱
    		// 关于它的介绍：https://www.caoyang2002.top/index.php/archives/369
        titckets_user: SmartVector<address>,
        number:vector<u64>,
        coins:Coin<AptosCoin>,
        is_closed:bool
    }

    // 一张奖票的价格
    public fun get_ticket_price():u64{TICKET_PRICE}
    const TICKET_PRICE:u64 = 10_000;

  	// 调用“抽奖方法”的方法
  	// 为了避免“测试-中止”攻击
    entry fun pick_winner() acquires Pools {
        draw_winner();
    }

    // 一个私有的方法，以保证安全
     fun draw_winner() acquires Pools{
     		// 全局借用奖池账户下的奖池
        let pool = borrow_global_mut<Pools>(@cccy);
        // 如果奖池没有开放就中止
        assert!(!pool.is_closed,HAS_CLOSE); // close ?
        // 如果没有人买票就中止
        assert!(!smart_vector::is_empty(&pool.titckets_user),NO_TICKETS); // buy tickets ?
        // 随机选择一个用户地址
        // 先获取一个数字，这个数字最大是 smart_vector 数组的长度，以确保通过元素的索引访问的时候不会越界
        let winner_id = randomness::u64_range(0,smart_vector::length(&pool.titckets_user));
        // 借出这个地址
        let winner = *smart_vector::borrow(&pool.titckets_user,winner_id);
        // 从资金池中取出 coin
        let coins = coin::extract_all(&mut pool.coins);
        // 存入到 winner 所代表的用户地址中
        coin::deposit<AptosCoin>(winner,coins);
        // 由于我没有多余的账户去测试，为了让我唯一的账户可以多次测试，所以注释了以下赋值操作
        // 但是我对这个变量复制的操作不是很理解，不是同一个用户来执行的时候能使用吗？安装我理解的逻辑，它将无法执行。我没有测试。
        // pool.is_closed = true;
        // 如果想返回这个中奖用户的地址值，就用下面的方法
        event::emit(
            Winner{
                value:winner
            }
        );
    }

    const HAS_CLOSE:u64 = 403; // 已关闭
    const NO_TICKETS:u64 = 404; // 没买票

    #[test_only]
    public(friend) fun init_module_test(caller:&signer)  {
        init_module(caller);
    }
}
```

---
title: 拜占庭将军问题
draft: true
---
The Byzantine Generals Problem
LESLIE LAMPORT, ROBERT SHOSTAK, and MARSHALL PEASE
SRI International
Reliable computer systems must handle malfunctioningcomponents that give conflicting information
to different parts of the system. This situation can be expressed abstractly in terms of a group of
generals of the Byzantine army camped with their troops around an enemy city. Communicatingonly
by messenger, the generals must agree upon a common battle plan. However, one or more of them
may be traitors who will try to confuse the others. The problem is to find an algorithm to ensure that
the loyal generals will reach agreement. It is shown that, using only oral messages, this problem is
solvable if and only if more than two-thirds of the generals are loyal; so a single traitor can confound
two loyal generals. With unforgeable written messages, the problem is solvable for any number of
generals and possible traitors. Applications of the solutions to reliable computer systems are then
discussed.
Categories and Subject Descriptors: C.2.4. [Computer-Communication Networks]: Distributed
Systems--network operating systems; D.4.4 [Operating Systems]: CommunicationsManagement--
network communication; D.4.5 [Operating Systems]: Reliability--fault tolerance
General Terms: Algorithms, Reliability
Additional Key Words and Phrases: Interactive consistency
/
1. INTRODUCTION
A r e l i a b l e c o m p u t e r s y s t e m m u s t be a b l e to cope w i t h t h e failure of o n e or m o r e
of its c o m p o n e n t s . A failed c o m p o n e n t m a y e x h i b i t a t y p e of b e h a v i o r t h a t is
o f t e n o v e r l o o k e d - - n a m e l y , s e n d i n g c o n f l i c t i n g i n f o r m a t i o n to d i f f e r e n t p a r t s of
t h e s y s t e m . T h e p r o b l e m of c o p i n g w i t h t h i s t y p e of failure is e x p r e s s e d a b s t r a c t l y
as t h e B y z a n t i n e G e n e r a l s P r o b l e m . W e d e v o t e t h e m a j o r p a r t of t h e p a p e r to a
d i s c u s s i o n of t h i s a b s t r a c t p r o b l e m a n d c o n c l u d e b y i n d i c a t i n g h o w o u r s o l u t i o n s
c a n be u s e d i n i m p l e m e n t i n g a r e l i a b l e c o m p u t e r s y s t e m .
W e i m a g i n e t h a t s e v e r a l d i v i s i o n s of t h e B y z a n t i n e a r m y a r e c a m p e d o u t s i d e
a n e n e m y city, e a c h d i v i s i o n c o m m a n d e d b y its o w n general. T h e g e n e r a l s c a n
c o m m u n i c a t e w i t h o n e a n o t h e r o n l y b y m e s s e n g e r . A f t e r o b s e r v i n g t h e e n e m y ,
t h e y m u s t d e c i d e u p o n a c o m m o n p l a n of a c t i o n . H o w e v e r , s o m e of t h e g e n e r a l s
This research was supported in part by the National Aeronautics and Space Administration under
contract NAS1-15428 Mod. 3, the Ballistic Missile Defense Systems Command under contract
DASG60-78-C-0046, and the Army Research Office under contract DAAG29-79-C-0102.
Authors' address: Computer Science Laboratory, SRI International, 333 Ravenswood Avenue, Menlo
Park, CA 94025.
Permission to copy without fee all or part of this material is granted provided that the copies are not
made or distributed for direct commercial advantage, the ACM copyright notice and the title of the
publication and its date appear, and notice is given that copying is by permission of the Association
for Computing Machinery. To copy otherwise, or to republish, requires a fee and/or specific
permission.
© 1982 ACM 0164-0925/82/0700-0382 $00.75
ACM Transactionson ProgrammingLanguagesand Systems,Vol.4, No. 3, July 1982,Pages 382-401.
The Byzantine Generals Problem 383
may be traitors, trying to prevent the loyal generals from reaching agreement.
The generals must have an algorithm to guarantee that
A. All loyal generals decide upon the same plan of action.
The loyal generals will all do what the algorithm says they should, but the
traitors may do anything they wish. The algorithm must guarantee condition A
regardless of what the traitors do.
The loyal generals should not only reach agreement, but should agree upon a
reasonable plan. We therefore also want to insure that
B. A small number of traitors cannot cause the loyal generals to adopt a bad
plan.
Condition B is hard to formalize, since it requires saying precisely what a bad
plan is, and we do not attempt to do so. Instead, we consider how the generals
reach a decision. Each general observes the enemy and communicates his obser-
vations to the others. Let v(i) be the information communicated by the ith
general. Each general uses some method for combining the values v (1) . . . . . v (n)
into a single plan of action, where n is the number of generals. Condition A is
achieved by having all generals use the same method for combining the infor-
mation, and Condition B is achieved by using a robust method. For example, if
the only decision to be made is whether to attack or retreat, then v(i) con be
General i's opinion of which option is best, and the final decision can be based
upon a majority vote among them. A small number of traitors can affect the
decision only if the loyal generals were almost equally divided between the two
possibilities, in which case neither decision could be called bad.
While this approach may not be the only way to satisfy conditions A and B, it
is the only one we know of. It assumes a method by which the generals
communicate their values v (i) to one another. The obvious method is for the ith
general to send v (i) by messenger to each other general. However, this does not
work, because satisfying condition A requires that every loyal general obtain the
same values v(1) . . . . . v(n), and a traitorous general may send different values to
different generals. For condition A to be satisfied, the following must be true:
1. Every loyal general must obtain the same information v (1) . . . . , v (n).
Condition 1 implies that a general cannot necessarily use a value of v(i)
obtained directly from the ith general, since a traitorous ith general may send
different values to different generals. This means that unless we are careful, in
meeting condition 1 we might introduce the possibility that the generals use a
value of v (i) different from the one sent by the ith general--even though the ith
general is loyal. We must not allow this to happen if condition B is to be met. For
example, we cannot permit a few traitors to cause the loya~ generals to base their
decision upon the values " r e t r e a t " , . . . , "retreat" if every loyal general sent the
value "attack". We therefore have the following requirement for each i:
2. If the ith general is loyal, then the value that he sends must be used by every
loyal general as the value of v (i).
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
384 L. Lamport, R. Shostak, and M. Pease
We can rewrite condition I as the condition that for every i (whether or not the
ith general is loyal),
1'. Any two loyal generals use the same value of v(i).
Conditions 1' and 2 are both conditions on the single value sent by the ith
general. We can therefore restrict our consideration to the problem of how a
single general sends his value to the others. We phrase this in terms of a
commanding general sending an order to his lieutenants, obtaining the following
problem.
Byzantine Generals Problem. A commanding general must send an order to
his n - 1 lieutenant generals such that
IC1. All loyal lieutenants obey the same order.
IC2. If the commanding general is loyal, then every loyal lieutenant obeys the
order he sends.
Conditions IC1 and IC2 are called the interactive consistency conditions. Note
that if the commander is loyal, then IC1 follows from IC2. However, the com-
mander need not be loyal.
To solve our original problem, the ith general sends his value of v(i) by using
a solution to the Byzantine Generals Problem to send the order "use v (i) as my
value", with the other generals acting as the lieutenants.
2. IMPOSSIBILITY RESULTS
T h e Byzantine Generals Problem seems deceptively simple. Its difficulty is
indicated by the surprising fact that if the generals can send only oral messages,
then no solution will work unless more than two-thirds of the generals are loyal.
In particular, with only three generals, no solution can work in the presence of a
single traitor. An oral message is one whose contents are completely under the
control of the sender, so a traitorous sender can transmit any possible message.
Such a message corresponds to the type of message that computers normally
send to one another. In Section 4 we consider signed, written messages, for which
this is not true.
We now show that with oral messages no solution for three generals can handle
a single traitor. For simplicity, we consider the case in which the only possible
decisions are "attack" or "retreat". Let us first examine the scenario pictured in
Figure 1 in which the commander is loyal and sends an "attack" order, but
Lieutenant 2 is a traitor and reports to Lieutenant 1 that he received a "retreat"
order. For IC2 to be satisfied, Lieutenant 1 must obey the order to attack.
Now consider another scenario, shown in Figure 2, in which the commander is
a traitor and sends an "attack" order to Lieutenant 1 and a "retreat" order to
Lieutenant 2. Lieutenant 1 does not know who the traitor is, and he cannot tell
what message the commander actually sent to Lieutenant 2. Hence, the scenarios
in these two pictures appear exactly the same to Lieutenant 1. If the traitor lies
consistently, then there is no way for Lieutenant 1 to distinguish between these
two situations, so he must obey the "attack" order in both of them. Hence,
whenever Lieutenant 1 receives an "attack" order from the commander, he must
obey it.
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
The Byzantine Generals Problem 385
f , , t ,
"he said 'retreat'"
Fig. 1. Lieutenant 2 a traitor.
y/ "he said 'retreat'"
Fig. 2. T h e c o m m a n d e r a traitor.
However, a similar argument shows that if Lieutenant 2 receives a "retreat"
order from the commander then he must obey it even if Lieutenant 1 tells him
that the commander said "attack". Therefore, in the scenario of Figure 2,
Lieutenant 2 must obey the "retreat" order while Lieutenant 1 obeys the "attack"
order, thereby violating condition IC1. Hence, no solution exists for three generals
that works in the presence of a single traitor.
This argument may appear convincing, but we strongly advise the reader to be
very suspicious of such nonrigorous reasoning. Although this result is indeed
correct, we have seen equally plausible "proofs" of invalid results. We know of no
area in computer science or mathematics in which informal reasoning is more
likely to lead to errors than in the study of this type of algorithm. For a rigorous
proof of the impossibility of a three-general solution that can handle a single
traitor, we refer the reader to [3].
Using this result, we can show that no solution with fewer than 3m + 1 generals
can cope with m traitorsJ The proof is by contradiction--we assume such a
' More precisely, no such solution exists for three or more generals, since the problem is trivial for two
generals.
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
386 L. Lamport, R. Shostak, and M. Pease
solution for a group of 3m or fewer and use it to construct a three-general solution
to the Byzantine Generals Problem that works with one traitor, which we know
to be impossible. To avoid confusion between the two algorithms, we call the
generals of the assumed solution Albanian generals, and those of the constructed
solution Byzantine generals. Thus, starting from an algorithm that allows 3m or
fewer Albanian generals to cope with m traitors, we construct a solution that
allows three Byzantine generals to handle a single traitor.
The three-general solution is obtained by having each of the Byzantine generals
simulate approximately one-third of the Albanian generals, so that each Byzan-
tine general is simulating at most m Albanian generals. The Byzantine com-
mander simulates the Albanian commander plus at most m - 1 Albanian
lieutenants, and each of the two Byzantine lieutenants simulates at most m
Albanian lieutenants. Since only one Byzantine general can be a traitor, and he
simulates at most m Albanians, at most m of the Albanian generals are traitors.
Hence, the assumed solution guarantees that IC1 and IC2 hold for the Albanian
generals. By IC1, all the Albanian lieutenants being simulated by a loyal Byzan-
tine lieutenant obey the same order, which is the order he is to obey. It is easy to
check that conditions IC1 and IC2 of the Albanian generals solution imply the
corresponding conditions for the Byzantine generals, so we have constructed the
required impossible solution.
One might think that the difficulty in solving the Byzantine Generals Problem
stems from the requirement of reaching exact agreement. We now demonstrate
that this is not the case by showing that reaching approximate agreement is just
as hard as reaching exact agreement. Let us assume that instead of trying to agree
on a precise battle plan, the generals must agree only upon an approximate time
of attack. More precisely, we assume that the commander orders the time of the
attack, and we require the following two conditions to hold:
IC1 '. All loyal lieutenants attack within 10 minutes of one another.
IC2'. If the commanding general is loyal, then every loyal lieutenant attacks
within 10 minutes of the time given in the commander's order.
(We assume that the orders are given and processed the day before the attack
and that the time at which an order is received is irrelevant--only the attack
time given in the order matters.}
Like the Byzantine Generals Problem, this problem is unsolvable unless more
than two-thirds of the generals are loyal. We prove this by first showing that if
there were a solution for three generals that coped with one traitor, then we could
construct a three-general solution to the Byzantine Generals Problem that also
worked in the presence of one traitor. Suppose the commander wishes to send an
"attack" or "retreat" order. He orders an attack by sending an attack time of 1:00
and orders a retreat by sending an attack time of 2:00, using the assumed
algorithm. Each lieutenant uses the following procedure to obtain his order.
(1) After receiving the attack time from the commander, a lieutenant does one
of the following:
(a) If the time is 1:10 or earlier, then attack.
(b) If the time is 1:50 or later, then retreat.
(c) Otherwise, continue to step (2).
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
The Byzantine Generals Problem • 387
(2) Ask the other lieutenant what decision he reached in step (1).
(a) If the other lieutenant reached a decision, then make the same decision
he did.
(b) Otherwise, retreat.
It follows from IC2' that if the commander is loyal, then a loyal lieutenant will
obtain the correct order in step (1), so IC2 is satisfied. If the commander is loyal,
then IC1 follows from IC2, so we need only prove IC1 under the assumption that
the commander is a traitor. Since there is at most one traitor, this means that
both lieutenants are loyal. It follows from I C I ' that if one lieutenant decides to
attack in step (1), then the other cannot decide to retreat in step (1). Hence,
either they will both come to the same decision in step (1) or at least one of them
will defer his decision until step (2). In this case, it is easy to see that they both
arrive at the same decision, so IC1 is satisfied. We have therefore constructed a
three-general solution to the Byzantine Generals Problem that handles one
traitor, which is impossible. Hence, we cannot have a three-general algorithm
that maintains I C I ' and IC2' in the presence of a traitor.
The method of having one general simulate m others can now be used to prove
that no solution with fewer than 3rn + 1 generals can cope with m traitors. The
proof is similar to the one for the original Byzantine Generals Problem and is left
to the reader.
3. A SOLUTION WITH ORAL MESSAGES
We showed above that for a solution to the Byzantine Generals Problem using
oral messages to cope with rn traitors, there must be at least 3m + 1 generals. We
now give a solution that works for 3m + 1 or more generals. However, we first
specify exactly what we mean by "oral messages". Each general is supposed to
execute some algorithm that involves sending messages to the other generals, and
we assume that a loyal general correctly executes his algorithm. The definition of
an oral message is embodied in the following assumptions which we make for the
generals' message system:
A1. Every message that is sent is delivered correctly.
A2. The receiver of a message knows who sent it.
A3. The absence of a message can be detected.
Assumptions A1 and A2 prevent a traitor from interfering with the communi-
cation between two other generals, since by A1 he cannot interfere with the
messages they do send, and by A2 he cannot confuse their intercourse by
introducing spurious messages. Assumption A3 will foil a traitor who tries to
prevent a decision by simply not sending messages. The practical implementation
of these assumptions is discussed in Section 6.
The algorithms in this section and in the following one require that each
general be able to send messages directly to every other general. In Section 5, we
describe algorithms which do not have this requirement.
A traitorous commander may decide not to send any order. Since the lieuten-
ants must obey some order, they need some default order to obey in this case. We
let R E T R E A T be this default order.
ACM Transactions on Progranuning Languages and Systems, Vol. 4, No. 3, July 1982.
388 L. Lamport, R. Shostak, and M. Pease
We inductively define the Oral Message algorithms OM(m), for all nonnegative
integers m, by which a c o m m a n d e r sends an order to n - 1 lieutenants. We show
t h a t OM(m) solves the Byzantine Generals P r o b l e m for 3m + 1 or more generals
in the presence of at most m traitors. We find it more convenient to describe this
algorithm in terms of the lieutenants "obtaining a value" rather t h a n "obeying an
order".
T h e algorithm assumes a function m a j o r i t y with the property t h a t if a majority
of the values vi equal v, then m a j o r i t y (Vl,.. •, v,-D equals v. (Actually, it assumes
a sequence of such f u n c t i o n s - - o n e for each n.) T h e r e are two natural choices for
the value of m a j o r i t y ( v 1 , . . . , v,-1):
1. T h e majority value a m o n g the vi if it exists, otherwise the value R E T R E A T ;
2. T h e median of the vi, assuming t h a t t h e y come from an ordered set.
T h e following algorithm requires only the aforementioned property of m a j o r i t y .
Algorithm OM(0).
(1) The commander sends his value to every lieutenant.
(2) Each lieutenant uses the value he receives from the commander, or uses the value
RETREAT if he receives no value.
Algorithm O M ( m ) , m > O.
(1) The commander sends his value to every lieutenant.
(2) For each i, let vi be the value Lieutenant i receives from the commander, or else be
RETREAT if he re :eives no value. Lieutenant i acts as the commander in Algorithm
OM(m - 1) to send the value vi to each of the n - 2 other lieutenants.
(3) For each i, and each j ~ i, let vj be the value Lieutenant i received from Lieutenant j
in step (2) (using Algorithm OM(m - 1)), or else RETREAT if he received no such
value. Lieutenant i uses the value majority (vl . . . . . v,-1 ).
T o u n d e r s t a n d how this algorithm works, we consider the case m = 1, n = 4.
Figure 3 illustrates the messages received by Lieutenant 2 when the c o m m a n d e r
sends the value v and L i e u t e n a n t 3 is a traitor. In the first step of OM(1), the
c o m m a n d e r sends v to all three lieutenants. I n the second step, L i e u t e n a n t 1
sends the value v to L i e u t e n a n t 2, using the trivial algorithm OM(0). Also in the
second step, the traitorous L i e u t e n a n t 3 sends L i e u t e n a n t 2 some other value x.
In step 3, L i e u t e n a n t 2 t h e n has v~ = v2 = v and v3 = x, so he obtains the correct
value v = m a j o r i t y ( v , v, x ) .
Next, we see w h a t h a p p e n s if the c o m m a n d e r is a traitor. Figure 4 shows the
values received by the lieutenants if a traitorous c o m m a n d e r sends three arbitrary
values x, y, and z to the three lieutenants. E a c h lieutenant obtains v~ = x, v2 = y,
and v3 = z, so t h e y all obtain the same value m a j o r i t y ( x , y, z ) in step (3),
regardless of w h e t h e r or not a n y of the three values x, y, and z are equal.
T h e recursive algorithm OM(m) invokes n - 1 separate executions of the
algorithm O M ( m - 1), each of which invokes n - 2 executions of OM(m - 2), etc.
This m e a n s that, for m > 1, a lieutenant sends m a n y separate messages to each
other lieutenant. T h e r e m u s t be some way to distinguish among these different
messages. T h e reader can verify t h a t all ambiguity is r e m o v e d if each lieutenant
i prefixes the n u m b e r i to the value vi t h a t he sends in step (2). As the recursion
"unfolds," the algorithm O M ( m - k) will be called (n - 1) . . . (n - k) times to
send a value prefixed by a sequence of k lieutenants' numbers.
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
/
a~
c~
p~
~JD
co O
.~'~
Z ~
v~
©
390 L. Lamport, R. Shostak, and M. Pease
T o prove the correctness of the algorithm OM{m) for a r b i t r a r y m, we first
p r o v e the following l e m m a .
LEMMA 1. F o r a n y m a n d k, A l g o r i t h m O M (m ) satisfies IC2 if there are more
t h a n 2k + m g e n e r a l s a n d at m o s t k traitors.
PROOF. T h e p r o o f is b y induction on m. IC2 only specifies w h a t m u s t h a p p e n
if the c o m m a n d e r is loyal. Using A1, it is easy to see t h a t the trivial algorithm
OM(0) works if the c o m m a n d e r is loyal, so the l e m m a is true for m = 0. We now
a s s u m e it is true for m - 1, m > 0, a n d p r o v e it for m.
In step (1), the loyal c o m m a n d e r sends a value v to all n - 1 lieutenants. In
step (2), each loyal lieutenant applies O M ( m - 1) with n - 1 generals. Since b y
h y p o t h e s i s n > 2k + m, we h a v e n - 1 > 2k + (m - 1), so we can a p p l y the
induction hypothesis to conclude t h a t every loyal lieutenant gets vj = v for each
loyal L i e u t e n a n t j. Since there are at m o s t k traitors, and n - 1 > 2k + (m - 1)
_> 2k, a m a j o r i t y of the n - 1 lieutenants are loyal. Hence, each loyal lieutenant
h a s vi = v for a m a j o r i t y of the n - 1 values i, so he obtains majority(v1 . . . . ,
v,-1) = v in step (3), proving IC2. []
T h e following t h e o r e m asserts t h a t Algorithm O M ( m ) solves the Byzantine
Generals Problem.
THEOREM 1. F o r a n y m, A l g o r i t h m O M (m ) satisfies conditions IC1 a n d IC2
i f there are m o r e t h a n 3m g e n e r a l s a n d at m o s t m traitors.
PROOF. T h e p r o o f is b y induction on m. I f there are no traitors, t h e n it is easy
to see t h a t OM(0) satisfies IC1 and IC2. W e therefore a s s u m e t h a t the t h e o r e m
is true for O M ( m - 1) a n d p r o v e it for O M ( m ) , m > 0.
W e first consider the case in which the c o m m a n d e r is loyal. B y taking k equal
to m in L e m m a 1, we see t h a t O M ( m ) satisfies IC2. IC1 follows f r o m IC2 if the
c o m m a n d e r is loyal, so we need only verify IC1 in the case t h a t the c o m m a n d e r
is a traitor.
T h e r e are at m o s t m traitors, and the c o m m a n d e r is one of them, so at m o s t
m - 1 of the lieutenants are traitors. Since t h e r e are m o r e t h a n 3m generals,
t h e r e are m o r e t h a n 3m - 1 lieutenants, and 3m - 1 > 3(m - 1). W e m a y
therefore a p p l y the induction h y p o t h e s i s to conclude t h a t O M ( m - 1) satisfies
conditions IC1 and IC2. Hence, f o r each j, a n y two loyal lieutenants get the s a m e
value for vj in step (3). (This follows f r o m IC2 if one of the two lieutenants is
L i e u t e n a n t j, a n d f r o m IC1 Otherwise.) Hence, a n y two loyal lieutenants get the
s a m e vector of values vl . . . . . Vn-~, and therefore obtain the s a m e value major-
ity(vl . . . . . Vn-1) in step (3), proving IC1. []
4. A SOLUTION WITH SIGNED MESSAGES
As we saw f r o m the scenario of Figures i and 2, it is the traitors' ability to lie t h a t
m a k e s the Byzantine Generals P r o b l e m so difficult. T h e p r o b l e m b e c o m e s easier
to solve if we can restrict t h a t ability. One w a y to do this is to allow the generals
to send unforgeable signed messages. M o r e precisely, we add to A1-A3 the
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
The Byzantine Generals Problem 391
following assumption:
A4 (a) A loyal general's signature cannot be forged, and any alteration of the
contents of his signed messages can be detected.
(b) Anyone can verify the authenticity of a general's signature.
N o t e t h a t we make no assumptions about a traitorous general's signature. In
particular, we allow his signature to be forged by a n o t h e r traitor, t h e r e b y
permitting collusion among the traitors.
Now t h a t we have introduced signed messages, our previous argument t h a t
four generals are required to cope with one traitor no longer holds. In fact, a
three-general solution does exist. We now give an algorithm t h a t copes with m
traitors for any n u m b e r of generals. (The problem is vacuous if there are fewer
t h a n m + 2 generals.)
In our algorithm, the c o m m a n d e r sends a signed order to each of his lieutenants.
E a c h lieutenant t h e n adds his signature to t h a t order and sends it to the other
lieutenants, who add their signatures and send it to others, and so on. This means
t h a t a lieutenant must effectively receive one signed message, make several copies
of it, and sign and send those copies. It does not m a t t e r how these copies are
obtained; a single message might be photocopied, or else each message might
consist of a stack of identical messages which are signed and distributed as
required.
Our algorithm assumes a function choice which is applied to a set of orders to
/obtain a single one. T h e only requirements we make for this function are
/
1. If the set V consists of the single element v, t h e n c h o i c e ( V ) = v.
2. choice(Q) = R E T R E A T , where O is the e m p t y set.
N o t e t h a t one possible definition is to let c h o i c e ( V ) be the median element of
V--assuming t h a t there is an ordering of the elements.
In the following algorithm, we let x : i denote the value x signed by General i.
Thus, v :j: i denotes the value v signed by j, and t h e n t h a t value v :j signed by i.
We let General 0 be the commander. In this algorithm, each lieutenant i maintains
a set Vi, containng the set of properly signed orders he has received so far. (If the
c o m m a n d e r is loyal, t h e n this set should never contain more t h a n a single
element.) Do not confuse Vi, the set of orders he has received, with the set of
messages t h a t he has received. T h e r e m a y be m a n y different messages with the
same order.
Algorithm S M (rn).
Initially Vi = 0.
(1) The commander signs and sends his value to every lieutenant.
(2) For each i:
(A) If Lieutenant i receives a message of the form v: 0 from the commander and he
has not yet received any order, then
(i) he lets V/equal (v);
(ii) he sends the message v: 0 : i to every other lieutenant.
A C M Transactions on P r o g r a m m i n g Languages and Systems, Vol. 4, No. 3, July 1982.
392 • L. Lamport, R. Shostak, and M. Pease
~ ' : 0
" a t t a c k " : 0 : 1
" r e t r e a t " : 0 : 2
Fig. 5. Algorithm SM(1); the c o m m a n d e r a traitor.
(B) If Lieutenant i receives a message of the form v : 0 :jl : -.. : Jk and v is not in the set
Vi, then
(i) he adds v to Vi;
(ii) if k < m, then he sends the message v:0 :jl : - . . :jk : i to every lieutenant other
than jl . . . . . jk.
(3) For each i: When Lieutenant i will receive no more messages, he obeys the order
choice( Vi).
N o t e t h a t in step (2), L i e u t e n a n t i ignores a n y message containing an order v t h a t
is already in the set Vi.
We have not specified how a lieutenant determines in step (3) t h a t he will
receive no more messages. B y induction on k, one easily shows t h a t for each
sequence of lieutenants j l , • • •, jk with k __ m, a lieutenant can receive at m o s t
one message of the form v : 0 : j l : . . . :jk in step (2). If we require t h a t L i e u t e n a n t
Jk either send such a message or else send a message reporting t h a t he will not
send such a message, t h e n it is easy to decide w h e n all messages have been
received. (By a s s u m p t i o n A3, a lieutenant can determine if a traitorous lieutenant
jk sends neither of those two messages.) Alternatively, time-out can be used to
determine w h e n no more messages will arrive. T h e use of time-out is discussed in
Section 6.
N o t e t h a t in step (2), L i e u t e n a n t i ignores a n y messages t h a t do not have the
proper form of a value followed by a string of signatures. If packets of identical
messages are used to avoid having to copy messages, this m e a n s t h a t he throws
away a n y packet t h a t does n o t consist of a sufficient n u m b e r of identical, properly
signed messages. (There should be (n - k - 2)(n - k - 3) . . - (n - m - 2) copies
of the message if it has been signed by k lieutenants.)
Figure 5 illustrates Algorithm SM(1) for the case of three generals when the
c o m m a n d e r is a traitor. T h e c o m m a n d e r sends an " a t t a c k " order to one lieutenant
and a " r e t r e a t " order to the other. B o t h lieutenants receive the two orders in step
(2), so after step (2) V1 -- V2 ffi {"attack", "retreat"}, and t h e y both obey the
order choice{ {"attack", "retreat"} ). Observe t h a t here, unlike the situation in
Figure 2, the lieutenants know the c o m m a n d e r is a traitor because his signature
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
The Byzantine Generals Problem • 393
appears on two different orders, and A4 states t h a t only he could have generated
those signatures.
In Algorithm SM(m), a lieutenant signs his name to acknowledge his receipt of
an order. If he is the ruth lieutenant to add his signature to the order, then t h a t
signature is not relayed to anyone else by its recipient, so it is superfluous. (More
precisely, assumption A2 makes it unnecessary.) In particular, the lieutenants
need not sign their messages in SM(1).
We now prove the correctness of our algorithm.
THEOREM 2. For any m, Algorithm S M ( m ) solves the Byzantine Generals
Problem if there are at most m traitors.
PROOF. We first prove IC2. If the c o m m a n d e r is loyal, t h e n he sends his signed
order v: 0 to every lieutenant in step (1). E v e r y loyal lieutenant will therefore
receive the order v in step (2)(A). Moreover, since no traitorous lieutenant can
forge any other message of the form v' :0, a loyal lieutenant can receive no
additional order in step (2)(B). Hence, for each loyal L i e u t e n a n t i, the set Vi
obtained in step (2) consists of the single order v, which he will obey in step (3)
by p r o p e r t y 1 of the choice function. This proves IC2.
Since IC1 follows from IC2 if the c o m m a n d e r is loyal, to prove IC1 we need
only consider the case in which the c o m m a n d e r is a traitor. Two loyal lieutenants
i and j obey the same order in step (3) if the sets of orders Vi and Vj t h a t they
receive in step (2) are the same. Therefore, to prove IC1 it suffices to prove that,
if i puts an order v into Vi in step (2), t h e n j must put the same order v into V1 in
step (2). T o do this, we must show t h a t j receives a properly signed message
containing t h a t order. If i receives the order v in step (2)(A), t h e n he sends it to
j in step (2)(A)(ii); s o j receives it (by A1). If i adds the order to Vi in step (2)(B),
t h e n he must receive a first message of the form v : 0 : jl : . . . : j~. I f j is one of the
fl, t h e n by A4 he must already have received the order v. If not, we consider two
cases:
1. k < m. In this case, i sends the message v : 0 : j l : . . . :jk:i to j; s o j must
receive the order v.
2. k = m. Since the c o m m a n d e r is a traitor, at most m - 1 of the lieutenants
are traitors. Hence, at least one of the lieutenants jl . . . . , jm is loyal. This loyal
lieutenant must have sent j the value v when he first received it, so j must
therefore receive t h a t value.
This completes the proof. []
5. MISSING C O M M U N I C A T I O N P A T H S
T h u s far, we have assumed t h a t a general can send messages directly to every
other general. We now remove this assumption. Instead, we suppose t h a t physical
barriers place some restrictions on who can send messages to whom. We consider
the generals to form the nodes of a simple, 2 finite undirected graph G, where an
arc between two nodes indicates t h a t those two generals can send messages
2 A s i m p l e g r a p h is one in which t h e r e is at m o s t one arc joining a n y two nodes, and every arc connects
two d i s t i n c t nodes.
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
394 L. Lamport, R. Shostak, and M. Pease
f
J
Fig. 6. A 3-regular graph. Fig. 7. A graph that is not 3-regular.
directly to one another. W e now extend Algorithms O M ( m ) and SM(m), which
a s s u m e d G to be completely connected, to m o r e general graphs.
T o extend our oral message algorithm OM(m), we need the following definition,
where two generals are said to be neighbors if t h e y are joined b y an arc.
Definition 1.
(a) A set of nodes (il, . . . , ip} is said to be a regular set of neighbors of a node
/ i f
(i) each ij is a neighbor of i, and
(ii) for a n y general k different f r o m i, there exist p a t h s yj,k f r o m ij to k not passing
t h r o u g h i such t h a t a n y two different p a t h s Yi,k h a v e no node in c o m m o n
o t h e r t h a n k.
(b) T h e g r a p h G is said to be p-regular if every node h a s a regular set of
neighbors consisting o f p distinct nodes.
Figure 6 shows a n e x a m p l e of a simple 3-regular graph. Figure 7 shows an
e x a m p l e of a g r a p h t h a t is not 3-regular because the central node h a s no regular
set of neighbors containing three nodes.
W e extend O M ( m ) to an algorithm t h a t solves the Byzantine Generals P r o b l e m
in the presence of rn traitors if the g r a p h G of generals is 3m-regular. (Note t h a t
a 3m-regular g r a p h m u s t contain at least 3m + 1 nodes.} For allpositive integers
m and p, we define the algorithm OM(m, p) as follows w h e n the g r a p h G of
generals isp-regular. ( O M ( m , p ) is not defined if G is notp-regular.) T h e definition
uses induction on m.
Algorithm OM (rn, p).
(0) Choose a regular set N of neighbors of the commander consisting o f p lieutenants.
(1) The commander sends his value to every lieutenant in N.
(2) For each i in N, let vi be the value Lieutenant i receives from the commander, or else
R E T R E A T if he receives no value. Lieutenant i sends vi to every other lieutenant k as
follows:
(A) If m = 1, then by sending the value along the path yi,k whose existence is
guaranteed by part (a) (ii) of Definition 1.
(B) If rn > 1, then by acting as the commander in the algorithm OM(m - 1, p - 1),
with the graph of generals obtained by removing the original commander from G.
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
The Byzantine Generals Problem 395
(3) For each k, and each i in N with i ~ k, let vi be the value Lieutenant k received from
Lieutenant i in step (2), or RETREAT if he received no value. Lieutenant k uses the
value majority(vi . . . . . . vi,), where N = {il. . . . . ip}.
Note t h a t removing a single node from a p-regular graph leaves a (p - 1)-
regular graph. Hence, one can apply the algorithm OM(m - 1, p - 1) in step
(2)(B).
We now prove t h a t OM(m, 3m) solves the Byzantine Generals Problem if there
are at most m traitors. T h e proof is similar to the proof for the algorithm OM(m)
and will just be sketched. It begins with the following extension of L e m m a 1.
LEMMA 2. F o r any m > 0 a n d a n y p >_ 2k + m, A l g o r i t h m O M (m, p) satisfies
IC2 i f there are at m o s t k traitors.
PROOF. For m -- 1, observe t h a t a lieutenant obtains the value majority(v1,
. . . , vp), where each vi is a value sent to him by the c o m m a n d e r along a p a t h
disjoint from the p a t h used to send the other values to him. Since there are at
most k traitors and p __ 2k + 1, more t h a n half of those paths are composed
entirely of loyal lieutenants. Hence, if the c o m m a n d e r is loyal, t h e n a majority of
the values vi will equal the value he sent, which implies that IC2 is satisfied.
Now assume the lemma for m - 1, m > 1. If the c o m m a n d e r is loyal, t h e n each
of the p lieutenants in N gets the correct value. Since p > 2k, a majority of t h e m
are loyal, and by the induction hypothesis each of t h e m sends the correct value
to every loyal lieutenant. Hence, each loyal lieutenant gets a majority of correct
values, t h e r e b y obtaining the correct value in step (3). []
T h e correctness of Algorithm OM(m, 3m) is an immediate consequence of the
following result.
THEOREM 3. F o r a n y m > 0 a n d a n y p >_ 3m, A l g o r i t h m O M ( m , p) solves the
B y z a n t i n e Generals P r o b l e m i f there are at m o s t m traitors.
PROOF. B y L e m m a 2, letting k = m, we see t h a t OM(m, p ) satisfies IC2. If the
c o m m a n d e r is loyal, t h e n IC1 follows from IC2, so we need only prove IC1 under
the assumption t h a t the c o m m a n d e r is a traitor. T o do this, we prove t h a t every
loyal lieutenant gets the same set of values vi in step (3). If m = 1, t h e n this
follows because all the lieutenants, including those in N, are loyal and the paths
~/i,k do not pass through the commander. For m > 1, a simple induction argument
can be applied, s i n c e p _ 3m implies t h a t p - 1 _ 3(m - 1). []
Our extension of Algorithm OM(m) requires t h a t the graph G be 3m-regular,
which is a r a t h e r strong connectivity hypothesis. 3 In fact, if there are only 3m +
1 generals (the m i n i m u m n u m b e r required), t h e n 3m-regularity means complete
connectivity, and Algorithm OM(m, 3m) reduces to Algorithm OM(m). In con-
trast, Algorithm SM(m) is easily extended to allow the weakest possible connec-
tivity hypothesis. Let us first consider how m u c h connectivity is needed for the
Byzantine Generals Problem to be solvable. IC2 requires t h a t a loyal lieutenant
obey a loyal commander. This is clearly impossible if the c o m m a n d e r cannot
communicate with the lieutenant. In particular, if every message from the
3A recent algorithm of Dolev [2] requires less connectivity.
ACMTransactionson ProgrammingLanguagesand Systems,Vol.4, No. 3, July 1982.
396 L. Lamport, R. Shostak, and M. Pease
commander to the lieutenant must be relayed by traitors, then there is no way to
guarantee that the lieutenant gets the commander's order. Similarly, IC1 cannot
be guaranteed if there are two lieutenants who can only communicate with one
another via traitorous intermediaries.
The weakest connectivity hypothesis for which the Byzantine Generals Prob-
lem is solvable is that the subgraph formed by the loyal generals be connected.
We show that under this hypothesis, the algorithm SM(n - 2) is a solution, where
n is the number of generals--regardless of the number of traitors. Of course, we
must modify the algorithm so that generals only send messages to where they
can be sent. More precisely, in step (1), the commander sends his signed order
only to his neighboring lieutenants; and in step (2)(B), Lieutenant i only sends
the message to every neighboring lieutenant not among the jr.
We prove the following more general result, where the diameter of a graph is
the smallest number d such that any two nodes are connected by a path
containing at most d arcs.
THEOREM 4. For any m and d, if there are at most m traitors and the
subgraph of loyal generals has diameter d, then Algorithm S M ( m + d - 1) (with
the above modification) solves the Byzantine Generals Problem.
PROOF. The proof is quite similar to that of T h e o r e m 2 and is just sketched
here. To prove IC2, observe that by hypothesis there is a path from the loyal
commander to a lieutenant i going through d - 1 or fewer loyal lieutenants.
Those lieutenants will correctly relay the order until it reaches i. As before,
assumption A4 prevents a traitor from forging a different order.
To prove IC1, we assume the commander is a traitor and must show that any
order received by a loyal lieutenant i is also received by a loyal lieutenant j.
Suppose i receives an order v : 0 :j~ : . . - :jk not signed by j. If k < m, then i will
send it to every neighbor who has not already received that order, and it will be
relayed t o j within d - 1 more steps. If k _> m, then one of the first m signers must
be loyal and must have sent it to all of his neighbors, whereupon it will be relayed
by loyal generals and will reach j within d - 1 steps. []
COROLLARY. If the graph of loyal generals is connected, then SM(n - 2) (as
modified above) solves the Byzantine Generals Problem for n generals.
PROOF. Let d be the diameter of the graph of loyal generals. Since the diameter
of a connected graph is less than the number of nodes, there must be more than
d loyal generals and fewer than n - d traitors. The result follows from the
theorem by letting m = n - d - 1. []
T h e o r e m 4 assumes that the subgraph of loyal generals is connected. Its proof
is easily extended to show that even if this is not the case, if there are at most m
traitors, then the algorithm SM(m + d - 1) has the following two properties:
1. Any two loyal generals connected by a path of length at most d passing
through only loyal generals will obey the same order.
2. If the commander is loyal, then any loyal lieutenant connected to him by a
path of length at most m + d passing only through loyal generals will obey his
order.
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
The Byzantine Generals Problem • 397
6. RELIABLE S Y S T E M S
Other than using intrinsically reliable circuit components, the only way we know
to implement a reliable computer system is to use several different "processors"
to compute the same result, and then to perform a majority vote on their outputs
to obtain a single value. (The voting may be performed within the system, or
externally by the users of the output.) This is true whether one is implementing
a reliable computer using redundant circuitry to protect against the failure of
individual chips, or a ballistic missile defense system using redundant computing
sites to protect against the destruction of individual sites by a nuclear attack.
The only difference is in the size of the replicated "processor".
The use of majority voting to achieve reliability is based upon the assumption
that all the nonfaulty processors will produce the same output. This is true so
long as they all use the same input. However, any single input datum comes from
a single physical component--for example, from some other circuit in the reliable
computer, or from some radar site in the missile defense system--and a malfunc-
tioning component can give different values to different processors. Moreover,
different processors can get different values even from a nonfaulty input unit if
they read the value while it is changing. For example, if two processors read a
clock while it is advancing, then one may get the old time and the other the new
time. This can only be prevented by synchronizing the reads with the advancing
of the clock.
In order for majority voting to yield a reliable system, the following two
conditions should be satisfied:
1. All nonfaulty processors must use the same input value (so they produce the
same output).
2. If the input unit is nonfaulty, then all nonfaulty processes use the value it
provides as input (so they produce the correct output).
These are just our interactive consistency conditions IC1 and IC2, where the
"commander" is the unit generating the input, the "lieutenants" are the proces-
sors, and "loyal" means nonfaulty.
It is tempting to try to circumvent the problem with a "hardware" solution.
For example, one might try to insure that all processors obtain the same input
value by having them all read it from the same wire. However, a faulty input unit
could send a marginal signal along the wire--a signal that can be interpreted by
some processors as a 0 and by others as a 1. There is no way to guarantee that
different processors will get the same value from a possibly faulty input device
except by having the processors communicate among themselves to solve the
Byzantine Generals Problem.
Of course, a faulty input device may provide meaningless input values. All that
a Byzantine Generals solution can do is guarantee that all processors use the
same input value. If the input is an important one, then there should be several
separate input devices providing redundant values. For example, there should be
redundant radars as well as redundant processing sites in a missile defense
system. However, redundant inputs cannot achieve reliability; it is still necessary
to insure that the nonfaulty processors use the redundant data to produce the
same output.
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
398 L. Lamport, R. Shostak, and M. Pease
In case the input device is nonfaulty but gives different values because it is
read while its value is changing, we still want the nonfaulty processors to obtain
a reasonable input value. It can be shown that, if the functions majority and
choice are taken to be the median functions, then our algorithms have the
property that the value obtained by the nonfaulty processors lies within the range
of values provided by the input unit. Thus, the nonfaulty processors will obtain
a reasonable value so long as the input unit produces a reasonable range of values.
We have given several solutions, but they have been stated in terms of
Byzantine generals rather than in terms of computing systems. We now examine
how these solutions can be applied to reliable computing systems. Of course,
there is no problem implementing a "general's" algorithm with a processor. The
problems lie in implementing a message passing system that meets assumptions
A1-A3 (assumptions A1-A4 for Algorithm SM(m)). We now consider these
assumptions in order.
A1. Assumption A1 states that every message sent by a nonfaulty processor is
delivered correctly. In real systems, communication lines can fail. For the oral
message algorithms OM(m) and OM(m, p), the failure of the communication line
joining two processors is indistinguishable from the failure of one of the proces-
sors. Hence, we can only guarantee that these algorithms will work in the presence
of up to m failures, be they processor or communication line failures. (Of course,
the failure of several communication lines attached to the same processor is
equivalent to a single processor failure.) If we assume that a failed communication
line cannot result in the forgery of a signed message--an assumption which we
will see below is quite reasonable, then our signed message algorithm SM(m) is
insensitive to communication line failure. More precisely, Theorem 4 remains
valid even with communication line failure. A failed communication line has the
same effect as simply removing the communication line--it lowers the connectiv-
ity of the processor graph.
A2. Assumption A2 states that a processor can determine the originator of any
message that it received. What is actually necessary is that a faulty processor not
be able to impersonate a nonfaulty one. In practice, this means that interprocess
communication be over fixed lines rather than through some message switching
network. (If a switching network is used, then faulty network nodes must be
considered, and the Byzantine Generals Problem appears again.) Note that
assumption A2 is not needed if A4 is assumed and all messages are signed, since
impersonation of another processor would imply forging its messages.
A3. Assumption A3 requires that the absence of a message can be detected.
T h e absence of a message can only be detected by its failure to arrive within
some fixed length of time--in other words, by the use of some time-out conven-
tion. The use of time-out to satisfy A3 requires two assumptions:
1. There is a fixed maximum time needed for the generation and transmission of
a message.
2. The sender and receiver have clocks that are synchronized to within some
fixed maximum error.
T h e need for the first assumption is fairly obvious, since the receiver must know
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
The Byzantine Generals Problem 399
how long he needs to wait for the message to arrive. (The generation time is how
long it takes the processor to send the message after receiving all the input
necessary to generate it.) The need for the second assumption is less obvious.
However, it can be shown that either this assumption or an equivalent one is
necessary to solve the Byzantine Generals Problem. More precisely, suppose that
we allow algorithms in which the generals take action only in the following
circumstances:
1. At some fixed initial time (the same for all generals).
2. Upon the receipt of a message.
3. When a randomly chosen length of time has elapsed. (I.e., a general can set a
timer to a random value and act when the timer goes off.)
{This yields the most general class of algorithms we can envision which does not
allow the construction of synchronized clocks.) It can be shown that no such
algorithm can solve the Byzantine Generals Problem if messages can be trans-
mitted arbitrarily quickly, even if there is an upper bound on message transmis-
sion delay. Moreover, no solution is possible even if we restrict the traitors so
that the only incorrect behavior they are permitted is the failure to send a
message. T h e proof of this result is beyond the scope of this pa, Jer. Note that
placing a lower as well as an upper bound on transmission delay ahows processors
to implement clocks by sending messages back and forth.
The above two assumptions make it easy to detect unsent messages. Let/z be
the maximum message generation and transmission delay, and assume the
nonfaulty processors have clocks that differ from one another by at most T at any
time. T h e n any message that a nonfaulty process should begin to generate by
time T on its clock will arrive at its destination by time T + # + T on the receiver's
clock. Hence, if the receiver has not received the message by that time, then it
may assume that it was not sent. (If it arrives later, then the sender must be
faulty, so the correctness of our algorithms does not depend upon the message
being sent.) By fLxing the time at which the input processor sends its value, one
can calculate until what time on its own clock a processor must wait for each
message. For example, in Algorithm SM(m) a processor must wait until time To
+ k(# + ~) for any message having k signatures, where To is the time (on his
clock) at which the commander starts executing the algorithm.
No two clocks run at precisely the same rate, so no matter how accurately the
processors' clocks are synchronized initially, they will eventually drift arbitrarily
far apart unless they are periodically resynchronlzed. We therefore have the
problem of keeping the processors' clocks all synchronized to within some fixed
amount, even if some of the processors are faulty. This is as difficult a problem
as the Byzantine Generals Problem itself. Solutions to the clock synchroniza'~ion
problem exist which are closely related to our Byzantine Generals solutions. T h e y
will be described in a future paper.
A4. Assumption A4 requires that processors be able to sign their messages in
such a way that a nonfaulty processor's signature cannot be forged. A signature
is a piece of redundant information Si(M) generated by process i from a data
item M. A message signed by i consists of a pair (M, Si(M)). To meet parts (a)
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
400 L. Lamport, R. Shostak, and M. Pease
and (b) of A4, the function Si must have the following two properties:
(a) If processor i is nonfaulty, then no faulty processor can generate Si(M).
(b) Given M and X, any process can determine i f X equals Si(M).
Property (a) can never be guaranteed, since Si(M) is just a data item, and a
faulty processor could generate any data item. However, we can make the
probability of its violation as small as we wish, thereby making the system as
reliable as we wish. How this is done depends upon the type of faults we expect
to encounter. There are two cases of interest:
1. Random Malfunction. By making Si a suitably "randomizing" function, we
can make the probability that a random malfunction in a processor generates a
correct signature essentially equal to the probability of its doing so through a
random choice procedure--that is, the reciprocal of the number of possible
signatures. The following is one method for doing this. Assume that messages are
encoded as positive integers less than P, where P is a power of two. Let Si(M)
equal M * Ki mod P, where Ki is a randomly chosen odd number less than P.
Letting K [ 1 be the unique number less than P such that Ki * K i 1 - 1 mod P, a
process can check that X = Si (M) by testing that M = X * K~ 1 mod P. If another
processor does not have Ki in its memory, then the probability of its generating
the correct signature M * Ki for a single (nonzero) message M should be l/P: its
probability of doing so by random choice. (Note that if the processor could obtain
Ki by some simple procedure, then there might be a larger probability of a faulty
processor j forging i's signature by substituting Ki for K/when trying to compute
Sj(M).)
2. Malicious Intelligence. If the faulty processor is being guided by a malicious
intelligence--for example, if it is a perfectly good processor being operated by a
human who is trying to disrupt the system--then the construction of the signature
function Si becomes a cryptography problem. We refer the reader to [1] and [4]
for a discussion of how this problem can be solved.
Note that it is easy to generate the signature Si (M) if the process has already
seen that signature. Hence, it is important that the same message never have to
be signed twice. This means that, when using SM(m) repeatedly to distribute a
sequence of values, sequence numbers should be appended to the values to
guarantee uniqueness.
7. CONCLUSION
We have presented several solutions to the Byzantine Generals Problem, under
various hypotheses, and shown how they can be used in implementing reliable
computer systems. These solutions are expensive in both the amount of time and
the number of messages required. Algorithms OM(m) and SM(m) both require
message paths of length up to m 4- 1. In other words, each lieutenant may have
to wait for messages that originated at the commander and were then relayed via
m other lieutenants. Fischer and Lynch have shown that this must be true for
any solution that can cope with m traitors, so our solutions are optimal in that
respect. Our algorithms for a graph that is not completely connected require
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
The Byzantine Generals Problem 401
message paths of length up to rn + d, where d is the diameter of the subgraph of
loyal generals. We suspect that this is also optimal.
Algorithms OM(m) and SM(m) involve sending up to (n - 1)(n - 2) . . .
(n - m - 1) messages. The number of separate messages required can certainly
be reduced by combining messages. It may also be possible to reduce the amount
of information transferred, but this has not been studied in detail. However, we
expect that a large number of messages will still be required.
Achieving reliability in the face of arbitrary malfunctioning is a difficult
problem, and its solution seems to be inherently expensive. The only way to
reduce the cost is to make assumptions about the type of failure that may occur.
For example, it is often assumed that a computer may fail to respond but will
never respond incorrectly. However, when extremely high reliability is required,
such assumptions cannot be made, and the full expense of a Byzantine Generals
solution is required.
REFERENCES
1. DIFFIE, W., AND HELLMAN, M.E. New directions in cryptography. IEEE Trans. Inf. Theory
IT-22 (Nov. 1976), 644-654.
2. DOLEV, D. The Byzantine generals strike again. J. Algorithms 3, 1 (Jan. 1982).
3. PEASE, M., SHOSTAK, R., AND LAMPORT, L. Reaching agreement in the presence of faults. J.
ACM 27, 2 (Apr. 1980), 228-234.
4. RIVEST, R.L., SHAMIR, A., AND ADLEMAN, L. A method for obtaining digital signatures and
public-key cryptosystems. Cornrnun. ACM 21, 2 (Feb. 1978), 120-126.
Received April 1980; revised November 1981; accepted November 1981
ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.
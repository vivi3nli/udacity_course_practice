# Unit 1 introduction
## terminology
### fully vs partially observable
perception-action cycle
### deterministic vs stochastic
### discrete vs continous
limited 
### benign vs adversarial
# Unit 2 problem solving
## definition of a problem

- initial state
- action(s)return a set of possible actions {a1,a2,a3..}
- result input(state,action) output(new state)
- goaltest input(State) return(ture or false)
- path cost input(state,action transition) output cost
- or step cost (s,a,'s) 

## 3 type of search
### breadth first
always shortest step 
### cheapest first
lowest cost
### depth first
most storage saving
if the path is infinite, has a possibility of not reaching the goal
## A* search
f = g + h minimize f

g = cheapest search

h = estimated nearest distance (greedy search) 

To clarify, the heuristic function is admissible if h(s) <= true cost, rather than necessarily being strictly smaller than the true cost.

## working condition

- fully observable
- known
- discrete(finite
- deterministic
- static

# unit 3 probability
## bayes network

### binary events
#### probablities 
$$P(A)=p$$
$$P(\neg A)=1-p$$
#### independence 
$$P(x,y)=P(x)*P(y)$$
$$x\bot y$$
#### total probebility
$$P(y)=\sum_{i=1}^{n}P(y|x=i)P(x=i)$$
$$P(\neg x|y)=1-P(x|y)$$
### simple bayes network
$$P(A|B)=\cfrac{P(B|A)*P(A)}{P(B)}$$
### conditional independence
cancer test1 and test2
$$T_2\bot T_1|C$$
$$P(T2|C,T1)=P(T2|C)$$
(when C is dependent/related to T1&T2, when C is known--as a condition, T1/T2 is independent)
$$求：P(T_2^+|T_1^+)$$
我的思路（错误）
$$P(T_2^+|T_1^+)=\cfrac{P(T_1^+,T_2^+)}{P(T_1^+)}=\cfrac{0.01*0.9*0.9+0.99*0.2*0.2}{0.01*0.9+0.99*0.2}$$
$$P(C|T^+)=\cfrac{0.01*0.9}{0.01*0.9+0.99*0.2}=0.043$$
$$P(T_2^+|T_1^+)=P(T_2^+|T_1^+,C)P(C|T_1^+)+P(T_2^+|T_1^+,\neg C)P(\neg C|T_1^+)=0.9*0.043+0.2*(1-0.043)=0.2301$$
compare to 
$$P(T2+)=0.01*0.9+0.99*0.2=0.207$$
conclusion:when T1+ is know, P(T2) is higher
### bayes networks
#### different types
two independent cause leading to one results
$$P(Sunny)=0.7$$
$$P(Raise)=0.01$$
$$P(Happy|S,R)=1$$
$$P(H|\neg S,R)=0.9
$$$$P(H|S,\neg R)=0.7
$$$$P(H|\neg S,\neg R)=0.1$$
$$两者相互独立，所以:P(R|S)=0.01=P(R)$$
$$求:P(R|H,S)$$
我的思路：
$$P(R|H,S)=\cfrac{P(R,H,S)}{P(H,S)}=\cfrac{P(R)*P(S)}{P(R)P(S)P(H|S,R)+P(\neg R)P(S)P(H|S,\neg R)}=\cfrac{0.7*0.01}{0.7*0.01+0.7*0.99*0.7}=0.01422$$
参考答案：with bayes rules
$$P(R|H,S)=\cfrac{P(H|R,S)P(R|S)}
{P(H|S)}$$

$$求：P(R|H)$$
我的思路：
$$P(R|H)=\cfrac{P(H|R)*P(R)}{P(H)}$$
$$P(H|R)=P(H|S,R)*P(S)+P(H|\neg S,R)*P(\neg S)=1*0.7+0.9*0.3=0.97$$
$$P(H)=P(H|S,R)P(S)P(R)+P(H|\neg S,R)P(\neg S)P(R)+P(H|S,\neg R)P(S)P(\neg R)+P(H|\neg S,\neg R)P(\neg S)P(\neg R)=1*0.01*0.7+0.9*0.3*0.01+0.7*0.7*0.99+0.1*0.3*0.99=0.5245
$$$$P(R|H)=\cfrac{0.97*0.01}{0.5245}=0.01849$$
comparing those two, $$P(R|H,S)=0.01422 $$$$P(R|H)=0.01849$$, when Sunny is known, you're happy less likely because of raise

$$求：P(R|H,\neg S)$$我的思路：
$$P(R|H,\neg S)=\frac{P(\neg S|H,R)P(R|H)}{P(\neg S|H)}$$
$$P(\neg S|H,R)=1-P(S|H,R)=1-\cfrac{P(S,H,R)}{P(H,R)}=1-\cfrac{0.7*0.01*1}{0.7*0.01*1+0.3*0.01*0.9}=0.2784$$
$$P(\neg S|H)=1-P(S|H)=1-\cfrac{P(H|S)P(S)}{P(H)}=1-\cfrac{(1*0.01+0.7*0.99)*0.7}{0.5245}=0.06177$$
$$P(R|H,\neg S)=\cfrac{0.2784*0.01849}{0.06177}=0.08333$$
参考答案：
$$P(H|R,\neg S)=\cfrac{P(H|R,\neg S)P(R|\neg S)}{P(H|\neg S)}=\cfrac{0.9*0.01}{P(H|\neg S,R)*P(R)+P(H|\neg S,\neg R)P(\neg R)}$$
对比：
$$P(R|H,S)=0.01422 $$
$$P(R|H,\neg S)=0.08333$$
when it's known H, S and R are not independet.
so in this way independent doesnot imply conditional independence

###[general bayes net](https://classroom.udacity.com/courses/cs271/lessons/48624746/concepts/487276200923#)


提示：尽量选择表格中**已有的**来展开


### [d-seperation](https://classroom.udacity.com/courses/cs271/lessons/48624746/concepts/487138290923#)
reachability
### parameter counts
### later:indepedence 


[*公式示例：*](http://jzqt.github.io/2015/06/30/Markdown%E4%B8%AD%E5%86%99%E6%95%B0%E5%AD%A6%E5%85%AC%E5%BC%8F/)
分号
$\frac{1}{3} 与 \cfrac{1}{3}$
加粗：
$\textbf{bold}$
上下标和求和：
$\sum_{i=1}^n a_i=0$
$f(x)=x^{x^x}$























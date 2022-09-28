# 1_Basic_PerfectSecrecy

我是懒狗，所以一大堆例子、证明都没写。会定义就行。

教材：

《Introduction to Modern Cryptography》（主要）
《The Joy of Cryptography》
《A Graduate Course in Applied Cryptography》

## Encryption scheme

$$\newcommand{\c}[1]{\mathcal{#1}}\newcommand{\Gen}{\textsf{Gen}}\newcommand{\Rand}{\textsf{Rand}}\newcommand{\Enc}{\textsf{Enc}}\newcommand{\Dec}{\textsf{Dec}}\newcommand{\Sign}{\textsf{Sign}}\newcommand{\Eval}{\textsf{Eval}}\newcommand{\poly}{\textrm{poly}}\newcommand{\negl}{\textrm{negl}}\newcommand{\bit}{\{0,1\}}\newcommand{\gl}{\textsf{gl}}\newcommand{\hc}{\textsf{hc}}\newcommand{\getsr}{\stackrel{\smash{\$}}\gets}$$

形如$(\c{K}, \c{M}, \c{C}, \Enc, \Dec, \Gen)$。（key space, message/plaintext space, ciphertext space, encoder, decoder, key generator）$\Gen$从$\c{K}$中随机sample一个key$k$，发送者从$\c{M}$中选一个明文$m$，得到密文$c=\Enc(k,m)$。接收者调用$\Dec(k,c)$得到明文。

## Perfect secrecy的多种定义

直观定义：对于任何密文，就算攻击者得到密文，也不能得到关于原文的任何信息。

> Perfect secrecy: 对任意$\c{M}$上的分布，$m$从该分布中随机sample一个值。令$K$为随机sample的key值，令$C=\Enc(K,M)$，则有
$$\forall m\in\c{M}, \forall c\in\c{C}, \Pr[M=m\mid C=c]=\Pr[M=m]$$

> Perfect indistinguishability: 对任意$m_0,m_1\in\c{M}$上的分布，$\Enc(K,m_0),\Enc(K,m_1)$的分布一致（统计距离为0）。
$$\forall c\in\c{C}, \Pr[\Enc(K,m_0)\to c]=\Pr[\Enc(K,m_1)\to c]$$

> Adversarial indistinguishability: 考虑一个游戏过程：一个对手$\c{A}$选择两个明文$m_0,m_1\in\c{M}$，然后随机生成$k\getsr \Gen,b\getsr\{0,1\}$，将$c=\Enc(k,m_b)$传给$\c{A}$，最后$\c{A}$试图猜测$b$的值。
对任意$\c{A}$，他猜对的概率为$\frac 12$。（为什么让对手选择明文？因为这可以更加安全，且现实中对手可以通过一些方式影响明文。）

书上证了三种定义互相等价（1、2等价很好证）。

很难知道Perfect secrecy的算法是否存在（与P=NP一样难）。

## One-Time Pad

如果双方都有和明文一样长的Key，很容易达到完美的安全。

![](vx_images/105405313239391.png =759x)
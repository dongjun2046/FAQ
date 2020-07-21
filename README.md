# 同态加密技术概述
​        伴随着人工智能、大数据和云计算等信息产业蓬勃发展的同时，数据安全和敏感数据（包括个人隐私）泄露问题日益严峻。数据泄露不仅造成公司形象受损、公信力降低，也直接或间接地导致公司经济的损失。企业对数据安全问题越来越重视，用户的个人隐私保护意识也越来越强烈。同时，一些法律法规提出了更严格的数据安全与隐私保护要求。欧洲联盟正式实施《通用数据保护条例》（General Data Protection Regulation，简称GDPR），对基本的个人身份信息、医疗敏感数据和网络行为信息等提出安全保护要求。国内相继也颁布了类似的法律法规，如《信息安全技术 个人信息安全规范》、《信息安全技术 大数据安全管理指南》和《信息安全技术 个人信息去标识化指南》等。为了应对数据安全与隐私保护挑战，企业除了应用传统的加解密技术外，还在根据不同的业务场景和需求，积极探索匿名化（Anonymity）、数据脱敏（Data Masking）和数字水印等新型技术，甚至一些前沿技术的实践与落地，如保留格式加密（Format-Preserving Encryption，简称FPE）和差分隐私等关键技术。然而，上述提到的几种技术无法解决第三方平台（如云环境）的数据处理过程的数据与隐私保护问题：① 传统加密技术使得加密后数据失去可用性；② 脱敏等变换后的数据产生了失真，无法得到精确的处理结果。同态加密技术是近年来被学术界和工业界十分看好的一种加密技术，可实现数据加密后仍然可以被处理。但是，现有的多数同态加密方案由于占用资源过大且速度过慢导致无法从理论实现实用化，目前仍然面临各种问题与挑战。
## 同态加密背景
### 背景介绍
​        同态加密的研究可以追溯到20世纪70年代，在RSA密码体制刚提出不久，1978年Rivest等人在题为《On data banks and privacy homomorphic》中首次提出了全同态加密的概念，也称为隐私同态。这一概念的提出成为密码学界的开放难题，同态加密是一种加密形式，允许用户直接对密文进行特定的代数运算，得到数据仍是加密的结果，与对明文进行同样的操作再将结果加密一样。同态加密优势在于用户在数据加密的情形下仍能对特定的加密数据进行分析和检索，提高了数据处理的效率，保证了数据安全传送，而且正确的加密数据仍能得到正确的解密结果。国外学者相继研究了满足乘法或满足加法的同态加密算法，在此基础上还提出了能同时满足有限次乘法与加法的同态密码。但直到2009年IBM研究员Gentry才构造出第一个全同态加密方案，解决了困扰密码学界三十多年的难题，同时掀起一股研究全同态加密方案的热潮。Gentry，一个斯坦福大学的博士生，基于理想格提出一个全同态加密方案。Craig Gentry. Fully Homomorphic Encryption Using Ideal Lattices. In the 41st ACM Symposium on Theory of Computing (STOC), 2009. 这篇论文是来自于他的博士论文：Craig Gentry. A Fully Homomorphic Encryption Scheme (Ph.D. thesis)。 Gentry的全同态加密方案是基于理想格构造的。

​        与普通加密算法只关注数据存储安全不同，同态加密算法关注的是数据处理安全，提供对加密数据进行加法和乘法处理的功能。数据处理权与数据所有权可以分离，这样企业可以防止自身数据泄露的同时，利用云服务的算力。使用同态加密算法，不持有私钥的用户也可以对加密数据进行处理，处理过程不会泄露任何原始数据信息。同时，持有私钥的用户对处理过的数据进行解密后，可得到正确的处理结果。

### 同态分类
​        同态加密类型，其实按照实现程度分为两种：部分同态加密SWHE(Somewhat Homomorphic Encryption) 和 全同态加密FHE(Fully Homomorphic Encryption)。这两个区别在于：

（1）SWHE：这种类型的同态加密只支持特定的函数，比如加法或者乘法。

（2）FHE：这种类型的同态加密支持任意的函数，只要这种函数可以通过算法描述，并用计算机能够实现。

（4）如果一个加密函数f只满足加法同态，就只能进行加减法运算；

（5）如果一个加密函数f只满足乘法同态，就只能进行乘除法运算;

（6）如果一个加密函数同时满足加法同态和乘法同态，称为全同态加密。那么这个使用这个加密函数完成各种加密后的运算(加减乘除、多项式求值、指数、对数、三角函数)

  目前的加密全同态方案主要有三种：

（1）基于理想格（ideal lattice）的方案：Gentry 和 Halevi 在 2011 年提出的基于理想格的方案可以实现 72 bit 的安全强度，对应的公钥大小约为 2.3 GB，同时刷新密文的处理时间需要几十分钟。

（2）基于整数上近似 GCD 问题的方案：Dijk 等人在 2010 年提出的方案（及后续方案）采用了更简化的概念模型，可以降低公钥大小至几十 MB 量级。

（3）基于带扰动学习（Learning With Errors，LWE）问题的方案：Brakerski 和 Vaikuntanathan 等在 2011 年左右提出了相关方案；Lopez-Alt A 等在 2012 年设计出多密钥全同态加密方案，接近实时多方安全计算的需求。

### 同态加密常见算法
（1）RSA 和ElGamal算法对于乘法操作是同态的。

（2）Paillier 和Benaloh算法则是对加法同态的。

（3）Gentry算法则是全同态的。

## 同态加密原理
### 加密原理
如果满足 f(A)+f(B)=f(A+B)f(A)+f(B)=f(A+B) ， 我们将这种加密函数叫做加法同态

如果满足 f(A)×f(B)=f(A×B)f(A)×f(B)=f(A×B) ，我们将这种加密函数叫做乘法同态。

⊕和⊙为某种数学运算。

如果加密算法满足：E(x + y) = E(x) ⊕ E(y)，我们将这种加密函数叫做加法同态 。

如果加密算法满足：E(x * y) = E(x) ⊙ E(y)，我们将这种加密函数叫做乘法同态 。

一个加密函数如果只满足加法同态，就只能进行加减法运算；如果只满足乘法同态，就只能进行乘除法运算；如果同时满足加法同态和乘法同态，称为完全同态。第一个满足加法和乘法同态的同态加密方法直到2009年才由Craig Gentry提出。

## Paillier加密同态算法举例
Paillier算法是公钥加密体系的一个代表，是由Paillier在1999年发明，是一种同态加密算法，关于同态加密，之前胜超也讲过，它只满足于加法同态，和零知识证明是一个标准的交易隐私保护方法。

Paillier算法是同态加密算法，同态加密除了能实现数据的基本加密，还能保证在密文上直接进行操作，其结果解密后与在明文上进行操作的结果一样。

Paillier算法不仅可以用于公钥加密，还可以应用于各种云计算应用，从安全角度来说，用户一般不敢将敏感信息直接放在第三方云上进行处理，但是如果用的是同态加密技术，那么用户可以放心地使用，将同态加密应用到云服务中，可以从根本上解决云服务中数据的保密存储和保密计算问题，从根本上解决了数据隐私的问题。

### Paillier同态属性
加法同态(两个密文的乘积将解密为它们相应的明文之和)
D(E(m1)∗E(m2)modn^2)=(m1+m2)modn

代码：
```java
/**
* This program is free software: you can redistribute it and/or modify itunder the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
* This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
* FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for
* more details You should have received a copy of the GNU General Public License along with
* this program. If not, see <http://www.gnu.org/licenses/>.
*/
import java.math.*;
import java.util.*;
/**
* Paillier Cryptosystem <br><br>
* References: <br>
* [1] Pascal Paillier, "Public-Key Cryptosystems Based on Composite Degree Residuosity Classes," EUROCRYPT'99.
* URL: <a href="http://www.gemplus.com/smart/rd/publications/pdf/Pai99pai.pdf">http://www.gemplus.com/smart/rd/publications/pdf/Pai99pai.pdf</a><br>
*
* [2] Paillier cryptosystem from Wikipedia.
* URL: <a href="http://en.wikipedia.org/wiki/Paillier_cryptosystem">http://en.wikipedia.org/wiki/Paillier_cryptosystem</a>
* @author Kun Liu (kunliu1@cs.umbc.edu)
* @version 1.0
*/
public class Paillier {

/**
* p and q are two large primes.
* lambda = lcm(p-1, q-1) = (p-1)*(q-1)/gcd(p-1, q-1).
*/
private BigInteger p, q, lambda;
/**
* n = p*q, where p and q are two large primes.
*/
public BigInteger n;
/**
* nsquare = n*n
*/
public BigInteger nsquare;
/**
* a random integer in Z*_{n^2} where gcd (L(g^lambda mod n^2), n) = 1.
*/
private BigInteger g;
/**
* number of bits of modulus
*/
private int bitLength;

/**
* Constructs an instance of the Paillier cryptosystem.
* @param bitLengthVal number of bits of modulus
* @param certainty The probability that the new BigInteger represents a prime number will exceed (1 - 2^(-certainty)). The execution time of this constructor is proportional to the value of this parameter.
*/
public Paillier(int bitLengthVal, int certainty) {
KeyGeneration(bitLengthVal, certainty);
}

/**
* Constructs an instance of the Paillier cryptosystem with 512 bits of modulus and at least 1-2^(-64) certainty of primes generation.
*/
public Paillier() {
KeyGeneration(512, 64);
}

/**
* Sets up the public key and private key.
* @param bitLengthVal number of bits of modulus.
* @param certainty The probability that the new BigInteger represents a prime number will exceed (1 - 2^(-certainty)). The execution time of this constructor is proportional to the value of this parameter.
*/
public void KeyGeneration(int bitLengthVal, int certainty) {
bitLength = bitLengthVal;
/*Constructs two randomly generated positive BigIntegers that are probably prime, with the specified bitLength and certainty.*/
p = new BigInteger(bitLength / 2, certainty, new Random());
q = new BigInteger(bitLength / 2, certainty, new Random());

n = p.multiply(q);
nsquare = n.multiply(n);

g = new BigInteger("2");
lambda = p.subtract(BigInteger.ONE).multiply(q.subtract(BigInteger.ONE)).divide(
p.subtract(BigInteger.ONE).gcd(q.subtract(BigInteger.ONE)));
/* check whether g is good.*/
if (g.modPow(lambda, nsquare).subtract(BigInteger.ONE).divide(n).gcd(n).intValue() != 1) {
System.out.println("g is not good. Choose g again.");
System.exit(1);
}
}

/**
* Encrypts plaintext m. ciphertext c = g^m * r^n mod n^2. This function explicitly requires random input r to help with encryption.
* @param m plaintext as a BigInteger
* @param r random plaintext to help with encryption
* @return ciphertext as a BigInteger
*/
public BigInteger Encryption(BigInteger m, BigInteger r) {
return g.modPow(m, nsquare).multiply(r.modPow(n, nsquare)).mod(nsquare);
}

/**
* Encrypts plaintext m. ciphertext c = g^m * r^n mod n^2. This function automatically generates random input r (to help with encryption).
* @param m plaintext as a BigInteger
* @return ciphertext as a BigInteger
*/
public BigInteger Encryption(BigInteger m) {
BigInteger r = new BigInteger(bitLength, new Random());
return g.modPow(m, nsquare).multiply(r.modPow(n, nsquare)).mod(nsquare);

}

/**
* Decrypts ciphertext c. plaintext m = L(c^lambda mod n^2) * u mod n, where u = (L(g^lambda mod n^2))^(-1) mod n.
* @param c ciphertext as a BigInteger
* @return plaintext as a BigInteger
*/
public BigInteger Decryption(BigInteger c) {
BigInteger u = g.modPow(lambda, nsquare).subtract(BigInteger.ONE).divide(n).modInverse(n);
return c.modPow(lambda, nsquare).subtract(BigInteger.ONE).divide(n).multiply(u).mod(n);
}

/**
* main function
* @param str intput string
*/
public static void main(String[] str) {
/* instantiating an object of Paillier cryptosystem*/
Paillier paillier = new Paillier();
/* instantiating two plaintext msgs*/
BigInteger m1 = new BigInteger("20");
BigInteger m2 = new BigInteger("60");
/* encryption*/
BigInteger em1 = paillier.Encryption(m1);
BigInteger em2 = paillier.Encryption(m2);
/* printout encrypted text*/
System.out.println(em1);
System.out.println(em2);
/* printout decrypted text */
System.out.println(paillier.Decryption(em1).toString());
System.out.println(paillier.Decryption(em2).toString());

/* test homomorphic properties -> D(E(m1)*E(m2) mod n^2) = (m1 + m2) mod n */
BigInteger product_em1em2 = em1.multiply(em2).mod(paillier.nsquare);
BigInteger sum_m1m2 = m1.add(m2).mod(paillier.n);
System.out.println("original sum: " + sum_m1m2.toString());
System.out.println("decrypted sum: " + paillier.Decryption(product_em1em2).toString());

/* test homomorphic properties -> D(E(m1)^m2 mod n^2) = (m1*m2) mod n */
BigInteger expo_em1m2 = em1.modPow(m2, paillier.nsquare);
BigInteger prod_m1m2 = m1.multiply(m2).mod(paillier.n);
System.out.println("original product: " + prod_m1m2.toString());
System.out.println("decrypted product: " + paillier.Decryption(expo_em1m2).toString());

}
}
```
输出：
```
12707656870470188428637837528447278227239134869392491431413242260655409952227523978290554669438828807216394853758855633929234107767526895835265153544056501456416421808517771011582302143863302437393325981831656448084184456024100905614982641726426780984484369748621107565776554980215687737956868087637363003360
33874823815913488762637447775383793243495045008440777649882480185359771475794365026589752899253256541972923831921866060262539909903360117783348350409991159501936736615060206247919283775803380083499692831903165086362551086171534412497522245936069557769032308134772408102904348732021299900573656122107087784584
20
60
original sum: 80
encrypted sum: 28144810547570475287441268618708101225326501402559153126830036291278690597585333463625516012995743273046805729438112669402476058515536083354442139139257796724081531595830420137923906579939303124139541277180856495449351833613952785316412045000688317899119225999580337128820084279665235799956655727662156590726
decrypted sum: 80
original product: 1200
encrypted product: 27399372798528893994472062779968842931289881082375635854433778828241350124430601982082217772379457630874093947822835517016416688828999602649427102947778267406845172558874053567861159888150615236358941818020689888563275017740384296528595184262887781160417076780325510989918604379227469932304204629408795410557
decrypted product: 1200
```
备注：上述例子基于数值处理，针对字符串的处理情况，可以将字符串先转换为字节，然后字节转化为整数，然后进行处理，原理一样。
## 同态加密应用
​        随着云计算的广泛应用，特别是云平台上的大量电子商务交易，如何安全有效地保护用户隐私与安全成为当今密码学研究领域的热点。若数据以明文形式进行存储则有可能将敏感数据暴露给云服务商，会给用户机密数据带来一系列的安全问题。为解决这一问题，同态加密方案应运而生，利用全同态加密方案对用户数据进行加密，再将密文发送到云端，数据在云端可以进行一系列的上传、下载、删除、更新、检索等操作，且操作的均是密文。该操作既避免了数据在传输过程中被拦截、复制、篡改或伪造等风险，也避免了数据存储方将数据泄露或在服务器端被攻破的危险。
### 安全云计算与委托计算场景

​       同态技术在该方面的应用可以使得我们在云环境下，充分利用云服务器的计算能力，实现对明文信息的运算，而不会有损私有数据的私密性。例如医疗机构通常拥有比较弱的数据处理能力，而需要第三方来实现数据处理分析以达到更好的医疗效果或者科研水平，这样他们就需要委托有较强数据处理能力的第三方实现数据处理（云计算中心），但是医院负有保护患者隐私的义务，不能直接将数据交给第三方。在同态加密技术的支持下，医疗机构就可以将加密后的数据发送至第三方，待第三方处理完成后便可返回给医疗结构。整个数据处理过程、数据内容对第三方是完全透明的。

​        得益于同态加密（Homomorphic Encryption）等先进密码技术，可以使得数据在整个分析和处理生命周期中，始终保持加密状态，用户无需解密即可生成数据洞察结果。比如在云计算场景中，数据拥有方将数据加密存储在云计算平台中，数据拥有方提交数据统计或处理任务，直接对加密数据进行操作即可，不需要在云平台中进行解密，因此存储方无法获取真实的数据内容。同态加密技术有利于企业内部和企业间的数字协作，实现安全的机器学习和数据挖掘任务，降低了数据泄露风险，同时完全遵守隐私保护法规。
### 数据安全托管与密文检索场景
​        用户（企业和个人）可以将自己的数据加密后托管到一个不信任的云服务器上，日后可以向云服务器查询自己所需要的信息，数据存储与查询都使用密文数据，服务器将检索到的密文数据发回。用户可以解密得到自己需要的信息，而托管服务器却对存储和检索的信息一无所知。此种方法同样适用于搜索引擎的数据检索。
### 数据共享开放场景
​        据 Gartner统计，随着大数据技术的成熟，全球超过60％的运营商已开始投资大数据，以期借助大数据技术实现从网络资产经营到数据资产经营的转型，而数据开放是实现这一转型的关键举措。但与此同时，随着数据的逐步开放，其所带来的数据安全与隐私保护等问题也日益呈现。如何在大数据时代既能通过数据开放获取商业利益，又能保障数据开放中的数据安全与隐私，是运营商目前迫切需要解决的问题。

​        运营商集团所拥有的的用户数据覆盖了位置、身份、上网、社交、支出、通信、终端和时序等多个维度，其全面性、多维性、中立性、完整性是其他企业难以比拟的、这些数据在各行业的营销场景中能够产生巨大的价值。但在通过数据开放获取长期商业利益的同时，运营商也必须提供足够的安全保护机制，规避来自内部和外部的，发生在数据存储、传输和使用过程中的敏感信息泄露风险。

​        运营商已经拥有大量高价值的数据资产，但想要真正有效地利用这些数据资产，将运营商数据与各领域行业知识及先进的人工智能技术相结合，充分挖掘数据价值，还需要引入各类具有深度行业背景或强大数据分析能力的企业，共同建设数据集市生态圈。在这一模式下，如何既充分发挥各方能力，整合数据、业务和算法资源，提升数据价值，又确保数据的私密性和安全性，是建设数据开放的商业模式时必须面对的挑战。
## 展望
​        当今正处于IT技术和应用的变革期，云、大数据、人工智能等技术的发展让人类社会从信息化向智能化升级，数据作为当今信息化和未来智能化时代的关键生产资料已经成为个人、组织和国家的重要经济资产和核心战略资本。现在可用的SWHE算法大部分也都是基于RSA模组的，所以和RSA算法有一样的问题，那就是一旦整数分解问题被解决，那么算法将变得不安全。而且现在已经证明，量子计算机已经可以解决整数分解问题。所以随着量子计算机的普及，这些算法都会有很大的破解风险。所以目前主流的加密算法已经开始研究格密码学等方向，格密码学已经被证明是量子计算安全的算法。格上标准困难问题至今没有量子算法可以破解或者撼动它，因此格上标准困难问题被认为是抗量子的。格上的加密方案最大特征：是一个含有噪音的方案。加密时往里添加噪音，主要是为了进一步提高安全性。然而恰好是这个噪音，导致加密的形式与解密形式比较简单。这种特性为构造全同态加密埋下了伏笔。当前，保护数据的隐私和安全已经成为全社会亟需且亟待解决的重要问题，因此同态加密的瓶颈一旦被突破，一定会拥有广阔的前景!
## 参考链接
https://zhuanlan.zhihu.com/p/52808772 <br>
https://blog.csdn.net/jason_cuijiahui/article/details/79121702<br>
https://blog.csdn.net/qq_33885461/article/details/86555560<br>
https://www.csee.umbc.edu/~kunliu1/research/Paillier.html<br>
https://www.cs.cmu.edu/~odonnell/hits09/gentry-homomorphic-encryption.pdf<br>

---
permalink: /CH1/
use_math: true
---

<style>
td {font-size:100% ;background-color: white;}
</style>



<h1 align="center"> Automatique Linéaire - Espace d'Etat</h1><br>
<div align="center", style="font-size:x-large"> Université de Lille</div><br>
<div align="center", style="font-size:large"> Faculté des Sciences et Technologies</div><br>
<div align="center", style="font-size:large"> Dept. EEA   Bât P2 307</div><br>
<div align="center"> Lotfi.Belkoura@univ-lille.fr</div>

<h2 align="center">Modèles d'état</h2>

### Motivation

- Les fonctions de transferts permettent une description de systèmes en termes d'entrées/sorties
- Il est souvent utile de pouvoir décrire (et estimer) des variables non mesurées dans un système (ex: courant aux bornes de l'armature dans un moteur électrique). C'est l'objet du traitement des processus dans un espace dit *espace d'état*.
- La connaissance de ces variables (d'état) permet une analyse et un contrôle plus complet qu'une approche entrées/sorties, avec une extension naturelle aux systèmes multivariables.


### Concept d'état: Définition

Soit un processus possédant $r$ entrées $u=(u_{1},u_{2},...,u_{r})^{t}$ et $m$ sorties $y=(y_{1},y_{2},...,y_{m})^{t}. $ Si un vecteur $x(t)$ à $n$ composantes (i.e. $x=(x_{1},x_{2},...,x_{n})^{t}$ est proposé pour représenter l'état du système, cette proposition sera pertinente s'il lui correspond un système d'équations de la forme:

$$
\begin{array}
[c]{l}%
\dot{x}=f(x,u,t)\qquad\text{dite }\mathbf{\acute{e}quation\ d}^{\prime
}\mathbf{\acute{e}tat}\\
y=h(x,u,t)\qquad\text{dite }\mathbf{\acute{e}quation\ de\,\,sortie}%
\end{array}
\right. 
$$

$$ \label{eq:MSE}\tag{1}
\mathrm{MSE}(\hat{\theta}) = \mathrm{Var}(\hat{\theta}) - \mathrm{Bias}(\hat{\theta},\theta)^2
$$

où $f=(f_{1},...,f_{n})^{t}$, et $h=(h_{1},...,h_{m})^{t}$. Dans cette représentation, $x(t)\in\mathbb{R}^{n}$ est appelé **vecteur d'état**, $u(t)\in\mathbb{R}^{r}$ est appelé vecteur de commande, et $y(t)\in\mathbb{R}^{m}$ est appelé vecteur de sorties.


Dans certaines situations où l'état, les commandes ou les sorties sont soumis à des **contraintes** (par ex: saturation des actionneurs), il convient d'être plus précis sur les ensembles dans lesquels évoluent ces vecteurs. On note alors

- $x(t)\in\mathcal{X}\subseteq\mathbb{R}^{n}$ avec ($x$,$\mathcal{X)}=$vecteur et espace d'état
- $u(t)\in\mathcal{U}\subseteq\mathbb{R}^{r}$ avec ($u$,$\mathcal{U)}= $ vecteur et espace de commande
- $y(t)\in\mathcal{Y}\subseteq\mathbb{R}^{m}$ avec ($y$,$\mathcal{Y)}= $ vecteur et espace de sortie


#### Exemple
Cet exemple simple est celui d'une masse $m$ mise en mouvement au moyen d'un couple $u(t)$ comme indiqué sur la figure suivante. On néglige en première approximation la masse de la tige (de longueur unitaire) ainsi que les frottements de l'articulation. La position de la masse est repérée par l'angle $\theta$ que fait la tige avec la verticale.

<center><img src="Figures/Pendule.svg" width="150px%"/></center>


Avec $g$ accélération de la gravité, l'équation du mouvement s'écrit:

\begin{equation*}
m\,\ddot{\theta}(t)+mg\,\sin\theta(t)=u(t)
\end{equation*}

Recherchons une représentation d'état de ce système. Si on propose pour vecteur d'état

\begin{equation*}
x=\left(\begin{array}{c}x_{1} \\ x_{2}\end{array}\right) =
\left(\begin{array}{c}\theta \\ \dot{\theta}\end{array}\right) 
\end{equation*}

on obtient

\begin{align*}
\dot x_{1}  & =f_{1}(x,u)=x_{2}\\
\dot x_{2}  & =f_{2}(x,u)=-g\,\sin x_{1}+u/m\\
y  & =h(x,u)=x_{1}%
\end{align*}

Le vecteur $x$ proposée représente donc bien un vecteur d'état possible.

### Le cas linéaire

Dans de nombreuses situations, la nature du processus ou encore le domaine (réduit) dans lequel évoluent les variables sont tels que les fonctions $f(x,u,t)$ et $h(x,u,t)$ possèdent les propriétés particulières suivantes:

- Elles sont \textbf{stationnaires }(ou invariantes dans le temps), en ce sens que le temps n'intervient pas explicitement dans les équations. En d'autres termes, $f(x,u,t):=f(x,u)$ et $h(x,u,t):=h(x,u)$.
- Elles sont \textbf{linéaires} par rapport à leurs arguments ($x$ et $u$) soit encore $f(x_{1}+x_{2},0)=f(x_{1},0)+f(x_{2},0)$, $f(0,u_{1}+u_{2})=f(0,u_{1})+f(0,u_{2})$, idem pour $h(x,u)$.

Dans ce cas la représentation d'état précédente pourra toujours se mettre sous la forme **matricielle**:

\begin{equation*}
\fbox{$\left.
\begin{array}
[c]{c}%
\dot{x}(t)=A\,x(t)+B\,u(t)\\
y(t)=C\,x(t)+D\,u(t)
\end{array}
\right.  $}%
\end{equation*}

dans laquelle $A$ est une matrice carrée de taille $n\times n$, $B$ est de taille $n\times r$, $C$ est de taille $m\times n$, et $D$ est de taille $m\times n$. Pour alléger l'écriture, on note parfois $\sum(A,B,C,D)$ un système linéaire stationnaire noté $\sum$ et décrit par les matrices $(A,B,C,D).$

Note: Dans le cas linéaire mais non invariant dans le temps, on obtient la représentation matricielle précédente avec des matrices qui dépendent du temps, soit $A(t)$, $B(t)$, $C(t)$ et $D(t)$.


#### Exemple du moteur à courant continu
Cet exemple est celui d'un système électromécanique dont le principe de fonctionnement est schématisé ci après. L'entrée du processus est la tension $u(t)$ aux bornes du circuit électrique, la sortie est la position $\theta (t)$ de l'arbre moteur.

Les paramètres constants du système sont: $R,L,$ respectivement la résistance et l'inductance du circuit électrique,  $f$ le coefficient de frottements visqueux, et $J$ l'inertie de l'arbre moteur. Le moteur délivre un couple $\Gamma (t)$ proportionnel au courant $i(t)$ qui le traverse (coefficient de
proportionnalité $k_1$). La force contre-électromotrice (fcem) $E(t)$ développée est proportionnelle à la vitesse $\omega (t)$ de rotation de l'arbre (coefficient de proportionnalité $k_2$).

<table width="90%">
<tr><td  width="60%">  <center><img src="Figures/moteur-theta.svg" width="80%"/></center> </td>
    <td>  
    \begin{align*} 
 & u(t) = Ri(t) + L\frac{di}{dt} + E(t)\\   
&J \ddot \theta =\Gamma (t)-f\dot \theta \\
     & E(t) = k_2\dot \theta(t) \\
     & \Gamma(t)=k_1 i(t)   
\end{align*} 
    </td>   
    </tr>
</table>

Ici (cas Siso), $r=m=1$. Proposons pour vecteur d'état:

\begin{equation*}
x=\left(
\begin{array}{c}%
x_{1} \\ x_{2} \\ x_{3}%
\end{array}
\right)=\left(
\begin{array}{c}%
\theta \\ \omega \\  i
\end{array}
\right)
\end{equation*}

où $\omega$ est la vitesse de rotation de l'arbre. En manipulant les équations précédentes du moteur, nous pouvons écrire:

\begin{align*}
\dot{\theta}  & =\omega\\
\dot{\omega}  & =\frac{k_{1}\,i-f\,\omega}{J}\\
\dot{i}  & =\frac{u-R\,i-k_{2}\omega}{L}%
\end{align*}

Ces équations admettent une écriture matricielle:

\begin{align*}
\dot{x}&=f(x,u)=\left(
\begin{array}{ccc}%
0 & 1 & 0\\
0 & \dfrac{-f}{J} & \dfrac{k_{1}}{J}\\
0 & \dfrac{-k_{2}}{L} & \dfrac{-R}{L}%
\end{array}
\right)  \,x+\left(\begin{array}{c}0\\0\\\dfrac{1}{L}\end{array}\right)  u=A\,x+B\,u \\
y&=h(x,u)=\left(\begin{array}{ccc}1 & 0 & 0\end{array}\right)  \,x+\left(  0\right)  \,u=C\,x+D\,u
\end{align*}


Le vecteur $x=(\theta,\omega,i)^{t}$ est donc bien acceptable en tant que vecteur d'état Noter que ce vecteur possède 3 composantes, ce qui correspond aussi à l'ordre de la fonction de transfert $G(p)$.


#### Exemple du générateur de vapeur
Une étude du comportement du générateur a permit de modéliser le comportement du processus sous forme
de fonctions de transfert interconnectées comme indiqué sur le schéma suivant. On se propose de fournir 
une repésenation d'état du système. Les FT mises en jeu étant du **premier ordre**, associons une variable
d'état $x_{i}$ à la sortie de chaque bloc (peu importe l'ordre), et notons temporairement $r_{i}$ les entrées correspondantes.<br><br>

<center><img src="Figures/Centrale-therm.svg" width="70%"/></center>
<br>
A chaque FT du premier ordre correspond une equation différentielle d'ordre 1 de la forme $\dot{x}_{i}=-a_{i}\,x_{i}+b_{i}\,r_{i}$, $i=1,...,4$. La lecture du schéma de fonctionnement fournit alors les
équations:
\begin{align*}
\dot{x}_{1}  & =-a_{1}\,x_{1}+b_{1}\,r_{1}\quad\quad \quad r_{1}=u_{2}\\
\dot{x}_{2}  & =-a_{2}\,x_{2}+b_{2}\,r_{2}\quad\quad \quad r_{2}=x_{1}+c_{1}u_{1}%
+c_{3}u_{3}\\
\dot{x}_{3}  & =-a_{3}\,x_{3}+b_{3}\,r_{3}\quad\quad \quad r_{3}=u_{3}\\
\dot{x}_{4}  & =-a_{4}\,x_{4}+b_{4}\,r_{4}\quad\quad \quad r_{4}=x_{3}+c_{4}x_{1}%
+c_{5}u_{1}+c_{6}x_{2}%
\end{align*}
et pour les sorties
\begin{align*}
y_{1}  & =x_{2}+c_{2}\,u_{1}\\
y_{2}  & =x_{4}%
\end{align*}

soit sous forme matricielle

\begin{equation*}
\dot{x}=f(x,u)=\left(
\begin{array}
{cccc}%
-a_{1} & 0 & 0 & 0\\
b_{2} & -a_{2} & 0 & 0\\
0 & 0 & -a_{3} & 0\\
b_{4}c_{4} & b_{4}c_{6} & b_{4} & -a_{4}%
\end{array}
\right)  \,x+\left(
\begin{array}
{ccc}%
0 & b_{1} & 0\\
b_{2}c_{1} & 0 & b_{2}c_{3}\\
0 & 0 & b_{3}\\
b_{4}c_{5} & 0 & 0
\end{array}
\right)  \,u
\end{equation*}


\begin{equation*}
y=h(x,u)=\left(
\begin{array}
{cccc}%
0 & 1 & 0 & 0\\
0 & 0 & 0 & 1
\end{array}
\right)  \,x+\left(
\begin{array}
{ccc}%
c_{2} & 0 & 0\\
0 & 0 & 0
\end{array}
\right)  \,u
\end{equation*}

C'est encore un système admettant la représentation matricielle $\dot{x}(t)=A\,x(t)+B\,u(t),$ et $y(t)=C\,x(t)+D\,u(t)$.



**Remarque**: Dans la représentation $\dot{x}=A\,x+B\,u,$ et $y=C\,x+D\,u$, $u(t)$ représente généralement le vecteur de **commande**, c'est à dire que nous pouvons agir sur ses différentes composantes $u_{1},...,u_{r}$.

Or, dans le cas du générateur de vapeur, si nous maîtrisons effectivement les entrées ''debit de fuel'' $u_{2}$ et ''débit d'eau'' $u_{3},$ la composante ''débit vapeur'' $u_{1}$ est une grandeur incontrôlable (demande du réseau électrique).

Pour être plus précis dans la représentation d'état précédente, il convient de séparer les commandes $u_{2},u_{3} $ de cette grandeur $u_{1}$ qui représente la consigne.

En notant par exemple $u=(u_{2},u_{3})^{t}$ et $w=u_{1}$, on peut réécrire l'équation d'état précédente d'un manière plus précise en séparant les commandes de la consigne sous la forme:

\begin{align*}
\dot{x}  & =Ax+B_{1}u+B_{2}w\\
y  & =Cx+D_{2}w
\end{align*}

expression dans lesquelles $B_{1}$ et $B_{2}$ sont des matrices formées des colonnes (2,3) et (1) de la matrice $B$, et $D_{2}$ est formée de la colonne (1) de $D.$


### Systèmes non linéaires, linéarisation
Soit un système décrit par les équations d'état non linéaires

\begin{align*}
\dot{x}  & =f(x,u)\\
y  & =h(x,u)
\end{align*}

où $f$ et $h$ sont suffisamment dérivables par rapport à leurs arguments. Supposons qu'il existe une trajectoire nominale (ou d'équilibre) c'est à dire un triplet $x_{e}(t)$, $y_{e}(t)$, et $u_{e}(t)$
qui vérifie:

\begin{align*}
\dot{x}_{e}  & =f(x_{e},u_{e})\\
y_{e}  & =h(x_{e},u_{e})
\end{align*}

Si on suppose de plus que $x(t)$, $y(t)$, et $u(t)$ restent voisins de $x_{e}(t)$, $y_{e}(t)$, et $u_{e}(t)$, on peut **linéariser**  ces équations, c'est à dire fournir une représentation d'état linéaire, valable pour des petits déplacements au voisinage de la trajectoire nominale. On introduit pour cela les écarts

\begin{equation*}
\zeta=x-x_{e},\quad\quad w=u-u_{e},\quad\quad z=y-y_{e}
\end{equation*}

et un développement en série de Taylor au premier ordre fournit

\begin{align*}
\dot{\zeta}  & \simeq A\zeta+Bw\\
z  & \simeq C\zeta+Dw
\end{align*}
expressions dans lesquelles

\begin{equation*}
\fbox{$
\begin{array}
[c]{c}
A=\left(  \dfrac{\partial f_{i}}{\partial x_{j}}\right)  _{|e},\qquad
B=\left(  \dfrac{\partial f_{i}}{\partial u_{j}}\right)  _{|e}\\
C=\left(  \dfrac{\partial h_{i}}{\partial x_{j}}\right)  _{|e},\qquad
D=\left(  \dfrac{\partial h_{i}}{\partial u_{j}}\right)  _{|e}
\end{array}
$}
\end{equation*}


#### Exemple
Pour l'exemple du pendule nous avions obtenu:

\begin{align*}
\dot{x}_{1}  & =f_{1}(x,u)=x_{2}\\
\dot{x}_{2}  & =f_{2}(x,u)=-g\,\sin x_{1}+u/m\\
y  & =h(x,u)=x_{1}%
\end{align*}

Cette équation est bien vérifiée à l'équilibre, i.e. pour la trajectoire $x_{e}(t)\equiv(0,0)^{t}$, $u_{e}(t)\equiv0$. Ainsi, pour de petits déplacements au voisinage de cet équilibre, nous pouvons écrire (ici $\zeta=x,\,w=u,\,z=y)$.

\begin{align*}
\dot{x}  & \simeq\left(\begin{array}{cc}%
\dfrac{\partial f_{1}}{\partial x_{1}} & \dfrac{\partial f_{1}}{\partial x_{2}}\\
\dfrac{\partial f_{2}}{\partial x_{1}} & \dfrac{\partial f}{\partial x_{2}}\end{array}
\right)  _{|e}x+\left(
\begin{array}{c}%
\dfrac{\partial f_{1}}{\partial u}\\\dfrac{\partial f_{2}}{\partial u}%
\end{array}
\right)  _{|e}u\\
y  & \simeq\left(\begin{array}{cc}%
\dfrac{\partial h}{\partial x_{1}} & \dfrac{\partial h}{\partial x_{2}}%
\end{array}
\right)  _{|e}\,x
\end{align*}

Les valeurs des dérivées partielles étant prises à l'équilibre, il vient

\begin{align*}
\dot{x}  & \simeq\left(\begin{array}{cc}%
0 & 1\\-g & 0\end{array}
\right)  x+\left(
\begin{array}{c}%
0\\1/m
\end{array}\right)  u\\
y  & \simeq\left(\begin{array}{cc}%
1 & 0
\end{array}
\right)  \,x
\end{align*}


### Représentation graphique
A l'équation $\dot{x}=(...)$ correspond un intégrateur (vectoriel), ce qui permet de représenter les systèmes linéaires invariants dans le temps, i.e. régis par

\begin{equation*}
\dot{x}(t)=A\,x(t)+B\,u(t)\,\,\, et\,\,\,  y(t)=C\,x(t)+D\,u(t)
\end{equation*}

sous la forme du diagramme fonctionnel suivant où les grandeurs sont vectorielles<br><br>
<center><img src="Figures/Rep-Graph1.svg" width="40%"/></center>


    [NbConvertApp] Converting notebook M1-CH1-Intro.ipynb to html


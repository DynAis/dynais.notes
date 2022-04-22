## Aufgabe 4.4
### a)
**Tor 1 an, Tor 2 aus:**
$$
\begin{aligned}
&r_{1}=\frac{R_{L_{2}}-R_{L 1}}{R_{L 2}+R_{21}}\\
&a_{1}=\frac{u_{1}}{\sqrt{R_{L 1}}}\\
&b_{2}=u_{1}\cdot\left(1+r_{1}\right)/\sqrt{R_{L2}}\\
&S_{12}=\frac{b_{2}}{a_{1}}\\
&S_{12}=\frac{\sqrt{R_{L_{1}}}\left(1+r_{1}\right)}{\sqrt{R_{L 2}}}=\frac{\sqrt{R_{L1} R_{L2}}\left(\frac{2 R_{L2}}{R_{L1}+R_{L2}}\right)}{R_{L 2}}=\frac{2 \sqrt{R_{L2} R_{L1}}}{R_{L2}+R_{L1}}\\
&b_{1}=u_{1} \cdot \frac{r_{1}}{\sqrt{R_{L 1}}}\\
&S_{11}=\frac{b_{1}}{a_{1}}=r_{1}=\frac{R_{L2}-R_{L1}}{R_{L1}+R_{L2}}
\end{aligned}
$$
**Tor 2 an, Tor 1 aus:**
$$
\begin{aligned}
&a_{2}=\frac{u_{2}}{\sqrt{R_{L2}}} \\
&r_{2}=\frac{R_{L1}-R_{L 2}}{R_{L1}+R_{L2}} \\
&b_{2}=u_{2} \cdot \frac{r_{2}}{\sqrt{R_{L2}}} \\
&b_{1}=u_{2}\cdot\left(1+r_{2}\right)/\sqrt{R_{L1}}\\
&S_{21}=\frac{b_{1}}{a_{2}}\\
&S_{21}=\frac{\left(1+r_{2}\right) / \sqrt{R_{L1}}}{\sqrt{R_{L 2}}}=\frac{2 \sqrt{R_{L1} R_{L 2}}}{R_{L1}+R_{L 2}} \\
&S_{22}=\frac{b_{2}}{a_{2}}=r_{2}=\frac{R_{L1}-R_{L2}}{R_{L 1}+R_{L2}}
\end{aligned}
$$

## b)
$$
\begin{aligned}
&S_{11}=\frac{R_{L 2}-R_{L 1}}{R_{L 1}+R_{L 2}}=-r_{1} \\
&S_{22}=\frac{R_{L 1}-R_{L 2}}{R_{L 1}+R_{L 2}}=r_{1} \\
&S_{12}=S_{21}=\frac{2 \sqrt{R_{L 1}+R_{L 2}}}{R_{L 1}+R_{L 2}}=\frac{2 \sqrt{\frac{1+r_1}{1-r_{1}} R_{L 2}^{2}}}{R_{L 2} \cdot \frac{1+r_{1}}{1-r_{1}}+R_{L 2}}=\frac{2 \sqrt{\frac{1+r_{1}}{1-r_{1}}}}{\frac{1+r_{1}}{1-r_{1}}+1} = (1-r_1)\cdot\sqrt{\frac{1+r_{1}}{1-r_{1}}} = \sqrt{1-r_{1}^{2}}
\end{aligned}
$$

## c)
Bei verlustlos Schaltung gibt es:
$$
\begin{aligned}
&\Sigma\left|S_{i j}\right|^{2}=1 \\
\end{aligned}
$$
und für diese Schaltung
$$
\begin{aligned}
&\left|S_{11}\right|^{2}+\left|S_{12}\right|^{2}+\left|S_{21}\right|^{2}+\left|S_{22}\right|^{2}=1 .
\end{aligned}
$$
deshalb diese Schaltung verlustlos ist.


## Aufgabe 4.13
### a)
$$
\left|S_{11}\right|^{2}+\left|S_{12}\right|^{2}+\left|S_{21}\right|^{2}+\left|S_{22}\right|^{2}=1
$$
## b)
**Tor 1 an, Tor 2 aus:**
$$
\begin{aligned}
r_{1} &=\frac{R-R_{L}}{3 R_{L}+R} \\
a_{1} &=u_{1} / \sqrt{2 R_{L}} \\
b_{1} &=u_{1} \cdot r_{1} / \sqrt{2 R_{L}} \\
S_{11} &=\frac{b_{1}}{a_{1}}=r_{1}=\frac{R-R_{L}}{3 R_{L}+R} \\
b_{2} &=u_{1} \cdot\left(1+r_{1}\right) \cdot \frac{R_{L}}{R_{L}+R} / \sqrt{R_{L}} \\
S_{21} &=\frac{b_{2}}{a_{1}}=\frac{R_{L}}{R_{L}+R} \cdot \frac{2 R_{L}+2 R}{3 R_{L}+R} \cdot \frac{\sqrt{2 R_{L}}}{\sqrt{R_{L}}} \\
&=\frac{2 \sqrt{2} R_{L}}{3 R_{L}+R}
\end{aligned}
$$
**Tor 2 an, Tor 1 aus:**
$$
\begin{aligned}
r_{2} &=\frac{R_{2}+R}{3 R_{L}+R} \\
S_{22} &=r_{2}=\frac{R_{2}+R}{3 R_{L}+R} \\
b_{1} &=U_{2}\left(l+r_{2}\right) \cdot \frac{2 R_{2}}{2 R_{L}+R} / \sqrt{2 R_{2}} \\
S_{12} &=\frac{b_{1}}{a_{2}}=\frac{2 R_{L}}{2 R_{L}+R} \cdot \frac{4 R_{L}+2 R}{3 R_{2}+R} \cdot \frac{1}{\sqrt{2}} \\
&=\frac{2 \sqrt{2} R_{2}}{3 R_{L}+R}
\end{aligned}
$$
## c)
Anpassung bedeutet keine Reflextion.
$$
\begin{aligned}
&S_{11} = 0\\
&S_{22} = 0\\
\end{aligned}
$$
Wenn $R=R_L$ , es gibt $S_{11} = 0$. Es gibt Anpassung von Tor 1 zu Tor 2.  
Und $S_{22}$ kann nicht gleich $0$.





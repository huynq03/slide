
# Thiết lập phương trình động học

**Mô hình phẳng $x\!-\!z$** (xem Hình 4 trang 3): đầu vào $u_1$ (lực dọc $b_3$), $u_3$ (mô men quanh $b_2$); góc gripper $\beta$, khoảng cách $L_g$.

1) **Tọa độ tổng quát**
$$
q=\begin{bmatrix}x_q&z_q&\theta&\beta\end{bmatrix}^T
$$

2) **Hình học (gripper từ quadrotor)**
$$
r_g=r_q+L_g\!\begin{bmatrix}\cos\beta\\0\\-\sin\beta\end{bmatrix}
$$

3) **Vận tốc** (lấy đạo hàm theo thời gian)
$$
\dot r_g=\dot r_q+L_g\!\begin{bmatrix}-\sin\beta\,\dot\beta\\0\\-\cos\beta\,\dot\beta\end{bmatrix}
$$

4) **Năng lượng**
$$
V=m_qgz_q+m_ggz_g,\qquad
T=\tfrac12\!\Big(m_q\|\dot r_q\|^2+m_g\|\dot r_g\|^2+J_q\omega_q^2+J_g\omega_g^2\Big)
$$

5) **Lực/tải tổng quát**
$$
F=\begin{bmatrix}u_1\sin\theta\\u_1\cos\theta\\u_3-\tau\\\tau\end{bmatrix}
$$

6) **Euler–Lagrange**
$$
\frac{d}{dt}\frac{\partial (T-V)}{\partial\dot q}-\frac{\partial (T-V)}{\partial q}=F
\;\Rightarrow\;
\ddot q=D^{-1}(F-C\dot q-G)
$$

7) **Các ma trận** (ký hiệu $s=\sin\beta,\; c=\cos\beta$)
$$
D=\begin{bmatrix}
m_g{+}m_q&0&0&-L_gm_g s\\
0&m_g{+}m_q&0&-L_gm_gc\\
0&0&J_q&0\\
- L_gm_g s&- L_gm_gc&0&J_g{+}L_g^2m_g
\end{bmatrix},
\quad
C=\begin{bmatrix}
0&0&0&-L_gm_gc\,\dot\beta\\
0&0&0&\;L_gm_g s\,\dot\beta\\
0&0&0&0\\
0&0&0&0
\end{bmatrix},
\quad
G=\begin{bmatrix}
0\\g(m_g{+}m_q)\\0\\-gL_gm_g c
\end{bmatrix}.
$$

# Từ Euler–Lagrange đến $\ddot q$

**Thiết lập:**  
$q=\begin{bmatrix}x_q & z_q & \theta & \beta\end{bmatrix}^T$,  
$r_g=r_q+L_g\begin{bmatrix}\cos\beta \\ 0 \\ -\sin\beta\end{bmatrix}$  

---

**1) Lagrangian $L=T-V$**

$$
V = m_q g z_q + m_g g z_g
$$

$$
T = \tfrac12\Big( m_q \|\dot r_q\|^2 + m_g \|\dot r_g\|^2 + J_q \dot\theta^2 + J_g \dot\beta^2 \Big)
$$

---

**2) Euler–Lagrange cho từng toạ độ**

$$
\frac{d}{dt}\frac{\partial L}{\partial \dot q_i}
-\frac{\partial L}{\partial q_i}
= Q_i
$$

với  

$$
Q=\begin{bmatrix}
u_1 \sin\theta \\
u_1 \cos\theta \\
u_3 - \tau \\
\tau
\end{bmatrix}
$$

---

**3) Ví dụ với $x_q$:**

$$
\frac{\partial L}{\partial \dot x_q} = (m_q+m_g)\dot x_q - m_g L_g \sin\beta \, \dot\beta
$$

$$
\frac{d}{dt}\frac{\partial L}{\partial \dot x_q}
= (m_q+m_g)\ddot x_q - m_g L_g (\sin\beta \, \ddot\beta + \cos\beta \, \dot\beta^2)
$$

Do $\tfrac{\partial L}{\partial x_q}=0$, ta có:

$$
(m_q+m_g)\ddot x_q - m_g L_g \sin\beta \, \ddot\beta
- m_g L_g \cos\beta \, \dot\beta^2
= u_1 \sin\theta
$$

---

**4) Ví dụ với $z_q$:**

$$
\frac{\partial L}{\partial \dot z_q} = (m_q+m_g)\dot z_q - m_g L_g \cos\beta \, \dot\beta
$$

$$
\frac{d}{dt}\frac{\partial L}{\partial \dot z_q}
= (m_q+m_g)\ddot z_q + m_g L_g \sin\beta \, \dot\beta^2 - m_g L_g \cos\beta \, \ddot\beta
$$

$$
\frac{\partial L}{\partial z_q} = (m_q+m_g) g
$$

Suy ra:

$$
(m_q+m_g)\ddot z_q - m_g L_g \cos\beta \, \ddot\beta
+ m_g L_g \sin\beta \, \dot\beta^2
+ (m_q+m_g) g
= u_1 \cos\theta
$$

---

**5) Hai phương trình còn lại (tóm tắt):**

$$
J_q \ddot\theta = u_3 - \tau
$$

$$
(J_g + m_g L_g^2)\ddot\beta - m_g L_g(\ddot x_q \sin\beta + \ddot z_q \cos\beta)
+ m_g g L_g \cos\beta = \tau
$$

---

**6) Dạng ma trận tổng quát**

$$
D(q)\ddot q + C(q,\dot q)\dot q + G(q) = F
$$

Suy ra:

$$
\ddot q = D^{-1}(F - C\dot q - G)
$$


# Tạo ma trận $D(q)$ và $C(q,\dot q)$ — Quy trình

**1) Chọn toạ độ tổng quát**  
$$
q=\begin{bmatrix}x_q & z_q & \theta & \beta\end{bmatrix}^T
$$

**2) Hình học** (gripper cách $L_g$):  
$$
r_g = r_q + L_g \begin{bmatrix}\cos\beta \\ 0 \\ -\sin\beta\end{bmatrix}, 
\quad \dot r_g = J_g(q)\,\dot q
$$

**3) Năng lượng**  
$$
T = \tfrac12\Big(m_q\|\dot r_q\|^2 + m_g\|\dot r_g\|^2 + J_q \dot\theta^2 + J_g \dot\beta^2\Big)
$$  

$$
V = m_q g z_q + m_g g z_g
$$

**4) Ma trận quán tính**  
$$
T = \tfrac12 \dot q^T D(q) \dot q 
\;\;\Rightarrow\;\;
D_{ij}(q) = \frac{\partial^2 T}{\partial \dot q_i\, \partial \dot q_j}
$$

**5) Trọng lực**  
$$
G_i(q) = \frac{\partial V}{\partial q_i}
$$

**6) Hạng Coriolis/ly tâm**  
Ký hiệu Christoffel:
$$
\Gamma_{ijk}=\tfrac12\!\left(\frac{\partial D_{ij}}{\partial q_k}
+\frac{\partial D_{ik}}{\partial q_j}
-\frac{\partial D_{jk}}{\partial q_i}\right)
$$  

$$
h_i=\sum_{j,k}\Gamma_{ijk}\,\dot q_j\,\dot q_k, 
\quad C(q,\dot q)\dot q = h(q,\dot q)
$$

**7) Phương trình tổng quát**  
$$
D(q)\ddot q + C(q,\dot q)\dot q + G(q) = F
$$

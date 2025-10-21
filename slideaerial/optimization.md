---
marp: true
theme: default
paginate: true
headingDivider: 1
header: "huynq03"
---

# Aerial Perching

**Prepared by:** Huy Quang Nguyen    

**Date:** 10/2025
---

# Optimization for Convex Function

---

## Phần 1: Tối Ưu Hóa (Optimization) là gì?


Tối ưu hóa là quá trình **tìm kiếm phương án tốt nhất** trong số tất cả các lựa chọn khả thi, nhằm mục đích:
* **Tối thiểu hóa (Minimize):** Chi phí, rủi ro, thời gian, sai số.
* **Tối đa hóa (Maximize):** Lợi nhuận, hiệu suất, độ bền.

---

## 3 Thành phần Cốt lõi của Bài toán Tối ưu

Mọi bài toán tối ưu hóa đều được định nghĩa bởi 3 thành phần:

1.  **Biến quyết định (Decision Variables) $x$**
    * Là những thứ bạn có thể kiểm soát hay thay đổi (ví dụ: vị trí con tàu).
2.  **Hàm mục tiêu (Objective Function) $f(x)$**
    * Là thứ bạn muốn tối thiểu/tối đa hóa (ví dụ: `min c^T * x` - đi ngược hướng mưa).
3.  **Ràng buộc (Constraints) $g(x), h(x)$**
    * Là các quy tắc, giới hạn mà $x$ phải tuân theo (ví dụ: $g(x) \le 0$ - phải ở trong vòng tròn an toàn).

---

## Các bài toán 

 
**Bài toán KHÔNG ràng buộc**
* Chỉ cần `min f(x)`.
* *Cách giải:* Đơn giản là đi theo hướng dốc nhất (ngược gradient, $-\nabla f$)..

**Bài toán CÓ ràng buộc**
* `min f(x)` *sao cho* $g(x) \le 0$.
* *Vấn đề:* Thuật toán phải liên tục "kiểm tra" ranh giới, không thể đi tự do.
* *Giải pháp:* Chúng ta cần các phương pháp tinh vi hơn, như dùng Hàm phạt (Penalty) hay KKT.

---

## Chuyển Ràng buộc $\to$ Hàm Phạt (Penalty)

Để biến bài toán "Khó" thành "Dễ" (không ràng buộc), ta dùng "hàm phạt".

**Ý tưởng:** "Bạn được đi bất cứ đâu, nhưng nếu vi phạm ràng buộc (ra khỏi vòng tròn), bạn sẽ bị phạt rất nặng."

**Hàm mục tiêu mới = $f(x) + P(x)$**
(Chi phí gốc + Án phạt)

* Nếu $x$ an toàn: $P(x) = 0$.
* Nếu $x$ vi phạm: $P(x) = +\infty$ (Hình phạt vô hạn).

Thuật toán sẽ *tự động* tránh vùng bị phạt vô hạn.

---

## Nhược điểm của các Hàm Phạt Đơn giản

1.  **Hàm phạt 0/Vô cùng:**
    * Tạo ra một "vách đá" **không liên tục (discontinuous)**.
    * Chúng ta không thể lấy Gradient (la bàn) tại vách đá $\implies$ thuật toán bị hỏng.
2.  **Hàm phạt Tuyến tính $u \cdot g(x)$:**
    * **Liên tục** (Tốt!).
    * *Nhược điểm:* Kết quả tối ưu bây giờ bị **phụ thuộc vào độ dốc $u$** (mức phạt).
    * Nó cũng vô tình tạo ra "phần thưởng" (reward) khi đi quá sâu vào vùng an toàn.

---

## Phần 2: Tính Lồi (Convexity)

* **Tập hợp lồi:** Nếu bạn kẻ một đường thẳng nối 2 điểm bất kỳ, cả đoạn thẳng đó phải nằm bên trong tập hợp (Không có "lỗ" hay "vết lõm").
* **Hàm lồi:** Đồ thị có dạng "cái bát" (luôn cong lên). Vùng *phía trên* đồ thị là một tập hợp lồi.

---

## Tại sao Tính Lồi lại "Ma Thuật"?

Bởi vì nó đảm bảo:
**Mọi Cực tiểu Cục bộ (Local Minimum) cũng là Cực tiểu Toàn cục (Global Minimum).**

* **Bài toán KHÔNG lồi (Núi non):**
    * Bạn có thể bị "mắc kẹt" ở một thung lũng nhỏ (cực tiểu cục bộ) mà không biết có thung lũng sâu hơn ở bên kia.
* **Bài toán LỒI (Cái bát):**
    * Bạn chỉ cần đi "xuống dốc" (theo gradient).
    * Bất kỳ điểm nào bạn dừng lại (đáy cục bộ) **chắc chắn** là điểm thấp nhất duy nhất của cả cái bát (toàn cục).

$\implies$ Các thuật toán sẽ tìm ra nghiệm tốt nhất tuyệt đối.

---

## Định nghĩa Đối ngẫu của Hàm lồi

Một định nghĩa khác (cực kỳ quan trọng) của hàm lồi:

> Một hàm là lồi **khi và chỉ khi** đồ thị của nó luôn nằm **PHÍA TRÊN** tất cả các đường/siêu phẳng tiếp tuyến (tangent) của nó.


---

## Hệ quả của Định nghĩa Tiếp tuyến

Định nghĩa này cho chúng ta một cách giải bài toán *không ràng buộc*:

1.  Nếu hàm $f(x)$ là **lồi**...
2.  ...và nó luôn nằm *trên* tiếp tuyến của nó...
3.  ...thì nếu chúng ta tìm được điểm $x^*$ mà tại đó tiếp tuyến **nằm ngang** (tức là $\nabla f(x^*) = 0$)...
4.  ...thì $x^*$ **chắc chắn** phải là điểm thấp nhất (cực tiểu toàn cục).

**Kết luận:** Đối với hàm lồi, bài toán tối ưu hóa $\min f(x)$ được đưa về bài toán giải phương trình $\nabla f(x) = 0$.

---

## Phần 3: Nguyên lý Đối ngẫu (Principle of Duality)

---

## Primal vs. Dual

**1. Bài toán Gốc (Primal Problem)**
* Là bài toán ban đầu của chúng ta.
* `min f(x)` (Tối thiểu chi phí)
* *sao cho* $g(x) \le 0$ (Tuân thủ ràng buộc).

**2. Bài toán Đối ngẫu (Dual Problem)**
* Là bài toán "bóng" của nó.
* Thường là một bài toán `max`.
* Biến của nó là các "mức phạt" $u$ (biến đối ngẫu).
* `max g(u)` (Tối đa hóa "giá" của ràng buộc).

---

## Đối ngẫu mạnh (Strong Duality)

Giá trị tối ưu của bài toán Dual luôn luôn $\le$ Giá trị tối ưu của bài toán Primal. (Khoảng cách này gọi là Duality Gap).

**Nhưng, khi bài toán là LỒI (Convex):**

Một điều kỳ diệu xảy ra gọi là **Đối ngẫu mạnh (Strong Duality)**:
`Giá trị tối ưu Dual = Giá trị tối ưu Primal`

**Tại sao điều này quan trọng?**
$\implies$ Thay vì giải bài toán Gốc (có thể khó), chúng ta có thể giải bài toán Đối ngẫu (có thể dễ hơn) và vẫn nhận được câu trả lời chính xác cho bài toán Gốc.

---

## Phần 4: Điều kiện KKT



Điều kiện Karush-Kuhn-Tucker (KKT) là **bộ quy tắc vàng** mà một điểm $(x^*, u^*)$ phải thỏa mãn để trở thành nghiệm tối ưu của một bài toán có ràng buộc.

Nó biến bài toán "tìm kiếm" (tối ưu hóa) thành bài toán "giải phương trình" (đại số).

---

## Xây dựng KKT: Hàm Lagrangian

Chúng ta bắt đầu bằng cách kết hợp hàm mục tiêu và hàm ràng buộc lại thành một hàm duy nhất: **Hàm Lagrangian $\mathcal{L}(x, u)$**.

Đây chính là hàm phạt tuyến tính mà chúng ta đã thấy:

**$\mathcal{L}(x, u) = f(x) + u \cdot g(x)$**

* $f(x)$: Chi phí gốc (muốn $\min$).
* $u \cdot g(x)$: Án phạt (muốn $\max$). $u$ là "giá" của vi phạm.

Giải bài toán gốc chính là tìm "điểm cân bằng" (saddle point) của hàm $\mathcal{L}$. Điều kiện KKT mô tả chính xác điểm cân bằng đó.

---

## 4 Điều kiện KKT (Bộ quy tắc)

Một điểm $(x^*, u^*)$ là tối ưu NẾU VÀ CHỈ NẾU nó thỏa mãn 4 điều kiện sau:

### 1. $\nabla_x \mathcal{L}(x^*, u^*) = 0$ (Cân bằng Gradient)
* **Ý nghĩa:** Tại điểm tối ưu, phải có sự cân bằng lực.
* $\nabla f(x^*) + u^* \nabla g(x^*) = 0$ $\implies$ **$\nabla f = -u^* \nabla g$**
* **Trực giác:** Gradient của mục tiêu ($\nabla f$) và gradient của ràng buộc ($\nabla g$) phải **ngược hướng** nhau. Không còn "kẽ hở" nào để lách vào (hai vùng màu vàng và xanh không giao nhau).

---

## 4 Điều kiện KKT (Tiếp theo)

### 2. $g(x^*) \le 0$ (Tính khả thi gốc)
* **Ý nghĩa:** Rất đơn giản. Nghiệm $x^*$ phải tuân thủ ràng buộc ban đầu (phải ở trong vòng tròn).

### 3. $u^* \ge 0$ (Tính khả thi đối ngẫu)
* **Ý nghĩa:** "Mức phạt" $u^*$ phải là số **không âm**.
* **Tại sao?** Nếu $u^*$ âm, nó sẽ trở thành "phần thưởng" (reward) cho việc vi phạm ($g(x) > 0$), làm hỏng toàn bộ bài toán.

---

## 4 Điều kiện KKT (Cuối cùng)

### 4. $u^* \cdot g(x^*) = 0$ (Điều kiện Bù yếu)
Đây là điều kiện thông minh nhất. Nó nói rằng:

**"Tại điểm tối ưu, hoặc là ràng buộc 'dư thừa', hoặc là 'mức phạt' của nó bằng 0."**

* **Case 1: $x^*$ ở BÊN TRONG** (Inactive)
    * $g(x^*) < 0$ (là số âm).
    * $\implies$ Ràng buộc này "dư thừa", không có tác dụng.
    * $\implies$ Để tích bằng 0, **$u^*$ phải bằng 0** (Mức phạt bằng 0).
* **Case 2: $x^*$ ở TRÊN RANH GIỚI** (Active)
    * $g(x^*) = 0$.
    * $\implies$ Ràng buộc này "có hiệu lực" (đang cản nghiệm lại).
    * $\implies$ Tích đã bằng 0, $u^*$ có thể là số dương ($u^* > 0$) để tạo "lực đẩy".
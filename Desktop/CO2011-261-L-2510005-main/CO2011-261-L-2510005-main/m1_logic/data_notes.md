# Data Dictionary & QA Notes (M1)

## 1. Cấu trúc dữ liệu (Data Dictionary)

Dựa trên file Anonymized Dataset, cấu trúc các tham số được ánh xạ như sau:

*   **Sets (Tập hợp):**
    *   **Tập Giám thị (I):** Định danh từ cột `MS của CÁN BỘ COI THI` (VD: CB001, CB002, CB025...).
    *   **Tập Ca thi (J):** Định danh bằng cách kết hợp cột `MS Ca thi` và `Cơ sở` (VD: Ca 20260518_5 tại Cơ sở 1).
    *   **Tập Cơ sở (C):** Lấy từ cột `Cơ sở` (Cơ sở 1, Cơ sở 2).

*   **Baseline (Lịch cơ sở):**
    *   Mỗi dòng trong bảng tính biểu diễn một phân công thực tế đã diễn ra Assign(i, j) = 1.
    *   Ví dụ: Dòng đầu tiên cho biết cán bộ CB001 được phân công vào ca 20260518_5, nhiệm vụ LTK_CBCT tại Cơ sở 1.

*   **Capacity (Sức chứa):**
    *   Xác định bằng cách đếm (count) số dòng có cùng `MS Ca thi` và `Cơ sở`.
    *   *Ví dụ minh họa:* Tại `MS Ca thi` = 20260525_2 ở Cơ sở 2, có tổng cộng 16 giám thị coi thi (CB009 đến CB024) và 1 thư ký (CB025). Vậy sức chứa yêu cầu (Capacity) cho ca này là 17.

*   **Availability (Độ sẵn sàng):**
    *   Lịch cơ sở chỉ ghi nhận các trường hợp giám thị có mặt (rảnh). Việc mô phỏng trạng thái bận/nghỉ phép sẽ được nội suy hoặc sinh ngẫu nhiên thông qua file `seed.txt` theo tài liệu hướng dẫn.

*   **Overlap (Sự trùng lặp):**
    *   Xác định qua cột `Ngày` và `GIỜ`. Hai ca thi có cùng giá trị Ngày, Giờ nhưng khác Cơ sở được xem là Overlap toàn phần.
    *   *Hard constraint:* Giám thị không thể xuất hiện ở 2 dòng có cùng `Ngày` + `GIỜ` mà khác `Cơ sở` (no double-booking).
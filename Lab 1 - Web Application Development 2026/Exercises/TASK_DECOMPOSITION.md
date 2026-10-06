# WORK BREAKDOWN STRUCTURE (WBS) & AI CONTRACT DECOMPOSITION

> **Dự án:** Lab 1 - Modern Web Foundations & AI-Assisted Engineering
> **Sinh viên:** [Nguyen Ha Linh] - [24520963]
> **Quy tắc:** Tuyệt đối không dùng One-Shot Prompting. Mọi sub-task phải được kiểm thử độc lập và đính kèm 1 Atomic Git Commit tương ứng.

---

## 1. Bảng Phân Rã Nhiệm Vụ (WBS Table)

| Task ID | Tên Sub-Task / Thành phần | Hợp đồng Kiến trúc (Contract / Constraints) | Tiêu chí Kiểm thử (Verification Gate) | Git Commit Message Mẫu | Trạng thái |
| :--- | :--- | :--- | :--- | :--- | :---: |
| **T-01** | Semantic DOM & A11y Contract | - 0 thẻ `<div>`<br>- Duy nhất 1 thẻ `<h1>`<br>- Đầy đủ các thẻ Landmark (`<header>`, `<nav>`, `<main>`, `<footer>`)<br>- Có `<a href="#main-content">Skip to content</a>` | Chrome DevTools -> Accessibility -> Kiểm tra Landmark Tree chuẩn WCAG | `feat(html): semantic landmark tree` | DONE |
| **T-02A**| Design Tokens & CSS Reset | - Khai báo CSS Custom Properties trong `:root`<br>- Thêm Universal Box-Sizing Reset (`*, *::before, *::after`)<br>- Không dùng thẻ `<style>` inline | Render đúng hệ màu mặc định, reset margin/padding thành 0 trên mọi trình duyệt | `feat(css): tokens & reset` | DONE |
| **T-03** | Responsive Grid Component | - Dùng CSS Grid 2D (`repeat(auto-fit, minmax(280px, 1fr))`)<br>- Sử dụng `gap` thay cho `margin` trên item con | Kiểm tra hiển thị responsive không bị cuộn ngang tại màn hình 375px (Mobile) | `feat(css): responsive grid` | - |
| **T-04** | Theme Engine & State Persistence | - Lưu trữ trạng thái sáng/tối trong `localStorage` với key `'theme'`<br>- Cập nhật thuộc tính `aria-pressed` trên nút bấm | Chuyển đổi Dark/Light mode mượt mà, giữ nguyên trạng thái khi Refresh trang (F5) | `feat(js): dark mode engine` | - |
| **T-05** | Decoupled Audio Engine | - Tách biệt dữ liệu bằng `data-sound` (hoặc `data-key`) trên HTML<br>- Bắt sự kiện `keydown` dùng `event.key`<br>- Chặn giữ phím bằng `event.repeat` | Không gây giật/trễ âm thanh khi nhấn giữ phím; không bị chồng chéo audio | `feat(js): decoupled audio engine logic` | - |

---

## 2. Chi Tiết Giai Đoạn Phân Rã (4-Stage Decomposition)

### Task T-01: Semantic DOM Architecture & A11y Contract
1. **Functional Slicing:** Dựng khung xương trang web độc lập, chưa áp dụng bất kỳ file CSS hay JS nào.
2. **Contract Definition:**
   * Landmark elements: `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`.
   * Thẻ liên kết bỏ qua: `<a href="#main-content" class="skip-link">`.
3. **Atomic Generation Prompt:**
   > **Nhiệm vụ:** Tạo cấu trúc HTML5 chuẩn ngữ nghĩa cho trang *Developer Portfolio*.
   >
    **Yêu cầu chi tiết:**
    * Không sử dụng bất kỳ thẻ `<div>` nào.
    * Sử dụng đúng các thẻ landmark: `<header>`, `<nav>`, `<main id="main-content">`, và `<footer>`.
    * Chỉ sử dụng duy nhất 1 thẻ `<h1>`.
    * Thêm 1 skip-link ở đầu `<body>`.
4. **Contract Verification:**
   * [x] Mở Chrome DevTools -> Accessibility -> Kiểm tra Landmark Tree.
   * [x] Kiểm tra bằng phím `Tab` để đảm bảo nhận `skip-link` đầu tiên.

---

### Task T-02A: CSS Reset & Design Tokens
1. **Functional Slicing:** Cấu hình hệ thống màu sắc và reset định dạng mặc định của trình duyệt.
2. **Contract Definition:**
   * CSS Variables: `--bg-primary`, `--text-primary`, `--accent`, `--card-bg`.
   * Reset rules: `box-sizing: border-box`, `margin: 0`, `padding: 0`.
3. **Atomic Generation Prompt:**
   > *"Viết file style.css khai báo các CSS Custom Properties trong :root cho 2 chế độ Light/Dark mode và cài đặt bộ reset box-sizing cho tất cả các phần tử (*, *::before, *::after)."*
4. **Contract Verification:**
   * [x] Kiểm tra phần tử trên DevTools xem `box-sizing` đã chuyển thành `border-box`.
   * [x] Đảm bảo không còn lề ẩn mặc định của thẻ `<body>`.

---

## 3. Nhật Ký Commit Git (Atomic Commit Log)

* `commit 1`: `docs(spec): define component contracts & WBS table`
* `commit 2`: `feat(html): semantic landmark tree`
* `commit 3`: `feat(css): tokens & reset`
* `commit 4`: `feat(css): responsive grid`
* `commit 5`: `feat(js): dark mode engine`
* `commit 6`: `feat(js): decoupled audio engine logic`

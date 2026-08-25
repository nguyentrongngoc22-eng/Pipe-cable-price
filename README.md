# PipePrice V5.0 — Kiểm tra giá MEP

Công cụ dự toán và **kiểm tra giá vật tư MEP** chạy hoàn toàn trên trình duyệt, không cần server, không cần cài đặt. Một file HTML duy nhất, không phụ thuộc thư viện ngoài.

> Quy đổi giá **ống thép, phụ kiện thép và cáp điện đồng** từ đơn giá vật liệu thị trường sang giá mục tiêu, rồi so sánh với báo giá nhà thầu.

## Tính năng

- **Tính giá ống thép** theo tiêu chuẩn BS 1387 (Medium/Heavy) và ASME B36.10 (SCH10/20/40/80), quy đổi từ giá thép cuộn sang ống thành phẩm qua hệ số hiệu chỉnh.
- **Tính giá phụ kiện thép** (cút, tê, côn, bích JIS 10K, nắp bịt, coupling…) theo bảng khối lượng DN hoặc ước tính hình học, cộng chi phí chế tạo/sơn mạ.
- **Tính giá cáp điện đồng** (CV/CVV/CXV/CXV-LSHF) theo khối lượng đồng (8,96 g/cm³), cộng vỏ/cách điện, giáp/màn chắn, gia công.
- **Tính giá ống gió tôn kẽm** (chữ nhật W×H hoặc tròn Ø) theo **2 dạng: theo mét dài (đ/m) và theo mét vuông (đ/m²)**; tự chọn chiều dày tôn theo cạnh lớn nhất (SMACNA), quy đổi khối lượng tôn (7,85 kg/m²·mm), cộng gia công, mặt bích/gông/bulông (gắn liền ống → tính vào vật tư), hao hụt, vận chuyển và O&P. **Treo đỡ tách riêng thành chi phí lắp đặt** (chỉ cộng khi báo giá là "vật tư + lắp đặt"), giống cơ chế cấp vật tư / lắp đặt của ống thép.
- **Dự toán BOQ**: gộp nhiều hạng mục, khóa đơn giá mục tiêu theo từng dòng tại thời điểm thêm.
- **Import báo giá Excel `.xlsx`** trực tiếp trong trình duyệt (tự nhận diện cột, không cần thư viện).
- **Xuất CSV**, **in A4**, **sao lưu/khôi phục BOQ** dạng JSON.
- Lưu tự động vào `localStorage`; giao diện tiếng Việt, responsive, hỗ trợ nhập số kiểu Việt/Anh.

## Sử dụng

Mở trực tiếp `index.html` bằng trình duyệt là dùng được ngay. Không cần build, không cần cài gì.

> ⚠️ Chức năng **Import Excel** cần trình duyệt hỗ trợ `DecompressionStream` (Chrome/Edge/Firefox bản mới, Safari 16.4+).

## Đưa lên GitHub Pages

1. Tạo repository mới trên GitHub và tải toàn bộ file trong thư mục này lên (kéo-thả cũng được).
2. Vào **Settings → Pages**.
3. Mục **Source** chọn nhánh `main` (hoặc `master`), thư mục `/ (root)`, rồi **Save**.
4. Chờ vài phút, truy cập địa chỉ dạng `https://<tên-tài-khoản>.github.io/<tên-repo>/`.

Vì `index.html` nằm ở gốc nên GitHub Pages sẽ tự phục vụ.

## Cài đặt lên điện thoại (PWA)

App hỗ trợ cài như ứng dụng (biểu tượng ngoài màn hình chính, chạy toàn màn hình, dùng offline). **Bắt buộc mở qua địa chỉ GitHub Pages (HTTPS) — không cài được khi mở file trực tiếp trên máy.**

- **Android (Chrome):** mở link Pages → menu ⋮ → **Cài đặt ứng dụng / Thêm vào màn hình chính**.
- **iPhone (Safari):** mở link Pages → nút **Chia sẻ** → **Thêm vào màn hình chính**.

Thành phần PWA đi kèm: `manifest.webmanifest`, `sw.js` (service worker, cache offline), `icon-192.png`, `icon-512.png`. Tất cả để phẳng cùng thư mục với `index.html`.

> Khi cập nhật app, đổi số `CACHE` trong `sw.js` (ví dụ `pipeprice-v5-1`) để trình duyệt tải lại bản mới.

## Cơ sở dữ liệu quy cách

- Ống: `W = 0,02466 × t × (D − t)` — BS 1387 / EN 10255, ASME B36.10M
- Cáp: `kg Cu/m = 0,00896 × S × số lõi × hệ số bện` — khối lượng riêng đồng 8,96 g/cm³
- Ống gió: diện tích bề mặt chữ nhật `= 2 × (W + H)`, ống tròn `= π × Ø` (m²/m); khối lượng tôn `= chiều dày(mm) × 7,85` (kg/m²); chiều dày theo cạnh lớn nhất: ≤750 → 0,6 · ≤1200 → 0,8 · ≤1800 → 1,0 · >1800 → 1,2 (mm)

> Khối lượng và giá là dự toán lý thuyết. Vật liệu, dung sai, cấu tạo và vận chuyển cần xác nhận theo báo giá nhà cung cấp thực tế.

## Tác giả

Phát triển bởi **Nguyễn Trọng Ngọc**.

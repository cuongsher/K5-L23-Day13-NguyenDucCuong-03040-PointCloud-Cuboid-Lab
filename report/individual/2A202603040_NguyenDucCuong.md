# Báo cáo Day 13 — Nguyễn Đức Cường, 2A202603040

## 1. Kết luận trước
2A202603040 Nguyễn Đức Cường, task `D13-2A202603040`, 10 frame: s01f00, s01f44, s02f06, s02f24, s03f16, s03f34, s04f22, s04f51, s05f04, s05f48. Windows 11, Chrome, CVAT 2.74.1, Ngồi cạnh: 2A202603240

Bảng A có 77 cuboid (s01f00 = 11, s01f44 = 11, s02f06 = 8, s02f24 = 7, s03f16 = 6, s03f34 = 5, s04f22 = 12, s04f51 = 6, s05f04 = 6, s05f48 = 5); frame ít nhất là s03f34 và s05f48 (5 cuboid). `selfcheck` còn cờ 2/77 cuboid (s01f00 idx 3, s01f44 idx 9).

Phần tin nhất là đáy cuboid
Phần yếu nhất là kích thước và hướng của một số hộp

## 2. Đọc frame (Bước 2)
Hai frame đọc kỹ. Ảnh: `t1-s01f00-3d.png`, `t1-s01f00-top.png`, `t1-s01f44-3d.png`, `t1-s01f44-top.png`.

| Frame | Phía trước xe ở cạnh nào của ảnh nhìn từ trên xuống; +x, +y chỉ về đâu | Mặt đường (phẳng/dốc; thấp hơn LiDAR ~ m) | Vật xa nhất đọc được (~ m) | Loại vật thấy | Vật phía sau / hai bên | Cụm chưa đọc được |
|---|---|---|---|---|---|---|
| s01f00 | | Thấp hơn LiDAR ~1,8 m (z đáy trung vị −1,84 m); nhóm xe ở ~40 m phía trước bên trái có z đáy −2,2 đến −2,3 m, nên đường thấp dần về phía đó | ~41 m (xe con, idx 7) | Xe con (11 cuboid) | Phía sau: 5 xe con ở 10–34 m (idx 2, 3, 4, 5, 11); bên trái: 1 xe con ở 3,3 m (idx 1) | |
| s01f44 | | Thấp hơn LiDAR ~1,8 m (z đáy trung vị −1,77 m), gần như phẳng trong 30 m | ~35 m (xe con, idx 9) | Xe con (11 cuboid) | Phía sau: 2 xe con ở 13 m và 27 m (idx 5, 6); bên trái: 1 xe con ở 6,6 m (idx 4) | |

3 điều chỉ camera cho biết:

3 điều chỉ LiDAR cho biết: khoảng cách thật tới từng xe (ví dụ xe gần nhất ở s01f00 cách 3,34 m); kích thước theo mét (xe con ~5,0 × 1,9 × 1,6 m); độ cao mặt đường so với cảm biến (~−1,8 m) và các vật ở phía sau xe, ngoài vùng nhìn của cam01.

Tám frame lướt:

| Frame | Phía trước ở cạnh nào của ảnh nhìn từ trên xuống | Điều lạ (nếu có) |
|---|---|---|
| s02f06 | | |
| s02f24 | | |
| s03f16 | | |
| s03f34 | | |
| s04f22 | | |
| s04f51 | | |
| s05f04 | | |
| s05f48 | | |

## 3. Ba cuboid có hướng dẫn (Bước 3)
Ảnh: `t2-a-car.png`, `t2-b-bus-truck.png`, `t2-c-ped-cyclist.png`.

| Vật | Frame, idx | Class | Mũi tên yaw đúng hướng? | Đáy chạm đường? | Đã kiểm Top/Side/Front + ảnh? | Kích thước trong bảng 4.3? |
|---|---|---|---|---|---|---|
| (a) xe con gần | s01f00, idx 1 | Car | | Có: khoảng hở 0,00 m (z đáy −1,845 m) | | 5,000 × 1,900 × 1,600 m; sedan 3,8–5,0 × 1,70–1,90 × 1,40–1,60 m: cả 3 chiều nằm ở cận trên |
| (b) xe buýt hoặc xe tải | s02f06, idx 2 | Bus | | Có: khoảng hở 0,15 m (z đáy −1,912 m) | | 11,147 × 3,034 × 3,203 m; xe buýt thường 10,0–12,5 × 2,50–2,60 × 3,00–3,50 m: rộng 3,034 m vượt khoảng |
| (c) người đi bộ hoặc xe hai bánh | s03f34, idx 2 | Pedestrian | | Có: khoảng hở 0,00 m (z đáy −1,760 m) | | 0,900 × 0,820 × 1,529 m; người lớn 0,4–0,9 × 0,5–0,9 × 1,50–1,95 m: trong khoảng |

Vòng hiệu chuẩn: không tham gia (task chung không có cuboid nào của tôi).

Vật bỏ qua vì không đủ cơ sở:

## 4. Bốn hiện tượng chất lượng (Bước 4)
Nguyên nhân ghi là **giả thuyết**. Frame mượn thì ghi rõ nguồn: task chung, hoặc MSSV của bạn cho mượn.

| Hiện tượng | Frame / tên ảnh / nguồn | Nguyên nhân (giả thuyết) | Thấy gì trên point cloud | Hệ quả khi gán (theo guideline) |
|---|---|---|---|---|
| 1. Bóng che | | | | |
| 2. Thưa ở xa | | | | |
| 3. Phản xạ thấp / ít điểm bất thường | | | | |
| 4. Điểm lạ | | | | |

## 5. Số từ cuboid của tôi (Bước 5)
Lấy từ `submission/D13-2A202603040-bangA.csv`; số điểm lấy từ cột `points_in` của `-tukiem.csv`. Mặt đường khoảng −1,7 m: z đáy lệch hơn 0,3 m là lơ lửng hoặc chìm.

| Cuboid (frame, idx, class) | z | h | z đáy = z − h/2 | dist_m | r = √(x²+y²+z²) | yaw_deg | Nhận xét (lơ lửng / chìm / chạm đường) |
|---|---|---|---|---|---|---|---|
| s01f00, 1, Car | −1,045 m | 1,600 m | −1,845 m | 3,34 m | 3,50 m | 270,0° | Chạm đường: lệch 0,15 m so với −1,7 m, khoảng hở với mặt đất tại chỗ 0,00 m |
| s01f44, 1, Car | −0,979 m | 1,512 m | −1,735 m | 10,92 m | 10,96 m | 269,3° | Chạm đường: lệch 0,04 m, khoảng hở 0,05 m |
| s01f00, 9, Car | −1,546 m | 1,600 m | −2,346 m | 40,20 m | 40,23 m | 89,2° | Lệch 0,65 m so với −1,7 m nhưng khoảng hở với mặt đất tại chỗ chỉ −0,13 m: mặt đường ở ~40 m thấp hơn, hộp hơi chìm 0,13 m, vẫn trong ngưỡng 0,3 m |

(a) Gần nhất: s03f16 idx 4 (Truck), `dist_m` = 2,84 m, r = 2,93 m. Xa nhất trong vùng chấm (≤ 50 m): s02f06 idx 4 (Car), `dist_m` = 45,13 m, r = 45,14 m. Xa nhất trong bảng A: s05f48 idx 5 (Car), `dist_m` = 143,63 m, r = 143,63 m (> 50 m, không được chấm).

(b) Người đi bộ s03f34 idx 2: 0,900 × 0,820 × 1,529 m, so với người lớn 0,4–0,9 × 0,5–0,9 × 1,50–1,95 m. Xe con s01f00 idx 1: 5,000 × 1,900 × 1,600 m, so với sedan 3,8–5,0 × 1,70–1,90 × 1,40–1,60 m. Người đi bộ có cả 3 chiều trong khoảng, nhưng dài 0,90 m và rộng 0,82 m sát cận trên, nên hộp có thể hơi rộng so với cụm điểm. Xe con có cả 3 chiều đúng bằng cận trên của sedan vì đây là kích thước mặc định, chưa chỉnh theo cụm điểm; nếu xe thật là sedan ngắn hơn thì dài 5,0 m là dư.

(c) Xe cùng chiều phía trước: s01f44 idx 1, `yaw_deg` = 269,3° (az_deg = 0,4°, ngay phía trước), gần 270° như kỳ vọng. Xe có hướng ngược lại ở phía trước: s04f22 idx 3, `yaw_deg` = 86,7° (az_deg = 58,3°), gần 90° (lệch 3,3°).

Mật độ theo khoảng cách (4 cuboid ở các `dist_m` khác nhau):

| Cuboid (frame, idx, class) | dist_m | Số điểm (`points_in`) |
|---|---|---|
| s05f04, 3, Car | 3,29 m | 5664 |
| s04f22, 12, Car | 14,53 m | 1239 |
| s02f06, 7, Car | 21,76 m | 276 |
| s01f00, 7, Car | 40,65 m | 108 |

Xa gấp ~4,4 lần (3,3 m → 14,5 m) thì số điểm còn ~1/4,6 (5664 → 1239); xa thêm ~2,8 lần (14,5 m → 40,7 m) thì còn ~1/11 (1239 → 108). Số điểm giảm nhanh hơn tỉ lệ với khoảng cách, cùng xu hướng với đường cong ở slide (1968 → 718 → 214 → 72 điểm từ 0–10 m tới 30–40 m). Số của tôi cao hơn trung vị slide ở mọi mức; giả thuyết: các xe được chọn đều ở gần làn, không bị che.

Tự kiểm: `selfcheck` cờ 2/77 cuboid: s01f00 idx 3 (ground_gap = 0,33 m; 204 điểm sát ngay ngoài mép) và s01f44 idx 9 (height = 2,40 m, ngoài khoảng 1,2–2,3 m của Car).

Hai cuboid đã sửa:

Đổi kiểm với 2A202603240:

## 6. Ý nghĩa của nhãn, cách dùng AI và điều còn chưa chắc
(a) Model 3D học vị trí và kích thước thật của vật để xe tính khoảng cách an toàn và lập đường đi, nên nhãn phải đo bằng mét trong hệ LiDAR

(b) Dùng AI (đã được lab coach cho phép):
- Công cụ: Claude Code (trợ lý lập trình).
- Câu hỏi chính: cài môi trường, chạy lệnh lab, sắp xếp dữ liệu; cách lọc bảng A bằng Excel

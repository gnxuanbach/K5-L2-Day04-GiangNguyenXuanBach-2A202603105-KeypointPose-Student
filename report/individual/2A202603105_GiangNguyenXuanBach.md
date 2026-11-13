# Báo cáo cá nhân — GiangNguyenXuanBach-2A202603105

Đổi tên file theo quy tắc `MSSV_HoTen.md`. Ví dụ: `20241234_NguyenVanAn.md`.

Dữ liệu: 12 ảnh người COCO val2017 (Lin et al., 2014) và 8 ảnh chân dung Wikimedia Commons, chỉ dùng trong lớp.

## 0. Thông tin học viên

- Họ tên:GiangNguyenXuanBach
- MSSV:2A202603105
- Email:gnxuanbach@gmail.com
- Link repository:https://github.com/gnxuanbach/K5-L2-Day04-GiangNguyenXuanBach-2A202603105-KeypointPose-Student
- Phiên bản CVAT (Help → About):2.74.1
- Máy: hệ điều hành Windows · RAM 8 GB · chạy CVAT chế độ lite
- Bộ ảnh (`src/exports/assignment.json` do `lab.py setup` tạo): có 
- Giờ bắt đầu: 16:30 12/11/2026
- Giờ kết thúc:8:30 13/11/2026

## 1. Kiểm tra label (CP0)

| Label | Kiểu | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
|---|---|---:|---|---|---:|
| `person` | person | 17 |có |có |19 |
| `face` |face | 13 |có | có| 13|

Mẫu `person` dựng theo người quay mặt về camera (các điểm `left_*` nằm bên phải khung mẫu)? Có 

Cách đổi cờ `occluded` / `outside` cho **một điểm** trên phiên bản CVAT này (một câu):
nhấn chuột vào điểm đó rồi nhấn q để gán cờ occluded, o để gán cờ outside 

## 2. Số lượng đã gán và thời gian (CP1, CP2)

| Nhóm ảnh | Số ảnh | Số skeleton đã gán | Số người dưới 60 px (không gán) | Số poster / gương / màn hình bỏ qua | Thời gian (phút) |
|---|---:|---:|---:|---:|---:|
| `easy` | 5 |5 |0 | 0|25 |
| `occluded` | 3 |6 |0 | 0| 18|
| `back` | 2 |4 |0 |0 |15 |
| `small` | 1 | 3| 0|0 | 7|
| `crowd` | 1 |3 |0 |0 |15 |
| `faces` | 8 | 8| — | 0| 25|

- Số ảnh người đã xong ở mốc phút 105: 10 / 10
- Thời gian thực tế (phút): CP1 93 · CP2 25 · CP3 25
- Ảnh tốn thời gian nhất là ảnh nào, vì sao?
là ảnh 413160.jpg vì ảnh này có đến tận 3 người, trong đó có 2 người bị occluded gần nửa người


## 3. Bảng ca khó (CP1, CP2)

Mỗi điểm bạn phân vân một dòng, nhất là phân vân giữa `v = 1` và `v = 0`, hoặc không chắc hướng người.

| Ảnh | Người / mặt | Điểm | Cờ đã chọn | Phân vân giữa | Lý do chọn |
|---|---|---|---:|---|---|
|000000297227.jpg | người #1 | nose, left_eye, right_eye| 0| v = 1 và v = 0| Người quay lưng về phía camera, hoàn toàn không thấy ngũ quan, chọn v = 0 vì không đoán được chính xác vị trí|
|000000106051.jpg |người #2 | right_wrist| 1| v = 1 và v = 0|Cổ tay bị mép áo che một phần nhưng thấy cẳng tay và bàn tay, ước lượng được |
| 000000147780.jpg|người #2 |left_knee, left_hip, right_knee, right_hip |1 | v = 1 và v = 0|Người ngồi trên xe, bị ngựa che phần hông và đùi, nhưng vẫn thấy cổ chân, ngồi thẳng có thể đoán vị trí hip rồi cùng ankle suy ra knee |

## 4. Bảng tự review (CP3)

Đi từ ảnh cuối về ảnh đầu. 5 ảnh người (ít nhất 2 ảnh `back` hoặc `crowd`) và 3 ảnh mặt. Ít nhất 8 dòng, kể cả dòng `ok`. Ghi lỗi trước, sửa sau.

Mã lỗi dùng đúng một trong: `lr_swap`, `vis_flag`, `position`, `missing`, `extra`, `ok`.

| Ảnh | Người / mặt | Điểm | Mã lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|---|
|000000351176.jpg | người #1 |toàn thân |lr_swap |người quay lưng, ban đầu kéo skeleton bị nhầm bên trái/phải |đã sửa |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |

Tổng hợp số lỗi theo mã:

| `lr_swap` | `vis_flag` | `position` | `missing` | `extra` | `ok` |
|---:|---:|---:|---:|---:|---:|
|1 | 0|0 |0 | 0| 0|

Điểm còn phân vân giữa `v = 1` và `v = 0` (ghi cả hai lựa chọn và lý do chọn):

...

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)

Tự kiểm tay trong file JSON:

| File | Người / mặt kiểm (ảnh, thứ tự) | Số phần tử `keypoints` | Điểm `outside` ra `v = 0`, `occluded` ra `v = 1`? | `num_keypoints` khớp? |
|---|---|---:|---|---|
| `GiangNguyenXuanBach_persons.zip` | 000000413160.jpg #3, id 2|51 |Đúng, 10 điểm v = 0, 3 điểm v = 1 | Khớp|
| `GiangNguyenXuanBach_persons.zip` |000000147780.jpg #1, id 5 | 51|2 điểm v = 0, 4 điểm v = 1 |Khớp |
| `GiangNguyenXuanBach_faces.zip` |face_219250.jpg #1, id 4| |39 |có 8 điểm v = 1 do kính râm |Khớp |

Sau khi xuất, CVAT ghi `occluded` thành `v = 1` và `outside` thành `v = 0`. Tọa độ của điểm `outside` trong file là `0, 0` hay tọa độ cũ? tọa độ cũ

Hai job đã chuyển sang completed trên CVAT? Có

Dán phần **TÓM TẮT** in ra từ `src/check_submission.py`:

```text
----- TÓM TẮT (dán vào báo cáo mục 5) -----
- File person: GiangNguyenXuanBach_persons.zip
  Số ảnh: 12 · số skeleton `person`: 21 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000019754=1, 000000106051=3, 000000147780=2, 000000175703=1, 000000220045=2, 000000297227=2, 000000308257=1, 000000343057=1, 000000349521=1, 000000351176=2, 000000360811=2, 000000413160=3
  Cờ v: v=2 219 (61%) · v=1 93 (26%) · v=0 45 (13%)
  num_keypoints trung bình: 14.9
- File face: GiangNguyenXuanBach_faces.zip
  Số ảnh: 8 · số skeleton `face`: 8 · mỗi annotation 39 số
  Skeleton theo ảnh: face_125051=1, face_175798=1, face_178208=1, face_219250=1, face_257657=1, face_415073=1, face_421231=1, face_449454=1
  Cờ v: v=2 96 (92%) · v=1 8 (8%) · v=0 0 (0%)
  num_keypoints trung bình: 13.0
- Ghi chú: 45 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.
- Số [LỖI]: 0 · số [CẢNH BÁO]: 3
Kết quả: ĐẠT (đọc lại từng cảnh báo ở trên)
```

Các `[CẢNH BÁO]` còn giữ nguyên và lý do:

  [CẢNH BÁO] 000000019754.jpg #1: cặp wrist nằm ngược phía so với các cặp còn lại. Có thể đổi trái/phải một cặp (`lr_swap`), hoặc tay / chân bắt chéo thật: kiểm lại. Giữ nguyên: người trong ảnh có pose khá phức tạp, không phải lỗi lr_swap
  [CẢNH BÁO] 000000308257.jpg #1: cặp ankle nằm ngược phía so với các cặp còn lại. Có thể đổi trái/phải một cặp (`lr_swap`), hoặc tay / chân bắt chéo thật: kiểm lại. Giữ nguyên: Tư thế người đang vắt chéo chân sang bên, ngồi khoanh chân hông phải lỗi lr_swap 
  [CẢNH BÁO] 000000343057.jpg #1: cặp hip, knee, ankle nằm ngược phía so với các cặp còn lại. Có thể đổi trái/phải một cặp (`lr_swap`), hoặc tay / chân bắt chéo thật: kiểm lại. Như trên

## 6. Ảnh chụp màn hình

1. Label `person` trong label constructor (đủ 17 điểm có tên):

   ![Label person](images/1_label_person.png)

2. Một người quay lưng đã gán, cờ đã đặt:

   ![Người quay lưng](images/2_nguoi_quay_lung.png)

3. Một khuôn mặt đã gán 13 điểm, phóng to vùng mắt:

   ![Khuôn mặt phóng to](images/3_mat_phong_to.png)

4. Một đoạn JSON xuất của một người:

   ![JSON export](images/4_json_export.png)

Nguồn ảnh: COCO val2017 / Wikimedia Commons.

## 7. Tự đánh giá

1. Lỗi bạn mắc nhiều nhất hôm nay, và cách bạn sẽ tránh ở dự án thật:

   Lỗi khi nhầm giữa bên trái và phải khi người quay lưng lại, đã tự khắc phục và rút kinh nghiệm khi làm bài

2. Một quy tắc bạn đề xuất thêm vào guideline (kèm ảnh ví dụ nếu có):

	không có

3. Nhãn của bạn đi vào model ở đâu? Chọn một lỗi bạn đã sửa và nói nó sẽ làm model học sai thế nào (heatmap, trọng số trong loss, hay bước lật ảnh):

   ...

## 8. Khó khăn và lỗi kỹ thuật

	gặp người quay lưng phải đảo ngược skeleton mà cvat không có chức năng swap trái phải nhanh

## Bonus (nếu làm)

### B1 — 3 ảnh người khó thêm

| Ảnh | Số skeleton | Số người dưới 60 px | Ca khó nhất |
|---|---:|---:|---|
| 000000337458.jpg|3 |0 |người bên trái đứng chéo người, bị occluded |
| 000000357549.jpg| 3| 0| người bên phải ngoài cùng, bị occluded gần nửa người|
|000000373426.jpg|3 | 0| người ở giữa đang ngồi, pose khó, bị occluded 1 phần |

Kết quả `src/check_submission.py` cho `HoVaTen_bonus_persons.zip`:

```text
(dán ở đây)
```

### B2 — 5 ảnh khuôn mặt đen trắng / hồng ngoại

Ảnh không màu khó hơn ở điểm nào? Kính râm trên ảnh hồng ngoại có còn là `v = 1` không?

Ảnh không màu ở các hình có bóng tối khó định vị chính xác các điểm mắt hơn, đặc biệt ở vùng hốc mắt có bóng đổ,Tia hồng ngoại có khả năng xuyên qua tròng kính râm tối màu nên mắt là `v=2` vì có thể nhìn được

### B3 — Model so với nhãn của tôi (không tính điểm) Không dùng

- Demo đã dùng: 
- Ảnh đã thử:

1. Model có trả điểm cho khớp bị che, hay khớp ngoài ảnh không? Confidence ở các điểm đó thế nào?

   ...

2. Với người quay lưng, model có đổi trái/phải không?

   ...

3. Bộ điểm của model có giống 17 điểm COCO không?

   ...

## 9. Tài liệu tham khảo và công cụ AI đã dùng
Hướng dẫn thực hành Lab Ngày 4

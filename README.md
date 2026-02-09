# Lịch Âm Dương Việt Nam (Enhanced) – Home Assistant Custom Card

[![HACS](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://hacs.xyz/)
![Version](https://img.shields.io/badge/version-2.3-blue.svg)

Thẻ (custom card) hiển thị **lịch Dương / Âm Việt Nam** theo kiểu “lịch bloc” truyền thống, kèm Can Chi – Giờ Hoàng Đạo – Tiết khí – Ngày lễ… và popup xem chi tiết.

> Card name: `custom:lich-am-duong-card` (element: `lich-am-duong-card`).  
> Phiên bản trong file JS: **2.3 (Feb 2026)** – tự thích ứng màu chữ theo theme sáng/tối.  

---

## ✨ Tính năng chính

- **Dương lịch**
  - Ngày / tháng / năm, thứ trong tuần (Tiếng Việt)
  - **Ngày lễ dương lịch** (VN & quốc tế)

- **Âm lịch**
  - Ngày / tháng (tên tháng âm) / năm âm
  - **Can Chi** (ngày – tháng – năm)
  - **12 con giáp** kèm emoji
  - **Giờ Hoàng Đạo**
  - **Tiết khí**
  - **Ngày lễ âm lịch** (Tết, Rằm, Vu Lan, Trung Thu…)

- **Tương tác**
  - Nút **lùi/tiến ngày**, **về hôm nay**
  - **Chọn ngày** (chuyển nhập theo dương hoặc âm rồi kích vào xem ngày này)
  - **Bấm vào ngày dương lịch** để mở **popup chi tiết** (nên làm/kiêng cữ, sao, ngày lễ…)

- **Giao diện**
  - Hỗ trợ **background normal / transparent**
  - Tuỳ chỉnh **độ trong suốt nền**
  - Tuỳ chỉnh **viền** (màu/độ dày/glow)
  - **Tự thích ứng màu** theo theme sáng/tối của Home Assistant
- **Giao diện trong suốt**
  **<img width="423" height="567" alt="image" src="https://github.com/user-attachments/assets/27c2346c-399b-4c8c-ba0c-5260708c9d91" />**
- **Giao diện normal**
  **<img width="417" height="557" alt="image" src="https://github.com/user-attachments/assets/023e485d-cfeb-4d8b-8459-eae49c4bf066" />**
- **Giao diện popup**
  <img width="413" height="549" alt="image" src="https://github.com/user-attachments/assets/d1f09b1c-40e1-4e92-a48a-95767b705021" />


---

## ✅ Yêu cầu

- Home Assistant có **Lovelace Dashboards**.
- Cài theo dạng **Resource (JavaScript module)** hoặc qua **HACS (Custom repository)**.

---

## 📦 Cài đặt

### Cách 1: Cài thủ công (khuyến nghị khi test nhanh)

1. Copy file `lich-block-am-duong.js` vào:
   - `config/www/lich-block-am-duong.js`
2. Vào **Settings → Dashboards → Resources** (hoặc *Cài đặt → Bảng điều khiển → Tài nguyên*)
3. **Add resource**
   - URL: `/local/lich-block-am-duong.js`
   - Type: **JavaScript Module**
4. Reload trình duyệt (Ctrl+F5) hoặc restart Home Assistant nếu cần.

### Cách 2: Cài qua HACS (Custom repository)

1. Vào **HACS → 3 Chấm góc trên bên phải (⋮) → Custom repositories**
2. Thêm repo của bạn (ví dụ): `https://github.com/TriTue2011/am-lich-lunar`
3. Chọn Category: **Dashboard**
4. Quay lại HACS, tìm `Block Âm Dương Việt Nam` và **Download**
5. Reload trình duyệt (Ctrl+F5)
<img width="1077" height="637" alt="image" src="https://github.com/user-attachments/assets/0557b60a-db5b-42ec-8d96-785aaf00b13a" />
<img width="561" height="459" alt="image" src="https://github.com/user-attachments/assets/28f74186-0a9d-4598-b3ce-98ccbf6cc596" />
<img width="1091" height="495" alt="image" src="https://github.com/user-attachments/assets/db48124c-ac9b-4cbe-8c9a-b565e0cb0c28" />

---

## 🧩 Cấu hình (Lovelace)

### Cấu hình tối thiểu

```yaml
type: custom:lich-am-duong-card
```

### Ví dụ nền thường + quote từ sensor

```yaml
type: custom:lich-am-duong-card
background: normal
quote_entity: sensor.daily_quote
```

### Ví dụ nền trong suốt + opacity

```yaml
type: custom:lich-am-duong-card
background: transparent
background_opacity: 0.3  # 0.0 → 1.0
quote_entity: sensor.daily_quote  # (tuỳ chọn)
```
### Ví dụ nền trong suốt full option

```yaml
type: custom:lich-am-duong-card
background: transparent
background_opacity: 1
quote_entity: input_text.daily_quote
border_color: rgba(255, 140, 0, 0.8)
border_width: 3
border_glow: true
```
### Tùy chọn nâng cao (theo `getStubConfig()`)

| Tuỳ chọn | Kiểu | Mặc định | Mô tả |
|---|---:|---:|---|
| `background` | string | `normal` | `normal` hoặc `transparent` |
| `background_opacity` | number | `0` | Độ trong suốt nền (0–1) |
| `quote_entity` | string | `""` | Entity chứa câu quote (state/attributes tuỳ sensor) |
| `border_color` | string | `""` | Màu viền (vd `#7b1fa2`) |
| `border_width` | number | `0` | Độ dày viền (px) |
| `border_glow` | boolean | `true` | Bật/tắt hiệu ứng glow của viền |

> Nếu `quote_entity` trống, card sẽ dùng bộ quote mặc định trong file JS.

---
## HƯỚNG DẪN TẠO input_text.daily_quote TRONG HOME ASSISTANT

### CÁCH 1: TẠO TRONG GIAO DIỆN (KHUYẾN NGHỊ)

Bước 1: Vào Settings → Devices & Services → Helpers
Bước 2: Nhấn “Create Helper”
Bước 3: Chọn loại “Text”
Bước 4: Nhập thông tin: - Name: Daily Quote - Entity ID:
input_text.daily_quote - Maximum length: 255 hoặc 500
Bước 5: Nhấn Save


### CÁCH 2: KHAI BÁO TRONG configuration.yaml

Thêm đoạn sau vào file configuration.yaml:
```yaml
input_text:
  daily_quote:
    name: Daily Quote
    max: 500
```

Sau đó Restart Home Assistant.
## 🛠️ Troubleshooting

- **Không thấy card / báo “Custom element doesn't exist”**
  - Kiểm tra đã add Resource đúng URL `/local/lich-block-am-duong.js`
  - Kiểm tra Resource type là **JavaScript Module**
  - Ctrl+F5 để xóa cache (đặc biệt khi bạn vừa cập nhật file JS)

- **Cập nhật version mà không đổi**
  - Trình duyệt còn cache: Ctrl+F5 hoặc mở tab ẩn danh để test
  - Nếu dùng HACS: update trong HACS rồi reload

---
## Automation dùng ai tự động tìm câu châm ngôn, danh ngôn, tục ngữ, ca dao
```yaml
alias: AI Quote (mỗi 1 giờ)
description: >-
  Mỗi 1 giờ lấy 1 câu nói nổi tiếng ngẫu nhiên và cập nhật vào
  input_text.daily_quote
triggers:
  - minutes: /20
    trigger: time_pattern
actions:
  - action: ai_task.generate_data
    data:
      task_name: quote
      entity_id: ai_task.benbap2011_ai_task_script
      instructions: >
        Hãy chọn ngẫu nhiên 1 câu châm ngôn, danh ngôn nổi tiếng từ một quốc gia
        bất kỳ trên thế giới, ca dao, tục ngữ Việt Nam, .

        Yêu cầu: 

        - Ưu tiên đa dạng quốc gia và tác giả, tránh lặp lại các nhân vật quá
        phổ biến. 

        - Nếu câu có tác giả xác định thì ghi rõ tác giả là ai. Nếu câu không có
        tác giả xác định thì tác giả là thể loại danh ngôn hay châm ngôn hay ca
        dao hay tục ngữ . 

        - Viết tiếng Việt, có đầy đủ dấu.

        - Không emoji, không xuống dòng.
      structure:
        quote:
          description: câu nói nổi tiếng
          required: true
          selector:
            text: null
        author:
          description: tác giả
          required: true
          selector:
            text: null
    response_variable: quote_result
  - wait_template: |
      {{ quote_result is defined and quote_result.data is defined
         and quote_result.data.quote is defined and quote_result.data.author is defined }}
    timeout: "00:01:00"
    continue_on_timeout: true
  - if:
      - condition: template
        value_template: "{{ wait.completed }}"
    then:
      - action: input_text.set_value
        target:
          entity_id: input_text.daily_quote
        data:
          value: >-
            {{ quote_result.data.quote | trim }} - ({{ quote_result.data.author
            | trim }})
    else:
      - stop: AI Task không trả kết quả kịp thời
mode: single

```
## 🙏 Credits

- Phát triển dựa trên code của **Nguyễn Tiến Khải** (đã được ghi chú trong file JS).
- Bản Enhanced: tối ưu UI, bổ sung tương tác & tự thích ứng theme.

---

## 📄 License

MIT License (xem file `LICENSE`).


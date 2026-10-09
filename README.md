
### Phân tích lỗi

* **Dòng lỗi:** `const basePrice = bookingReservation.priceKey;`
* **Nguyên nhân:** Dot notation (`.priceKey`) tìm thuộc tính tên là `"priceKey"` (không tồn tại $\rightarrow$ trả về `undefined`) thay vì lấy giá trị của biến `priceKey` (`"roomPrice"`). Đúng phải dùng Bracket notation: `bookingReservation[priceKey]`.
* **Hậu quả:** `basePrice` là `undefined`, phép tính `undefined * 0.3` và `undefined + surcharge` đều sinh ra `NaN`.

### Bảng Test Cases

| **Trường hợp kiểm thử**                   | **Dữ liệu đầu vào**                                 | **Kết quả sai thực tế**  | **Kết quả đúng mong đợi**     |
| ---------------------------------------------------- | -------------------------------------------------------------- | ---------------------------------- | ----------------------------------------- |
| **TC01:**Check-in sớm (< 12h)                       | `roomPrice: 1500000checkInHour: 9``priceKey: "roomPrice"`  | `surcharge: NaNtotalAmount: NaN` | `surcharge: 450000totalAmount: 1950000` |
| **TC02:**Check-in đúng giờ (**$\ge$**12h) | `roomPrice: 2000000checkInHour: 14``priceKey: "roomPrice"` | `surcharge: 0totalAmount: NaN`   | `surcharge: 0totalAmount: 2000000`      |

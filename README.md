# 1Byte Store Coding Convention
Đây là hướng dẫn chính thức về các quy cách khi phát triển dự án 1Byte Store (web-app & mobile-app)

## Cấu hình Webstorm
### Cấu hình Prettier
Đây công cụ tự động định dạng mã nguồn (code formatter), giúp đảm bảo mã nguồn luôn có cấu trúc và định dạng đẹp, dễ đọc, đồng nhất.

**Settings** > **Languages & Frameworks** >  **JavaScript** > **Prettier**
<img width="1508" height="869" alt="image" src="https://github.com/user-attachments/assets/4e549f42-8f7c-450e-8091-f84a8cd3b4da" />

### Cấu hình ESLint
Đây là một công cụ phân tích mã nguồn (linter), giúp phát hiện lỗi trong mã, và đảm bảo rằng mã tuân thủ các quy tắc nhất định đã được cấu hình trước đó.

**Settings** > **Languages & Frameworks** > **Javascript** > **Code Quality Tools** > **ESLint**
<img width="1503" height="873" alt="image" src="https://github.com/user-attachments/assets/e408f2d0-e7a6-42ab-a8ff-a1cb29813ebc" />

### Cấu hình Actions on Save
Đây là phần cấu hình giúp tự động thực hiện một số thao tác như:
- Reformat code (định dạng mã)
- Optimize imports (tối ưu import)
- Run code inspections
- Compile hoặc chạy linter/formatter (ví dụ: ESLint, Prettier)

Việc này đảm bảo mã nguồn luôn sạch, nhất quán cũng hạn chế việc sửa conflict do khác style giữa các team member của 1Byte

**Settings** > **Tools** > **Actions on Save**
<img width="1505" height="866" alt="image" src="https://github.com/user-attachments/assets/ff6c3c45-5d41-4c41-a211-233a397384ae" />

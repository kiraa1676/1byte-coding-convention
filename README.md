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

## Cấu trúc thư mục dự án
```
├── assets
│   ├── fonts
│   ├── images
│   └── scss
├── components
│   ├── utils
├── constants
├── data
|   ├── en
|   └── km
├── i18n
├── layouts
├── libraries
├── middleware
├── mixins
├── modules
├── pages
├── plugins
├── router
├── schemes
├── server-middleware
├── services
├── static
└── store
```

### 1. assets

Chứa các tệp tĩnh chưa được biên dịch như SCSS, hình ảnh, fonts...

- fonts/: Font chữ tùy chỉnh.
- images/: Ảnh dùng trong giao diện (logo, icon, ảnh đại diện,...). Được sử dụng bằng cách import vào Vue component.
- scss/: Các tệp SCSS/SASS (biến màu sắc, mixins, style chung...).

### 2. components

Chứa các Vue components tái sử dụng trong nhiều nơi, điển hình như FAQ, IUSelect, Heading Area, các FormConfig cho các service..
**utils/**: Thư mục con chứa các component được sử dụng trực tiếp trong Vue component thông qua cơ chế auto-import. Thường được sử dụng với lazy-load. Ví dụ `<LazyUtilsFAQ :faq="FAQ"></LazyUtilsFAQ>`

### 3. constants
Chứa các hằng số, enums, cấu hình, hoặc các giá trị hardcode được sử dụng trong toàn bộ dự án.

### 4. data
Chứa các dữ liệu tĩnh liên quan đến nội dung trang như FAQ, Specifications, Top use cases,... dạng json. Các nội dung có mang tính chất đa ngôn ngữ sẽ được phân loại vào các thư mục ngôn ngữ tương ứng: `en` hoặc `km`.

### 5. i18n
Chứa cấu hình và các file dịch đa ngôn ngữ, dựa trên package `@nuxtjs/i18n`.

### 6. layouts
Chứa các layout của trang.

### 7. libraries
Chứa các thư viện tùy chỉnh.

### 8. middleware
Chứa các middleware chạy trước khi render trang (SSR + CSR).

### 9. mixins
Chứa các mixin Vue dùng chung giữa nhiều component.

### 10. modules
Chứa các module tuỳ chỉnh mở rộng từ Nuxt.

### 11. pages
Chứa các trang có trong ứng dụng, đăng ký ở `router`.

### 12. plugins
Chứa các plugin được sử dụng trong ứng dụng, ví dụ: helpers, logger, api, seo,...

### 13. router
Đăng ký router tùy chỉnh thay dựa trên package `@nuxtjs/router`. Liên kết với các trang ở thư mục `pages`.

### 14. server-middleware
Chứa các middleware phía server: ví dụ redirect về mobile-app từ web-app và ngược lại hoặc redirect về đúng website của quốc gia dựa trên `cf-ipcountry`.

### 15. services
Chứa logic gọi API (wrapper từ axios plugin).

### 16. static
Chứa tài nguyên tĩnh được truy cập trực tiếp thông qua URL mà không sử dụng bằng cách import, ví dụ: `/robots.txt`, `/favicon.ico`.

### 17. store
Vuex store – chứa state toàn cục cho ứng dụng.

## Quy cách phát triển Vue Component
Các quy tắc này dựa trên các nguyên tắc phát triển từ các team member tiền nhiệm kèm theo phong cách viết (Style Guide) chính thức được công bố dành cho Vue.js 2: https://v2.vuejs.org/v2/style-guide/.

### Quy tắc đặt tên
Tên component được đặt theo quy tăc: PascalCase + Multi-word.
Ví dụ: TodoList, TodoItem, HtmlBlock,...
Đối với route component hoặc các component đặc thù thì có thể sử dụng dạng viết tắt hoặc Single-word.
Ví dụ: FAQ, Promotion, Affiliate,...

### Quy tắc về cấu trúc Component
#### Đối với component đơn lẻ
Component được đặt ngay bên trong một thư có tên trùng với tên component.
Ví dụ:
```
├── TodoList
    └── TodoList.vue
```

#### Đối với component phức tạp
Khi muốn tách component cha thành các component con, các component con được đặt vào thư mục `components/` cùng cấp với component cha.
Ví dụ:
```
├── TodoList
|   ├── TodoList.vue
        └── components
            └── TodoItem
                └── TodoItem.vue
```

### Quy tắc sử dụng Component
#### Quy tắc import
- Luôn bắt đầu đường dẫn với ký tự `~`.
Ví dụ:
```
import TldFaq from '~/pages/DomainTldDetail/components/TldFaq/TldFaq';
```
- Luôn sử dụng đường dẫn đầy đủ khi import, không sử dụng đường dẫn tương đối
Ví dụ:
```
import CloudHostingForm from '~/components/services-form-config/CloudHostingForm/CloudHostingForm';
import DomainTransferInput from '~/pages/DomainTransfer/components/DomainTransferForm/components/DomainTransferInput/DomainTransferInput';
```

### Quy tắc về component tag
- Sử dụng kebab-case đối với các component từ thư viện bên ngoài, ví dụ BootstrapVue.
Ví dụ:
```
<b-form-group></b-form-group>
<b-card></b-card>
<b-container>
  <b-row>
    <b-col>1 of 3</b-col>
    <b-col>2 of 3</b-col>
    <b-col>3 of 3</b-col>
  </b-row>
</b-container>
``` 
- Sử dụng PascalCase hoặc dạng Acronym đối với các component tự phát triển.
Ví dụ:
```
<TopUpAmount></TopUpAmount>
<DomainTransferForm></DomainTransferForm>
```
**Lưu ý**: luôn sử dụng thẻ đóng cho component, không sử dụng self-closing component.

### Quy tắc về nơi đặt component
Không có ràng buộc cụ thể về nơi đặt component, các team member của 1Byte sử dụng kinh nghiệm cá nhân của mình để phân tích và tìm chỗ đặt cho phù hợp dựa trên các tiêu chí:
1. `components/utils/`
- Có thể tái sử dụng ở nhiều nơi.
- Có style sử dụng chung.

2. `pages/[page_component]/components/` hoặc `pages/[page_component]/components/[page_child_component]/components`
- Chia giao diện trang hiện tại thành các thành phần nhỏ, giảm độ phức tạp, dễ quản lý.
- Có style phức tạp nhưng thuộc trang.
- Có logic phức tạp nhưng thuộc trang.

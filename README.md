# 1Byte Store Style Guide
Đây là hướng dẫn chính thức về các quy tắc khi phát triển dự án 1Byte Store (web-app & mobile-app)

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
- images/: Ảnh dùng trong giao diện (logo, icon, ảnh đại diện, ảnh dùng các page hoặc module cụ thể,...). Được sử dụng bằng cách import vào Vue component.
- scss/: Các tệp SCSS/SASS (biến màu sắc, mixins, style chung...).

### 2. components

Chứa các Vue components tái sử dụng trong nhiều nơi, điển hình như `FAQ`, `IUSelect`, `HeadingArea`, các `FormConfig` cho các service..
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

### 14. schemes
Nơi định nghĩa các custom scheme cho `@nuxtjs/auth-next`. Chủ yếu liên quan đến các logic cho auth.

### 15. server-middleware
Chứa các middleware phía server: ví dụ redirect về `mobile-app` từ `web-app` và ngược lại hoặc redirect về đúng website của quốc gia dựa trên `cf-ipcountry`.

### 16. services
Chứa logic gọi API (wrapper từ axios plugin).

### 17. static
Chứa tài nguyên tĩnh được truy cập trực tiếp thông qua URL mà không sử dụng bằng cách import, ví dụ: `/robots.txt`, `/favicon.ico`.

### 18. store
Vuex store – chứa state toàn cục cho ứng dụng.

## Quy cách phát triển Vue Component
Các quy tắc này dựa trên các nguyên tắc phát triển từ các team member tiền nhiệm kèm theo phong cách viết (Style Guide) chính thức được công bố dành cho Vue.js 2: https://v2.vuejs.org/v2/style-guide/.

### Quy tắc đặt tên
Tên component được đặt theo quy tăc: PascalCase + Multi-word.
Ví dụ: `TodoList`, `TodoItem`, `HtmlBlock`,...
Đối với route component hoặc các component đặc thù thì có thể sử dụng dạng Acronym hoặc Single-word.
Ví dụ: `FAQ`, `Promotion`, `Affiliate`,...

### Quy tắc về cấu trúc thư mục Component
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
    └── TodoList.vue
        └── components
            └── TodoItem
                └── TodoItem.vue
```

### Quy tắc sử dụng Component
#### Quy tắc import
- Luôn bắt đầu đường dẫn với ký tự `~`.
- Kết thúc đường dẫn không chứa phần mở rộng `.vue`.
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
- Sử dụng kebab-case đối với các component từ thư viện bên ngoài, ví dụ `bootstrap-vue`.
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
<FAQ></FAQ>
```

### Quy tắc về nơi đặt component
Không có ràng buộc cụ thể về nơi đặt component, các team member của 1Byte sử dụng kinh nghiệm cá nhân của mình để phân tích và tìm chỗ đặt cho phù hợp dựa trên các tiêu chí:
1. `components/`
- Sử dụng cho layout.
- Có thể tái sử dụng ở nhiều nơi nhưng ưu tiên dùng chung với `<ClientOnly>`.
   
2. `components/utils/`
- Có thể tái sử dụng ở nhiều nơi.
- Có style sử dụng chung.

3. `pages/[page_component]/components/` hoặc `pages/[page_component]/components/[page_child_component]/components`
- Chia giao diện trang hiện tại thành các thành phần nhỏ, giảm độ phức tạp, dễ quản lý.
- Có style phức tạp nhưng thuộc trang hiện tại.
- Có logic phức tạp nhưng thuộc trang hiện tại.

### Lazy loading components
Mặc định, dự án đã được cấu hình để scan & auto-import các component từ thư mục `components/utils`. Nếu sử dụng các component có trong thư mục này, chỉ cần đặt vào template dạng `<LazyUtils[ComponentName]></LazyUtils[ComponentName]>` mà không cần import.
Ví dụ:
```
<LazyUtilsPartners />
<LazyUtilsAwardsRecognition />
<LazyUtilsHeadingArea></LazyUtilsHeadingArea>
<LazyUtilsFAQ></LazyUtilsFAQ>
<LazyUtilsExportContract />
```

### Bootsrap Vue
Dự án được phát triển dựa trên các component dựng sẵn từ package `bootstrap-vue`, tuy nhiên chỉ có một số component được cài đặt để sử dụng mà không cần import. Bao gồm:
| Plugin                | Component Tags |
|-----------------------|----------------|
| `AlertPlugin`         | `<b-alert>` |
| `AspectPlugin`        | `<b-aspect>` |
| `BadgePlugin`         | `<b-badge>` |
| `BreadcrumbPlugin`    | `<b-breadcrumb>`, `<b-breadcrumb-item>` |
| `ButtonPlugin`        | `<b-button>` |
| `ButtonGroupPlugin`   | `<b-button-group>`, `<b-button-toolbar>` |
| `CardPlugin`          | `<b-card>`, `<b-card-body>`, `<b-card-header>`, `<b-card-footer>`, `<b-card-title>`, `<b-card-sub-title>` |
| `CollapsePlugin`      | `<b-collapse>` |
| `EmbedPlugin`         | `<b-embed>` |
| `FormPlugin`          | `<b-form>` |
| `FormCheckboxPlugin`  | `<b-form-checkbox>`, `<b-form-checkbox-group>` |
| `FormGroupPlugin`     | `<b-form-group>` |
| `FormInputPlugin`     | `<b-form-input>` |
| `FormRadioPlugin`     | `<b-form-radio>`, `<b-form-radio-group>` |
| `FormSelectPlugin`    | `<b-form-select>`, `<b-form-select-option>`, `<b-form-select-option-group>` |
| `FormTagsPlugin`      | `<b-form-tags>` |
| `FormTextareaPlugin`  | `<b-form-textarea>` |
| `ImagePlugin`         | `<b-img>`, `<b-img-lazy>` |
| `InputGroupPlugin`    | `<b-input-group>`, `<b-input-group-prepend>`, `<b-input-group-append>`, `<b-input-group-text>` |
| `LayoutPlugin`        | `<b-container>`, `<b-row>`, `<b-col>` |
| `LinkPlugin`          | `<b-link>` |
| `ListGroupPlugin`     | `<b-list-group>`, `<b-list-group-item>` |
| `MediaPlugin`         | `<b-media>`, `<b-media-body>` |
| `ModalPlugin`         | `<b-modal>` |
| `OverlayPlugin`       | `<b-overlay>` |
| `SpinnerPlugin`       | `<b-spinner>` |
| `TablePlugin`         | `<b-table>`, `<b-table-lite>` |
| `TabsPlugin`          | `<b-tabs>`, `<b-tab>` |
| `ToastPlugin`         | `<b-toast>` (hoặc dùng qua `$bvToast`) |
| `TooltipPlugin`       | `v-b-tooltip` (directive, không có component tag) |

Để sử dụng các component từ `bootstrap-vue` ngoài danh sách trên, hãy import và đăng ký trực tiếp.
Ví dụ:
```
<script>
import { BNav, BNavItem } from 'bootstrap-vue';

export default {
    components: { BNav, BNavItem },
}
</script>
```

### Quy tắc về cấu trúc Single-File Component

#### Cấu trúc chung
Đảm bảo thứ tự `template`, `script`, `style`.
```
<template></template>

<script></script>

<style lang="scss" scoped></style>
```

#### Các quy tắc dành cho thẻ template
1. Sử dụng dạng camelCase cho id nếu sử dụng trực tiếp. Ví dụ: `<b-form-select id="osAddonName">`.
2. Sử dụng dạng kebab-case cho prop. Ví dụ `<LazyUtilsFAQ :faq="FAQ" class="pb-4s my-4s">`.
3. Sử dụng dạng camelCase cho slot name. Ví dụ: `<slot name="mainTitleHtml"></slot>`.
4. Ưu tiên sử dụng v-if trên `template` hơn là unstyled `div` nếu thẻ chứa v-if không cần style đặc biệt.
Thay đổi
```
<div v-if="condition">
    <LazyUtilsAwardsRecognition />
    <LazyUtilsPartners />
</div>
```
Thành
```
<template v-if="condition">
    <LazyUtilsAwardsRecognition />
    <LazyUtilsPartners />
</template>
```
Hoặc
```
<div v-if="condition" class="class-1 class-2">
    <LazyUtilsAwardsRecognition />
    <LazyUtilsPartners />
</div>
```
5. Hạn chế sử dụng `v-html` để tạo html từ chuỗi truyền vào. Ưu tiên sử dụng i18n template với component interpolation.

#### Các quy tắc dành cho thẻ script
1. Đảm bảo các property cơ bản sau đây cấu trúc theo thứ tự:
```
export default {
    name: 'ExampleComponent',
    components: {},
    mixins: [],
    props: {},
    async asyncData() {},
    data() {
        return {};
    },
    head() {},
    computed: {},
}
```
2. Đường dẫn các tập tin js khi import không chứa phần mở rộng `.js`.
3. Sử dụng dạng camelCase + `Mixin` cho mixins. Ví dụ: `import errorMixin from '~/mixins/error';`
4. Các nguyên tắc đặt tên props:
- Sử dụng số nhiều cho Array, ví dụ `items`, `users`.
- Sử dụng số ít cho Object, ví dụ `item`, `user`.
- Sử dụng prefix `is`, `has`, `can`, `should` cho Boolean. Ví dụ `isVisible`, `hasItem`, `canSubmit`, `shouldRedirect`.
- Linh hoạt sử dụng các từ chỉ số lượng như `num`, `count`, `size`,... cho Number. 
4. Luôn chỉ định `type`, `default` hoặc `required` khi khai báo prop.
5. Đưa các khai báo liên quan đến Vuex lên trên.

Thay đổi
```
computed: {
    ...mapGetters('cart', ['baseSubtotal']),
    user() {
        return this.$auth.user;
    },
    ...mapGetters('user', ['balance', 'trialConditions']),
}
```
Thành
```
computed: {
    ...mapGetters('cart', ['baseSubtotal']),
    ...mapGetters('user', ['balance', 'trialConditions']),
    user() {
        return this.$auth.user;
    },
}
```

#### Các quy tắc dành cho thẻ style
1. Chỉ sử dụng `scoped` và `scss`.
2. File scss có tên trùng tên và nằm cùng cấp với component.
Cấu trúc
```
├── TodoList
    ├── TodoList.vue
    └── TodoList.scss
```
Khai báo
```
<style lang="scss" scoped>
@import 'TodoList';
</style>
```

### Quy tắc về Styling cho Component
Store sử dụng package `bootstrap-vue` làm nền tảng cho giao diện, với các tuỳ biến riêng về màu sắc và khoảng cách. Các component được tùy chỉnh theo hướng ưu tiên sử dụng các utility class có sẵn của Bootstrap, kết hợp với các utility class đã được xây dựng sẵn trước đó.

#### Cấu trúc thư mục
```
├── assets
    └── scss
        ├── _mixins.scss
        ├── _var.scss
        ├── general.scss
        ├── helpers.scss
        └── theme.scss
```
1. **_mixins.scss**: chứa mixin và function toàn cục về breakpoint, flex, line-clamps,...
2. **_var.scss**: chứa các biến toàn cục về font chữ, font size, grid breakpoints, khoảng cách, màu sắc,...
3. **general.scss**: file sytle chính cho toàn bộ trang. Chứa bootstrap, cấu hình font chữ, các class hoặc các style ghi đè toàn cục.
4. **helpers.scss**: file style chính cho toàn bộ trang. Chứa các utility-class mở rộng, cấu hình các màu sắc có thể sử dụng trực tiếp từ utility-class. Ví dụ: `text-blue-dianne`, `bg-alabaster-2`, `max-w-600-px`,...
5. **theme.scss**: chứa cấu hình theme styling. Chỉ dùng trong trường hợp phát triển giao diện trang chủ mang tính chất theo mùa.

#### Các quy tắc khi Styling
1. Luôn ưu tiên sử dụng các class có sẵn từ Bootstrap + **helpers.scss**.
2. Tuỳ theo mức độ phổ biến của màu sắc trên giao diện mà: ưu tiên sử dụng màu sắc đã được khai báo trong **helpers.scss** để sử dụng utility-class > Sử dụng màu sắc được khai báo trong **_var.scss** vào custom style > Khai báo màu sắc trực tiếp vào custom style. Hạn chế thấp nhất có thể việc thêm màu sắc vào **helpers.scss**.
3. Bám sát grid breakpoints và các container width được khai báo trong **_var.scss**. Ưu tiên sử dụng mixins media-breakpoint. Kèm theo đó:
- `web-app`: min width là 1400px. Ngoài việc triển khai giao diện theo Figma cũng cần đảm bảo giao diện ở Macbook 14" (1612px) được hài hoà.
- `mobile-app`: min width là 320px.
4. Ưu tiên Bootstrap grid > flexbox hoặc grid.
5. Khi triển khai custom styling:
- Sử dụng `dvh` thay cho `vh` để đảm bảo chiều cao luôn động theo khung nhìn thiết bị.
- Ưu tiên triển khai dưới dạng quy tắc BEM.
- Ưu tiên các giá trị được khai báo sẵn trong **_var.scss**.
- Ưu tiên truyền prop cho phép custom class > sử dụng `::v-deep`.
- Vẫn là ưu tiên bám sát grid breakpoint đã được khai báo sẵn trong **_var.scss**.

### Code Samples
Cung cấp những đoạn mã nguồn mẫu đã và đang được sử dụng trong mã nguồn để giải quyết các vấn đề chung.

#### 1. Đăng ký trang mới
```
const Promotion = () => import('~/pages/Promotion/Promotion').then((m) => m.default || m);
const routes = [
{
    path: '/promotion',
    name: 'promotion',
    component: Promotion,
    meta: {
        metaTags: META.PROMOTION,
        sitemap: false, // Hoặc bỏ qua
    },
},
];
```

#### 2. Xử lý `asyncData` và template
Luôn bọc các xử lý API bên trong `asyncData` với `$helpers.catchAndReturnArray` cho Array,  `$helpers.catchAndReturnObject` cho Object hoặc `$helpers.catchAndReturnValue` với giá trị tuỳ ý nhằm đảm bảo luôn có giá trị mặc định được trả về.
```
async asyncData({ app, store, route }) {
    const [FAQ, { reviews, schemas }, blogs] = await Promise.all([
        app.$helpers.catchAndReturnValue(
            () => app.$api.schemas.getBusinessFeedbacks(),
            {
                reviews: [],
                schemas: [],
            }
        ),
        app.$helpers.catchAndReturnArray(() =>
            app.$api.blog.getBlogsByKey(app.getRouteBaseName(route))
        ),
    ]);
    return {
        schemas,
        reviews,
        blogs,
    };
}
```

#### 3. Xử lý API
Luôn xử lý lỗi thông qua `handleThrowError` từ `errorMixin`.
```
import errorMixin from '~/mixins/error';

export default {
    mixins: [errorMixin],
    data() {
        return {
            loading: false,
            items: [],
        };
    },
    methods: {
        async getManualInvoices() {
            try {
                this.loading = loading;
                this.items = await this.$api.user.getManualInvoices();
            } catch (error) {
                this.handleThrowError(error);
            } finally {
                this.loading = false;
            }
        },
    }
}
```

#### 4. Xử lý loading
Ngoài việc xử lý loading trong nội tại component thông qua `b-overlay`, `b-spinner` hay `b-skeleton`, dự án còn xây dựng sẵn các loại loading sau đây:

1. Global loading
```
// Bật
this.$store.commit('loading/setLoading', true);
// Tắt
this.$store.commit('loading/setLoading', false);
```

2. Cart loading (dành riêng cho trang checkout)
```
// Bật
this.$store.commit('cart/SET_LOADING', true);
// Tắt
this.$store.commit('cart/SET_LOADING', false);
```

#### 5. Toast notifications
```
this.$store.commit('message/setMessage', {
    type: 'success', // type dựa trên variants của Bootstrap
    message: this.$t('message.SUBSCRIPTION_SUCCESSFULLY'),
});
```

#### 6. i18n component interpolation
Local message
```
{
    message: Use a different email address or {login} to the existing account,
}
```
Thay thế `{login}` bằng giá nút nhấn mở login modal
```
<i18n path="message" tag="div">
    <template #login>
        <b-button @click="openLoginPopup">
            {{ $t('button.login') }}
        </b-button>
    </template>
</i18n>
```

#### 7. Sử dụng `localePath` để tạo URL dựa trên locale hiện tại
Ví dụ, URL: `/term-and-conditions`.
```
this.localePath({ name: 'term-and-conditions' })
// locale en: /term-and-conditions
// locale km: /km/term-and-conditions
```

#### 8. Sử dụng `computed` để triển khai `v-model` thay vì `@input`
```
export default {
    props: {
      value: {
        type: String,
        default: ''
      }
    },
    computed: {
      model: {
        get() {
          return this.value
        },
        set(value) {
          this.$emit('input', value)
        }
      }
    }
}
```

#### 9. Sử dụng quy tắc BEM khi triển khai giao diện phức tạp
Template
```
<ul class="four-easy-step-list">
    <li
        v-for="(item, idx) in steps"
        :key="idx"
        class="four-easy-step-list__item"
    >
        <div class="flex-grow-1 px-2s pt-2s pb-3">
            <div class="four-easy-step-list__item-title">
                {{ $t(item.title) }}
            </div>
            <div class="four-easy-step-list__item-content">
                {{ $t(item.content) }}
            </div>
        </div>
    </li>
</ul>
```
CSS
```
.four-easy-step {
     &-list {
        counter-reset: number;
        &__item {
            $number-width: 64px;
            $number-height: 80px;
            &:before {
                counter-increment: number;
                content: counter(number);
                width: $number-width;
                height: $number-height;
                color: $color-malibu;
                font-weight: map-get($font-weights, 'medium');
            }
            &-title {
                // Custom CSS
            }
            &-content {
                // Custom CSS
            }
        }
    }
}
```

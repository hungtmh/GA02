# Tây Du Ký – Team Website

Website giới thiệu nhóm Tây Du Ký và các thành viên. Được xây dựng với HTML và Tailwind CSS.

## Công nghệ sử dụng

- **HTML5** - Cấu trúc trang web
- **Tailwind CSS 3** - Framework CSS với design system tùy chỉnh
- **JavaScript** - Mobile menu toggle
- **Vercel** - Hosting platform

## Design System

### Màu sắc
- **Primary**: Emerald (màu chủ đạo)
- **Accent**: Indigo (màu phụ)
- **Surface**: Slate (nền tối)
- **Theme**: Dark mode mặc định

### Components
- Header với navigation responsive
- Card system (card, card-hover, card-gradient)
- Buttons và Badges (8 variants)
- Sidebar sticky
- Hero sections với gradient
- Grid layouts responsive

## Cấu trúc dự án

```
GA2/
├── index.html              # Trang chủ
├── html/                   # Các trang phụ
│   ├── about.html         # Về nhóm
│   ├── contact.html       # Liên hệ
│   ├── mission.html       # Sứ mệnh
│   ├── vision.html        # Tầm nhìn
│   └── values.html        # Giá trị cốt lõi
├── members/               # Trang cá nhân thành viên
│   ├── tran-manh-hung.html
│   ├── bui-duong-duy-cuong.html
│   ├── nguyen-anh-khoa.html
│   ├── nguyen-tan-thang.html
│   └── ninh-van-khai.html
├── css/
│   ├── input.css          # Tailwind source với custom components
│   └── output.css         # CSS đã compile (minified)
├── js/
│   └── script.js          # Mobile menu toggle
├── assets/
│   └── images/            # Logo và ảnh thành viên
├── tailwind.config.js     # Cấu hình Tailwind
└── package.json           # Dependencies và build scripts
```

## Cài đặt và phát triển

### Yêu cầu
- Node.js và npm

### Cài đặt dependencies
```bash
npm install
```

### Build CSS
```bash
# Build một lần (minified)
npm run build:css

# Watch mode (tự động rebuild khi có thay đổi)
npm run watch:css
```

### Chạy local
Mở `index.html` trực tiếp trong browser hoặc dùng Live Server.

## Tùy chỉnh Design System

### Thay đổi màu sắc
Chỉnh sửa `tailwind.config.js`:
```js
colors: {
  primary: colors.emerald,    // Đổi màu primary
  accent: colors.indigo,      // Đổi màu accent
  surface: colors.slate,      // Đổi màu nền
}
```

### Thêm component mới
Thêm vào `css/input.css` trong `@layer components`:
```css
@layer components {
  .my-component {
    @apply bg-surface-800 p-4 rounded-lg;
  }
}
```

Sau đó rebuild CSS: `npm run build:css`

## Cấu trúc trang

Tất cả các trang sử dụng layout nhất quán:
- **Header**: Logo, navigation menu (Trang chủ, Về nhóm, Liên hệ)
- **Main**: Grid layout (sidebar + content)
- **Footer**: Copyright info

### Responsive Breakpoints
- Mobile: < 768px (stack layout)
- Tablet: 768px - 1024px
- Desktop: > 1024px (grid layout)

## Thành viên nhóm

- **Trần Mạnh Hùng** - Team Lead
- **Bùi Dương Duy Cường** - Member
- **Nguyễn Anh Khoa** - Member
- **Nguyễn Tấn Thắng** - Member
- **Ninh Văn Khải** - Member

## Hosting

Website được deploy tự động trên Vercel khi có commit mới vào branch `main`.

## License

Copyright © 2025 Tây Du Ký Team. All rights reserved.


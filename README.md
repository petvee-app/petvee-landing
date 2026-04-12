# PetVee Landing Page

Landing page cho [PetVee](https://petvee.app) — Ứng dụng AI chăm sóc sức khoẻ thú cưng đầu tiên tại Việt Nam.

## Deploy lên GitHub Pages

1. Tạo repo mới trên GitHub: `petvee-landing`
2. Push toàn bộ folder này lên
3. Vào **Settings → Pages → Source** → chọn `main` branch → Save
4. Vào **Settings → Pages → Custom domain** → nhập `petvee.app`
5. Thêm DNS records bên PA Vietnam (xem bên dưới)

## DNS Setup (PA Vietnam)

Thêm các records sau vào DNS management của `petvee.app`:

| Type  | Name | Value                      |
|-------|------|----------------------------|
| A     | @    | 185.199.108.153            |
| A     | @    | 185.199.109.153            |
| A     | @    | 185.199.110.153            |
| A     | @    | 185.199.111.153            |
| CNAME | www  | your-username.github.io    |

Thay `your-username` bằng GitHub username của bạn.

## Files

- `index.html` — Landing page chính
- `privacy.html` — Chính sách bảo mật
- `terms.html` — Điều khoản sử dụng
- `CNAME` — Custom domain cho GitHub Pages

## Cần thay đổi

- [ ] Thay logo icon PV bằng logo chính thức từ Gigi
- [ ] Thêm link App Store thật khi có
- [ ] Thêm link Google Play thật khi có
- [ ] Cập nhật social media links
- [ ] Setup email hello@petvee.app và privacy@petvee.app

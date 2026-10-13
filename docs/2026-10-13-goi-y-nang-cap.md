# Gợi ý nâng cấp — rà soát 2026-10-13

> Lấy từ đợt rà soát chéo 19 repo của chủ sở hữu (ma trận vệ sinh ở [seeker19110/stored, mục 23 §8.1](https://github.com/seeker19110/stored/blob/main/23-own-repos-lessons/README.md); gợi ý tích hợp ở §7b của cùng file). Số liệu đo bằng lệnh trên HEAD (đếm `uses:` ghim SHA 40 ký tự, khối `permissions:`, `dependabot.yml`, `.claude/settings.json`), không suy ra từ văn xuôi. Đây là **đề xuất**, chưa sửa code. Mỗi mục kèm bằng chứng để kiểm lại trước khi làm; mục nào đã xử lý thì đánh dấu hoặc xoá.

## Hiện trạng đo được

| HEAD đọc               | Action ghim SHA | Workflow thiếu `permissions:` cấp đầu | Dependabot   | LICENSE · SECURITY | File test |
| ---------------------- | --------------- | ------------------------------------- | ------------ | ------------------ | --------- |
| `098d769` (2026-10-09) | 0/92            | `ci.yml`, `release.yml`               | **không có** | có · có            | 873       |

## Đề xuất (🔴 cao · 🟠 trung bình · 🟢 nhẹ)

| #   | Mức | Đề xuất                                                                                                                                                                 | Bằng chứng                                                                                                                                                                                                                                            | Kiểm xong khi                                              |
| --- | --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| 1   | 🟠  | Đặt lại nhánh mặc định về `main`                                                                                                                                        | Nhánh mặc định trên GitHub đang là `agent/javascript-vite-rollup-esbuild-adapters` (`rea-agents` 2.1.0, HEAD 20/7/2026), trong khi `main` đã ở 6.1.0 (`098d769`, 9/10/2026). Người xem và các lệnh clone mặc định đều nhận bản cũ hơn 4 phiên bản lớn | `git ls-remote --symref origin HEAD` trỏ `refs/heads/main` |
| 2   | 🟠  | Đồng bộ `main` với upstream `morluto/rea` (6.1.0 → 6.4.0)                                                                                                               | `package.json` trên `main` ghi 6.1.0; upstream HEAD `c462a4e` (13/10/2026) ghi 6.4.0                                                                                                                                                                  | Phiên bản khớp upstream                                    |
| 3   | 🟢  | Thêm `permissions: contents: read` cấp đầu cho `ci.yml` và `release.yml` (nâng quyền ở job cần); ghim 92 `uses:` theo SHA nếu repo dùng để chạy, không chỉ để tham khảo | Ghim 0/92; `release.yml` không có `permissions:` cấp đầu, nên mọi job release đều thừa hưởng quyền mặc định của repo                                                                                                                                  | `grep -L "^permissions:" .github/workflows/*.yml` rỗng     |

## Giữ nguyên (điểm mạnh)

- 873 file test và các workflow chạy công cụ thật (Hopper, Ghidra, JS replay); Evidence v2 (observation / inference / unknown), authority fail-closed kèm `plan_digest`. Khi dẫn, **ghi nguồn upstream `morluto/rea`**.

## Gợi ý tích hợp từ catalog `stored`

- Đối chiếu với Reverser + Ghidra của Decepticon (stored mục 12 §3g); quét bằng SkillSpector / mantis trước khi chạy tool lạ (mục 12 §3e).

## Ghi chú chung

- Ghim action theo SHA bằng [pinact](https://github.com/suzuki-shunsuke/pinact) hoặc [ratchet](https://github.com/sethvargo/ratchet), giữ comment tag (`# v7.0.1`), rồi để Dependabot `github-actions` tự nâng SHA. Đây là cách projects-template, xboss và Sales-Hunter đang làm.
- Chuẩn tham chiếu là `seeker19110/projects-template`: 25/25 action ghim SHA, mọi workflow có `permissions:` cấp đầu, Dependabot cho npm, github-actions và pip.

# Bài 2 — Phát hành Docker Image khi gắn Git Tag `v*.*.*`

## File chính

- `.github/workflows/release.yml` (root repo — Actions chỉ chạy file ở đây)
- Bản copy nộp: `homework/session_12/ex2/.github/workflows/release.yml`

## Trigger

```yaml
on:
  push:
    tags:
      - 'v*.*.*'
```

## Job `release-image`

1. `actions/checkout@v5`
2. `docker/login-action@v3` → GHCR (`secrets.REGISTRY_TOKEN`)
3. `docker/metadata-action@v5` → tag theo Git tag
4. `docker/build-push-action@v5` → build & push `ghcr.io/<owner>/<repo>:v1.0.0`

## Chuẩn bị Secret

Repo → **Settings** → **Secrets and variables** → **Actions**

- Name: `REGISTRY_TOKEN`
- Value: PAT classic có quyền `write:packages` (và `read:packages`)

## Kiểm tra

```bash
git tag v1.0.0
git push origin v1.0.0
```

1. Tab **Actions** → workflow **Release Docker Image** chạy.
2. **Packages** (sidebar repo / profile) → image `ghcr.io/tamisimi/hn_ks24_cntt4_it219_session12_bai02` tag **v1.0.0**.
3. Chụp màn hình Packages để nộp.

## Lưu ý

- Push tag `v1.0.0` mới kích hoạt; push commit thường **không** chạy workflow này.
- Tên package trên GHCR thường **chữ thường**.

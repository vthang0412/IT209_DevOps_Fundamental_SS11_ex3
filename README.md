# Báo cáo Bài 3: Gradle Dependency Caching

## 1. Mục tiêu

Cấu hình Gradle Dependency Caching trong GitHub Actions nhằm tái sử dụng các thư viện đã tải và giảm thời gian thực thi CI.

## 2. Cấu hình

Trong file `.github/workflows/ci.yml`, sử dụng:

```yaml
- name: Setup Java 21
  uses: actions/setup-java@v4
  with:
    distribution: temurin
    java-version: '21'
    cache: gradle
    cache-dependency-path: student-api/*.gradle*
```

## 3. Kết quả thực nghiệm

| Tiêu chí | Lần chạy 1 | Lần chạy 2 |
|---|---|---|
| Tổng thời gian CI | 1 phút 38 giây | 1 phút 03 giây |
| Thời gian Setup Java | 1 giây | 2 giây |
| Trạng thái cache | Chưa tìm thấy cache | Khôi phục cache thành công |

Tổng thời gian CI giảm 35 giây, tương đương khoảng 35,7%..

## 4. Kết luận

Gradle Dependency Caching đã hoạt động thành công. Lần chạy thứ hai khôi phục được cache và tổng thời gian CI giảm từ 1 phút 38 giây xuống 1 phút 03 giây. Kết quả cho thấy caching có thể giúp giảm thời gian thực thi workflow.
# Report Page

## Pipeline

Pipeline của project được thực hiện theo các bước chính như sau:

- **Thiết lập môi trường**:
  - Tạo môi trường ảo bằng Anaconda với Python 3.10
  - Cập nhật pip và cài đặt các thư viện cần thiết từ file `requirements_core.txt`
  - Cài đặt PyTorch với CUDA để hỗ trợ tăng tốc (nếu có GPU)

- **Kiểm tra môi trường**:
  - Chạy `python src/env_check.py` để kiểm tra cấu hình và sinh ra các file:
    - `logs/lab0_run.log`
    - `results/lab0_env.json`

- **Chạy chương trình chính**:
  - Thực thi `python src/hello_nlp.py` để chạy pipeline NLP cơ bản
  - Kết quả được lưu tại `results/lab0_metrics.json`

- **Kiểm thử (Testing)**:
  - Sử dụng `pytest -q` để kiểm tra tính đúng đắn của chương trình
  - Kết quả: 4 tests passed, 2 tests expected fail (xfailed), đảm bảo hệ thống hoạt động đúng yêu cầu

---

## Vấn đề gặp phải và cách xử lý

Trong quá trình cài đặt và chạy môi trường, gặp lỗi liên quan đến OpenMP:

> `OMP: Error #15: Initializing libiomp5md.dll, but found libiomp5md.dll already initialized.`

### Nguyên nhân:
Lỗi này xảy ra do xung đột giữa các thư viện sử dụng OpenMP (như PyTorch, NumPy hoặc các thư viện liên quan), dẫn đến việc nhiều bản sao của `libiomp5md.dll` được load đồng thời.

### Cách xử lý:
Thiết lập biến môi trường để cho phép chương trình tiếp tục chạy:

```bash
set KMP_DUPLICATE_LIB_OK=TRUE
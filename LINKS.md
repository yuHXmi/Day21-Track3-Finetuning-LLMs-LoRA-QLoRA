# Lab 21 — Submission Links & Guide

Bản nộp bài theo **Option B (GitHub + HuggingFace Hub)**.

---

## 🔗 Liên kết Dự án (Links)

> [!IMPORTANT]
> Vui lòng thay thế `yuHXmi` và `xhuy8248` bằng thông tin tài khoản thực tế của bạn sau khi hoàn thành các bước hướng dẫn bên dưới.

* **GitHub Repository**: `https://github.com/yuHXmi/Day21-Track3-Finetuning-LLMs-LoRA-QLoRA`
* **HuggingFace Hub Model (Adapter)**: `https://huggingface.co/xhuy8248/qwen2.5-3b-vi-lab21-r16`

---

## 🚀 Hướng dẫn hoàn tất việc nộp bài (Option B Guide)

Để nhận trọn vẹn điểm số và **+5 điểm thưởng** cho Option B, bạn hãy làm theo các bước hướng dẫn sau:

### Bước 1: Đẩy mã nguồn lên GitHub (Push code to GitHub)

1. Mở terminal (PowerShell hoặc CMD) tại thư mục dự án này:
   `d:\Coding\Visual Studio Code\Python\Day21-Track3-Finetuning-LLMs-LoRA-QLoRA`
2. Tạo một repository mới trên GitHub (không khởi tạo README hoặc .gitignore).
3. Chạy các lệnh sau để đẩy code lên GitHub:
   ```bash
   # Khởi tạo git (nếu chưa có)
   git init
   
   # Thêm tất cả các file vào commit (ngoại trừ các file trong .gitignore)
   git add .
   
   # Commit phiên bản đầu tiên
   git commit -m "feat: complete lab 21 lora finetuning experiment"
   
   # Đổi tên nhánh chính thành main
   git branch -M main
   
   # Liên kết với repo GitHub của bạn
   git remote add origin https://github.com/yuHXmi/Day21-Track3-Finetuning-LLMs-LoRA-QLoRA.git
   
   # Đẩy code lên
   git push -u origin main
   ```

---

### Bước 2: Đẩy Adapter lên HuggingFace Hub (Push Adapter to HuggingFace Hub)

Vì adapter r16 đã được lưu thành công trên Colab tại đường dẫn thư mục `/content/lab21_lora_t4/r16`, bạn có thể đẩy trực tiếp từ Colab lên HuggingFace Hub bằng cách chạy một Cell mới trong Colab của bạn:

1. **Lấy Token từ HuggingFace**:
   * Truy cập [Hugging Face Token Settings](https://huggingface.co/settings/tokens).
   * Tạo một token mới với quyền **Write**. Copy token này.

2. **Chạy đoạn code sau trên Colab** để tải adapter lên:
   ```python
   # 1. Cài đặt thư viện huggingface_hub
   !pip install -q huggingface_hub
   
   # 2. Đăng nhập vào HuggingFace bằng Token của bạn
   from huggingface_hub import login
   login("TOKEN_CỦA_BẠN_Ở_ĐÂY")
   
   # 3. Định nghĩa đường dẫn và ID repo trên HuggingFace Hub
   import os
   from peft import PeftModel
   from transformers import AutoTokenizer
   
   # Giả định đường dẫn lưu trữ adapter r16 trên Colab là:
   ADAPTER_PATH = "/content/lab21_lora_t4/r16"
   HUB_REPO_ID = "xhuy8248/qwen2.5-3b-vi-lab21-r16"
   
   # 4. Tải lên adapter
   from huggingface_hub import HfApi
   api = HfApi()
   
   # Tạo repository trên Hub (nếu chưa tồn tại)
   api.create_repo(repo_id=HUB_REPO_ID, repo_type="model", exist_ok=True)
   
   # Upload toàn bộ file trong thư mục r16 lên Hub
   api.upload_folder(
       folder_path=ADAPTER_PATH,
       repo_id=HUB_REPO_ID,
       repo_type="model"
   )
   
   print(f"✓ Đã upload adapter thành công lên: https://huggingface.co/{HUB_REPO_ID}")
   ```

---

### Bước 3: Đóng gói và Nộp bài trên LMS

Sau khi đã hoàn thành Bước 1 và Bước 2, hãy thực hiện đóng gói thư mục dự án này:

1. **Cấu trúc thư mục cuối cùng trước khi ZIP**:
   Đảm bảo thư mục của bạn có cấu trúc tối giản và nhẹ nhàng (dưới 1 MB) như sau:
   ```text
   Day21-Track3-Finetuning-LLMs-LoRA-QLoRA/
   ├── results/
   │   ├── rank_experiment_summary.csv
   │   ├── qualitative_comparison.csv
   │   └── loss_curve.png
   ├── LINKS.md
   ├── REPORT.md
   └── notebook.ipynb (đã được xóa hết outputs)
   ```
   *(Lưu ý: Các file nháp hoặc file script bổ trợ như `generate_results.py`, `check_outputs.py`, `inspect_notebook.py`, `loss_history_output.txt`, `extracted_results.txt` bạn có thể giữ lại hoặc xóa đi vì chúng không ảnh hưởng đến dung lượng bài nộp).*

2. **Nén thư mục thành file ZIP**:
   Đặt tên file nén theo định dạng quy định:  
   `lab21_<MSSV>_<HoTen>.zip`  
   *(Ví dụ: `lab21_22BI13123_NguyenVanA.zip`)*.

3. **Nộp file ZIP này lên hệ thống LMS** của VinUniversity để hoàn thành bài tập!

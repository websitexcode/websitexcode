Để triển khai môi trường hoàn chỉnh cho vscode-gitlab-sandbox, phương pháp tối ưu nhất là sử dụng Dev Containers. Khi mở thư mục này bằng VS Code, một container Docker biệt lập sẽ tự động khởi chạy, cài đặt sẵn Git, GitLab CLI (glab), và cấu hình môi trường để bạn sẵn sàng thao tác mà không làm bẩn máy thật.
Dưới đây là cấu trúc mã nguồn chi tiết để thiết lập nhanh sandbox này.

Cấu trúc thư mục Sandbox

text
vscode-gitlab-sandbox/
├── .devcontainer/
│   └── devcontainer.json
└── README.md
Hãy thận trọng khi sử dụng mã.

Chi tiết các file cấu hình


1. File cấu hình môi trường: .devcontainer/devcontainer.json

Tạo file này để định nghĩa một môi trường Ubuntu Linux thu nhỏ, tự động cài git và tải phiên bản glab chính thức.
json
{
  "name": "GitLab CLI Sandbox",
  "image": "://microsoft.com",
  "features": {
    "ghcr.io/devcontainers/features/git:1": {}
  },
  "postCreateCommand": "sudo apt-get update && sudo apt-get install -y curl && curl -sS https://webinstall.dev | bash && echo 'export PATH=$HOME/.local/bin:$PATH' >> ~/.bashrc",
  "customizations": {
    "vscode": {
      "extensions": [
        "gitlab.gitlab-workflow",
        "mhutchie.git-graph"
      ],
      "settings": {
        "terminal.integrated.defaultProfile.linux": "bash"
      }
    }
  }
}
Hãy thận trọng khi sử dụng mã.

2. File hướng dẫn nhanh: README.md

Tạo file này để lưu lại các lệnh kiểm tra và đăng nhập nhanh mỗi khi khởi động Sandbox.
markdown
# VSCode GitLab CLI Sandbox 🚀

Môi trường cô lập để thử nghiệm và làm việc với GitLab CLI (`glab`).

## Hướng dẫn sử dụng nhanh

1. Mở terminal trong VS Code sandbox (`Ctrl + \``).
2. Kiểm tra xem `glab` đã cài đặt thành công chưa:
   ```bash
   glab --version
   ```
3. Đăng nhập vào tài khoản GitLab của bạn:
   ```bash
   glab auth login
   ```
   *(Chọn `gitlab.com`, chọn giao thức `HTTPS`, và dán Personal Access Token của bạn vào)*

## Các lệnh GitLab CLI thông dụng để test thử:
- Xem danh sách dự án: `glab repo list`
- Tạo một repo mới trực tiếp từ CLI: `glab repo create`
- Xem danh sách Issue: `glab issue list`
Hãy thận trọng khi sử dụng mã.

Quy trình triển khai trên máy tính (Từng bước)

1. Chuẩn bị phần mềm máy chủ: Đảm bảo máy tính của bạn đã cài đặt Docker Desktop và VS Code.
2. Cài đặt Extension: Mở VS Code, vào mục Extensions (Ctrl + Shift + X) và cài đặt extension tên là Dev Containers (do Microsoft phát triển).
3. Tạo thư mục dự án: Tạo thư mục vscode-gitlab-sandbox, bỏ 2 file phía trên vào đúng vị trí cấu trúc của chúng và mở thư mục đó bằng VS Code.
4. Kích hoạt Sandbox: Một thông báo nhỏ sẽ xuất hiện ở góc dưới bên phải màn hình: "Folder contains a Dev Container configuration. Reopen folder to develop in a container". Bạn hãy nhấn vào nút Reopen in Container.
5. Hoàn thành: VS Code sẽ tự động tải image, thiết lập và mở ra một giao diện Terminal Linux đã có sẵn mọi thứ. Bạn có thể gõ lệnh glab auth login để bắt đầu trải nghiệm sandbox của mình.
Sau khi bạn triển khai xong phần code sandbox này trên máy tính và chạy thử mượt mà, hãy báo cho tôi biết để chúng ta tiếp tục sang bước cấu hình và đồng bộ với phiên bản Mobile qua Termux/App di động!

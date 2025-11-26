# Permissions for 'C:{customised path}\\ssh-key-project.pem' are too open.
# It is required that your private key files are NOT accessible by others.
# This private key will be ignored.

## Solution
윈도우 cmd 혹은 tabby 등 터미널에서 pem 파일을 이용해 다른 서버에 접근할 경우,
pem 파일이 특정 경로에 위치해야 접근 가능하다.

### 접근 경로
C:\Users\{user}\.ssh\ssh-key-project.pem



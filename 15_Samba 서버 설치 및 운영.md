### 1. Samba 서버 소개:

Samba는 리눅스 및 유닉스 계열 운영 체제에서 Windows와 호환되는 파일 및 프린터 공유를 제공하는 오픈 소스 소프트웨어입니다. 주로 SMB/CIFS 프로토콜을 사용하여 파일 및 프린터를 Windows 클라이언트와 공유하고, 리눅스 시스템을 Windows 네트워크에 통합하는 데 사용됩니다.

### 2. 리눅스에서 윈도우즈 폴더와 프린터 사용:
![img_2.png](Image/14장부터%2017장/img_2.png)
Samba를 사용하여 리눅스 시스템에서 Windows 폴더 및 프린터를 공유하려면 다음 단계를 따를 수 있습니다:

- **Samba 설치:**
  Samba를 설치해야 합니다. 대부분의 리눅스 배포판에서는 패키지 관리자를 통해 간단하게 설치할 수 있습니다.

  ```bash
  # Ubuntu/Debian
  sudo apt-get install samba

  # CentOS/RHEL
  sudo yum install samba
  ```

- **Samba 서비스 시작 및 활성화:**
  Samba 서비스를 시작하고 부팅 시 자동으로 활성화합니다.

  ```bash
  sudo systemctl start smbd
  sudo systemctl enable smbd
  ```

- **Samba 사용자 계정 설정:**
  Samba에 접근할 수 있는 사용자를 설정합니다.

  ```bash
  sudo smbpasswd -a username
  ```

- **Samba 설정 파일 수정:**
  Samba의 주요 설정 파일인 `smb.conf`를 수정하여 공유 폴더 및 프린터를 정의합니다.

  ```plaintext
  [global]
    workgroup = WORKGROUP
    security = user

  [shared_folder]
    path = /path/to/shared/folder
    writable = yes
    guest ok = yes
    read only = no

  [printer]
    path = /path/to/printer
    printable = yes
    printer name = myprinter
    guest ok = yes
  ```

  `global` 섹션은 모든 자원들의 공유를 위한 설정을, `[shared_folder]` 및 `[printer]`는 각각 공유되는 디렉토리 및 프린터에 대한 설정을 나타냅니다.

- **Samba 서비스 재시작:**
  설정을 적용하려면 Samba 서비스를 다시 시작합니다.

  ```bash
  sudo systemctl restart smbd
  ```

### 3. Samba 서버 설정 파일 (`smb.conf`):

`/etc/samba/smb.conf`는 Samba의 주요 설정 파일이며, 전역 설정과 각 공유 디렉토리에 대한 설정이 포함됩니다.

```plaintext
[global]
  workgroup = WORKGROUP
  security = user

[shared_folder]
  path = /path/to/shared/folder
  writable = yes
  guest ok = yes
  read only = no

[printer]
  path = /path/to/printer
  printable = yes
  printer name = myprinter
  guest ok = yes
```

- `[global]`: 모든 자원들의 공유를 위한 설정
- `[shared_folder]`: 공유되는 디렉토리에 대한 설정
- `[printer]`: 공유되는 프린터에 대한 설정

이 설정은 간단한 예시이며, 실제 환경에 따라 필요한 설정을 추가하거나 수정할 수 있습니다.
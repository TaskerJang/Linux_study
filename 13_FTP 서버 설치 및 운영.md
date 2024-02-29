### 1. FTP(파일 전송 프로토콜)
FTP는 파일을 서버와 클라이언트 간에 전송하기 위한 프로토콜입니다. 주로 웹 호스팅이나 서버 관리 등에서 파일 업로드 및 다운로드에 사용됩니다. FTP는 클라이언트와 서버 간에 데이터를 전송하는 데 사용되며, 일반적으로 사용자 이름 및 암호를 통해 인증됩니다.

### 2. pure-ftpd 서버 구축 절차
`pure-ftpd`는 간단하면서도 안정적인 FTP 서버 중 하나입니다. 아래는 Linux 환경에서 `pure-ftpd`를 사용하여 FTP 서버를 구축하는 기본적인 절차입니다. 이 예제는 Ubuntu 기반을 기준으로 합니다.

   a. **패키지 설치:**

      
      sudo apt-get update
      sudo apt-get install pure-ftpd
      

   b. **서버 구성 및 실행:**

`pure-ftpd`는 시스템 서비스로 실행될 수 있습니다.
      
      sudo service pure-ftpd start
      

   c. **사용자 계정 생성:**

FTP에 접속할 수 있는 사용자 계정을 생성합니다.
      
      sudo pure-pw useradd USERNAME -u ftpuser -d /path/to/directory
      sudo pure-pw mkdb
     

   d. **인증 설정:**

설정 파일을 열어서 특정 사용자 및 인증 방법을 구성합니다.
      
      sudo nano /etc/pure-ftpd/conf/UnixAuthentication
      

   e. **실제 서비스 설정:**

쓰기 권한 및 다른 서비스 설정을 수정하려면 설정 파일을 엽니다.
      
      sudo nano /etc/pure-ftpd/conf/pure-ftpd.conf
      

   f. **서비스 재시작:**

설정 변경 후에는 서비스를 재시작합니다.
      
      sudo service pure-ftpd restart
      

   g. **방화벽 구성:**

방화벽에서 FTP 포트(기본적으로 21번)를 열어주어 외부에서 접속할 수 있도록 합니다.

   이러한 단계는 참고용이며, 실제로는 보안 및 구체적인 운영 환경에 따라 추가 구성이 필요할 수 있습니다. 서비스를 운영 전에 보안 및 사용자 권한을 적절히 설정하여 안전하게 운영하는 것이 중요합니다.
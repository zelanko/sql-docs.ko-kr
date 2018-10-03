---
title: Linux의 SQL Server 문제 해결 | Microsoft Docs
description: Linux에서 SQL Server를 사용 하는 것에 대 한 문제 해결 팁을 제공 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.openlocfilehash: 5adbd3cb58791fc38d534a64d1a76ab2e329c1bc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610500"
---
# <a name="troubleshoot-sql-server-on-linux"></a>Linux에서 SQL Server 문제 해결

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에는 Docker 컨테이너 또는 Linux에서 실행 하는 Microsoft SQL Server의 문제를 해결 하는 방법을 설명 합니다. Linux의 SQL Server의 문제를 해결할 때의 알려진된 제한 사항이 지원 되는 기능을 검토 해야 합니다 [Linux 릴리스 노트의 SQL Server](sql-server-linux-release-notes.md)합니다.

> [!TIP]
> 자주 묻는 질문에 답변에 대 한 참조를 [의 SQL Server Linux FAQ](sql-server-linux-faq.md)합니다.

## <a id="connection"></a> 연결 오류 문제 해결
Linux SQL Server에 연결 하는 데 문제가 있는 경우 확인할 몇 가지 사항입니다. 

- 서버 이름 또는 IP 주소를 클라이언트 컴퓨터에서 연결할 수 있는지 확인 합니다.

   > [!TIP]
   > Ubuntu 컴퓨터의 IP 주소를 찾으려면 다음 예제와 같이 ifconfig 명령을 실행할 수 있습니다.
   >
   >   ```bash
   >   sudo ifconfig eth0 | grep 'inet addr'
   >   ```
   > Red Hat에 대 한 다음 예제와 같이 ip 주소를 사용할 수 있습니다.
   >
   >   ```bash
   >   sudo ip addr show eth0 | grep "inet"
   >   ```
   > 예외적으로이 기술은 Azure Vm에 연결합니다. Azure Vm에 대 한 [Azure portal에서 VM에 대 한 공용 IP를 찾을](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#connect)합니다.

- 해당 하는 경우 방화벽에서 SQL Server 포트 (기본값 1433)를 열었는지 확인 합니다.

- Azure Vm에 대 한 권한이 있는지 확인 한 [기본 SQL Server 포트에 대 한 네트워크 보안 그룹 규칙](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#remote)합니다.

- 사용자 이름 및 암호 포함 되지 않도록 입력 오류 또는 추가 공백이 나 잘못 된 대/소문자 구분을 확인 합니다.

- 다음 예제와 같이 서버 이름 사용 하 여 프로토콜 및 포트 번호를 명시적으로 설정 하려고 합니다. **tcp:servername, 1433**합니다.

- 연결 오류 및 시간 제한에는 네트워크 연결 문제가 발생할 수 있습니다. 사용자 연결 정보 및 네트워크 연결을 확인 한 후 연결을 다시 시도 합니다.

## <a name="manage-the-sql-server-service"></a>SQL Server 서비스를 관리 합니다.

다음 섹션에는 시작, 중지, 다시 시작 및 SQL Server 서비스의 상태를 확인 하는 방법을 보여 줍니다. 

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>Ubuntu 및 Red Hat Enterprise Linux (RHEL)-서비스 관리 

이 명령을 사용 하 여 SQL Server 서비스의 상태를 확인 합니다.

   ```bash
   sudo systemctl status mssql-server
   ```

중지, 시작 또는 다음 명령을 사용 하 여 필요에 따라 SQL Server 서비스를 다시 시작 수 있습니다.

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

### <a name="manage-the-execution-of-the-mssql-docker-container"></a>Mssql Docker 컨테이너의 실행을 관리

다음 명령을 실행 하 여 만든된 최신 SQL Server Docker 컨테이너의 상태 및 컨테이너 ID를 가져올 수 있습니다 (아래에서 ID가 합니다 **컨테이너 ID** 열):

   ```bash
   sudo docker ps -l
   ```
   
다음 명령을 사용 하 여 필요에 따라 SQL Server 서비스를 다시 시작 하거나 중지할 수 있습니다.
   
   ```bash
   sudo docker stop <container ID>
   sudo docker restart <container ID>
   ```

> [!TIP]
> Docker에 대 한 자세한 문제 해결 팁을 참조 하세요 [SQL Server 문제 해결 Docker 컨테이너](sql-server-linux-configure-docker.md#troubleshooting)합니다.

## <a name="access-the-log-files"></a>로그 파일에 액세스
   
Linux 및 Docker 설치에서 /var/opt/mssql/log/errorlog 파일에 SQL Server 엔진 로그입니다. 이 디렉터리를 찾을 수 'superuser' 모드에 포함 되도록 해야 합니다.

설치 관리자 로그 여기: / var/선택/mssql/설정-< 설치 시간을 나타내는 타임 스탬프 > 다음과 같은 '고양이' 또는 'vim' 같은 모든 utf-16 호환 도구를 사용 하 여 오류 로그 파일을 찾아볼 수 있습니다. 

   ```bash
   sudo cat errorlog
   ```

원한다 면 변환할 수도 있습니다 파일 읽기를 사용 하 여 u t F-8로 '자세한' 또는 '작은' 다음 명령을 사용 하 여:
   
   ```bash
   sudo iconv –f UTF-16LE –t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>확장 이벤트

SQL 명령을 통해 확장된 이벤트를 쿼리할 수 있습니다.  확장된 이벤트에 대 한 자세한 정보를 찾을 수 있습니다 [여기](https://technet.microsoft.com/library/bb630282.aspx):

## <a name="crash-dumps"></a>크래시 덤프 

Linux에서 로그 디렉터리에 덤프를 찾습니다. Linux 코어 덤프에 대해 /var/opt/mssql/log 디렉터리에서 확인 (. tar.gz2 확장) 또는 SQL 미니 덤프 (.mdmp 확장명)

코어 덤프에 대 한 
   ```bash
   sudo ls /var/opt/mssql/log | grep .tar.gz2 
   ```

SQL 덤프에 대 한 
   ```bash
   sudo ls /var/opt/mssql/log | grep .mdmp 
   ```
   
## <a name="start-sql-server-in-minimal-configuration-or-in-single-user-mode"></a>최소 구성에서 하거나 단일 사용자 모드로 SQL Server를 시작 합니다.

### <a name="start-sql-server-in-minimal-configuration-mode"></a>최소 구성 모드로 SQL Server 시작
예를 들어 오버 커밋 메모리 같은 구성 값의 설정 때문에 서버를 시작할 수 없을 경우에 유용합니다.
  
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -f
   ```

### <a name="start-sql-server-in-single-user-mode"></a>단일 사용자 모드로 SQL Server를 시작 합니다.
특정 상황에서는 시작 옵션-m을 사용 하 여 단일 사용자 모드로 SQL Server의 인스턴스를 시작 해야 합니다. 예를 들어 서버 구성 옵션을 변경하거나 손상된 master 데이터베이스 또는 다른 시스템 데이터베이스를 복구하려고 할 수도 있습니다. 예를 들어, 하려는 서버 구성 옵션을 변경 하거나 손상된 된 master 데이터베이스 또는 다른 시스템 데이터베이스를 복구 합니다.   

단일 사용자 모드로 SQL Server를 시작 합니다.
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m
   ```

SQLCMD 사용 하 여 단일 사용자 모드로 SQL Server를 시작 합니다.
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
   ```
  
> [!WARNING]  
>  "mssql" 사용자와 함께 Linux에서 SQL Server를 시작하여 향후 시작 문제를 방지합니다. "sudo -u mssql /opt/mssql/bin/sqlservr [시작 옵션]" 예제 

실수로 다른 사용자를 사용 하 여 SQL Server를 시작한, 다시 systemd를 사용 하 여 SQL Server를 시작 하기 전에 'mssql' 사용자에 게 SQL Server 데이터베이스 파일의 소유권을 변경 해야 합니다. 예를 들어, 'mssql' 사용자에 게 /var/opt/mssql 아래에 있는 모든 데이터베이스 파일의 소유권을 변경 하려면 다음 명령을 실행합니다

   ```bash
   chown -R mssql:mssql /var/opt/mssql/
   ```

## <a name="rebuild-system-databases"></a>시스템 데이터베이스 다시 작성
마지막 수단으로는 master 다시 작성 하도록 선택할 수 있습니다 하 고 모델 데이터베이스를 다시 기본 버전입니다.

> [!WARNING]
> 이러한 절차를 수행 **SQL Server 시스템 데이터를 모두 삭제** 구성한! 사용자 데이터베이스 (하지만 자체 사용자 데이터베이스가 아닌)에 대 한 정보가 포함 됩니다. 다음을 비롯 한 시스템 데이터베이스에 저장 된 다른 정보와 삭제 됩니다: 마스터 키 정보, 모든 인증서에 마스터, SA 로그인 암호 msdb에서 작업 관련 정보, msdb 및 sp_configure 옵션에서 DB 메일 정보 로드 합니다. 의미를 이해 하는 경우에 사용!

1. SQL Server를 중지 합니다.

   ```bash
   sudo systemctl stop mssql-server
   ```

1. 실행할 **sqlservr** 사용 하 여 합니다 **강제 설치** 매개 변수입니다. 

   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr --force-setup
   ```
   
   > [!WARNING]
   > 이전 경고를 확인 하세요. 이 실행 해야는 또한 합니다 **mssql** 여기에 표시 된 대로 사용자입니다.

1. "복구를 완료 되었습니다." 메시지가 표시, CTRL + C 키를 누릅니다. SQL Server 종료

1. SA 암호를 다시 구성 합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-sa-password
   ```
   
1. SQL Server를 시작 하 고 서버를 다시 구성 합니다. 여기에 복원 또는 다시 사용자 데이터베이스를 연결 합니다.

   ```bash
   sudo systemctl start mssql-server
   ```

## <a name="improve-performance"></a>성능 향상

데이터베이스 디자인, 하드웨어 및 작업 부하 요구 등 성능에 영향을 주는 여러 요인이 있습니다. 성능 향상을 위해 찾으려는 경우이 문서에서 모범 사례를 검토 하 여 시작 [성능 모범 사례 및 Linux의 SQL Server에 대 한 구성 지침](sql-server-linux-performance-best-practices.md)합니다. 다음 성능 문제 해결에 대 한 사용 가능한 도구 중 일부를 탐색 합니다.

- [쿼리 저장소](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [시스템 동적 관리 뷰 (Dmv)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
- [SQL Server Management Studio의 성능 대시보드](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)

## <a name="common-issues"></a>일반적인 문제

1. 원격 SQL Server 인스턴스에 연결할 수 없습니다.

   문서의 문제 해결 섹션을 참조 하세요 [Linux의 SQL Server에 연결](#connection)합니다.

2. 오류: 호스트 이름이 15 자 여야 합니다 또는 작습니다.

   SQL Server Debian 패키지를 설치 하려는 컴퓨터의 이름이 15 자를 초과할 때마다 발생 하는 알려진 문제입니다. 컴퓨터의 이름을 변경 이외의 대안이 없습니다 않습니다. 이 작업을 수행 하는 하나의 방법은 호스트 파일을 편집 하 고 컴퓨터를 다시 부팅 하 여 것입니다. 다음 [웹 사이트 가이드](http://www.cyberciti.biz/faq/ubuntu-change-hostname-command/) 이에 대해 자세히 설명 합니다.

3. 시스템 관리 (SA) 암호를 재설정 합니다.

   시스템 관리자 (SA) 암호를 잊어버린 다른 이유로 다시 설정 해야 할 경우 다음이 단계를 수행 합니다.

   > [!NOTE]
   > 다음 단계를 일시적으로 SQL Server 서비스를 중지합니다.

   호스트 터미널에 로그인 하 고 다음 명령을 실행 한 다음 지시에 따라 SA 암호를 다시 설정:

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. 암호에 특수 문자를 사용 합니다.

   SQL Server 로그인 암호에 일부 문자를 사용 하는 경우 터미널에서 Linux 명령에서 사용 하는 경우 백슬래시를 사용 하 여 이스케이프 해야 합니다. 예를 들어, 이스케이프 처리 해야 달러 기호 ($)를 사용 하 여 언제 든 지 터미널 명령/셸 스크립트에서:

   작동 하지 않습니다.

   ```bash
   sudo sqlcmd -S myserver -U sa -P Test$$
   ```

   작동 합니다.

   ```bash
   sqlcmd -S myserver -U sa -P Test\$\$
   ```

   리소스: [특수 문자](http://tldp.org/LDP/abs/html/special-chars.html)
   [Escaping](http://tldp.org/LDP/abs/html/escapingsection.html)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

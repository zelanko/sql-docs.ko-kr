---
title: SQL Server on Linux 문제 해결
description: SQL Server on Linux 사용에 대한 문제 해결 팁을 제공합니다.
author: VanMSFT
ms.author: vanto
ms.date: 05/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.openlocfilehash: a4103e22facbb717b6797b91d8b218cc6ce4b0b7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79288117"
---
# <a name="troubleshoot-sql-server-on-linux"></a>SQL Server on Linux 문제 해결

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux 또는 Docker 컨테이너에서 실행되는 Microsoft SQL Server 문제를 해결하는 방법을 설명합니다. SQL Server on Linux 문제를 해결하는 경우 [SQL Server on Linux 릴리스 정보](sql-server-linux-release-notes.md)에서 지원되는 기능 및 알려진 제한 사항을 검토해야 합니다.

> [!TIP]
> 질문과 대답은 [SQL Server on Linux FAQ](sql-server-linux-faq.md)를 참조하세요.

## <a name="troubleshoot-connection-failures"></a><a id="connection"></a> 연결 오류 문제 해결
Linux SQL Server에 연결하는 데 어려움이 있는 경우 몇 가지 사항을 확인해야 합니다.

- **localhost**를 사용하여 로컬로 연결할 수 없는 경우에는 IP 주소 127.0.0.1을 대신 사용해 보세요. **localhost**가 이 주소에 제대로 매핑되어 있지 않을 수 있습니다.

- 클라이언트 머신에서 서버 이름 또는 IP 주소에 연결할 수 있는지 확인합니다.

   > [!TIP]
   > Ubuntu 머신의 IP 주소를 찾으려면 다음 예제와 같이 ifconfig 명령을 실행하면 됩니다.
   >
   >   ```bash
   >   sudo ifconfig eth0 | grep 'inet addr'
   >   ```
   > Red Hat의 경우 다음 예제와 같이 ip addr을 사용할 수 있습니다.
   >
   >   ```bash
   >   sudo ip addr show eth0 | grep "inet"
   >   ```
   > 이 기술에는 Azure VM과 관련된 한 가지 예외가 있습니다. Azure VM의 경우 [Azure Portal에서 VM의 공용 IP를 찾습니다](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#connect).

- 해당하는 경우 방화벽에서 SQL Server 포트(기본값 1433)를 열었는지 확인합니다.

- Azure VM의 경우 [기본 SQL Server 포트에 대한 네트워크 보안 그룹 규칙](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#remote)이 있는지 확인합니다.

- 사용자 이름 및 암호에 오타, 추가 공백 또는 잘못된 대/소문자가 포함되지 않았는지 확인합니다.

- 다음 예제와 같이 서버 이름을 사용하여 프로토콜 및 포트 번호를 명시적으로 설정해 봅니다. **tcp:servername,1433**.

- 네트워크 연결 문제로 인해 연결 오류 및 시간 초과가 발생할 수도 있습니다. 연결 정보 및 네트워크 연결을 확인한 후 연결을 다시 시도하세요.

## <a name="manage-the-sql-server-service"></a>SQL Server 서비스 관리

다음 섹션에서는 SQL Server 서비스를 시작, 중지, 다시 시작하고 해당 상태를 확인하는 방법을 보여 줍니다.

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>RHEL(Red Hat Enterprise Linux) 및 Ubuntu에서 mssql-server 서비스 관리 

다음 명령을 사용하여 SQL Server 서비스의 상태를 확인합니다.

   ```bash
   sudo systemctl status mssql-server
   ```

다음 명령을 사용하여 필요에 따라 SQL Server 서비스를 중지, 시작 또는 다시 시작할 수 있습니다.

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

### <a name="manage-the-execution-of-the-mssql-docker-container"></a>mssql Docker 컨테이너의 실행 관리

다음 명령을 실행하여 생성된 최신 SQL Server Docker 컨테이너의 상태 및 컨테이너 ID를 가져올 수 있습니다(ID는 **CONTAINER ID** 열에 있음).

   ```bash
   sudo docker ps -l
   ```
   
다음 명령을 사용하여 필요에 따라 SQL Server 서비스를 중지하거나 다시 시작할 수 있습니다.
   
   ```bash
   sudo docker stop <container ID>
   sudo docker restart <container ID>
   ```

> [!TIP]
> Docker에 대한 자세한 문제 해결 팁은 [SQL Server Docker 컨테이너 문제 해결](sql-server-linux-configure-docker.md#troubleshooting)을 참조하세요.

## <a name="access-the-log-files"></a>로그 파일 액세스
   
SQL Server 엔진은 Linux 및 Docker 설치의 /var/opt/mssql/log/errorlog 파일에 기록합니다. 이 디렉터리를 찾아보려면 '슈퍼 사용자' 모드에 있어야 합니다.

설치 관리자는 /var/opt/mssql/setup-<설치 시간을 나타내는 타임스탬프>에 기록합니다. 다음과 같이 'vim' 또는 'cat' 같은 UTF-16 호환 도구를 사용하여 오류 로그 파일을 찾아볼 수 있습니다. 

   ```bash
   sudo cat errorlog
   ```

원하는 경우 다음 명령을 사용하여 파일을 UTF-8로 변환하여 '자세히' 또는 '간단히' 읽을 수도 있습니다.
   
   ```bash
   sudo iconv -f UTF-16LE -t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>확장 이벤트

SQL 명령을 통해 확장 이벤트를 쿼리할 수 있습니다.  확장 이벤트에 대한 자세한 내용은 [여기](https://technet.microsoft.com/library/bb630282.aspx)를 참조하세요.

## <a name="crash-dumps"></a>크래시 덤프 

Linux의 로그 디렉터리에서 덤프를 검색합니다. /var/opt/mssql/log 디렉터리에서 Linux 코어 덤프(.tar.gz2 확장) 또는 SQL 미니덤프(.mdmp 확장)가 있는지 확인합니다.

코어 덤프의 경우 
   ```bash
   sudo ls /var/opt/mssql/log | grep .tar.gz2 
   ```

SQL 덤프의 경우 
   ```bash
   sudo ls /var/opt/mssql/log | grep .mdmp 
   ```
   
## <a name="start-sql-server-in-minimal-configuration-or-in-single-user-mode"></a>최소 구성 또는 단일 사용자 모드로 SQL Server 시작

### <a name="start-sql-server-in-minimal-configuration-mode"></a>최소 구성 모드로 SQL Server 시작
예를 들어 오버 커밋 메모리 같은 구성 값의 설정 때문에 서버를 시작할 수 없을 경우에 유용합니다.
  
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -f
   ```

### <a name="start-sql-server-in-single-user-mode"></a>단일 사용자 모드로 SQL Server 시작
특정 상황에서는 시작 옵션 -m을 사용하여 SQL Server의 인스턴스를 단일 사용자 모드로 시작해야 할 수 있습니다. 예를 들어 서버 구성 옵션을 변경하거나 손상된 master 데이터베이스 또는 다른 시스템 데이터베이스를 복구하려고 할 수도 있습니다. 예를 들어 서버 구성 옵션을 변경하거나 손상된 master 데이터베이스 또는 다른 시스템 데이터베이스를 복구하려고 할 수도 있습니다.   

단일 사용자 모드로 SQL Server 시작
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m
   ```

SQLCMD를 사용하여 단일 사용자 모드로 SQL Server 시작
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
   ```
  
> [!WARNING]  
>  "mssql" 사용자와 함께 Linux에서 SQL Server를 시작하여 향후 시작 문제를 방지합니다. "sudo -u mssql /opt/mssql/bin/sqlservr [시작 옵션]" 예제 

실수로 다른 사용자로 SQL Server를 시작한 경우에는 systemd를 사용하여 SQL Server를 시작하기 전에 SQL Server 데이터베이스 파일의 소유권을 다시 'mssql' 사용자로 변경해야 합니다. 예를 들어 /var/opt/mssql 아래에 있는 모든 데이터베이스 파일의 소유권을 'mssql' 사용자로 변경하려면 다음 명령을 실행합니다.

   ```bash
   chown -R mssql:mssql /var/opt/mssql/
   ```

## <a name="rebuild-system-databases"></a>시스템 데이터베이스 다시 빌드
마지막 수단으로 master 및 model 데이터베이스를 다시 기본 버전으로 다시 빌드하도록 선택할 수 있습니다.

> [!WARNING]
> 이 단계를 통해 구성한 **모든 SQL Server 시스템 데이터가 삭제**됩니다. 여기에는 사용자 데이터베이스에 대한 정보가 포함되며 사용자 데이터베이스 자체는 포함되지 않습니다. 시스템 데이터베이스에 저장된 마스터 키 정보, master에 로드된 인증서, SA 로그인 암호, msdb의 작업 관련 정보, msdb의 DB 메일 정보 및 sp_configure 옵션을 포함한 다른 정보도 삭제됩니다. 의미를 이해하는 경우에만 사용하세요.

1. SQL Server를 중지합니다.

   ```bash
   sudo systemctl stop mssql-server
   ```

1. **force-setup** 매개 변수를 사용하여 **sqlservr**을 실행합니다. 

   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr --force-setup
   ```
   
   > [!WARNING]
   > 이전 경고를 참조하세요. 또한 여기에 표시된 대로 이 명령을 **mssql** 사용자로 실행해야 합니다.

1. “복구가 완료 되었습니다.” 라는 메시지가 표시되면 CTRL+C를 누릅니다. 이렇게 하면 SQL Server가 종료됩니다.

1. SA 암호를 다시 구성합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-sa-password
   ```
   
1. SQL Server를 시작하고 서버를 다시 구성합니다. 여기에는 사용자 데이터베이스 복원 및 다시 연결이 포함됩니다.

   ```bash
   sudo systemctl start mssql-server
   ```

## <a name="improve-performance"></a>성능 향상

데이터베이스 디자인, 하드웨어 및 워크로드 요청을 포함하여 성능에 영향을 주는 여러 요인이 있습니다. 성능을 향상시키려면 먼저 [SQL Server on Linux에 대한 성능 모범 사례 및 구성 지침](sql-server-linux-performance-best-practices.md) 문서에서 모범 사례를 검토하세요. 그런 다음, 성능 문제 해결에 사용할 수 있는 몇 가지 도구를 살펴봅니다.

- [쿼리 저장소](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [시스템 DMV(동적 관리 뷰)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
- [SQL Server Management Studio의 성능 대시보드](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)

## <a name="common-issues"></a>일반적인 문제

1. 원격 SQL Server 인스턴스에 연결할 수 없습니다.

   [SQL Server on Linux에 연결](#connection) 문서의 문제 해결 섹션을 참조하세요.

2. 오류: 호스트 이름은 15자 이하여야 합니다.

   이 문제는 SQL Server Debian 패키지를 설치하려는 머신의 이름이 15자를 초과할 때마다 발생하는 알려진 문제입니다. 현재는 머신 이름을 변경하는 것 외에는 해결 방법이 없습니다. 이를 수행하는 한 가지 방법은 호스트 이름 파일을 편집하고 머신을 다시 부팅하는 것입니다. 다음 [웹 사이트 가이드](https://www.cyberciti.biz/faq/ubuntu-change-hostname-command/)에서 이 내용을 자세히 설명합니다.

3. SA(시스템 관리) 암호 다시 설정.

   SA(시스템 관리자) 암호를 잊어버린 경우 또는 다른 이유로 암호를 다시 설정해야 하는 경우 이 단계를 수행합니다.

   > [!NOTE]
   > 다음 단계는 SQL Server 서비스를 일시적으로 중지합니다.

   호스트 터미널에 로그인하고, 다음 명령을 실행하고, 프롬프트에 따라 SA 암호를 다시 설정합니다.

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. 암호에 특수 문자 사용.

   SQL Server 로그인 암호에 일부 문자를 사용하는 경우 터미널에서 Linux 명령에 해당 문자를 사용할 때 백슬래시로 이스케이프해야 할 수 있습니다. 예를 들어 터미널 명령/셸 스크립트에서 사용하는 경우에는 항상 달러 기호($)를 이스케이프해야 합니다.

   작동하지 않음:

   ```bash
   sudo sqlcmd -S myserver -U sa -P Test$$
   ```

   작동함:

   ```bash
   sqlcmd -S myserver -U sa -P Test\$\$
   ```

   리소스: [특수 문자](https://tldp.org/LDP/abs/html/special-chars.html)
   [이스케이프](https://tldp.org/LDP/abs/html/escapingsection.html)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

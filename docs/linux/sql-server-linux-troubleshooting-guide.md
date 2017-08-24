---
title: "Linux에서 SQL Server 문제 해결 | Microsoft Docs"
description: "SQL Server 2017 Linux에서 사용 하기 위한 문제 해결 팁을 제공 합니다."
author: annashres
ms.author: anshrest
manager: jhubbard
ms.date: 05/08/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 21b7d94bcf15e1ae2d99dd44f4b0030929b92111
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="troubleshoot-sql-server-on-linux"></a>Linux에서 SQL Server 문제 해결

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

이 문서에서는 Docker 컨테이너에서 또는 Linux에서 실행 중인 Microsoft SQL Server 문제를 해결 하는 방법을 설명 합니다. Linux에서 SQL Server의 문제를 해결할 때이 비공개 미리 보기 릴리스의 제한 사항 기억 확인 하십시오. 이러한 목록을 찾을 수 있습니다는 [릴리스 정보](sql-server-linux-release-notes.md)합니다.

## <a id="connection"></a>연결 오류 문제 해결
Linux SQL Server에 연결 하는 데 문제가 있는 경우 확인할 몇 가지 있습니다. 

- 서버 이름 또는 IP 주소는 클라이언트 컴퓨터에서 연결할 수 있는지 확인 합니다.

   > [!TIP]
   > Ubuntu 컴퓨터의 IP 주소를 확인 하려면 다음 예제와 같이 ifconfig 명령을 실행할 수 있습니다.
   >
   >   ```bash
   >   sudo ifconfig eth0 | grep 'inet addr'
   >   ```
   > Red Hat에 대 한 다음 예제와 같이 ip 주소를 사용할 수 있습니다.
   >
   >   ```bash
   >   sudo ip addr show eth0 | grep "inet"
   >   ```
   > 이 기술은 한 가지 예외는 Azure Vm을 연결합니다. Azure Vm에 대 한 [Azure 포털에서 VM에 대 한 공용 IP를 찾을](sql-server-linux-azure-virtual-machine.md#connect)합니다.

- 해당 하는 경우 방화벽에서 SQL Server 포트 (기본값 1433)를 열었는지 확인 합니다.

- Azure Vm에 대 한 권한이 있는지 확인 한 [기본 SQL Server 포트에 대 한 네트워크 보안 그룹 규칙](sql-server-linux-azure-virtual-machine.md#remote)합니다.

- 사용자 이름 및 암호 포함 되지 않도록 입력 오류 또는 추가 공백이 나 잘못 된 대/소문자를 확인 합니다.

- 다음과 같은 서버 이름으로 프로토콜 및 포트 번호를 명시적으로 설정 하려고: **tcp:servername, 1433**합니다.

- 연결 오류 및 시간 제한에도 네트워크 연결 문제가 발생할 수 있습니다. 연결 정보 및 네트워크 연결을 확인 한 후 연결을 다시 시도 하십시오.

## <a name="manage-the-sql-server-service"></a>SQL Server 서비스를 관리 합니다.

다음 섹션에는 시작, 중지, 다시 시작 하 고, SQL Server 서비스의 상태를 확인 하는 방법을 보여 줍니다. 

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>Red Hat Enterprise Linux (RHEL) 및 Ubuntu mssql 서버 서비스를 관리 합니다. 

이 명령을 사용 하는 SQL Server 서비스의 상태의 상태를 확인 합니다.

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

(ID는 "컨테이너 ID" 열 수는) 다음 명령을 실행 하 여 만든된 최신 SQL Server Docker 컨테이너의 상태 및 컨테이너 ID를 가져올 수 있습니다.

   ```bash
   sudo docker ps -l
   ```
   
다음 명령을 사용 하 여 필요에 따라 SQL Server 서비스를 다시 시작 하거나 중지할 수 있습니다.
   
   ```bash
   sudo docker stop <container ID>
   sudo docker restart <container ID>
   ```

> [!TIP]
> Docker에 대 한 자세한 문제 해결 팁에 대 한 참조 [SQL Server 문제 해결 Docker 컨테이너](sql-server-linux-configure-docker.md#troubleshooting)합니다.

## <a name="access-the-log-files"></a>로그 파일에 액세스
   
SQL Server 엔진 Linux과 Docker를 모두 설치에서 /var/opt/mssql/log/errorlog 파일에 로깅. 이 디렉터리를 찾을 수 'superuser' 모드에 포함 되도록 해야 합니다.

설치 관리자 로그 여기: / var/옵트인/mssql/설정-< 설치의 시간을 나타내는 타임 스탬프 > 다음과 같이 '분류기' 또는 'vim' 같은 모든 u t F-16 호환 도구 사용 하 여 오류 로그 파일을 찾아볼 수 있습니다. 

   ```bash
   sudo cat errorlog
   ```

원하는 경우 변환할 수도 있습니다는 파일을 u t F-8로 읽을 수 '' 다소간 '' 다음 명령을 사용 합니다.
   
   ```bash
   sudo iconv –f UTF-16LE –t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>확장 이벤트

SQL 명령을 통해 확장된 이벤트를 쿼리할 수 있습니다.  확장된 이벤트에 대 한 자세한 정보를 찾을 수 [여기](https://technet.microsoft.com/en-us/library/bb630282.aspx):

## <a name="crash-dumps"></a>크래시 덤프 

Linux에서 로그 디렉터리에 덤프를 찾습니다. Linux 핵심 덤프 /var/opt/mssql/log 디렉터리에서 확인 하십시오 (. tar.gz2 확장) 또는 SQL 미니 덤프 (.mdmp 확장명)

코어 덤프에 대 한 
   ```bash
   sudo ls /var/opt/mssql/log | grep .tar.gz2 
   ```

SQL 덤프에 대 한 
   ```bash
   sudo ls /var/opt/mssql/log | grep .mdmp 
   ```

## <a name="common-issues"></a>일반적인 문제

1. 원격 SQL Server 인스턴스에 연결할 수 없습니다.

   항목의 문제 해결 섹션을 참조 [Linux에서 SQL Server에 연결](#connection)합니다.

2. 오류: 호스트 이름이 15 자 여야 합니다 또는 작습니다.

   SQL Server Debian 패키지 설치를 시도 하는 컴퓨터 이름이 15 자 보다 긴 될 때마다 발생 하는 알려진 문제입니다. 현재 제공 아닌 컴퓨터의 이름을 변경 하는 다른 해결 방법은 없습니다. 이 작업을 수행할 가지 방법은 호스트 파일을 편집 하는 컴퓨터 다시 부팅 하는 것입니다. 다음 [웹 사이트 가이드](http://www.cyberciti.biz/faq/ubuntu-change-hostname-command/) 이에 대해 자세히 설명 합니다.

3. 시스템 관리 (SA) 암호 다시 설정 합니다.

   시스템 관리자 (SA) 암호를 잊어버린 또는 다른 이유로 다시 설정 해야 할 경우에 다음이 단계를 수행 하십시오.

   > [!NOTE]
   > 다음 단계에 따라 SQL Server 서비스를 일시적으로 중지 됩니다.

   호스트 터미널을 로그인 하 고 다음 명령을 실행 한 다음 지시에 따라 SA 암호를 다시 설정:

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. 암호에 특수 문자를 사용 합니다.

   SQL Server 로그인 암호의 일부 문자를 사용 하는 경우 Linux 터미널에 사용 하는 경우 이스케이프 해야 합니다. $ 이스케이프 해야 합니다는 백슬래시 문자를 사용 하 여 언제 든 지 사용 터미널 명령/셸 스크립트에서:

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

## <a name="support"></a>지원

커뮤니티를 통해 사용 가능 하 고 엔지니어링 팀에서 모니터링 되는 것이 지원은합니다. 특정 질문에 대 한 다음 리소스를 사용 합니다.

- [DBA 스택 Exchange](https://dba.stackexchange.com/questions/tagged/sql-server): 데이터베이스 관리 질문 하기
- [스택 오버플로](http://stackoverflow.com/questions/tagged/sql-server): 개발 질문 하기
- [MSDN 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver): 기술 관련 질문
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback): 요청 기능 및 버그를 보고 합니다.
- [Reddit](https://www.reddit.com/r/SQLServer/): SQL Server에 설명

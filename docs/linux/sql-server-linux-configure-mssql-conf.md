---
title: Linux에서 SQL Server 설정 구성 | Microsoft Docs
description: 이 문서에서는 Linux의 SQL Server 설정을 구성 하려면 mssql-conf 도구를 사용 하는 방법을 설명 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/31/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.openlocfilehash: a8a4cd22d4637c2d6fd86bf61d25c16dda728394
ms.sourcegitcommit: fafb9b5512695b8e3fc2891f9c5e3abd7571d550
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50753590"
---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>Mssql-conf 도구를 사용 하 여 Linux에서 SQL Server 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

**mssql conf** Red Hat Enterprise Linux, SUSE Linux Enterprise Server 및 Ubuntu 용 SQL Server 2017을 사용 하 여 설치 하는 구성 스크립트입니다. 이 유틸리티를 사용 하 여 다음 매개 변수를 설정할 수 있습니다.

|||
|---|---|
| [에이전트](#agent) | SQL Server 에이전트를 사용 하도록 설정 |
| [데이터 정렬](#collation) | Linux의 SQL Server에 대 한 새 데이터 정렬을 설정 합니다. |
| [고객 의견](#customerfeedback) | SQL Server Microsoft에 피드백을 전송 여부를 선택 합니다. |
| [데이터베이스 메일 프로필](#dbmail) | Linux의 SQL Server에 대 한 기본 데이터베이스 메일 프로필을 설정 합니다. |
| [기본 데이터 디렉터리](#datadir) | 새 SQL Server 데이터베이스 데이터 파일 (.mdf)에 대 한 기본 디렉터리를 변경 합니다. |
| [기본 로그 디렉터리](#datadir) | 새 SQL Server 데이터베이스 로그 (.ldf) 파일에 대 한 기본 디렉터리를 변경합니다. |
| [기본 master 데이터베이스 디렉터리](#masterdatabasedir) | Master 데이터베이스 및 로그 파일용 기본 디렉터리를 변경합니다.|
| [기본 master 데이터베이스 파일 이름](#masterdatabasename) | Master 데이터베이스 파일의 이름을 변경합니다. |
| [기본 덤프 디렉터리](#dumpdir) | 새 메모리 덤프 및 기타 문제 해결 파일에 대 한 기본 디렉터리를 변경 합니다. |
| [기본 오류 로그 디렉터리](#errorlogdir) | 새 SQL Server 오류 로그, 기본 Profiler 추적, 시스템 상태 세션 XE를 및 Hekaton 세션 XE 파일용 기본 디렉터리를 변경합니다. |
| [기본 백업 디렉터리](#backupdir) | 새 백업 파일용 기본 디렉터리를 변경 합니다. |
| [형식 덤프](#coredump) | 수집 덤프 메모리 덤프 파일의 유형을 선택 합니다. |
| [고가용성](#hadr) | 가용성 그룹을 사용 하도록 설정 합니다. |
| [로컬 감사 디렉터리](#localaudit) | 로컬 감사 파일에 추가할 디렉터리를 설정 합니다. |
| [로캘](#lcid) | 사용 하도록 SQL Server에 대 한 로캘을 설정 합니다. |
| [메모리 제한](#memorylimit) | SQL Server에 대 한 메모리 한계를 설정 합니다. |
| [TCP 포트](#tcpport) | SQL Server 연결을 수신 하는 위치는 포트를 변경 합니다. |
| [TLS](#tls) | 전송 수준 보안을 구성 합니다. |
| [추적 플래그](#traceflags) | 사용 하려는 서비스는 추적 플래그를 설정 합니다. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

**mssql conf** 와 함께 설치 되는 구성 스크립트는 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] Red Hat Enterprise Linux, SUSE Linux Enterprise Server 및 Ubuntu에 대 한 합니다. 이 유틸리티를 사용 하 여 다음 매개 변수를 설정할 수 있습니다.

|||
|---|---|
| [에이전트](#agent) | SQL Server 에이전트를 사용 하도록 설정 |
| [데이터 정렬](#collation) | Linux의 SQL Server에 대 한 새 데이터 정렬을 설정 합니다. |
| [고객 의견](#customerfeedback) | SQL Server Microsoft에 피드백을 전송 여부를 선택 합니다. |
| [데이터베이스 메일 프로필](#dbmail) | Linux의 SQL Server에 대 한 기본 데이터베이스 메일 프로필을 설정 합니다. |
| [기본 데이터 디렉터리](#datadir) | 새 SQL Server 데이터베이스 데이터 파일 (.mdf)에 대 한 기본 디렉터리를 변경 합니다. |
| [기본 로그 디렉터리](#datadir) | 새 SQL Server 데이터베이스 로그 (.ldf) 파일에 대 한 기본 디렉터리를 변경합니다. |
| [기본 master 데이터베이스 파일 디렉터리](#masterdatabasedir) | 기존 SQL 설치에서 master 데이터베이스 파일용 기본 디렉터리를 변경합니다.|
| [기본 master 데이터베이스 파일 이름](#masterdatabasename) | Master 데이터베이스 파일의 이름을 변경합니다. |
| [기본 덤프 디렉터리](#dumpdir) | 새 메모리 덤프 및 기타 문제 해결 파일에 대 한 기본 디렉터리를 변경 합니다. |
| [기본 오류 로그 디렉터리](#errorlogdir) | 새 SQL Server 오류 로그, 기본 Profiler 추적, 시스템 상태 세션 XE를 및 Hekaton 세션 XE 파일용 기본 디렉터리를 변경합니다. |
| [기본 백업 디렉터리](#backupdir) | 새 백업 파일용 기본 디렉터리를 변경 합니다. |
| [형식 덤프](#coredump) | 수집 덤프 메모리 덤프 파일의 유형을 선택 합니다. |
| [고가용성](#hadr) | 가용성 그룹을 사용 하도록 설정 합니다. |
| [로컬 감사 디렉터리](#localaudit) | 로컬 감사 파일에 추가할 디렉터리를 설정 합니다. |
| [로캘](#lcid) | 사용 하도록 SQL Server에 대 한 로캘을 설정 합니다. |
| [메모리 제한](#memorylimit) | SQL Server에 대 한 메모리 한계를 설정 합니다. |
| [Microsoft Distributed Transaction Coordinator](#msdtc) | Linux에서 MSDTC 문제 해결 및 구성 합니다. |
| [MLServices Eula](#mlservices-eula) | Mlservices 패키지에 대 한 R 및 Python Eula를 수락 합니다. SQL Server 2019 에서만 적용 됩니다.|
| [TCP 포트](#tcpport) | SQL Server 연결을 수신 하는 위치는 포트를 변경 합니다. |
| [TLS](#tls) | 전송 수준 보안을 구성 합니다. |
| [추적 플래그](#traceflags) | 사용 하려는 서비스는 추적 플래그를 설정 합니다. |

::: moniker-end

> [!TIP]
> 이러한 설정 중 일부 환경 변수를 사용 하 여 구성할 수도 있습니다. 자세한 내용은 [환경 변수를 사용 하 여 SQL Server 구성 설정](sql-server-linux-configure-environment-variables.md)합니다.

## <a name="usage-tips"></a>사용 팁

* Always On 가용성 그룹 및 공유 디스크 클러스터의 경우 항상 각 노드에서 동일한 구성 변경 내용을 확인 합니다.

* 공유 디스크 클러스터 시나리오의 경우 하지를 다시 시작 합니다 **mssql server** 서비스 변경 내용을 적용 합니다. SQL Server가 응용 프로그램으로 실행 됩니다. 대신 다음 다시 온라인 상태가 오프 라인 리소스를 수행 합니다.

* 이러한 예제는 전체 경로 지정 하 여 mssql conf를 실행 합니다. **/opt/mssql/bin/mssql-conf**합니다. 대신 해당 경로로 이동 하려는 경우 mssql conf 현재 디렉터리의 컨텍스트에서 실행: **. / mssql conf**합니다.

## <a id="agent"></a> SQL Server 에이전트를 사용 하도록 설정

합니다 **sqlagent.enabled** 수 있습니다 [SQL Server 에이전트](sql-server-linux-run-sql-server-agent-job.md)합니다. SQL Server 에이전트는 기본적으로 사용 하지 않도록 설정 합니다. 하는 경우 **sqlagent.enabled** 없는 mssql.conf 설정 파일에서 SQL Server는 SQL Server 에이전트는 사용 하지 않도록 내부적으로 가정 합니다.

이 설정을 변경 하려면 다음 단계를 사용 합니다.

1. SQL Server 에이전트를 사용 하도록 설정 합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   ```

2. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="collation"></a> SQL Server 데이터 정렬 변경

합니다 **데이터 정렬 설정** 옵션 지원 되는 데이터 정렬 중에 데이터 정렬 값을 변경 합니다.

1. 첫 번째 [모든 사용자 데이터베이스를 백업](sql-server-linux-backup-and-restore-database.md) 서버의 합니다.

1. 다음 사용 합니다 [sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) 저장 프로시저를 사용자 데이터베이스를 분리 합니다.

1. 실행 합니다 **데이터 정렬 설정** 옵션 및 지시를 따릅니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. Mssql conf 유틸리티는 지정 된 데이터 정렬 값으로 변경 하 고 서비스를 다시 시작 하려고 합니다. 모든 오류가 있는 경우 롤백됩니다 데이터 정렬을 이전 값입니다.

1. 사용자 데이터베이스 백업을 복원 합니다.

지원 되는 데이터 정렬 목록을 실행 합니다 [sys.fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) 함수: `SELECT Name from sys.fn_helpcollations()`합니다.

## <a id="customerfeedback"></a> 고객 피드백을 구성 합니다.

합니다 **telemetry.customerfeedback** 설정은 SQL Server 또는 Microsoft에 피드백을 전송 하는지 여부를 변경 합니다. 기본적으로이 값 설정할지 **true** 모든 버전에 대 한 합니다. 값을 변경 하려면 다음 명령을 실행 합니다.

> [!IMPORTANT]
> 해제할 수 있습니다 하지 고객 의견을 무료로 SQL Server, Express 및 Developer 버전입니다.

1. 사용 하 여 루트로 mssql conf 스크립트를 실행 합니다 **설정** 에 대 한 명령을 **telemetry.customerfeedback**합니다. 다음 예제에서는 지정 하 여 고객 피드백 해제 **false**합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

자세한 내용은 [Linux의 SQL Server에 대 한 의견](sql-server-linux-customer-feedback.md) 하며 [SQL Server 개인정보취급방침](http://go.microsoft.com/fwlink/?LinkID=868444)합니다.

## <a id="datadir"></a> 기본 데이터 또는 로그 디렉터리 위치 변경

합니다 **filelocation.defaultdatadir** 하 고 **filelocation.defaultlogdir** 설정을 새 데이터베이스 및 로그 파일이 만들어지는 위치를 변경 합니다. 기본적으로이 위치는 /var/opt/mssql/data는입니다. 이러한 설정을 변경 하려면 다음 단계를 사용 합니다.

1. 새 데이터베이스에 대 한 대상 디렉터리 데이터 및 로그 파일을 만듭니다. 다음 예제에서는 새 **/tmp 데이터** 디렉터리:

   ```bash
   sudo mkdir /tmp/data
   ```

1. 소유자 및 디렉터리의 그룹을 변경 합니다 **mssql** 사용자:

   ```bash
   sudo chown mssql /tmp/data
   sudo chgrp mssql /tmp/data
   ```

1. Mssql conf를 사용 하 여 사용 하 여 기본 데이터 디렉터리를 변경 합니다 **설정** 명령:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

1. 이제이 새 위치에 생성 된 새 데이터베이스에 대 한 모든 데이터베이스 파일 저장할 됩니다. 새 데이터베이스의 로그 (.ldf) 파일의 위치를 변경 하려는 경우 다음 "set" 명령을 사용할 수 있습니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. 이 명령은 또한 가정/tmp 로그 디렉터리가 있는 사용자 및 그룹에 속하는 것 **mssql**합니다.


## <a id="masterdatabasedir"></a> 기본 master 데이터베이스 파일 디렉터리 위치 변경

합니다 **filelocation.masterdatafile** 하 고 **filelocation.masterlogfile** 설정 변경 내용을 master 데이터베이스 파일에 대 한 SQL Server 엔진은 여기서 위치 합니다. 기본적으로이 위치는 /var/opt/mssql/data는입니다.

이러한 설정을 변경 하려면 다음 단계를 사용 합니다.

1. 새 오류 로그 파일에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp masterdatabasedir** 디렉터리:

   ```bash
   sudo mkdir /tmp/masterdatabasedir
   ```

1. 소유자 및 디렉터리의 그룹을 변경 합니다 **mssql** 사용자:

   ```bash
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
   ```

1. Mssql conf를 사용 하 여 사용 하 여 마스터 데이터 및 로그 파일에 대 한 기본 master 데이터베이스 디렉터리를 변경 합니다 **설정** 명령:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
   ```

   > [!NOTE]
   > 마스터 데이터 및 로그 파일을 이동 하는 것 외에도 다른 모든 시스템 데이터베이스의 기본 위치는 이동이 합니다.

1. SQL Server 서비스를 중지 합니다.

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Master.mdf 및 masterlog.ldf를 이동 합니다.

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf 
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
   ```

1. SQL Server 서비스를 시작 합니다.

   ```bash
   sudo systemctl start mssql-server
   ```

   > [!NOTE]
   > SQL Server는 지정된 된 디렉터리에서 master.mdf 및 mastlog.ldf 파일을 찾을 수 없으면, 시스템 데이터베이스의 템플릿 복사본이 지정된 된 디렉터리에 자동으로 생성 됩니다 및 SQL Server 성공적으로 시작 됩니다. 그러나 사용자 데이터베이스, 서버 로그인, 서버 인증서, 암호화 키, SQL 에이전트 작업 또는 이전 SA 로그인 암호와 같은 메타 데이터를 새 마스터 데이터베이스에서 업데이트 되지 않습니다. SQL Server를 중지 하 고 지정된 된 새 위치에 이전 master.mdf 및 mastlog.ldf 이동할 기존 메타 데이터를 사용 하 여 계속 하려면 SQL Server를 시작 해야 합니다.
 
## <a id="masterdatabasename"></a> Master 데이터베이스 파일의 이름 변경

합니다 **filelocation.masterdatafile** 하 고 **filelocation.masterlogfile** 설정 변경 내용을 master 데이터베이스 파일에 대 한 SQL Server 엔진은 여기서 위치 합니다. Master 데이터베이스 및 로그 파일의 이름을 변경 하려면이 사용할 수도 있습니다. 

이러한 설정을 변경 하려면 다음 단계를 사용 합니다.

1. SQL Server 서비스를 중지 합니다.

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Mssql conf를 사용 하 여 사용 하 여 마스터 데이터 및 로그 파일에 대 한 예상 되는 마스터 데이터베이스 이름을 변경 합니다 **설정** 명령:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /var/opt/mssql/data/masternew.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.mastlogfile /var/opt/mssql/data/mastlognew.ldf
   ```

   > [!IMPORTANT]
   > Master 데이터베이스의 이름을 변경 및 SQL Server를 성공적으로 시작 된 후 로그 파일 수 있습니다. 초기 실행 하기 전에 SQL Server에서는 master.mdf 및 mastlog.ldf 이라는 이름으로 파일을 사용 합니다.

1. Master 데이터베이스 데이터 및 로그 파일의 이름 변경 

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /var/opt/mssql/data/masternew.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /var/opt/mssql/data/mastlognew.ldf
   ```

1. SQL Server 서비스를 시작 합니다.

   ```bash
   sudo systemctl start mssql-server
   ```

## <a id="dumpdir"></a> 기본 덤프 디렉터리 위치 변경

합니다 **filelocation.defaultdumpdir** 변경 하는 메모리 및 SQL 덤프 생성 되는 충돌이 있을 때마다 기본 위치를 설정 합니다. 기본적으로 이러한 파일은 /var/opt/mssql/log에 생성 됩니다.

이 새 위치를 설정 하려면 다음 명령을 사용 합니다.

1. 새 덤프 파일에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp 덤프** 디렉터리:

   ```bash
   sudo mkdir /tmp/dump
   ```

1. 소유자 및 디렉터리의 그룹을 변경 합니다 **mssql** 사용자:

   ```bash
   sudo chown mssql /tmp/dump
   sudo chgrp mssql /tmp/dump
   ```

1. Mssql conf를 사용 하 여 사용 하 여 기본 데이터 디렉터리를 변경 합니다 **설정** 명령:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="errorlogdir"></a> 기본 오류 로그 파일 디렉터리 위치 변경

합니다 **filelocation.errorlogfile** 설정 변경 내용을 새 오류 로그, 기본 프로파일러 추적, 시스템 상태 세션과 XE 및 Hekaton XE 세션 파일 만들어지는 위치입니다. 기본적으로이 위치는 /var/opt/mssql/log은입니다. SQL 오류 로그 파일 설정 되어 있는 디렉터리에는 다른 로그에 대 한 기본 로그 디렉터리를 됩니다.

이러한 설정을 변경 하려면:

1. 새 오류 로그 파일에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp 로그** 디렉터리:

   ```bash
   sudo mkdir /tmp/logs
   ```

1. 소유자 및 디렉터리의 그룹을 변경 합니다 **mssql** 사용자:

   ```bash
   sudo chown mssql /tmp/logs
   sudo chgrp mssql /tmp/logs
   ```

1. Mssql conf를 사용 하 여 사용 하 여 기본 오류 로그 파일 이름을 변경 합니다 **설정** 명령:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.errorlogfile /tmp/logs/errorlog
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```


## <a id="backupdir"></a> 기본 백업 디렉터리 위치 변경

합니다 **filelocation.defaultbackupdir** 변경 내용을 백업 파일이 생성 되는 기본 위치를 설정 합니다. 기본적으로 이러한 파일은 /var/opt/mssql/data에 생성 됩니다.

이 새 위치를 설정 하려면 다음 명령을 사용 합니다.

1. 새 백업 파일에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/백업** 디렉터리:

   ```bash
   sudo mkdir /tmp/backup
   ```

1. 소유자 및 디렉터리의 그룹을 변경 합니다 **mssql** 사용자:

   ```bash
   sudo chown mssql /tmp/backup
   sudo chgrp mssql /tmp/backup
   ```

1. Mssql conf "집합" 명령 사용 하 여 기본 백업 디렉터리를 변경 하려면 사용 합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="coredump"></a> 코어 덤프 설정 지정

SQL Server 프로세스 중에 예외가 발생 하는 경우 SQL Server 메모리 덤프를 만듭니다.

SQL Server를 수집 한다는 덤프 메모리 형식을 제어에 대 한 두 가지 옵션 사항이: **coredump.coredumptype** 하 고 **coredump.captureminiandfull**합니다. 이러한 코어 덤프 캡처의 두 단계와 관련이 있습니다. 

첫 번째 단계 캡처에 의해 제어 됩니다 합니다 **coredump.coredumptype** 예외 중 생성 된 덤프 파일의 형식을 결정 하는 설정입니다. 두 번째 단계는 경우 사용 하도록 설정 합니다 **coredump.captureminiandfull** 설정 합니다. 경우 **coredump.captureminiandfull** 덤프를 true로 설정 하 여 지정 된 파일 **coredump.coredumptype** 생성 됩니다 및 두 번째 미니 덤프가 생성 됩니다. 설정 **coredump.captureminiandfull** false 사용 하지 않도록 설정 하려면 두 번째 캡처를 시도 합니다.

1. 사용 하 여 미니 및 전체 덤프를 캡처하려면 여부를 결정 합니다 **coredump.captureminiandfull** 설정 합니다.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    기본값: **false**

1. 덤프 파일의 유형을 지정 합니다 **coredump.coredumptype** 설정 합니다.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    기본값: **miniplus**

    다음 표에서 가능한 **coredump.coredumptype** 값입니다.

    | 형식 | Description |
    |-----|-----|
    | **mini** | 미니 최소 덤프 파일 형식입니다. 스레드 및 프로세스의 모듈을 확인 하려면 Linux 시스템 정보를 사용 합니다. 덤프는 호스트 환경 스레드 스택 및 모듈을 포함합니다. 간접 메모리 참조 또는 전역 포함 되지 않습니다. |
    | **miniplus** | Mini, miniPlus 비슷합니다 있지만 추가 메모리를 포함 하는 것입니다. SQLPAL 및 덤프에는 다음과 같은 메모리 영역을 추가 하 고 호스트 환경의 내부 구조를 인식 합니다.</br></br> -다양 한 전역 변수</br> -모든 메모리 64TB 이상</br> -모든 지역에 이름이 지정 **/proc/$ pid/매핑**</br> 스레드 및 스택 간접 메모리</br> 스레드 정보</br> -Teb의 및 Peb의 연결</br> 모듈 정보</br> VMM 및 VAD 트리 |
    | **filtered** | 빼기 기반 필터링된 사용 하 여 디자인 있는 프로세스의 모든 메모리를 특별히 제외 되지 않은 포함 합니다. 디자인은 SQLPAL 및 호스트 환경에 특정 지역 덤프에서 제외의 내부 구조를 이해 합니다.
    | **full** | 전체 영역을 모두 포함 하는 전체 프로세스 덤프에 위치한 **/proc/$ pid/매핑**합니다. 이 통해 제어 되지 **coredump.captureminiandfull** 설정 합니다. |

## <a id="dbmail"></a> Linux에서 SQL Server에 대 한 기본 데이터베이스 메일 프로필 설정

합니다 **sqlpagent.databasemailprofile** 전자 메일 경고에 대 한 기본 DB 메일 프로필을 설정할 수 있습니다.

```bash
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```
## <a id="hadr"></a> 고가용성

합니다 **hadr.hadrenabled** 옵션을 사용 하면 SQL Server 인스턴스에서 가용성 그룹입니다. 다음 명령은 가용성 그룹을 설정 하 여 사용 하도록 설정 **hadr.hadrenabled** 1입니다. 설정 적용 하려면 SQL Server를 다시 시작 해야 합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

가용성 그룹을 사용 하 여 사용이 방법에 대 한 자세한 내용은 다음 두 항목을 참조 하세요.

- [Linux의 SQL Server에 대 한 Always On 가용성 그룹 구성](sql-server-linux-availability-group-configure-ha.md)
- [Linux의 SQL Server에 대 한 읽기-배율 가용성 그룹 구성](sql-server-linux-availability-group-configure-rs.md)


## <a id="localaudit"></a> 로컬 감사 디렉터리 설정

합니다 **telemetry.userrequestedlocalauditdirectory** 설정은 로컬 감사를 활성화 하 고 디렉터리를 설정할 수 있는 로컬 감사 로그가 있습니다 만들어집니다.

1. 새 로컬 감사 로그에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/감사** 디렉터리:

   ```bash
   sudo mkdir /tmp/audit
   ```

1. 소유자 및 디렉터리의 그룹을 변경 합니다 **mssql** 사용자:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. 사용 하 여 루트로 mssql conf 스크립트를 실행 합니다 **설정할** 명령에 **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

자세한 내용은 [Linux의 SQL Server에 대 한 고객 의견](sql-server-linux-customer-feedback.md)합니다.

## <a id="lcid"></a> SQL Server 로캘을 변경합니다

합니다 **language.lcid** 를 지원 되는 언어 식별자 (LCID) 변경 내용을 SQL Server 로캘을 설정 합니다. 

1. 다음 예에서는 프랑스어로 로캘을 변경 (1036):

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. 변경 내용을 적용 하려면 SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="memorylimit"></a> 메모리 제한 설정

합니다 **memory.memorylimitmb** SQL Server에 컨트롤의 크기 (MB)의 사용 가능한 실제 메모리를 설정 합니다. 기본값은 실제 메모리의 80%입니다.

1. 사용 하 여 루트로 mssql conf 스크립트를 실행 합니다 **설정** 에 대 한 명령을 **memory.memorylimitmb**합니다. 다음 예제에서는 SQL server 3.25 GB (3328 MB)에 사용 가능한 메모리를 변경합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. 변경 내용을 적용 하려면 SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="msdtc"></a> MSDTC를 구성 합니다.

합니다 **network.rpcport** 하 고 **distributedtransaction.servertcpport** 설정은 MSDTC Microsoft Distributed Transaction Coordinator ()를 구성 하는 데 사용 됩니다. 이러한 설정을 변경 하려면 다음 명령을 실행 합니다.

1. 사용 하 여 루트로 mssql conf 스크립트를 실행 합니다 **설정** "network.rpcport"에 대 한 명령:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport <rcp_port>
   ```

2. "Distributedtransaction.servertcpport" 설정 합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport <servertcpport_port>
   ```

이러한 값을 설정 하는 것 외에도 라우팅을 구성 하 고 방화벽 포트 135에 대 한 업데이트도 해야 합니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 하세요. [Linux에서 MSDTC를 구성 하는 방법](sql-server-linux-configure-msdtc.md)합니다.

가지 mssql-conf 모니터링과 MSDTC 문제 해결에 사용할 수 있는 다른 몇 가지 설정이 있습니다. 다음 테이블에는 이러한 설정이 간략하게 설명합니다. 용도에 대 한 자세한 내용은 Windows 지원 문서에서 세부 정보를 참조 하세요 [MS DTC에 대 한 진단 추적을 사용 하는 방법을](https://support.microsoft.com/en-us/help/926099/how-to-enable-diagnostic-tracing-for-ms-dtc-on-a-windows-based-compute)합니다.

| mssql conf 설정 | Description |
|---|---|
| distributedtransaction.allowonlysecurerpccalls | 분산된 트랜잭션에 대 한 보안만 rpc 호출을 구성 합니다. |
| distributedtransaction.fallbacktounsecurerpcifnecessary | 배포에 대 한 보안만 rpc 호출을 구성 합니다. |트랜잭션
| distributedtransaction.maxlogsize | DTC 트랜잭션 로그 파일 크기 (mb)입니다. 기본값은 64MB |
| distributedtransaction.memorybuffersize | 추적 저장 되는 순환 버퍼 크기입니다. 이 크기 (mb) 이며 기본값은 10MB |
| distributedtransaction.servertcpport | MSDTC rpc 서버 포트 |
| distributedtransaction.trace_cm | 연결 관리자에서 추적 |
| distributedtransaction.trace_contact | 풀 연락처 및 연락처를 추적합니다. |
| distributedtransaction.trace_gateway | 추적 게이트웨이 원본 |
| distributedtransaction.trace_log | 로그 추적 |
| distributedtransaction.trace_misc | 추적을 다른 범주로 분류 될 수 없습니다. |
| distributedtransaction.trace_proxy | MSDTC 프록시에 생성 되는 추적 |
| distributedtransaction.trace_svc | 추적 서비스 및.exe 파일 시작 |
| distributedtransaction.trace_trace | 자체 추적 인프라 |
| distributedtransaction.trace_util | 여러 위치에서 호출 되는 추적 유틸리티 루틴 |
| distributedtransaction.trace_xa | XA 트랜잭션 관리자 (XATM) 추적 원본 |
| distributedtransaction.tracefilepath | 추적 파일을 저장할 폴더 |
| distributedtransaction.turnoffrpcsecurity | 분산된 트랜잭션에 대 한 RPC 보안을 사용할지 설정 합니다. |

::: moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="mlservices-eula"></a> MLServices Eula에 동의

추가 [기계 학습 R 또는 Python 패키지](sql-server-linux-setup-machine-learning.md) 데이터베이스 엔진 R 및 Python의 오픈 소스 배포에 대 한 라이선스 동의 필요 합니다. 다음 표에서 모든 사용 가능한 명령 또는 mlservices Eula 관련 된 옵션을 열거 합니다. 동일한 EULA 매개 변수는 설치 된 기능에 따라 R 및 Python에 사용 됩니다.

```bash
# For all packages: database engine and mlservices
# Setup prompts for mlservices EULAs, which you need to accept
sudo /opt/mssql/bin/mssql-conf setup

# Add R or Python to an existing installation
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml

# Alternative valid syntax
# Add R or Python to an existing installation
sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y

# Rescind EULA acceptance
sudo /opt/mssql/bin/mssql-conf unset EULA accepteulaml
```

EULA 동의 직접 추가할 수도 있습니다는 [mssql.conf 파일](#mssql-conf-format):

```ini
[EULA]
accepteula = Y
accepteulaml = Y
```

:::moniker-end

## <a id="tcpport"></a> TCP 포트를 변경 합니다.

합니다 **network.tcpport** 변경 내용을 SQL Server 연결에 대 한 수신 대기 하는 TCP 포트를 설정 합니다. 기본적으로이 포트를 1433으로 설정 됩니다. 포트를 변경 하려면 다음 명령을 실행 합니다.

1. "Network.tcpport"에 대 한 "set" 명령 사용 하 여 루트로 mssql conf 스크립트를 실행 합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

2. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

3. SQL Server에 연결할 때 호스트 이름 또는 IP 주소를 다음 쉼표 (,)를 사용 하 여 사용자 지정 포트를 지정 해야 합니다. 예를 들어, SQLCMD에 연결 하려면 다음 명령을 사용 합니다.

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a id="tls"></a> TLS 설정 지정

Linux에서 실행 중인 SQL Server 인스턴스에 대 한 TLS를 구성 하는 다음 옵션입니다.

|옵션 |Description |
|--- |--- |
|**network.forceencryption** |1 인 경우 다음 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 암호화에 대 한 모든 연결을 강제로 수행 합니다. 기본적으로이 옵션은 0입니다. |
|**network.tlscert** |인증서에 절대 경로 파일 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] TLS를 사용 합니다. 예: `/etc/ssl/certs/mssql.pem` 인증서 파일 mssql 계정에서 액세스할 수 있어야 합니다. 사용 하 여 파일에 대 한 액세스를 제한 하는 것이 좋습니다 `chown mssql:mssql <file>; chmod 400 <file>`합니다. |
|**network.tlskey** |개인 키를 절대 경로 파일 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] TLS를 사용 합니다. 예: `/etc/ssl/private/mssql.key` 인증서 파일 mssql 계정에서 액세스할 수 있어야 합니다. 사용 하 여 파일에 대 한 액세스를 제한 하는 것이 좋습니다 `chown mssql:mssql <file>; chmod 400 <file>`합니다. |
|**network.tlsprotocols** |tls 프로토콜은 SQL Server에서 허용 하는 쉼표로 구분 된 목록입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 항상 가장 강력한 허용된 프로토콜을 협상 하도록 시도 합니다. 클라이언트가 허용 된 프로토콜을 지원 하지 않는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 연결 시도 거부 합니다.  호환성을 위해 모든 지원 되는 프로토콜 (예: 1.2, 1.1, 1.0) 기본적으로 허용 됩니다.  클라이언트에서 TLS 1.2를 지원 하는 경우 TLS 1.2만을 허용 하는 것이 좋습니다. |
|**network.tlsciphers** |허용 하는 암호 지정 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] TLS에 대 한 합니다. 이 문자열 당 포맷 되어 있어야 [OpenSSL의 암호화 목록 형식으로](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html)입니다. 일반적으로이 옵션을 변경할 필요가 없습니다. <br /> 기본적으로 다음 암호화 허용 됩니다. <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **network.kerberoskeytabfile** |Kerberos keytab 파일의 경로 |

TLS 설정을 사용 하 여 예제를 보려면 [Linux의 SQL Server 연결 암호화](sql-server-linux-encrypted-connections.md)합니다.

## <a id="traceflags"></a> 추적 플래그 사용/사용 안 함

이렇게 **traceflag** 옵션을 사용 하거나 SQL Server 서비스의 시작에 대 한 추적 플래그를 사용 하지 않도록 설정 합니다. 설정/해제는 추적 플래그는 다음 명령을 사용 합니다.

1. 다음 명령을 사용 하 여 추적 플래그를 사용 하도록 설정 합니다. Traceflag 1234 예를 들어:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. 별도로 지정 하 여 여러 추적 플래그를 설정할 수 있습니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. 유사한 방식으로 지정 하 고 추가 하 여 하나 이상의 활성화 된 추적 플래그를 비활성화할 수는 **해제** 매개 변수:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. 변경 내용을 적용 하려면 SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>설정을 제거합니다

사용 하 여 만든 설정을 해제할 `mssql-conf set`, 호출 **mssql conf** 사용 하 여는 `unset` 옵션 및 설정의 이름입니다. 이 기본값으로 효과적으로 돌아가기 설정을 지웁니다.

1. 다음 예에서는 삭제 합니다 **network.tcpport** 옵션입니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>현재 설정 보기

보려면의 내용을 출력 하려면 다음 명령을 실행 하는 설정을 구성 합니다 **mssql.conf** 파일:

```bash
sudo cat /var/opt/mssql/mssql.conf
```

이 파일에 표시 되지 않은 모든 설정을 기본값으로 사용 하는 참고 합니다. 다음 섹션에서는 샘플을 제공 **mssql.conf** 파일입니다.


## <a id="mssql-conf-format"></a> mssql.conf 형식

다음 **/var/opt/mssql/mssql.conf** 파일은 각 설정에 대 한 예제를 제공 합니다. 이 형식을 사용 하 여 수동으로 변경 하는 **mssql.conf** 필요에 따라 파일입니다. 파일을 수동으로 변경한 수행 하는 경우 변경 내용을 적용 하기 전에 SQL Server를 다시 시작 해야 있습니다. 사용 하 여 **mssql.conf** 파일 Docker를 사용 하 여 Docker 있어야 [데이터를 유지](sql-server-linux-configure-docker.md)합니다. 먼저 전체를 추가 **mssql.conf** 호스트 디렉터리에 파일을 다음 컨테이너를 실행 합니다. 이러한 예제가 [의견](sql-server-linux-customer-feedback.md)합니다.

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```ini
[EULA]
accepteula = Y

[coredump]
captureminiandfull = true
coredumptype = full

[filelocation]
defaultbackupdir = /var/opt/mssql/data/
defaultdatadir = /var/opt/mssql/data/
defaultdumpdir = /var/opt/mssql/data/
defaultlogdir = /var/opt/mssql/data/

[hadr]
hadrenabled = 0

[language]
lcid = 1033

[memory]
memorylimitmb = 4096

[network]
forceencryption = 0
ipaddress = 10.192.0.0
kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
tcpport = 1401
tlscert = /etc/ssl/certs/mssql.pem
tlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
tlskey = /etc/ssl/private/mssql.key
tlsprotocols = 1.2,1.1,1.0

[sqlagent]
databasemailprofile = default
errorlogfile = /var/opt/mssql/log/sqlagentlog.log
errorlogginglevel = 7

[telemetry]
customerfeedback = true
userrequestedlocalauditdirectory = /tmp/audit

[traceflag]
traceflag0 = 1204
traceflag1 = 2345
traceflag = 3456
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```ini
[EULA]
accepteula = Y
accepteulaml = Y

[coredump]
captureminiandfull = true
coredumptype = full

[distributedtransaction]
servertcpport = 51999

[filelocation]
defaultbackupdir = /var/opt/mssql/data/
defaultdatadir = /var/opt/mssql/data/
defaultdumpdir = /var/opt/mssql/data/
defaultlogdir = /var/opt/mssql/data/

[hadr]
hadrenabled = 0

[language]
lcid = 1033

[memory]
memorylimitmb = 4096

[network]
forceencryption = 0
ipaddress = 10.192.0.0
kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
rpcport = 13500
tcpport = 1401
tlscert = /etc/ssl/certs/mssql.pem
tlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
tlskey = /etc/ssl/private/mssql.key
tlsprotocols = 1.2,1.1,1.0

[sqlagent]
databasemailprofile = default
errorlogfile = /var/opt/mssql/log/sqlagentlog.log
errorlogginglevel = 7

[telemetry]
customerfeedback = true
userrequestedlocalauditdirectory = /tmp/audit

[traceflag]
traceflag0 = 1204
traceflag1 = 2345
traceflag = 3456
```

::: moniker-end

## <a name="next-steps"></a>다음 단계

대신 환경 변수를 사용 하 여 이러한 구성 변경 내용의 일부를, 참조 [환경 변수를 사용 하 여 SQL Server 구성 설정](sql-server-linux-configure-environment-variables.md)합니다.

다른 관리 도구 및 시나리오를 참조 하세요 [Linux의 SQL Server 관리](sql-server-linux-management-overview.md)합니다.

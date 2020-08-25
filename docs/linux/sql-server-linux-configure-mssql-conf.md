---
title: Linux에서 SQL Server 설정 구성
description: 이 문서에서는 mssql-conf 도구를 사용하여 Linux에서 SQL Server 설정을 구성하는 방법을 설명합니다.
author: VanMSFT
ms.author: vanto
ms.date: 08/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.openlocfilehash: 2e21b8f811af5887147ddb71b211e3a876b728d2
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180015"
---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>mssql-conf 도구를 사용하여 SQL Server on Linux 구성

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

**mssql-conf**는 Red Hat Enterprise Linux, SUSE Linux Enterprise Server 및 Ubuntu용 SQL Server 2017과 함께 설치되는 구성 스크립트입니다. 구성 값이 저장되는 [**mssql.conf 파일**](#mssql-conf-format)을 수정합니다. **mssql-conf** 유틸리티를 사용하여 다음 매개 변수를 설정할 수 있습니다.

|매개 변수|설명|
|---|---|
| [에이전트](#agent) | SQL Server 에이전트를 사용하도록 설정합니다. |
| [데이터 정렬](#collation) | SQL Server on Linux에 대한 새 데이터 정렬을 설정합니다. |
| [고객 의견](#customerfeedback) | SQL Server에서 사용자 의견을 Microsoft에 보낼지 여부를 선택합니다. |
| [데이터베이스 메일 프로필](#dbmail) | SQL Server on Linux의 기본 데이터베이스 메일 프로필을 설정합니다. |
| [기본 데이터 디렉터리](#datadir) | 새 SQL Server 데이터베이스 데이터 파일(.mdf)의 기본 디렉터리를 변경합니다. |
| [기본 로그 디렉터리](#datadir) | 새 SQL Server 데이터베이스 로그(.ldf) 파일의 기본 디렉터리를 변경합니다. |
| [기본 master 데이터베이스 디렉터리](#masterdatabasedir) | master 데이터베이스 및 로그 파일의 기본 디렉터리를 변경합니다.|
| [기본 master 데이터베이스 파일 이름](#masterdatabasename) | master 데이터베이스 파일의 이름을 변경합니다. |
| [기본 덤프 디렉터리](#dumpdir) | 새 메모리 덤프 및 기타 문제 해결 파일의 기본 디렉터리를 변경합니다. |
| [기본 오류 로그 디렉터리](#errorlogdir) | 새 SQL Server 오류 로그, 기본 프로파일러 추적, 시스템 상태 세션 XE 및 Hekaton 세션 XE 파일의 기본 디렉터리를 변경합니다. |
| [기본 백업 디렉터리](#backupdir) | 새 백업 파일의 기본 디렉터리를 변경합니다. |
| [덤프 형식](#coredump) | 수집할 덤프 메모리 덤프 파일의 형식을 선택합니다. |
| [고가용성](#hadr) | 가용성 그룹을 사용하도록 설정합니다. |
| [로컬 감사 디렉터리](#localaudit) | 로컬 감사 파일을 추가할 디렉터리를 설정합니다. |
| [로캘](#lcid) | 사용할 SQL Server의 로캘을 설정합니다. |
| [메모리 제한](#memorylimit) | SQL Server의 메모리 제한을 설정합니다. |
| [네트워크 설정](#network) | SQL Server에 대한 추가 네트워크 설정입니다. |
| [Microsoft Distributed Transaction Coordinator](#msdtc) | Linux에서 MSDTC를 구성하고 문제를 해결합니다. |
| [TCP 포트](#tcpport) | SQL Server가 연결을 수신 대기하는 포트를 변경합니다. |
| [TLS](#tls) | 전송 수준 보안을 구성합니다. |
| [추적 플래그](#traceflags) | 서비스에서 사용할 추적 플래그를 설정합니다. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

**mssql-conf**는 Red Hat Enterprise Linux, SUSE Linux Enterprise Server 및 Ubuntu용 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]와 함께 설치되는 구성 스크립트입니다. 이 유틸리티를 사용하여 다음 매개 변수를 설정할 수 있습니다.

|매개 변수|설명|
|---|---|
| [에이전트](#agent) | SQL Server 에이전트 사용 |
| [데이터 정렬](#collation) | SQL Server on Linux에 대한 새 데이터 정렬을 설정합니다. |
| [고객 의견](#customerfeedback) | SQL Server에서 사용자 의견을 Microsoft에 보낼지 여부를 선택합니다. |
| [데이터베이스 메일 프로필](#dbmail) | SQL Server on Linux의 기본 데이터베이스 메일 프로필을 설정합니다. |
| [기본 데이터 디렉터리](#datadir) | 새 SQL Server 데이터베이스 데이터 파일(.mdf)의 기본 디렉터리를 변경합니다. |
| [기본 로그 디렉터리](#datadir) | 새 SQL Server 데이터베이스 로그(.ldf) 파일의 기본 디렉터리를 변경합니다. |
| [기본 master 데이터베이스 파일 디렉터리](#masterdatabasedir) | 기존 SQL 설치에서 master 데이터베이스 파일의 기본 디렉터리를 변경합니다.|
| [기본 master 데이터베이스 파일 이름](#masterdatabasename) | master 데이터베이스 파일의 이름을 변경합니다. |
| [기본 덤프 디렉터리](#dumpdir) | 새 메모리 덤프 및 기타 문제 해결 파일의 기본 디렉터리를 변경합니다. |
| [기본 오류 로그 디렉터리](#errorlogdir) | 새 SQL Server 오류 로그, 기본 프로파일러 추적, 시스템 상태 세션 XE 및 Hekaton 세션 XE 파일의 기본 디렉터리를 변경합니다. |
| [기본 백업 디렉터리](#backupdir) | 새 백업 파일의 기본 디렉터리를 변경합니다. |
| [덤프 형식](#coredump) | 수집할 덤프 메모리 덤프 파일의 형식을 선택합니다. |
| [고가용성](#hadr) | 가용성 그룹을 사용하도록 설정합니다. |
| [로컬 감사 디렉터리](#localaudit) | 로컬 감사 파일을 추가할 디렉터리를 설정합니다. |
| [로캘](#lcid) | 사용할 SQL Server의 로캘을 설정합니다. |
| [메모리 제한](#memorylimit) | SQL Server의 메모리 제한을 설정합니다. |
| [Microsoft Distributed Transaction Coordinator](#msdtc) | Linux에서 MSDTC를 구성하고 문제를 해결합니다. |
| [MLServices EULA](#mlservices-eula) | mlservices 패키지에 대한 R 및 Python EULA에 동의합니다. SQL Server 2019에만 적용됩니다.|
| [네트워크 설정](#network) | SQL Server에 대한 추가 네트워크 설정입니다. |
| [outboundnetworkaccess](#mlservices-outbound-access) |[mlservices](sql-server-linux-setup-machine-learning.md) R, Python 및 Java 확장의 아웃바운드 네트워크 액세스를 사용하도록 설정합니다.|
| [TCP 포트](#tcpport) | SQL Server가 연결을 수신 대기하는 포트를 변경합니다. |
| [TLS](#tls) | 전송 수준 보안을 구성합니다. |
| [추적 플래그](#traceflags) | 서비스에서 사용할 추적 플래그를 설정합니다. |

::: moniker-end

> [!TIP]
> 이 설정 중 일부는 환경 변수를 사용하여 구성할 수도 있습니다. 자세한 내용은 [환경 변수를 사용하여 SQL Server 설정 구성](sql-server-linux-configure-environment-variables.md)을 참조하세요.

## <a name="usage-tips"></a>사용 팁

* Always On 가용성 그룹 및 공유 디스크 클러스터의 경우 항상 각 노드에서 동일하게 구성을 변경합니다.

* 공유 디스크 클러스터 시나리오의 경우 변경 내용을 적용하려면 **mssql-server** 서비스를 다시 시작하지 마세요. SQL Server가 애플리케이션으로 실행되고 있습니다. 대신, 리소스를 오프라인으로 전환한 후 다시 온라인으로 전환합니다.

* 이 예제에서는 전체 경로: **/opt/mssql/bin/mssql-conf**를 지정하여 mssql-conf를 실행합니다. 해당 경로로 이동하려면 현재 디렉터리 **./mssql-conf**의 컨텍스트에서 mssql-conf를 실행합니다.

## <a name="enable-sql-server-agent"></a><a id="agent"></a> SQL Server 에이전트 사용

**sqlagent.enabled** 설정은 [SQL Server 에이전트](sql-server-linux-run-sql-server-agent-job.md)를 사용하도록 설정합니다. 기본적으로 SQL Server 에이전트는 사용하지 않도록 설정됩니다. **sqlagent.enabled**가 mssql.conf 설정 파일에 있는 경우 SQL Server는 내부적으로 SQL Server 에이전트가 사용하지 않도록 설정되었다고 간주합니다.

이 설정을 변경하려면 다음 단계를 사용합니다.

1. SQL Server 에이전트를 사용하도록 설정합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   ```

2. SQL Server 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

### <a name="set-the-default-database-mail-profile-for-sql-server-on-linux"></a><a id="dbmail"></a> SQL Server on Linux의 기본 데이터베이스 메일 프로필 설정

**sqlpagent.databasemailprofile**을 사용하여 메일 경고의 기본 DB 메일 프로필을 설정할 수 있습니다.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```

### <a name="sql-agent-error-logs"></a><a id="agenterrorlog"></a> SQL 에이전트 오류 로그

**sqlpagent.errorlogfile** 및 **sqlpagent.errorlogginglevel** 설정을 사용하면 각각 SQL 에이전트 로그 파일 경로 및 로깅 수준을 설정할 수 있습니다. 

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.errorfile <path>
```

SQL 에이전트 로깅 수준은 다음과 같은 비트 마스크 값입니다.

- 1 = 오류
- 2 = 경고
- 4 = 정보

모든 수준을 캡처하려면 값으로 `7`을 사용합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.errorlogginglevel <level>
```

## <a name="change-the-sql-server-collation"></a><a id="collation"></a> SQL Server 데이터 정렬 변경

**set-collation** 옵션은 데이터 정렬 값을 지원되는 데이터 정렬로 변경합니다.

1. 먼저 서버에서 [모든 사용자 데이터베이스를 백업](sql-server-linux-backup-and-restore-database.md)합니다.

1. 그런 다음, [sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) 저장 프로시저를 사용하여 사용자 데이터베이스를 분리합니다.

1. **set-collation** 옵션을 실행하고 다음 프롬프트를 따릅니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. mssql-conf 유틸리티는 지정된 데이터 정렬 값으로 변경하고 서비스를 다시 시작하려고 시도합니다. 오류가 있는 경우 데이터 정렬을 이전 값으로 롤백합니다.

1. 사용자 데이터베이스 백업을 복원합니다.

지원되는 데이터 정렬 목록을 보려면 [sys.fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) 함수를 다음과 같이 실행합니다. `SELECT Name from sys.fn_helpcollations()`.

## <a name="configure-customer-feedback"></a><a id="customerfeedback"></a> 고객 의견 구성

**telemetry.customerfeedback** 설정은 SQL Server에서 사용자 의견을 Microsoft에 보낼지 여부를 변경합니다. 기본적으로 이 값은 모든 버전에 대해 **true**로 설정됩니다. 값을 변경하려면 다음 명령을 실행합니다.

> [!IMPORTANT]
> SQL Server, Express 및 Developer의 체험 버전에 대한 고객 의견은 끌 수 없습니다.

1. **telemetry.customerfeedback**에 대해 **set** 명령을 사용하여 mssql-conf 스크립트를 루트 권한으로 실행합니다. 다음 예제에서는 **false**를 지정하여 고객 의견을 끕니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. SQL Server 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

자세한 내용은 [SQL Server on Linux에 대한 고객 의견](sql-server-linux-customer-feedback.md) 및 [SQL Server 개인정보처리방침](https://go.microsoft.com/fwlink/?LinkID=868444)을 참조하세요.

## <a name="change-the-default-data-or-log-directory-location"></a><a id="datadir"></a> 기본 데이터 또는 로그 디렉터리 위치 변경

**filelocation.defaultdatadir** 및 **filelocation.defaultlogdir** 설정은 새 데이터베이스 및 로그 파일이 생성되는 위치를 변경합니다. 기본적으로 이 위치는 /var/opt/mssql/data입니다. 이 설정을 변경하려면 다음 단계를 사용합니다.

1. 새 데이터베이스 데이터 및 로그 파일의 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/data** 디렉터리를 만듭니다.

   ```bash
   sudo mkdir /tmp/data
   ```

1. 디렉터리의 소유자 및 그룹을 **mssql** 사용자로 변경합니다.

   ```bash
   sudo chown mssql /tmp/data
   sudo chgrp mssql /tmp/data
   ```

1. mssql-conf를 사용하여 **set** 명령으로 기본 데이터 디렉터리를 변경합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data
   ```

1. SQL Server 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

1. 이제 만들어진 새 데이터베이스의 모든 데이터베이스 파일이 새 위치에 저장됩니다. 새 데이터베이스의 로그(.ldf) 파일 위치를 변경하려는 경우 다음 “set” 명령을 사용할 수 있습니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. 또한 이 명령은 /tmp/log 디렉터리가 존재하고 사용자 및 그룹 **mssql**이 사용하고 있다고 간주합니다.


## <a name="change-the-default-master-database-file-directory-location"></a><a id="masterdatabasedir"></a> 기본 master 데이터베이스 파일 디렉터리 위치 변경

**filelocation.masterdatafile** 및 **filelocation.masterlogfile** 설정은 SQL Server 엔진이 master 데이터베이스 파일을 검색하는 위치를 변경합니다. 기본적으로 이 위치는 /var/opt/mssql/data입니다.

이 설정을 변경하려면 다음 단계를 사용합니다.

1. 새 오류 로그 파일의 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/masterdatabasedir** 디렉터리를 만듭니다.

   ```bash
   sudo mkdir /tmp/masterdatabasedir
   ```

1. 디렉터리의 소유자 및 그룹을 **mssql** 사용자로 변경합니다.

   ```bash
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
   ```

1. mssql-conf를 사용하여 **set** 명령으로 마스터 데이터 및 로그 파일의 기본 master 데이터베이스 디렉터리를 변경합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
   ```

   > [!NOTE]
   > 마스터 데이터와 로그 파일을 이동할 뿐 아니라 다른 모든 시스템 데이터베이스의 기본 위치도 이동합니다.

1. SQL Server 서비스를 중지합니다.

   ```bash
   sudo systemctl stop mssql-server
   ```

1. master.mdf 및 masterlog.ldf를 이동합니다.

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf 
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
   ```

1. SQL Server 서비스를 시작합니다.

   ```bash
   sudo systemctl start mssql-server
   ```

   > [!NOTE]
   > SQL Server가 지정된 디렉터리에서 master.mdf 및 mastlog.ldf 파일을 찾을 수 없으면 시스템 데이터베이스의 템플릿 기반 복사본이 지정된 디렉터리에 자동으로 생성되고 SQL Server가 시작됩니다. 그러나 사용자 데이터베이스, 서버 로그인, 서버 인증서, 암호화 키, SQL 에이전트 작업 또는 이전 SA 로그인 암호와 같은 메타데이터는 새 master 데이터베이스에서 업데이트되지 않습니다. SQL Server를 중지하고, 이전 master.mdf 및 mastlog.ldf를 지정된 새 위치로 이동하고, SQL Server를 시작하여 기존 메타데이터를 계속 사용해야 합니다.
 
## <a name="change-the-name-of-master-database-files"></a><a id="masterdatabasename"></a> master 데이터베이스 파일의 이름 변경

**filelocation.masterdatafile** 및 **filelocation.masterlogfile** 설정은 SQL Server 엔진이 master 데이터베이스 파일을 검색하는 위치를 변경합니다. 또한 master 데이터베이스 및 로그 파일의 이름을 변경하는 데 이 설정을 사용할 수 있습니다. 

이 설정을 변경하려면 다음 단계를 사용합니다.

1. SQL Server 서비스를 중지합니다.

   ```bash
   sudo systemctl stop mssql-server
   ```

1. mssql-conf를 사용하여 **set** 명령으로 마스터 데이터 및 로그 파일의 예상 master 데이터베이스 이름을 변경합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /var/opt/mssql/data/masternew.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.mastlogfile /var/opt/mssql/data/mastlognew.ldf
   ```

   > [!IMPORTANT]
   > SQL Server가 시작된 후 master 데이터베이스 및 로그 파일의 이름만 변경할 수 있습니다. 처음 실행하기 전에 SQL Server는 파일 이름이 master.mdf 및 mastlog.ldf일 것으로 예상합니다.

1. master 데이터베이스 및 로그 파일의 이름 변경 

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /var/opt/mssql/data/masternew.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /var/opt/mssql/data/mastlognew.ldf
   ```

1. SQL Server 서비스를 시작합니다.

   ```bash
   sudo systemctl start mssql-server
   ```

## <a name="change-the-default-dump-directory-location"></a><a id="dumpdir"></a> 기본 덤프 디렉터리 위치 변경

**filelocation.defaultdumpdir** 설정은 크래시가 발생할 때마다 메모리 및 SQL 덤프가 생성되는 기본 위치를 변경합니다. 기본적으로 이 파일은 /var/opt/mssql/log에 생성됩니다.

이 새 위치를 설정하려면 다음 명령을 사용합니다.

1. 새 덤프 파일의 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/dump** 디렉터리를 만듭니다.

   ```bash
   sudo mkdir /tmp/dump
   ```

1. 디렉터리의 소유자 및 그룹을 **mssql** 사용자로 변경합니다.

   ```bash
   sudo chown mssql /tmp/dump
   sudo chgrp mssql /tmp/dump
   ```

1. mssql-conf를 사용하여 **set** 명령으로 기본 데이터 디렉터리를 변경합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump
   ```

1. SQL Server 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="change-the-default-error-log-file-directory-location"></a><a id="errorlogdir"></a> 기본 오류 로그 파일 디렉터리 위치 변경

**filelocation.errorlogfile** 설정은 새 오류 로그, 기본 프로파일러 추적, 시스템 상태 세션 XE 및 Hekaton 세션 XE 파일이 생성되는 위치를 변경합니다. 기본적으로 이 위치는 /var/opt/mssql/log입니다. SQL 오류 로그 파일이 설정된 디렉터리는 다른 로그의 기본 로그 디렉터리가 됩니다.

이 설정을 변경하려면:

1. 새 오류 로그 파일의 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/logs** 디렉터리를 만듭니다.

   ```bash
   sudo mkdir /tmp/logs
   ```

1. 디렉터리의 소유자 및 그룹을 **mssql** 사용자로 변경합니다.

   ```bash
   sudo chown mssql /tmp/logs
   sudo chgrp mssql /tmp/logs
   ```

1. mssql-conf를 사용하여 **set** 명령으로 기본 오류 로그 파일 이름을 변경합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.errorlogfile /tmp/logs/errorlog
   ```

1. SQL Server 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

`errorlog.numerrorlogs` 설정을 사용하면 로그를 순환하기 전에 유지 관리되는 오류 로그 수를 지정할 수 있습니다.

## <a name="change-the-default-backup-directory-location"></a><a id="backupdir"></a> 기본 백업 디렉터리 위치 변경

**filelocation.defaultbackupdir** 설정은 백업 파일이 생성되는 기본 위치를 변경합니다. 기본적으로 이 파일은 /var/opt/mssql/data에 생성됩니다.

이 새 위치를 설정하려면 다음 명령을 사용합니다.

1. 새 백업 파일의 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/backup** 디렉터리를 만듭니다.

   ```bash
   sudo mkdir /tmp/backup
   ```

1. 디렉터리의 소유자 및 그룹을 **mssql** 사용자로 변경합니다.

   ```bash
   sudo chown mssql /tmp/backup
   sudo chgrp mssql /tmp/backup
   ```

1. mssql-conf를 사용하여 “set” 명령으로 기본 백업 디렉터리를 변경합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup
   ```

1. SQL Server 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="specify-core-dump-settings"></a><a id="coredump"></a> 코어 덤프 설정 지정

SQL Server 프로세스 중 하나에서 예외가 발생하면 SQL Server는 메모리 덤프를 만듭니다.

SQL Server가 수집하는 메모리 덤프 유형을 제어하는 두 가지 옵션인 **coredump.coredumptype** 및 **coredump.captureminiandfull**이 있습니다. 이 옵션은 코어 덤프 캡처의 두 단계와 관련이 있습니다. 

첫 번째 단계 캡처는 예외 발생 시 생성된 덤프 파일의 형식을 결정하는 **coredump.coredumptype** 설정을 통해 제어됩니다. **coredump.captureminiandfull** 설정을 사용하여 두 번째 단계를 사용하도록 설정합니다. **coredump.captureminiandfull**가 true로 설정하면 **coredump.coredumptype**을 통해 지정된 덤프 파일이 생성되고 두 번째 미니 덤프도 생성됩니다. **coredump.captureminiandfull**을 false로 설정하면 두 번째 캡처 시도가 사용하지 않도록 설정됩니다.

1. **coredump.captureminiandfull** 설정을 사용하여 미니 및 전체 덤프를 둘 다 캡처할지 여부를 결정합니다.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    기본값: **false**

1. **coredump.coredumptype** 설정을 사용하여 덤프 파일 형식을 지정합니다.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    기본값: **miniplus**

    다음 표에는 가능한 **coredump.coredumptype** 값이 나와 있습니다.

    | Type | Description |
    |-----|-----|
    | **mini** | Mini는 가장 작은 덤프 파일 형식입니다. Linux 시스템 정보를 사용하여 프로세스의 스레드 및 모듈을 결정합니다. 덤프에는 호스트 환경 스레드 스택 및 모듈만 포함됩니다. 간접 메모리 참조 또는 전역은 포함되지 않습니다. |
    | **miniplus** | MiniPlus는 mini와 비슷하지만 추가 메모리를 포함합니다. 다음 메모리 영역을 덤프에 추가하여 SQLPAL 및 호스트 환경의 내부를 이해합니다.</br></br> - 다양한 전역</br> - 64TB를 초과하는 모든 메모리</br> - **/proc/$pid/maps**에 있는 모든 명명된 영역</br> - 스레드 및 스택의 간접 메모리</br> - 스레드 정보</br> - 연결된 Teb 및 Peb</br> - 모듈 정보</br> - VMM 및 VAD 트리 |
    | **filtered** | Filtered는 별도로 제외하는 경우가 아니면 프로세스의 모든 메모리가 포함되는 빼기 기반 디자인을 사용합니다. 이 디자인은 덤프에서 특정 영역을 제외하고 SQLPAL 및 호스트 환경의 내부를 이해합니다.
    | **full** | Full은 **/proc/$pid/maps**에 있는 모든 영역을 포함하는 전체 프로세스 덤프입니다. **coredump.captureminiandfull** 설정을 통해 제어되지 않습니다. |

## <a name="high-availability"></a><a id="hadr"></a> 고가용성

**hadr.hadrenabled** 옵션은 SQL Server 인스턴스에서 가용성 그룹을 사용하도록 설정합니다. 다음 명령은 **hadr.hadrenabled**를 1로 설정하여 가용성 그룹을 사용하도록 설정합니다. 설정을 적용하려면 SQL Server를 다시 시작해야 합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

가용성 그룹에서 이 설정을 사용하는 방법에 대한 자세한 내용은 다음 두 항목을 참조하세요.

- [SQL Server on Linux에 대해 Always On 가용성 그룹 구성](sql-server-linux-availability-group-configure-ha.md)
- [SQL Server on Linux에 대해 읽기 확장 가용성 그룹 구성](sql-server-linux-availability-group-configure-rs.md)


## <a name="set-local-audit-directory"></a><a id="localaudit"></a> 로컬 감사 디렉터리 설정

**telemetry.userrequestedlocalauditdirectory** 설정은 로컬 감사를 사용하도록 설정하며 이를 통해 로컬 감사 로그가 생성되는 디렉터리를 설정할 수 있습니다.

1. 새 로컬 감사 로그의 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/audit** 디렉터리를 만듭니다.

   ```bash
   sudo mkdir /tmp/audit
   ```

1. 디렉터리의 소유자 및 그룹을 **mssql** 사용자로 변경합니다.

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. **telemetry.userrequestedlocalauditdirectory**에 대해 **set** 명령을 사용하여 mssql-conf 스크립트를 루트 권한으로 실행합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. SQL Server 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

자세한 내용은 [SQL Server on Linux에 대한 고객 의견](sql-server-linux-customer-feedback.md)을 참조하세요.

## <a name="change-the-sql-server-locale"></a><a id="lcid"></a> SQL Server 로캘 변경

**language.lcid** 설정은 SQL Server 로캘을 지원되는 언어 식별자(LCID)로 변경합니다. 

1. 다음 예제에서는 로캘을 프랑스어(1036)로 변경합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. 변경 내용을 적용하려면 SQL Server 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="set-the-memory-limit"></a><a id="memorylimit"></a> 메모리 제한 설정

**memory.memorylimitmb** 설정은 SQL Server에 사용 가능한 실제 메모리 크기(MB)를 제어합니다. 기본값은 실제 메모리의 80%입니다.

1. **memory.memorylimitmb**에 대해 **set** 명령을 사용하여 mssql-conf 스크립트를 루트 권한으로 실행합니다. 다음 예제에서는 SQL Server에 사용할 수 있는 메모리를 3.25GB(3328MB)로 변경합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. 변경 내용을 적용하려면 SQL Server 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

### <a name="additional-memory-settings"></a>추가 메모리 설정

다음 옵션은 메모리 설정에 사용할 수 있습니다.

|옵션 |Description |
|--- |--- |
| memory.disablememorypressure | SQL Server는 메모리 압력을 사용하지 않도록 설정합니다. 값은 `true` 또는 `false`일 수 있습니다. |
| memory.memory_optimized | SQL Server 메모리 최적화 기능인 영구 메모리 파일 향상 기능, 메모리 보호를 사용하거나 사용하지 않도록 설정합니다. 값은 `true` 또는 `false`일 수 있습니다. |

## <a name="configure-msdtc"></a><a id="msdtc"></a> MSDTC 구성

**network.rpcport** 및 **distributedtransaction.servertcpport** 설정은 MSDTC(Microsoft Distributed Transaction Coordinator)를 구성하는 데 사용됩니다. 이 설정을 변경하려면 다음 명령을 실행합니다.

1. “network.rpcport”에 대해 **set** 명령을 사용하여 mssql-conf 스크립트를 루트 권한으로 실행합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport <rcp_port>
   ```

2. 그런 다음, “distributedtransaction.servertcpport” 설정을 설정합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport <servertcpport_port>
   ```

이 값을 설정하는 것 외에도 라우팅을 구성하고 포트 135에 대한 방화벽을 업데이트해야 합니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 [Linux에서 MSDTC를 구성하는 방법](sql-server-linux-configure-msdtc.md)을 참조하세요.

MSDTC를 모니터링하고 문제 해결하는 데 사용할 수 있는 mssql-conf에 대한 여러 가지 다른 설정이 있습니다. 다음 표에서는 이 설정에 대해 간략하게 설명합니다. 해당 사용에 대한 자세한 내용은 Windows 지원 문서 [How to enable diagnostic tracing for MS DTC](https://support.microsoft.com/help/926099/how-to-enable-diagnostic-tracing-for-ms-dtc-on-a-windows-based-compute)(MS DTC에 대한 진단 추적을 사용하도록 설정하는 방법)의 세부 정보를 참조하세요.

| mssql-conf 설정 | Description |
|---|---|
| distributedtransaction.allowonlysecurerpccalls | 분산 트랜잭션에 대한 보안 전용 RPC 호출 구성 |
| distributedtransaction.fallbacktounsecurerpcifnecessary | 분산 트랜잭션에 대한 보안 전용 RPC 호출을 구성 |
| distributedtransaction.maxlogsize | DTC 트랜잭션 로그 파일 크기(MB). 기본값은 64MB임 |
| distributedtransaction.memorybuffersize | 추적이 저장되는 순환 버퍼 크기. 이 크기는 MB단위이며 기본값은 10MB임 |
| distributedtransaction.servertcpport | MSDTC rpc 서버 포트 |
| distributedtransaction.trace_cm | 연결 관리자의 추적 |
| distributedtransaction.trace_contact | 연락처 풀 및 연락처 추적 |
| distributedtransaction.trace_gateway | 게이트웨이 원본 추적 |
| distributedtransaction.trace_log | 로그 추적 |
| distributedtransaction.trace_misc | 다른 범주로 분류할 수 없는 추적. |
| distributedtransaction.trace_proxy | MSDTC 프록시에서 생성된 추적 |
| distributedtransaction.trace_svc | 서비스 및 .exe 파일 시작 추적 |
| distributedtransaction.trace_trace | 추적 인프라 자체 |
| distributedtransaction.trace_util | 여러 위치에서 호출되는 유틸리티 루틴 추적 |
| distributedtransaction.trace_xa | XATM(XA 트랜잭션 관리자) 추적 원본 |
| distributedtransaction.tracefilepath | 추적 파일을 저장해야 하는 폴더 |
| distributedtransaction.turnoffrpcsecurity | 분산 트랜잭션에 대한 RPC 보안 사용 또는 사용 안 함 |

::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="accept-mlservices-eulas"></a><a id="mlservices-eula"></a> MLServices EULA 동의

데이터베이스 엔진에 [기계 학습 R 또는 Python 패키지](sql-server-linux-setup-machine-learning.md)를 추가하려면 R 및 Python의 오픈 소스 배포에 대한 사용 조건에 동의해야 합니다. 다음 표에서는 mlservices EULA에 관련된 사용 가능한 모든 명령 또는 옵션을 열거합니다. 동일한 EULA 매개 변수는 설치된 항목에 따라 R 및 Python에 사용됩니다.

```bash
# For all packages: database engine and mlservices
# Setup prompts for mlservices EULAs, which you need to accept
sudo /opt/mssql/bin/mssql-conf setup

# Add R or Python to an existing installation
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml

# Alternative valid syntax
# Adds the EULA section to the INI and sets acceptulam to yes
sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y

# Rescind EULA acceptance and removes the setting
sudo /opt/mssql/bin/mssql-conf unset EULA accepteulaml
```

[mssql.conf 파일](#mssql-conf-format)에 직접 EULA 동의를 추가할 수도 있습니다.

```ini
[EULA]
accepteula = Y
accepteulaml = Y
```
:::moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="enable-outbound-network-access"></a><a id="mlservices-outbound-access"></a> 아웃바운드 네트워크 액세스 사용

[SQL Server Machine Learning Services](sql-server-linux-setup-machine-learning.md) 기능에서 R, Python 및 Java 확장에 대한 아웃바운드 네트워크 액세스는 기본적으로 사용하지 않도록 설정됩니다. 아웃바운드 요청을 사용하도록 설정하려면 mssql-conf를 사용하여 “outboundnetworkaccess” 부울 속성을 설정합니다.

속성을 설정한 후 SQL Server 실행 패드 서비스를 다시 시작하여 INI 파일에서 업데이트된 값을 읽습니다. 다시 시작 메시지가 확장성 관련 설정이 수정될 때마다 사용자에게 알려줍니다.

```bash
# Adds the extensibility section and property.
# Sets "outboundnetworkaccess" to true.
# This setting is required if you want to access data or operations off the server.
sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1

# Turns off network access but preserves the setting
sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 0

# Removes the setting and rescinds network access
sudo /opt/mssql/bin/mssql-conf unset extensibility.outboundnetworkaccess
```

[mssql.conf 파일](#mssql-conf-format)에 직접 “outboundnetworkaccess”를 추가할 수도 있습니다.

```ini
[extensibility]
outboundnetworkaccess = 1
```
:::moniker-end

## <a name="change-the-tcp-port"></a><a id="tcpport"></a> TCP 포트 변경

**network.tcpport** 설정은 SQL Server가 연결을 수신 대기하는 TCP 포트를 변경합니다. 기본적으로 이 포트는 1433으로 설정됩니다. 포트를 변경하려면 다음 명령을 실행합니다.

1. “network.tcpport”에 대해 “set” 명령을 사용하여 mssql-conf 스크립트를 루트 권한으로 실행합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

2. SQL Server 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

3. 이제 SQL Server에 연결할 때 호스트 이름 또는 IP 주소 뒤에 쉼표(,)를 사용하여 사용자 지정 포트를 지정해야 합니다. 예를 들어 SQLCMD와 연결하려면 다음 명령을 사용합니다.

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a name="specify-tls-settings"></a><a id="tls"></a> TLS 설정 지정

다음 옵션은 Linux에서 실행되는 SQL Server 인스턴스에 대해 TLS를 구성합니다.

|옵션 |Description |
|--- |--- |
|**network.forceencryption** |1인 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 모든 연결을 강제로 암호화합니다. 기본적으로 이 옵션은 0입니다. |
|**network.tlscert** |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 TLS에 사용하는 인증서 파일의 절대 경로입니다. 예제:   `/etc/ssl/certs/mssql.pem`  인증서 파일은 mssql 계정으로 액세스할 수 있어야 합니다. `chown mssql:mssql <file>; chmod 400 <file>`을 사용하여 파일에 대한 액세스를 제한하는 것이 좋습니다. |
|**network.tlskey** |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 TLS에 사용하는 프라이빗 키 파일의 절대 경로입니다. 예제:  `/etc/ssl/private/mssql.key`  인증서 파일은 mssql 계정으로 액세스할 수 있어야 합니다. `chown mssql:mssql <file>; chmod 400 <file>`을 사용하여 파일에 대한 액세스를 제한하는 것이 좋습니다. |
|**network.tlsprotocols** |SQL Server에서 허용하는 TLS 프로토콜의 쉼표로 구분된 목록입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 항상 가장 강력한 허용 프로토콜을 협상하려고 시도합니다. 클라이언트에서 허용되는 프로토콜을 지원하지 않으면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 연결 시도를 거부합니다.  호환성을 위해 지원되는 모든 프로토콜이 기본적으로 허용됩니다(1.2, 1.1, 1.0).  클라이언트에서 TLS 1.2을 지원하는 경우 TLS 1.2만 허용하는 것이 좋습니다. |
|**network.tlsciphers** |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 TLS에 대해 허용하는 암호화를 지정합니다. 이 문자열은 [OpenSSL의 암호화 목록 형식](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html)에 따라 형식을 지정해야 합니다. 일반적으로 이 옵션을 변경할 필요가 없습니다. <br /> 기본적으로 다음 암호화가 허용됩니다. <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **network.kerberoskeytabfile** |Kerberos keytab 파일의 경로입니다. |

TLS 설정 사용에 대한 예제는 [SQL Server on Linux에 대한 연결 암호화](sql-server-linux-encrypted-connections.md)를 참조하세요.

## <a name="network-settings"></a><a id="network"></a> 네트워크 설정

[자습서: SQL Server on Linux와 Active Directory 인증 사용](sql-server-linux-active-directory-authentication.md)에서 SQL Server on Linux와 AD 인증 사용에 대한 포괄적인 정보를 참조하세요.

다음 옵션은 `mssql-conf`를 사용하여 구성할 수 있는 추가 네트워크 설정입니다.

|옵션 |Description |
|--- |--- |
| network.disablesssd | AD 계정 정보에 대한 SSSD 쿼리를 사용하지 않도록 설정하며 기본적으로 LDAP 호출로 지정됩니다. 값은 `true` 또는 `false`일 수 있습니다. |
| network.enablekdcfromkrb5conf | krb5.conf에서 KDC 정보를 조회할 수 있도록 설정합니다. 값은 `true` 또는 `false`일 수 있습니다. |
| network.forcesecureldap | 도메인 컨트롤러에 연결하는 데 LDAPS를 사용하도록 강제 적용합니다. 값은 `true` 또는 `false`일 수 있습니다. |
| network.ipaddress | 들어오는 연결을 위한 IP 주소입니다. |
| network.kerberoscredupdatefrequency | 업데이트해야 하는 kerberos 자격 증명 검사 사이의 시간(초)입니다. 값은 정수입니다.|
| network.privilegedadaccount | AD 인증에 사용할 권한을 가진 AD 사용자입니다. 값은 `<username>`입니다. 자세한 내용은 [자습서: Linux에서 SQL Server와 Active Directory 인증 사용](sql-server-linux-active-directory-authentication.md#spn)|
| uncmapping | 로컬 경로에 UNC 경로를 매핑합니다. 예: `sudo /opt/mssql/bin/mssql-conf set uncmapping //servername/sharename /tmp/folder`. |

## <a name="enabledisable-traceflags"></a><a id="traceflags"></a> 추적 플래그 사용/사용 안 함

이 **추적 플래그** 옵션은 SQL Server 서비스를 시작하기 위해 추적 플래그를 사용하거나 사용하지 않도록 설정합니다. 추적 플래그를 사용하거나 사용하지 않도록 설정하려면 다음 명령을 사용합니다.

1. 다음 명령을 사용하여 추적 플래그를 사용하도록 설정합니다. 예를 들어 추적 플래그 1234의 경우:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. 여러 추적 플래그를 개별적으로 지정하여 사용하도록 설정할 수 있습니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. 이와 비슷한 방식으로 하나 이상의 사용하도록 설정된 추적 플래그를 지정하고 **off** 매개 변수를 추가하여 해당 추적 플래그를 사용하지 않도록 설정할 수 있습니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. 변경 내용을 적용하려면 SQL Server 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>설정 제거

`mssql-conf set`를 사용하여 지정된 설정을 해제하려면 **mssql-conf**를 `unset` 옵션 및 설정 이름과 함께 호출합니다. 이렇게 하면 설정이 삭제되고 효과적으로 기본값으로 돌아갑니다.

1. 다음 예제에서는 **network.tcpport** 옵션을 삭제합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. SQL Server 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>현재 설정 보기

구성된 설정을 보려면 다음 명령을 실행하여 **mssql.conf** 파일의 콘텐츠를 출력합니다.

```bash
sudo cat /var/opt/mssql/mssql.conf
```

이 파일에 표시되지 않는 모든 설정은 해당 기본값을 사용합니다. 다음 섹션에서는 샘플 **mssql.conf** 파일을 제공합니다.


## <a name="mssqlconf-format"></a><a id="mssql-conf-format"></a> mssql.conf 형식

다음 **/var/opt/mssql/mssql.conf** 파일은 각 설정에 대한 예제를 제공합니다. 이 형식을 사용하여 필요에 따라 **mssql.conf** 파일을 수동으로 변경할 수 있습니다. 수동으로 파일을 변경하는 경우 변경 내용이 적용되기 전에 SQL Server를 다시 시작해야 합니다. Docker와 함께 **mssql.conf** 파일을 사용하려면 Docker가 [데이터를 유지](sql-server-linux-configure-docker.md)하도록 해야 합니다. 먼저 호스트 디렉터리에 전체 **mssql.conf** 파일을 추가한 후 컨테이너를 실행합니다. [고객 의견](sql-server-linux-customer-feedback.md)에 이에 대한 예제가 있습니다.

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

대신 환경 변수를 사용하여 이와 같은 일부 구성을 변경하려면 [환경 변수를 사용하여 SQL Server 설정 구성](sql-server-linux-configure-environment-variables.md)을 참조하세요.

다른 관리 도구 및 시나리오는 [SQL Server on Linux 관리](sql-server-linux-management-overview.md)를 참조하세요.

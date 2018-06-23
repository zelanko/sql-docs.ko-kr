---
title: Linux에서 SQL Server 설정 구성 | Microsoft Docs
description: 이 문서에서는 Linux에서 SQL Server 2017 설정을 구성 하는 mssql conf 도구를 사용 하는 방법을 설명 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 06/22/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.openlocfilehash: 9506096746c0f93b147f8040bbd7066e99d69bad
ms.sourcegitcommit: 23e71a8afba194e0893f31532db0aaa29288acb2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2018
ms.locfileid: "36329488"
---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>Mssql conf 도구와 함께 Linux에서 SQL Server 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

**mssql conf** 은 Red Hat Enterprise Linux, SUSE Linux Enterprise Server 및 Ubuntu에 대 한 SQL Server 2017와 함께 설치 되는 구성 스크립트입니다. 이 유틸리티를 사용 하 여 다음 매개 변수를 설정할 수 있습니다.

|||
|---|---|
| [에이전트](#agent) | SQL Server 에이전트를 사용 하도록 설정 |
| [데이터 정렬](#collation) | Linux에서 SQL Server에 대 한 새로운 데이터 정렬이 설정 합니다. |
| [고객 의견](#customerfeedback) | SQL Server를 Microsoft로 피드백을 보냅니다 여부를 선택 합니다. |
| [데이터베이스 메일 프로필](#dbmail) | Linux에서 SQL Server에 대 한 기본 데이터베이스 메일 프로필 설정 |
| [기본 데이터 디렉터리](#datadir) | 새 SQL Server 데이터베이스 데이터 파일 (.mdf)에 대 한 기본 디렉터리를 변경 합니다. |
| [기본 로그 디렉터리](#datadir) | 새 SQL Server 데이터베이스 로그 (.ldf) 파일에 대 한 기본 디렉터리를 변경합니다. |
| [기본 master 데이터베이스 파일 디렉터리](#masterdatabasedir) | 기존 SQL 설치에서 master 데이터베이스 파일에 대 한 기본 디렉터리를 변경합니다.|
| [기본 master 데이터베이스 파일 이름](#masterdatabasename) | Master 데이터베이스 파일의 이름을 변경합니다. |
| [기본 덤프 디렉터리](#dumpdir) | 새 메모리 덤프 및 기타 문제 해결 파일에 대 한 기본 디렉터리를 변경 합니다. |
| [기본 오류 로그 디렉터리](#errorlogdir) | 새 SQL Server 오류 로그, 기본 프로파일러 추적, 시스템 상태 세션 XE 및 Hekaton 세션 XE 파일에 대 한 기본 디렉터리를 변경합니다. |
| [기본 백업 디렉터리](#backupdir) | 새 백업 파일에 대 한 기본 디렉터리를 변경 합니다. |
| [덤프 유형](#coredump) | 수집할 덤프 메모리 덤프 파일의 형식을 선택 합니다. |
| [고가용성](#hadr) | 가용성 그룹을 사용 하도록 설정 합니다. |
| [로컬 감사 디렉터리](#localaudit) | 설정 된 로컬 감사 파일을 추가 하는 디렉터리입니다. |
| [로캘](#lcid) | 사용 하도록 SQL Server에 대 한 로캘을 설정 합니다. |
| [메모리 제한](#memorylimit) | SQL Server에 대 한 메모리 제한을 설정 합니다. |
| [TCP 포트](#tcpport) | SQL Server 연결에 대 한 수신 위치는 포트를 변경 합니다. |
| [TLS](#tls) | 전송 수준 보안을 구성 합니다. |
| [Traceflag](#traceflags) | 서비스를 사용 하려고 합니다. traceflag를 설정 합니다. |

> [!TIP]
> 이러한 설정 중 일부를 환경 변수와 구성할 수도 있습니다. 자세한 내용은 참조 [환경 변수를 사용 하 여 SQL Server 구성 설정](sql-server-linux-configure-environment-variables.md)합니다.

## <a name="usage-tips"></a>사용 팁

* Always On 가용성 그룹 및 공유 디스크 클러스터의 경우 항상 각 노드에서 동일한 구성 변경 내용을 확인 합니다.

* 공유 디스크 클러스터 시나리오에 대 한 마십시오 다시 시작 하는 **mssql 서버** 서비스 변경 내용을 적용 합니다. SQL Server가 응용 프로그램으로 실행 됩니다. 대신, 오프 라인 상태로 만들었다가 다시 온라인 다음 리소스를 수행 합니다.

* 전체 경로 지정 하는 이러한 예제를 실행 하 여 mssql conf: **/opt/mssql/bin/mssql-conf**합니다. 대신 해당 경로로 이동 하기로 선택한 경우 mssql conf 현재 디렉터리의 컨텍스트에서 실행: **. / mssql conf**합니다.

## <a id="agent"></a> SQL Server 에이전트를 사용 하도록 설정

**sqlagent.enabled** 있습니다 [SQL Server 에이전트](sql-server-linux-run-sql-server-agent-job.md)합니다. SQL Server 에이전트는 기본적으로 비활성화 됩니다. 경우 **sqlagent.enabled** 다음 SQL Server는 내부적으로 SQL Server 에이전트를 사용할 수 있음을 가정 mssql.conf 설정 파일에 나타나지 않습니다.

이 설정을 변경 하려면 다음 단계를 사용 합니다.

1. SQL Server 에이전트를 사용 하도록 설정 합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="collation"></a> SQL Server 데이터 정렬 변경

**데이터 정렬 설정** 지원 되는 데이터 정렬 중 하나에 있는 데이터 정렬 값을 변경 하는 옵션입니다.

1. 첫 번째 [모든 사용자 데이터베이스를 백업](sql-server-linux-backup-and-restore-database.md) 서버에 있습니다.

1. 다음 사용 하 여는 [sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) 저장 프로시저를 사용자 데이터베이스를 분리 합니다.

1. 실행 된 **데이터 정렬 설정** 따르다 및 옵션:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. Mssql conf 유틸리티는 지정 된 데이터 정렬 값으로 변경 하 고 서비스를 다시 시작 하려고 합니다. 오류가 있는 경우 롤백됩니다 데이터 정렬은 이전 값으로.

1. 사용자 데이터베이스 백업을 복원 합니다.

지원 되는 데이터 정렬 목록에 대 한 실행은 [sys.fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) 함수: `SELECT Name from sys.fn_helpcollations()`합니다.

## <a id="customerfeedback"></a> 고객 의견을 구성 합니다.

**telemetry.customerfeedback** 설정은 SQL Server 또는 Microsoft에 피드백을 보냅니다 있는지 여부를 변경 합니다. 기본적으로이 값 설정 **true** 모든 버전에 대 한 합니다. 값을 변경 하려면 다음 명령을 실행 합니다.

> [!IMPORTANT]
> 해제할 수 있습니다 없습니다 고객 의견을 무료로 버전의 SQL Server, Express 및 개발자.

1. 루트 및 mssql conf 스크립트를 실행 하는 중는 **설정** 명령을 **telemetry.customerfeedback**합니다. 다음 예에서는 지정 하 여 고객 의견 해제 **false**합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

자세한 내용은 참조 [Linux에서 SQL Server에 대 한 고객 의견](sql-server-linux-customer-feedback.md) 및 [SQL Server 개인정보취급방침](http://go.microsoft.com/fwlink/?LinkID=868444)합니다.

## <a id="datadir"></a> 기본 데이터 또는 로그 디렉터리 위치를 변경 합니다.

**filelocation.defaultdatadir** 및 **filelocation.defaultlogdir** 설정은 새 데이터베이스 및 로그 파일이 만들어지는 위치를 변경 합니다. 기본적으로이 위치는 /var/opt/mssql/data는입니다. 이러한 설정을 변경 하려면 다음 단계를 사용 합니다.

1. 새 데이터베이스에 대 한 대상 디렉터리 데이터 및 로그 파일을 만듭니다. 다음 예제에서는 새 **/tmp/데이터** 디렉터리:

   ```bash
   sudo mkdir /tmp/data
   ```

1. 소유자 및 그룹 디렉터리의 변경 된 **mssql** 사용자:

   ```bash
   sudo chown mssql /tmp/data
   sudo chgrp mssql /tmp/data
   ```

1. Mssql conf를 사용 하 여 사용 하 여 기본 데이터 디렉터리를 변경 하는 **설정** 명령:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

1. 이제이 새 위치에 만든 새 데이터베이스에 대 한 모든 데이터베이스 파일을 저장 됩니다. 새 데이터베이스의 로그 (.ldf) 파일의 위치를 변경 하려는 경우 다음 "set" 명령을 사용할 수 있습니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. 이 명령은/tmp/로그 디렉터리가 있는지 그리고 사용자 및 그룹에서 또한 가정 **mssql**합니다.


## <a id="masterdatabasedir"></a> 기본 master 데이터베이스 파일 디렉터리 위치를 변경 합니다.

**filelocation.masterdatafile** 및 **filelocation.masterlogfile** 변경 master 데이터베이스 파일에 대 한 SQL Server 엔진을 찾는 위치 위치를 설정 합니다. 기본적으로이 위치는 /var/opt/mssql/data는입니다. 

이러한 설정을 변경 하려면 다음 단계를 사용 합니다.

1. 새 오류 로그 파일에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/masterdatabasedir** 디렉터리:

   ```bash
   sudo mkdir /tmp/masterdatabasedir
   ```

1. 소유자 및 그룹 디렉터리의 변경 된 **mssql** 사용자:

   ```bash
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
   ```

1. Mssql conf를 사용 하 여 사용 하 여 마스터 데이터 및 로그 파일에 대 한 기본 master 데이터베이스 디렉터리를 변경 하는 **설정** 명령:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
   ```

1. SQL Server 서비스를 중지 합니다.

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Master.mdf 및 masterlog.ldf 이동 합니다. 

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf 
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
   ```

1. SQL Server 서비스를 시작 합니다.

   ```bash
   sudo systemctl start mssql-server
   ```
   
> [!NOTE]
> SQL Server는 지정된 된 디렉터리에서 master.mdf 및 mastlog.ldf 파일을 찾을 수 없으면, 시스템 데이터베이스의 템플릿 기반 복사본 자동으로 지정된 된 디렉터리에서 만들어지고 SQL Server 성공적으로 시작 됩니다. 그러나 새 master 데이터베이스에서 사용자 데이터베이스, 서버 로그인, 서버 인증서, 암호화 키, SQL 에이전트 작업 또는 이전 SA 로그인 암호와 같은 메타 데이터 업데이트 되지 않습니다. SQL Server를 중지 하 고 이전 master.mdf 및 mastlog.ldf 지정 된 새 위치로 이동할 기존 메타 데이터를 사용 하 여 계속 하려면 SQL Server를 시작 해야 합니다. 


## <a id="masterdatabasename"></a> Master 데이터베이스 파일의 이름을 변경 합니다.

**filelocation.masterdatafile** 및 **filelocation.masterlogfile** 변경 master 데이터베이스 파일에 대 한 SQL Server 엔진을 찾는 위치 위치를 설정 합니다. 기본적으로이 위치는 /var/opt/mssql/data는입니다. 이러한 설정을 변경 하려면 다음 단계를 사용 합니다.

1. SQL Server 서비스를 중지 합니다.

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Mssql conf를 사용 하 여 사용 하 여 마스터 데이터 및 로그 파일에 대 한 예상 되는 마스터 데이터베이스 이름을 변경 하는 **설정** 명령:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /var/opt/mssql/data/masternew.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.mastlogfile /var/opt/mssql/data /mastlognew.ldf
   ```

1. Master 데이터베이스 데이터 및 로그 파일의 이름을 변경합니다 

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /var/opt/mssql/data/masternew.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /var/opt/mssql/data/mastlognew.ldf
   ```

1. SQL Server 서비스를 시작 합니다.

   ```bash
   sudo systemctl start mssql-server
   ```



## <a id="dumpdir"></a> 기본 덤프 디렉터리 위치를 변경 합니다.

**filelocation.defaultdumpdir** 설정 변경 사항을 충돌이 있을 때마다 메모리 및 SQL 덤프는 생성 되는 위치는 기본 위치입니다. 기본적으로 이러한 파일은 /var/opt/mssql/log에서 생성 됩니다.

이 새 위치를 설정 하려면 다음 명령을 사용 합니다.

1. 새 덤프 파일에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/덤프** 디렉터리:

   ```bash
   sudo mkdir /tmp/dump
   ```

1. 소유자 및 그룹 디렉터리의 변경 된 **mssql** 사용자:

   ```bash
   sudo chown mssql /tmp/dump
   sudo chgrp mssql /tmp/dump
   ```

1. Mssql conf를 사용 하 여 사용 하 여 기본 데이터 디렉터리를 변경 하는 **설정** 명령:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="errorlogdir"></a> 기본 오류 로그 파일 디렉터리 위치를 변경 합니다.

**filelocation.errorlogfile** 설정 변경 사항을 새 오류 로그, 기본 프로파일러 추적, 시스템 상태 세션 XE 및 Hekaton 세션 XE 파일 만들어지는 위치입니다. 기본적으로이 위치는 /var/opt/mssql/log은입니다. SQL 오류 로그 파일 설정 되어 있는 디렉터리에는 다른 로그에 대 한 기본 로그 디렉터리가 됩니다.

이러한 설정을 변경 하려면:

1. 새 오류 로그 파일에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/logs** 디렉터리:

   ```bash
   sudo mkdir /tmp/logs
   ```

1. 소유자 및 그룹 디렉터리의 변경 된 **mssql** 사용자:

   ```bash
   sudo chown mssql /tmp/logs
   sudo chgrp mssql /tmp/logs
   ```

1. Mssql conf를 사용 하 여 기본 오류 로그 파일 이름으로 변경 하는 **설정** 명령:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.errorlogfile /tmp/logs/errorlog
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```


## <a id="backupdir"></a> 기본 백업 디렉터리 위치를 변경 합니다.

**filelocation.defaultbackupdir** 설정 변경 내용을 기본 위치는 백업 파일이 생성 됩니다. 기본적으로 이러한 파일은 /var/opt/mssql/data에서 생성 됩니다.

이 새 위치를 설정 하려면 다음 명령을 사용 합니다.

1. 새 백업 파일에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/백업** 디렉터리:

   ```bash
   sudo mkdir /tmp/backup
   ```

1. 소유자 및 그룹 디렉터리의 변경 된 **mssql** 사용자:

   ```bash
   sudo chown mssql /tmp/backup
   sudo chgrp mssql /tmp/backup
   ```

1. Mssql conf를 사용 하 여 "set" 명령 사용 하 여 기본 백업 디렉터리를 변경 하려면:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="coredump"></a> 코어 덤프 설정 지정

SQL Server 프로세스 중 하나에서 예외가 발생 하는 경우 SQL Server 메모리 덤프를 만듭니다.

SQL Server를 수집 덤프 메모리의 형식을 제어에 대 한 두 가지 옵션이 사항이: **coredump.coredumptype** 및 **coredump.captureminiandfull**합니다. 이러한 핵심 덤프 캡처의 두 단계와 관련이 있습니다. 

첫 번째 단계 캡처에 의해 제어 되는 **coredump.coredumptype** 예외 중에 생성 된 덤프 파일의 유형을 결정 하는 설정입니다. 두 번째 단계가 때 활성화 됩니다는 **coredump.captureminiandfull** 설정 합니다. 경우 **coredump.captureminiandfull** 덤프를 true로 설정 되어로 지정 된 파일 **coredump.coredumptype** 생성 되는 두 번째 미니 덤프를 생성 하 고 합니다. 설정 **coredump.captureminiandfull** false로 두 번째 캡처 시도 합니다.

1. 포함 하는 미니 및 전체 덤프를 캡처하려면 것인지 결정는 **coredump.captureminiandfull** 설정 합니다.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    기본값: **false**

1. 덤프 파일의 유형을 지정는 **coredump.coredumptype** 설정 합니다.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    기본값: **miniplus**

    다음 표에서 가능한 **coredump.coredumptype** 값입니다.

    | 형식 | Description |
    |-----|-----|
    | **mini** | 미니는 가장 작은 덤프 파일 형식입니다. 스레드 및 프로세스에서 모듈을 확인 하려면 Linux 시스템 정보를 사용 합니다. 호스트 환경 스레드 스택 및 모듈 덤프에 포함 되어 있습니다. 간접 메모리 참조 또는 전역 변수는 포함 되지 않습니다. |
    | **miniplus** | MiniPlus 미니, 유사 하지만 추가 메모리를 포함 합니다. 내부 SQLPAL와 덤프에는 다음과 같은 메모리 영역을 추가 하는 호스트 환경을 이해:</br></br> -다양 한 전역 변수</br> -64TB 이상의 모든 메모리</br> -모든 영역에는 명명 된 **/proc/$ pid/매핑**</br> 스레드 및 스택 간접 메모리</br> 스레드 정보</br> -관련 Teb의 및 Peb의</br> 모듈 정보</br> VMM 및 VAD 트리 |
    | **filtered** | 여기서는 프로세스의 모든 메모리는 구체적으로 제외 되지 않은 경우 포함 빼기 기반 필터링된 사용 하 여 디자인 합니다. 디자인은 호스트 환경에 특정 지역 덤프에서 제외 하 고 SQLPAL의 내부를 이해 합니다.
    | **full** | 에 모든 영역을 포함 하는 전체 프로세스 덤프 있는 전체 **/proc/$ pid/매핑**합니다. 에 의해 제어 되지이 **coredump.captureminiandfull** 설정 합니다. |

## <a id="dbmail"></a> Linux에서 SQL Server에 대 한 기본 데이터베이스 메일 프로필 설정

**sqlpagent.databasemailprofile** 전자 메일 경고에 대 한 기본 DB 메일 프로필을 설정할 수 있습니다.

```bash
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```
## <a id="hadr"></a> 고가용성

**hadr.hadrenabled** 옵션을 사용 하면 SQL Server 인스턴스에서 가용성 그룹입니다. 다음 명령은 설정 하 여 가용성 그룹을 사용 하면 **hadr.hadrenabled** 1입니다. 설정에 대해 적용 되려면 SQL Server를 다시 시작 해야 합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

이 기능의 사용 방법을 가용성 그룹이 포함 된 정보를 다음 두 항목을 참조 하십시오.

- [Linux에서 SQL Server에 대 한에 Always On 가용성 그룹 구성](sql-server-linux-availability-group-configure-ha.md)
- [Linux에서 SQL Server에 대 한 읽기 확장성이 가용성 그룹을 구성 합니다.](sql-server-linux-availability-group-configure-rs.md)

## <a id="localaudit"></a> 로컬 감사 디렉터리 설정

**telemetry.userrequestedlocalauditdirectory** 설정은 로컬 감사를 활성화 하 고 로컬 감사를 기록 하는 디렉터리 설정할 있습니다 만들어집니다.

1. 새 로컬 감사 로그에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/감사** 디렉터리:

   ```bash
   sudo mkdir /tmp/audit
   ```

1. 소유자 및 그룹 디렉터리의 변경 된 **mssql** 사용자:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. 루트 및 mssql conf 스크립트를 실행 하는 중는 **설정** 명령을 **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

자세한 내용은 참조 [Linux에서 SQL Server에 대 한 고객 의견](sql-server-linux-customer-feedback.md)합니다.

## <a id="lcid"></a> SQL Server 로캘을 변경합니다

**language.lcid** 설정 변경 내용을 SQL Server 로캘을 지원 되는 언어 식별자 (LCID)입니다. 

1. 다음 예에서는 프랑스어로 로캘을 변경 (1036):

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. 변경 내용을 적용 하려면 SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="memorylimit"></a> 메모리 제한을 설정합니다

**memory.memorylimitmb** 컨트롤 실제 메모리 양을 mb 단위로 사용할 수 있는 SQL Server에 설정 합니다. 기본값은 실제 메모리의 80%입니다.

1. 루트 및 mssql conf 스크립트를 실행 하는 중는 **설정** 명령을 **memory.memorylimitmb**합니다. 다음 예제에서는 SQL server 3.25 GB (3328 MB)에 사용할 수 있는 메모리를 변경합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. 변경 내용을 적용 하려면 SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="tcpport"></a> TCP 포트를 변경

**network.tcpport** 설정 변경 내용을 SQL Server 연결에 대 한 수신 대기 하는 TCP 포트입니다. 기본적으로이 포트를 1433 설정 됩니다. 포트를 변경 하려면 다음 명령을 실행 합니다.

1. "Network.tcpport"에 대 한 "설정" 명령 사용 하 여 루트로 mssql conf 스크립트를 실행 합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

1. SQL Server에 연결할 때 다음 호스트 이름이 나 IP 주소 쉼표 (,)로 사용자 지정 포트를 지정 해야 합니다. 예를 들어 SQLCMD를 연결 하려면 다음 명령을 사용 합니다.

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a id="tls"></a> TLS 설정 지정

다음 옵션 Linux에서 실행 중인 SQL Server의 인스턴스에 대 한 TLS를 구성 합니다.

|옵션 |Description |
|--- |--- |
|**network.forceencryption** |1 인 경우, 다음 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 암호화에 대 한 모든 연결을 강제로 수행 합니다. 기본적으로이 옵션은 0입니다. |
|**network.tlscert** |인증서에 절대 경로 파일 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] TLS를 사용 합니다. 예: `/etc/ssl/certs/mssql.pem` 인증서 파일 mssql 계정에서 액세스할 수 있어야 합니다. 사용 하 여 파일에 대 한 액세스를 제한 하는 것이 좋습니다 `chown mssql:mssql <file>; chmod 400 <file>`합니다. |
|**network.tlskey** |개인 키에 절대 경로 파일 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] TLS를 사용 합니다. 예: `/etc/ssl/private/mssql.key` 인증서 파일 mssql 계정에서 액세스할 수 있어야 합니다. 사용 하 여 파일에 대 한 액세스를 제한 하는 것이 좋습니다 `chown mssql:mssql <file>; chmod 400 <file>`합니다. |
|**network.tlsprotocols** |프로토콜은 SQL Server에서 허용 하는 TLS의 쉼표로 구분 된 목록입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 항상 가장 강력한 허용 된 프로토콜을 협상 하도록 시도 합니다. 클라이언트가 허용 된 모든 프로토콜을 지원 하지 않는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 연결 시도 거부 합니다.  호환성을 위해 지원 되는 모든 프로토콜은 기본 (1.2, 1.1, 1.0)에서 허용 됩니다.  TLS 1.2를 지원 하려면 클라이언트, TLS 1.2만을 허용 하는 것이 좋습니다. |
|**network.tlsciphers** |허용 하는 암호 지정 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] TLS에 대 한 합니다. 이 문자열 당 포맷 해야 [OpenSSL의 암호화 목록 형식](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html)합니다. 일반적으로이 옵션을 변경할 필요가 없습니다. <br /> 기본적으로 다음 암호 허용 됩니다. <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **network.kerberoskeytabfile** |Kerberos keytab 파일에 대 한 경로 |

TLS 설정을 사용 하 여의 예제를 보려면 [Linux에서 SQL Server 연결 암호화](sql-server-linux-encrypted-connections.md)합니다.

## <a id="traceflags"></a> Traceflag 설정/해제

이 **traceflag** 옵션 사용 하거나 SQL Server 서비스의 시작을 위한 traceflag를 사용 하지 않도록 설정 합니다. 설정/해제는 traceflag에는 다음 명령을 사용 합니다.

1. 다음 명령을 사용 하 여 traceflag 사용 하도록 설정 합니다. Traceflag 1234에 대 한 예를 들어:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. 별도로 지정 하 여 여러 traceflag를 설정할 수 있습니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. 비슷한 방식으로 지정 하 고 추가 하 여 하나 이상의 활성화 된 traceflag를 비활성화할 수 있습니다는 **오프** 매개 변수:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. 변경 내용을 적용 하려면 SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>설정을 제거합니다

설정 하지 않으려면 모든 설정을 사용해 서 변경 `mssql-conf set`, 호출 **mssql conf** 와 `unset` 옵션 및 설정의 이름입니다. 이 값이 기본값으로 효과적으로 돌아가 설정을 지웁니다.

1. 다음 예제에서는 지웁니다는 **network.tcpport** 옵션입니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>현재 설정 보기

보려면 구성 설정의 내용을 출력 하려면 다음 명령을 실행 하는 **mssql.conf** 파일:

```bash
sudo cat /var/opt/mssql/mssql.conf
```

이 파일에 표시 되지 않은 모든 설정을 기본값으로 사용 하 고 있는지 확인 합니다. 다음 섹션에서는 예제를 제공 **mssql.conf** 파일입니다.

## <a name="mssqlconf-format"></a>mssql.conf 형식

다음 **/var/opt/mssql/mssql.conf** 파일 각 설정에 대 한 예제를 제공 합니다. 변경 하려면 수동으로이 형식을 사용할 수는 **mssql.conf** 필요에 따라 파일입니다. 파일을 변경 수동으로 수행 하는 경우 변경 내용을 적용 하기 전에 SQL Server를 다시 시작 해야 있습니다. 사용 하 여 **mssql.conf** 파일 Docker로 Docker 있어야 [데이터 유지](sql-server-linux-configure-docker.md)합니다. 먼저 전체 추가 **mssql.conf** 호스트 디렉터리에 파일을 다음 컨테이너를 실행 합니다. 이러한 형식의 예로 [고객 의견](sql-server-linux-customer-feedback.md)합니다.

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

## <a name="next-steps"></a>다음 단계

대신 환경 변수를 사용 하 여 이러한 구성 변경의 일부를, 참조 [환경 변수를 사용 하 여 SQL Server 구성 설정](sql-server-linux-configure-environment-variables.md)합니다.

다른 관리 도구 및 시나리오에 대 한 참조 [Linux에서 SQL Server 관리](sql-server-linux-management-overview.md)합니다.

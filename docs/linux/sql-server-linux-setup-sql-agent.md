---
title: Linux에서 SQL Server 에이전트를 설치 합니다. | Microsoft Docs
description: 이 문서에서는 Linux에서 SQL Server 에이전트를 설치 하는 방법을 설명 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.openlocfilehash: ef5029798d2898f321ce7813e97d184ec829b693
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="install-sql-server-agent-on-linux"></a>Linux에서 SQL Server 에이전트를 설치 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

 [SQL Server 에이전트](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) 예약 된 SQL Server 작업을 실행 합니다. SQL Server 2017 CU4 이상에서는 SQL Server 에이전트와 함께 제공 됩니다.는 **mssql 서버** 을 패키지 하 고 기본적으로 비활성화 됩니다. 이 릴리스의 버전 정보와 함께 SQL Server 에이전트에 대 한 지원 되는 기능에 대 한 자세한 내용은 참조는 [릴리스 정보](sql-server-linux-release-notes.md)합니다.

 SQL Server 에이전트를 사용/설치:
- [버전 2017 CU4 이상, SQL Server 에이전트를 사용 하도록 설정](#EnableAgentAfterCU4)
- [버전 2017 CU3 및 아래의 SQL Server 에이전트를 설치](#InstallAgentBelowCU4)


## <a name="EnableAgentAfterCU4">버전 2017 CU4 이상, SQL Server 에이전트를 사용 하도록 설정</a>

 SQL Server 에이전트를 사용 하려면 다음 단계를 수행 합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> 2017 c u 3에서에서 업그레이드 하는 또는 에이전트가 설치 된 SQL Server 에이전트 허용 됩니다 이전 및 자동으로 사용 하도록 설정 하는 경우 에이전트 패키지 제거 됩니다.  

## <a name="InstallAgentBelowCU4">버전 2017 CU3 및 아래의 SQL Server 에이전트를 설치</a>

> [!NOTE]
> 아래 설치 지침에는 SQL Server 버전 2017 c u 3에 적용 됩니다. 먼저 SQL Server 에이전트를 설치 하기 전에 [SQL Server 2017 설치](sql-server-linux-setup.md#platforms)합니다. 이 구성 요소의 키 및 설치할 때 사용 하는 저장소는 **mssql 서버 에이전트** 패키지 합니다.

플랫폼에 대 한 SQL Server 에이전트를 설치 합니다.
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name="RHEL">RHEL에 설치</a>

다음 단계를 사용 하 여 설치 하는 **mssql 서버 에이전트** Red Hat Enterprise Linux에 합니다. 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

이미 있는 경우 **mssql 서버 에이전트** 있습니다 다음 명령 사용 하 여 최신 버전으로 업데이트할 수 설치 합니다.

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

오프 라인 설치 해야 할 경우에 SQL Server 에이전트 패키지 다운로드를 찾습니다는 [릴리스 정보](sql-server-linux-release-notes.md)합니다. 다음 문서에 설명 된 동일한 오프 라인 설치 단계를 사용 하 여 [SQL Server 설치](sql-server-linux-setup.md#offline)합니다.

### <a name="ubuntu">Ubuntu에 설치</a>

다음 단계를 사용 하 여 설치 하는 **mssql 서버 에이전트** ubuntu 합니다. 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

이미 있는 경우 **mssql 서버 에이전트** 있습니다 다음 명령 사용 하 여 최신 버전으로 업데이트할 수 설치 합니다.

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

오프 라인 설치 해야 할 경우에 SQL Server 에이전트 패키지 다운로드를 찾습니다는 [릴리스 정보](sql-server-linux-release-notes.md)합니다. 다음 문서에 설명 된 동일한 오프 라인 설치 단계를 사용 하 여 [SQL Server 설치](sql-server-linux-setup.md#offline)합니다.

### <a name="SLES">SLES에 설치</a>

설치 하려면 다음 단계를 사용 하 여는 **mssql 서버 에이전트** SUSE Linux Enterprise Server에 있습니다. 

설치 **mssql 서버 에이전트** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

이미 있는 경우 **mssql 서버 에이전트** 있습니다 다음 명령 사용 하 여 최신 버전으로 업데이트할 수 설치 합니다.

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

오프 라인 설치 해야 할 경우에 SQL Server 에이전트 패키지 다운로드를 찾습니다는 [릴리스 정보](sql-server-linux-release-notes.md)합니다. 다음 문서에 설명 된 동일한 오프 라인 설치 단계를 사용 하 여 [SQL Server 설치](sql-server-linux-setup.md#offline)합니다.

## <a name="next-steps"></a>다음 단계
SQL Server 에이전트를 사용 하 여 일정을 만들고 작업을 실행 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Linux에서 SQL Server 에이전트 작업 실행](sql-server-linux-run-sql-server-agent-job.md)합니다.

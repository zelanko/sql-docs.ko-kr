---
title: Linux의 SQL Server 에이전트를 설치 합니다. | Microsoft Docs
description: 이 문서에서는 Linux의 SQL Server 에이전트를 설치 하는 방법을 설명 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.openlocfilehash: eae6d3389405f6c70e486d0569a65ca5d0a0d15d
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38061871"
---
# <a name="install-sql-server-agent-on-linux"></a>Linux에서 SQL Server 에이전트를 설치 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

 합니다 [SQL Server 에이전트](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) 예약 된 SQL Server 작업을 실행 합니다. SQL Server 2017 CU4부터 SQL Server 에이전트에 포함 됩니다. 합니다 **mssql server** 을 패키지 하 고 기본적으로 비활성화 됩니다. 이 릴리스의 버전 정보와 함께 SQL Server 에이전트를 지 원하는 기능에 대 한 내용은 참조는 [릴리스](sql-server-linux-release-notes.md)합니다.

 SQL Server 에이전트를 설치/사용:
- [버전 2017 CU4 이상, SQL Server 에이전트를 사용 하도록 설정](#EnableAgentAfterCU4)
- [아래 및 버전 2017 CU3에 대 한 SQL Server 에이전트 설치](#InstallAgentBelowCU4)


## <a name="EnableAgentAfterCU4">버전 2017 CU4 이상, SQL Server 에이전트를 사용 하도록 설정</a>

 SQL Server 에이전트를 사용 하려면 다음 단계를 수행 합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> 2017 CU3에서에서 업그레이드 하는 경우 아래 에이전트가 설치 된 SQL Server 에이전트 됩니다 자동으로 사용 하도록 설정 하 고 이전 에이전트 패키지 제거 됩니다.  

## <a name="InstallAgentBelowCU4">아래 및 버전 2017 CU3에 대 한 SQL Server 에이전트 설치</a>

> [!NOTE]
> 아래 설치 지침은 아래 SQL Server 버전 2017 CU3에 적용 됩니다. 먼저 SQL Server 에이전트를 설치 하기 전에 [SQL Server 2017 설치](sql-server-linux-setup.md#platforms)합니다. 키 및 설치할 때 사용 하는 리포지토리를 구성 합니다 **mssql server 에이전트** 패키지 있습니다.

플랫폼에 대 한 SQL Server 에이전트를 설치 합니다.
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name="RHEL">RHEL 설치</a>

다음 단계를 사용 하 여 설치 합니다 **mssql server 에이전트** Red Hat Enterprise Linux에서. 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

이미 있는 경우 **mssql server 에이전트** 설치를 업데이트할 수 있습니다 다음 명령 사용 하 여 최신 버전으로 합니다.

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

오프 라인 설치에 필요한 경우 찾습니다에서 SQL Server 에이전트 패키지 다운로드 합니다 [릴리스](sql-server-linux-release-notes.md)합니다. 다음 문서에서 설명한 동일한 오프 라인 설치 단계를 사용 하 여 [Install SQL Server](sql-server-linux-setup.md#offline)합니다.

### <a name="ubuntu">Ubuntu에 설치</a>

다음 단계를 사용 하 여 설치 합니다 **mssql server 에이전트** ubuntu 합니다. 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

이미 있는 경우 **mssql server 에이전트** 설치를 업데이트할 수 있습니다 다음 명령 사용 하 여 최신 버전으로 합니다.

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

오프 라인 설치에 필요한 경우 찾습니다에서 SQL Server 에이전트 패키지 다운로드 합니다 [릴리스](sql-server-linux-release-notes.md)합니다. 다음 문서에서 설명한 동일한 오프 라인 설치 단계를 사용 하 여 [Install SQL Server](sql-server-linux-setup.md#offline)합니다.

### <a name="SLES">SLES의 설치</a>

다음 단계를 사용 하 여 설치 합니다 **mssql server 에이전트** SUSE Linux Enterprise server입니다. 

설치 **mssql server 에이전트** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

이미 있는 경우 **mssql server 에이전트** 설치를 업데이트할 수 있습니다 다음 명령 사용 하 여 최신 버전으로 합니다.

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

오프 라인 설치에 필요한 경우 찾습니다에서 SQL Server 에이전트 패키지 다운로드 합니다 [릴리스](sql-server-linux-release-notes.md)합니다. 다음 문서에서 설명한 동일한 오프 라인 설치 단계를 사용 하 여 [Install SQL Server](sql-server-linux-setup.md#offline)합니다.

## <a name="next-steps"></a>다음 단계
SQL Server 에이전트를 사용 하 여 만들기, 예약 하며, 작업을 실행 하는 방법에 대 한 자세한 내용은 참조 하세요. [Linux에서 SQL Server 에이전트 작업을 실행](sql-server-linux-run-sql-server-agent-job.md)합니다.

---
title: "Linux에서 SQL Server 에이전트를 설치 합니다. | Microsoft Docs"
description: "이 항목에서는 Linux에서 SQL Server 에이전트를 설치 하는 방법에 설명 합니다."
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.workload: On Demand
ms.openlocfilehash: 873c2da961db577889a3fca4139e325083d609e9
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="install-sql-server-agent-on-linux"></a>Linux에서 SQL Server 에이전트를 설치 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 에이전트를 설치 하는 다음 단계를 수행 (**mssql 서버 에이전트**) linux. [SQL Server 에이전트](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) 예약 된 SQL Server 작업을 실행 합니다. 이 버전의 SQL Server 에이전트에 대 한 지원 되는 기능에 대 한 자세한 내용은 참조는 [릴리스 정보](sql-server-linux-release-notes.md)합니다.

> [!NOTE]
> 먼저 SQL Server 에이전트를 설치 하기 전에 [SQL Server 2017 설치](sql-server-linux-setup.md#platforms)합니다. 이 구성 요소의 키 및 설치할 때 사용 하는 저장소는 **mssql 서버 에이전트** 패키지 합니다.

플랫폼에 대 한 SQL Server 에이전트를 설치 합니다.

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">RHEL에 설치</a>

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

오프 라인 설치 해야 할 경우에 SQL Server 에이전트 패키지 다운로드를 찾습니다는 [릴리스 정보](sql-server-linux-release-notes.md)합니다. 다음 항목에 설명 된 동일한 오프 라인 설치 단계를 사용 하 여 [SQL Server 설치](sql-server-linux-setup.md#offline)합니다.

## <a name="ubuntu">Ubuntu 설치</a>

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

오프 라인 설치 해야 할 경우에 SQL Server 에이전트 패키지 다운로드를 찾습니다는 [릴리스 정보](sql-server-linux-release-notes.md)합니다. 다음 항목에 설명 된 동일한 오프 라인 설치 단계를 사용 하 여 [SQL Server 설치](sql-server-linux-setup.md#offline)합니다.

## <a name="SLES">SLES에 설치</a>

설치 하려면 다음 단계를 사용 하 여는 **mssql 서버 에이전트** SUSE Linux Enterprise Server에 있습니다. 

Install **mssql-server-agent** 

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

오프 라인 설치 해야 할 경우에 SQL Server 에이전트 패키지 다운로드를 찾습니다는 [릴리스 정보](sql-server-linux-release-notes.md)합니다. 다음 항목에 설명 된 동일한 오프 라인 설치 단계를 사용 하 여 [SQL Server 설치](sql-server-linux-setup.md#offline)합니다.

## <a name="next-steps"></a>다음 단계
SQL Server 에이전트를 사용 하 여 일정을 만들고 작업을 실행 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Linux에서 SQL Server 에이전트 작업 실행](sql-server-linux-run-sql-server-agent-job.md)합니다.

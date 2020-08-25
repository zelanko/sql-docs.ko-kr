---
title: Linux에서 SQL Server 에이전트 구성
description: Linux에서 SQL Server 에이전트를 사용하도록 설정하거나 설치하는 방법을 알아봅니다. SQL Server 2017 CU4부터는 SQL Server 에이전트가 mssql-server 패키지에 포함되어 있습니다.
author: VanMSFT
ms.author: vanto
ms.date: 12/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.openlocfilehash: 6554acf46da19a9833cf649bce34a455cbc92e5b
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/11/2020
ms.locfileid: "88088813"
---
# <a name="install-sql-server-agent-on-linux"></a>Linux에 SQL Server 에이전트 설치

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 Linux에서 SQL Server 에이전트를 사용하도록 설정하거나 설치하는 방법을 설명합니다.

[SQL Server 에이전트](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)는 예약된 SQL Server 작업을 실행합니다. SQL Server 2017 CU4부터 SQL Server 에이전트는 **mssql-server** 패키지에 포함되어 있으며 기본적으로 사용하지 않도록 설정됩니다. 버전 정보와 함께 이 SQL Server 에이전트 릴리스에 지원되는 기능에 대한 자세한 내용은 [릴리스 정보](sql-server-linux-release-notes.md)를 참조하세요.

## <a name="instructions"></a>Instructions

Linux에서 SQL Server 에이전트를 사용하려면 먼저 다음 단계를 수행하여 SQL Server 에이전트를 사용하도록 설정하거나 설치합니다.

1. `/etc/hosts` 파일에 호스트 이름(도메인 포함 및 제외)을 추가합니다. 다음 줄은 호스트 이름 항목 형식의 예를 보여 줍니다.

   ```bash
   "IP Address" "hostname"
   "IP Address" "hostname.domain.com"
   ```

1. 사용 중인 SQL Server 버전에 따라 다음 섹션 중 하나의 지침을 따르세요.

   | 버전 | Instructions |
   |---|---|
   | SQL Server 2017 CU4 이상</br>SQL Server 2019 | [SQL Server 에이전트 사용](#EnableAgentAfterCU4) |
   | SQL Server 2017 CU3 이하 | [SQL Server 에이전트 설치](#InstallAgentBelowCU4) |

## <a name="enable-the-sql-server-agent"></a><a id="EnableAgentAfterCU4"></a>SQL Server 에이전트 사용

SQL Server 2019 및 SQL Server 2017 CU4 이상에서는 SQL Server 에이전트를 사용하도록 설정하기만 하면 됩니다. 별도의 패키지를 설치할 필요가 없습니다.

SQL Server 에이전트를 사용하도록 설정하려면 다음 단계를 수행합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> 에이전트가 설치된 2017 CU3 이하에서 업그레이드하는 경우 SQL Server 에이전트는 자동으로 사용하도록 설정되고 이전 에이전트 패키지가 제거됩니다.  

## <a name="install-the-sql-server-agent"></a><a name="InstallAgentBelowCU4"></a>SQL Server 에이전트 설치

SQL Server 2017 CU3 및 이전 버전에서는 SQL Server 에이전트 패키지를 설치해야 합니다.

> [!NOTE]
> 아래 설치 지침은 SQL Server 버전 2017 CU3 이하에 적용됩니다. SQL Server 에이전트를 설치하기 전에 먼저 [SQL Server를 설치](sql-server-linux-setup.md#platforms)합니다. 이렇게 하면 **mssql-server-polybase** 패키지를 설치할 때 사용하는 키 및 리포지토리가 구성됩니다.

플랫폼에 대한 SQL Server 에이전트를 설치합니다.
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name=""></a><a name="RHEL">RHEL에 설치</a>

다음 단계를 사용하여 Red Hat Enterprise Linux에서 **mssql-server-agent**를 설치합니다. 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

**mssql-server-agent**가 이미 설치된 경우 다음 명령을 사용하여 최신 버전으로 업데이트할 수 있습니다.

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

오프라인 설치가 필요한 경우 [릴리스 정보](sql-server-linux-release-notes.md)에서 SQL Server 에이전트 패키지 다운로드를 찾습니다. 그런 다음, [SQL Server 설치](sql-server-linux-setup.md#offline) 문서에 설명된 것과 동일한 오프라인 설치 단계를 사용합니다.

### <a name=""></a><a name="ubuntu">Ubuntu에 설치</a>

다음 단계에 따라 Ubuntu에 **mssql-server-agent**를 설치합니다. 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

**mssql-server-agent**가 이미 설치된 경우 다음 명령을 사용하여 최신 버전으로 업데이트할 수 있습니다.

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

오프라인 설치가 필요한 경우 [릴리스 정보](sql-server-linux-release-notes.md)에서 SQL Server 에이전트 패키지 다운로드를 찾습니다. 그런 다음, [SQL Server 설치](sql-server-linux-setup.md#offline) 문서에 설명된 것과 동일한 오프라인 설치 단계를 사용합니다.

### <a name=""></a><a name="SLES">SLES에 설치</a>

다음 단계를 사용하여 SUSE Linux Enterprise Server에서 **mssql-server-agent**를 설치합니다. 

**mssql-server-agent** 설치 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

**mssql-server-agent**가 이미 설치된 경우 다음 명령을 사용하여 최신 버전으로 업데이트할 수 있습니다.

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

오프라인 설치가 필요한 경우 [릴리스 정보](sql-server-linux-release-notes.md)에서 SQL Server 에이전트 패키지 다운로드를 찾습니다. 그런 다음, [SQL Server 설치](sql-server-linux-setup.md#offline) 문서에 설명된 것과 동일한 오프라인 설치 단계를 사용합니다.

## <a name="next-steps"></a>다음 단계
SQL Server 에이전트를 사용하여 작업을 만들고 예약 및 실행하는 방법에 대한 자세한 내용은 [Linux에서 SQL Server 에이전트 작업 실행](sql-server-linux-run-sql-server-agent-job.md)을 참조하세요.

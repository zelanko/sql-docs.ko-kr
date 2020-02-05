---
title: SQL Server on Docker를 사용하는 분산 트랜잭션(MSDTC)
description: Docker의 SQL Server 컨테이너에 있는 분산 트랜잭션에 MSDTC(Microsoft Distributed Transaction Coordinator)를 사용하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 99c17e04e4352df91ad3c6028b3ec88fc5022c50
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558407"
---
# <a name="how-to-use-distributed-transactions-with-sql-server-on-docker"></a>Docker의 SQL Server에서 분산 트랜잭션을 사용하는 방법

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 분산 트랜잭션을 위해 Docker에서 SQL Server Linux 컨테이너를 설정하는 방법을 설명합니다.

SQL Server 컨테이너 이미지는 분산 트랜잭션에 필요한 MSDTC(Microsoft Distributed Transaction Coordinator)를 사용할 수 있습니다. MSDTC에 대한 통신 요구 사항을 이해하려면 [Linux에서 MSDTC(Microsoft Distributed Transaction Coordinator)를 구성하는 방법](sql-server-linux-configure-msdtc.md)을 참조하세요. 이 문서에서는 SQL Server Docker 컨테이너와 관련된 특별한 요구 사항 및 시나리오를 설명합니다.

## <a name="configuration"></a>구성

Docker용 컨테이너에서 MSDTC 트랜잭션을 사용하도록 설정하려면 다음 두 가지 새 환경 변수를 설정해야 합니다.

- **MSSQL_RPC_PORT**: RPC 엔드포인트 매퍼 서비스가 바인딩되고 수신 대기하는 TCP 포트입니다.  
- **MSSQL_DTC_TCP_PORT**: MSDTC 서비스가 수신 대기하도록 구성된 포트입니다.

### <a name="pull-and-run"></a>풀 및 실행

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

다음 예제에서는 이 환경 변수를 사용하여 MSDTC에 대해 구성된 단일 SQL Server 2017 컨테이너를 풀하고 실행하는 방법을 보여 줍니다. 이를 통해 호스트의 모든 애플리케이션과 통신할 수 있습니다.

```bash
docker run \
   -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -e 'MSSQL_RPC_PORT=135' -e 'MSSQL_DTC_TCP_PORT=51000' \
   -p 51433:1433 -p 135:135 -p 51000:51000  \
   -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run `
   -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -e "MSSQL_RPC_PORT=135" -e "MSSQL_DTC_TCP_PORT=51000" `
   -p 51433:1433 -p 135:135 -p 51000:51000  `
   -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

다음 예제에서는 이 환경 변수를 사용하여 MSDTC에 대해 구성된 단일 SQL Server 2019 컨테이너를 풀하고 실행하는 방법을 보여 줍니다. 이를 통해 호스트의 모든 애플리케이션과 통신할 수 있습니다.

```bash
docker run \
   -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -e 'MSSQL_RPC_PORT=135' -e 'MSSQL_DTC_TCP_PORT=51000' \
   -p 51433:1433 -p 135:135 -p 51000:51000  \
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run `
   -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -e "MSSQL_RPC_PORT=135" -e "MSSQL_DTC_TCP_PORT=51000" `
   -p 51433:1433 -p 135:135 -p 51000:51000  `
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

> [!IMPORTANT]
> 이전 명령은 Linux에서 실행되는 Docker에 대해서만 작동합니다. Windows 기반 Docker의 경우 Windows 호스트는 이미 포트 135에서 수신 대기합니다. Windows 기반 Docker의 `-p 135:135` 매개 변수를 제거할 수 있지만 몇 가지 제한 사항이 있습니다. 생성된 컨테이너는 호스트와 관련된 분산 트랜잭션에 사용할 수 없으며, 호스트에 있는 docker 컨테이너 간의 분산 트랜잭션에만 참여할 수 있습니다.

이 명령에서 **RPC 엔드포인트 매퍼** 서비스는 포트 135에 바인딩되고 **MSDTC** 서비스는 docker 가상 네트워크 내의 포트 51000에 바인딩되었습니다. SQL Server TDS 통신은 docker 가상 네트워크 내의 포트 1433에서 발생합니다. 이 포트는 TDS 포트 51433, RPC 엔드포인트 매퍼 포트 135 및 MSDTC 포트 51000으로 호스트에 외부적으로 공개되었습니다.

> [!NOTE]
> RPC 엔드포인트 매퍼 및 MSDTC 포트는 호스트와 컨테이너에서 동일하지 않아도 됩니다. 따라서 RPC 엔드포인트 매퍼 포트가 컨테이너에서 135로 구성된 경우에는 잠재적으로 포트 13501 또는 호스트 서버의 사용 가능한 다른 포트에 매핑될 수 있습니다.

## <a name="configure-the-firewall"></a>방화벽 구성

호스트와 통신하거나 호스트를 통해 통신하려면 호스트 서버에서 컨테이너에 대한 방화벽도 구성해야 합니다. Docker 컨테이너가 외부 통신을 위해 공개하는 모든 포트에 대한 방화벽을 엽니다. 이전 예제에서는 포트 135, 51433 및 51000에 해당합니다. 이 포트는 호스트 자체의 포트이며 컨테이너에서 매핑되는 포트가 아닙니다. 따라서 컨테이너의 RPC 엔드포인트 매퍼 포트 51000이 호스트 포트 51001에 매핑된 경우 호스트와 통신하려면 방화벽에서 포트 51001(51000이 아님)이 열려 있어야 합니다.  

다음 예제에서는 Ubuntu에서 이 규칙을 만드는 방법을 보여 줍니다.

```bash
sudo ufw allow from any to any port 51433 proto tcp
sudo ufw allow from any to any port 51000 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

다음 예제에서는 RHEL(Red Hat Enterprise Linux)에서 이 작업을 수행하는 방법을 보여 줍니다.

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=51433/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

## <a name="configure-port-routing-on-the-host"></a>호스트에서 포트 라우팅 구성

이전 예제에서는 단일 Docker 컨테이너가 RPC 포트 135를 호스트의 포트 135에 매핑하기 때문에 이제 호스트를 통한 분산 트랜잭션은 추가 구성 없이도 작동합니다. SQL Server는 이러한 컨테이너에서 상승된 권한으로 실행되므로 루트로 실행되는 컨테이너에서 포트 135를 직접 사용할 수 있습니다. 컨테이너 외부 또는 루트가 아닌 컨테이너의 SQL Server의 경우 컨테이너에 13500과 같은 다른 임시 포트를 사용해야 하며 포트 135에 대한 트래픽은 해당 포트로 라우팅되어야 합니다. 또한 컨테이너 포트 135에서 임시 포트까지 컨테이너 내에서 포트 라우팅 규칙도 구성해야 합니다.

또 컨테이너의 포트 135를 호스트의 다른 포트(예: 13500)에 매핑하려면 호스트에서 포트 라우팅을 구성해야 합니다. 이를 통해 docker 컨테이너는 호스트 및 다른 외부 서버를 통해 분산 트랜잭션에 참여할 수 있습니다.

라우팅 포트에 대한 자세한 내용은 [포트 라우팅 구성](sql-server-linux-configure-msdtc.md#configure-port-routing)을 참조하세요.

> [!NOTE]
> SQL Server 2017은 기본적으로 루트 컨테이너에서 실행되는 반면 SQL Server 2019 컨테이너는 루트가 아닌 사용자로 실행됩니다.

## <a name="next-steps"></a>다음 단계

Linux의 MSDTC에 대한 자세한 내용은 [Linux에서 MSDTC(Microsoft Distributed Transaction Coordinator)를 구성하는 방법](sql-server-linux-configure-msdtc.md)을 참조하세요.

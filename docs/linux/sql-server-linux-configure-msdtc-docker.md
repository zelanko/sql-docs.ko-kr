---
title: Docker에서 SQL Server를 사용 하 여 분산된 트랜잭션을 사용 하는 방법 | Microsoft Docs
description: 이 문서에서는 Linux에서 MSDTC를 구성 하기 위한 Dprovides 연습은 사용 하는 방법을 설명 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 09/25/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: fbe682f39c496441a209ca52bede9a0726671c62
ms.sourcegitcommit: 56fb7b648adae2c7b81bd969de067af1a2b54180
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2019
ms.locfileid: "57227106"
---
# <a name="how-to-use-distributed-transactions-with-sql-server-on-docker"></a>Docker에서 SQL Server를 사용 하 여 분산된 트랜잭션을 사용 하는 방법

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 분산된 트랜잭션에 대 한 Docker에서 SQL Server Linux 컨테이너를 설정 하는 방법에 설명 합니다.

SQL Server 2019 미리 보기부터 컨테이너 이미지 Distributed Transaction Coordinator MSDTC (Microsoft) 분산된 트랜잭션에 대 한 필요한 지원 합니다. MSDTC에 대 한 통신 요구 사항을 이해 하려면 참조 [Linux에는 MSDTC Microsoft Distributed Transaction Coordinator ()를 구성 하는 방법](sql-server-linux-configure-msdtc.md)합니다. 이 문서에는 특별 한 요구 사항 및 SQL Server Docker 컨테이너와 관련 된 시나리오를 설명 합니다.

## <a name="configuration"></a>Configuration

Docker 컨테이너에서 MSDTC 트랜잭션의 사용 하려면 두 개의 새로운 환경 변수를 설정 해야 합니다.

- **MSSQL_RPC_PORT**: RPC 종점 매퍼 서비스로을 바인딩하고 수신 대기 하는 TCP 포트입니다.  
- **MSSQL_DTC_TCP_PORT**: 포트에서 수신 하도록 MSDTC 서비스가 구성 되어 있는지 합니다.

### <a name="pull-and-run"></a>끌어오기 및 실행

다음 예제에서는 이러한 환경 변수를 사용 하 여 끌어오기를 MSDTC에 대해 구성 된 단일 SQL Server 컨테이너를 실행 하는 방법을 보여 줍니다. 따라서 모든 호스트에서 모든 응용 프로그램과 통신할 수 있습니다.

```bash
docker run \
   -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -e 'MSSQL_RPC_PORT=135' -e 'MSSQL_DTC_TCP_PORT=51000' \
   -p 51433:1433 -p 135:135 -p 51000:51000  \
   -d mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu
```

> [!IMPORTANT]
> Linux에서 실행 되는 Docker에 대 한 이전 명령 에서만 작동 합니다. Windows에서 docker를 Windows 호스트 포트 135에서 이미 수신 대기합니다. 제거할 수는 `-p 135:135` 매개 변수가 있지만 Windows에서 Docker에 대 한 몇 가지 제한 사항이 있습니다. 결과 컨테이너 다음 사용할 수 없습니다 호스트와 관련 된 분산된 트랜잭션에 대 한 이 옵션은 호스트에서 docker 컨테이너 간에 분산 트랜잭션에 참여할 수 있습니다.

이 명령에는 **RPC 끝점 매퍼** 서비스 포트 135에 바인딩된 및 **MSDTC** 포트 51000 docker virtual network 내에서 서비스 바인딩 되었습니다. SQL Server TDS 통신 docker virtual network 내에서 포트 1433에서 발생합니다. 이러한 포트 외부적으로 노출 된 TDS 포트 51433, RPC 끝점 매퍼 포트 135, 51000 MSDTC 포트와 호스트 합니다.

> [!NOTE]
> RPC 끝점 매퍼 및 MSDTC 포트를 호스트와 컨테이너에서 동일한 수 없습니다. 따라서 컨테이너에 135를 RPC 종점 매퍼가 포트를 구성 하는 동안이 잠재적으로 매핑할 수 있습니다 13501 또는 다른 사용 가능한 포트를 호스트 서버의 포트입니다.

## <a name="configure-the-firewall"></a>방화벽 구성

호스트와 통신 하기 위해도 컨테이너에 대 한 호스트 서버에서 방화벽을 구성 해야 합니다. 열린 모든 방화벽 포트는 docker 컨테이너 외부 통신에 노출 합니다. 이전 예제에서는 포트 135, 51433, 및 51000가 됩니다. 이들은, 자체 호스트의 포트 및 컨테이너에 매핑할 포트에 없습니다. 따라서 RPC 끝점 매퍼 포트 51000 컨테이너의 호스트 포트 51001 매핑한 다음 포트가 호스트와의 통신에 대 한 방화벽에 51001 (없습니다 51000) 열어야 합니다.  

다음 예제에서는 Ubuntu에서 이러한 규칙을 만드는 방법을 보여 줍니다.

```bash
sudo ufw allow from any to any port 51433 proto tcp
sudo ufw allow from any to any port 51000 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

다음 예제에서는 어떻게 수행할 수 있습니다 Red Hat Enterprise Linux (RHEL)를 보여 줍니다.

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=51433/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

## <a name="configure-port-routing-on-the-host"></a>호스트의 포트 라우팅 구성

이전 예제에서는 단일 Docker 컨테이너 호스트에 포트 135 RPC 포트 135를 매핑하므로 호스트를 사용 하 여 분산된 트랜잭션을 이제 함께 해야 추가 구성 없이 합니다. 것 직접 포트는 컨테이너에 135를 사용 하 여 SQL Server 컨테이너에서 상승 된 권한으로 실행 되므로 note 합니다. 컨테이너 외부에서 SQL Server에 대 한 다른 사용 후 삭제 포트 사용 해야 하며 포트 135에 트래픽이 라우팅되어야 하며, 그런 다음 해당 포트에 합니다.

그러나 컨테이너의 포트 135를 호스트에서 다른 포트 13500 같은 지도 하려는 않은 경우 다음 해야 호스트에서 포트 라우팅 구성 합니다. 이렇게 하면 docker 컨테이너를 호스트와 다른 외부 서버를 사용 하 여 분산된 트랜잭션에 참여할 수 있습니다. 자세한 내용은 [포트 라우팅 구성](sql-server-linux-configure-msdtc.md#configure-port-routing)합니다.

## <a name="next-steps"></a>다음 단계

Linux에서 MSDTC에 대 한 자세한 내용은 참조 하세요 [Linux에는 MSDTC Microsoft Distributed Transaction Coordinator ()를 구성 하는 방법](sql-server-linux-configure-msdtc.md)합니다.

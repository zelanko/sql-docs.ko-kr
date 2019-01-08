---
title: Linux에서 MSDTC를 구성 하는 방법 | Microsoft Docs
description: 이 문서에서는 Linux에서 MSDTC를 구성 하기 위한 연습을 제공 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 127f39075a1b84b1250a27003efeb28083d1adbd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52513195"
---
# <a name="how-to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-on-linux"></a>Linux에는 MSDTC Microsoft Distributed Transaction Coordinator ()를 구성 하는 방법

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 linux의 Microsoft Distributed Transaction Coordinator (MSTDC)를 구성 하는 방법을 설명 합니다. Linux에서 MSDTC 지원 SQL Server 2019 미리 보기에서 도입 되었습니다.

## <a name="overview"></a>개요

분산된 트랜잭션 내 SQL Server에서 MSDTC 및 RPC 끝점 매퍼 기능을 도입 하 여 SQL Server Linux에서 사용할 수 있습니다. 기본적으로 RPC 끝점 매핑 프로세스 들어오는 RPC 요청에 대해 포트 135에서 수신 하 고 적절 한 구성 요소 (예: MSDTC 서비스)는 라우팅합니다. Linux에서 잘 알려진 포트 (포트 1024 보다 작은 숫자를) 바인딩할 슈퍼 사용자 권한이 필요 합니다. 시스템 관리자는 RPC 끝점 매퍼 프로세스에 대 한 루트 권한으로 SQL Server 시작을 방지 하려면 SQL Server RPC 끝점 매핑 프로세스에 135 포트에서 트래픽을 라우팅하는 NAT 번역을 작성 하도록 iptables를 사용 해야 합니다.

SQL Server 2019 mssql conf 유틸리티에 대 한 두 가지 구성 매개 변수를 소개합니다.

| mssql conf 설정 | Description |
|---|---|
| **network.rpcport** | RPC 끝점 매퍼 프로세스에 바인딩되는 TCP 포트입니다. |
| **network.servertcpport** | MSDTC 서버 수신 하는 포트입니다. 그렇지 않은 경우 설정 MSDTC 서비스가 사용 하 여 임의의 임시 포트에서 서비스를 시작 하면 및 방화벽 예외는 MSDTC 서비스가 통신 계속 실행 되도록 다시 구성 해야 합니다. |

이러한 설정 및 기타 관련된 MSDTC 설정에 대 한 자세한 내용은 참조 하세요. [mssql-conf 도구를 사용 하 여 Linux에서 SQL Server 구성](sql-server-linux-configure-mssql-conf.md#msdtc)합니다.

## <a name="supported-msdtc-configurations"></a>지원 되는 MSDTC 구성

다음 MSDTC 구성이 지원 됩니다.

- OLE TX 분산 트랜잭션 Linux의 SQL Server에 대 한 JDBC 및 ODBC 공급자에 대 한 합니다.
- JDBC 공급자를 사용 하 여 Linux에서 SQL Server에 대해 XA 분산 트랜잭션.
- 연결 된 서버에 분산된 트랜잭션입니다.

제한 사항 및 미리 보기의 MSDTC에 대 한 알려진된 문제 [Linux에서 SQL Server 2019 미리 보기에 대 한 릴리스](sql-server-linux-release-notes-2019.md#msdtc)합니다.

## <a name="msdtc-configuration-steps"></a>MSDTC 구성 단계

MSDTC 통신 및 기능을 구성 하는 방법은 세 가지 단계가 있습니다. 필요한 구성 단계를 수행 되지 않으며 SQL Server가 MSDTC 기능을 사용 하지 않습니다.

- 구성할 **network.rpcport** 하 고 **distributedtransaction.servertcpport** mssql 구성이 사용 하 여
- 통신을 허용 하도록 방화벽 구성 **rpcport**를 **servertcpport**, 및 포트 135입니다.
- Linux SQL Server로 리디렉션되도록 포트 135에서 RPC 통신 서버 라우팅 구성 **network.rpcport**합니다.

다음 섹션에서는 각 단계에 대 한 자세한 지침을 제공 합니다.

## <a name="configure-rpc-and-msdtc-ports"></a>MSDTC 및 RPC 포트를 구성 합니다.

먼저 구성 **network.rpcport** 하 고 **distributedtransaction.servertcpport** mssql 구성이 사용 하 여

1. Mssql conf를 사용 하 여 설정 합니다 **network.rpcport** 값입니다. 다음 예제에서는 13500로 설정합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport 13500
   ```

2. 설정 된 **distributedtransaction.servertcpport** 값입니다. 다음 예제에서는 51999로 설정합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport 51999
   ```

3. SQL Server를 다시 시작하십시오.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="configure-the-firewall"></a>방화벽 구성

마지막 단계에서 통신을 허용 하도록 방화벽을 구성 하는 것 **rpcport**를 **servertcpport**, 및 포트 135입니다.  이 통해 RPC 끝점 매핑 프로세스 및 MSDTC 프로세스 외부에서 다른 트랜잭션 관리자 및 코디네이터를 전달할 수 있습니다. 이 대 한 실제 단계는 Linux 배포판 및 방화벽에 따라 달라 집니다. 

다음 예제에서는 Ubuntu에서 이러한 규칙을 만드는 방법을 보여 줍니다.

```bash
sudo ufw allow from any to any port 51999 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

다음 예제에서는 어떻게 수행할 수 있습니다 Red Hat Enterprise Linux (RHEL)를 보여 줍니다.

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

다음 섹션에서 포트 라우팅 구성 하기 전에 방화벽을 구성 하는 것이 반드시 합니다. 방화벽을 새로 고쳐 일부 경우에는 포트 라우팅 규칙을 지울 수 있습니다.

## <a name="configure-port-routing"></a>포트 라우팅 구성

RPC 통신 포트 135에서 SQL Server로 리디렉션되도록 Linux server 라우팅 테이블을 구성할 **network.rpcport**합니다. 다른 배포에 전달 하는 포트에 대 한 구성 메커니즘은 달라질 수 있습니다. Firewalld 서비스를 사용 하지 않는 배포판에서는 iptable 규칙에는이 작업을 수행 하는 효율적인 메커니즘입니다. 이러한 distrubution의 예는 Ubuntu 16.04 및 SUSE Enterprise Linux v12입니다. 다음 명령을 다시 부팅 한 후 규칙을 복원 하기 위한 지침을 제공 하므로 iptable 규칙 재부팅 하는 동안 유지 되지 않습니다 수 있습니다.

1. 포트 135에 대 한 라우팅 규칙을 만듭니다. 다음 예제에서는 포트 135는 이전 섹션에 정의 된 RPC 포트 13500에 전달 됩니다. 대체 `<ipaddress>` 서버의 IP 주소를 사용 하 여 합니다.

   ```bash
   iptables -t nat -A PREROUTING -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL  \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   iptables -t nat -A OUTPUT -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   ```

   `--comment RpcEndPointMapper` 이전 명령에서 매개 변수가 후속 명령에서 이러한 규칙을 관리 하는 데 도움이 됩니다.

2. 다음 명령을 사용 하 여 만든 라우팅 규칙을 보려면:

   ```bash
   iptables -S -t nat | grep "RpcEndPointMapper"
   ```

3. 라우팅 규칙은 컴퓨터에 파일로 저장 합니다.

   ```bash
   iptables-save > /etc/iptables.conf
   ```

4. 규칙을 다시 부팅 한 후 다시 로드 하려면 다음 명령을 추가 `/etc/rc.local` (Ubuntu 또는 RHEL)에 또는 `/etc/init.d/after.local` (SLES)에 대 한 합니다.

   ```bash
   iptables-restore < /etc/iptables.conf
   ```

**iptables 저장** 하 고 **iptables 복원은** 명령을 저장 하 고 iptables 항목을 복원 하는 기본 메커니즘을 제공 합니다. Linux 배포에 따라 있습니다 수 더 고급 또는 사용할 수 있는 옵션을 자동화 합니다. 예를 들어, Ubuntu 대안은 합니다 **iptables 영구** 패키지 항목을 지속 되도록 할 것입니다. 

Firewalld 서비스를 사용 하는 배포에서 동일한 서비스가 내부 포트 전달을 확인 하 고 서버에서 포트를 열기 위한 사용할 수 있습니다. 예를 들어, Red Hat Enterprise Linux에서 사용 해야 firewalld 서비스 (-를 사용 하 여 방화벽 cmd 구성 유틸리티를 통해 추가-앞으로-포트 또는 비슷한 옵션이)를 만들고 영구 포트 전달 iptables를 사용 하는 대신 규칙을 관리 합니다.

```bash
firewall-cmd --permanent --add-forward-port=port=135:proto=tcp:toport=13500
```

> [!IMPORTANT]
> 이전 단계에는 고정된 IP 주소를 가정합니다. SQL Server 인스턴스에 대 한 IP 주소 (수동 또는 DHCP)으로 인해 변경 되 면 제거 하 고 iptables를 사용 하 여 만들어진 경우 라우팅 규칙을 다시 만들어야 합니다. 이전을 제거 하려면 다음 명령을 다시 작성 하거나 기존 라우팅 규칙을 삭제 해야 하는 경우 사용할 수 있습니다 `RpcEndPointMapper` 규칙:
> 
> ```bash
> iptables -S -t nat | grep "RpcEndPointMapper" | sed 's/^-A //' | while read rule; do iptables -t nat -D $rule; done
> ```

## <a name="verify"></a>확인

이 시점에서 SQL Server 분산된 트랜잭션에 참여할 수 있어야 합니다. SQL Server가 수신 대기를 확인 하려면 다음을 실행 합니다 **netstat** 명령 (RHEL를 사용 하는 경우 먼저 설치 해야 할 수 있습니다 합니다 **net 도구** 패키지):

```bash
sudo netstat -tulpn | grep sqlservr
```

다음과 유사한 출력이 표시 됩니다.

```bash
tcp 0 0 0.0.0.0:1433 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 127.0.0.1:1434 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 0.0.0.0:13500 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 0.0.0.0:51999 0.0.0.0:* LISTEN 13911/sqlservr
tcp6 0 0 :::1433 :::* LISTEN 13911/sqlservr
tcp6 0 0 ::1:1434 :::* LISTEN 13911/sqlservr
tcp6 0 0 :::13500 :::* LISTEN 13911/sqlservr
tcp6 0 0 :::51999 :::* LISTEN 13911/sqlservr
```

그러나 다시 시작 후 SQL 서버가 시작 되지 않으며에서 수신 대기 합니다 **servertcpport** 첫 번째 트랜잭션 배포까지 합니다. 이 경우 첫 번째 분산된 트랜잭션에 될 때까지이 예제의 51999 포트에서 수신 대기 하는 SQL Server 표시 되지 것입니다.

## <a name="next-steps"></a>다음 단계

Linux의 SQL Server에 대 한 자세한 내용은 참조 하세요. [Linux의 SQL Server](sql-server-linux-overview.md)합니다.

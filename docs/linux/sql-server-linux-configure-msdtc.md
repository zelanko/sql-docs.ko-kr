---
title: Linux에서 MSDTC를 구성하는 방법
description: 이 문서에서는 Linux에서 MSDTC를 구성하기 위한 연습을 제공합니다.
author: VanMSFT
ms.author: vanto
ms.date: 08/01/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: a39e0a743053db694efc2d0e8176e659d7e376d1
ms.sourcegitcommit: 58f1d5498c87bfe0f6ec4fd9d7bbe723be47896b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68995872"
---
# <a name="how-to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-on-linux"></a>Linux에서 MSDTC(Microsoft Distributed Transaction Coordinator)를 구성하는 방법

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux에서 MSDTC(Microsoft Distributed Transaction Coordinator)를 구성하는 방법을 설명합니다.

> [!NOTE]
> Linux의 MSDTC는 누적 업데이트 16부터 SQL Server 2017에서 지원됩니다.

## <a name="overview"></a>개요

SQL Server 내에 MSDTC 및 RPC 엔드포인트 매퍼 기능을 도입하여 SQL Server on Linux에서 분산 트랜잭션을 사용할 수 있습니다. 기본적으로 RPC 엔드포인트 매핑 프로세스는 들어오는 RPC 요청을 포트 135에서 수신하고 원격 요청에 등록된 구성 요소 정보를 제공합니다. 원격 요청은 엔드포인트 매퍼에서 반환된 정보를 사용하여 MSDTC 서비스와 같은 등록된 RPC 구성 요소와 통신할 수 있습니다. 프로세스에서 Linux의 잘 알려진 포트(1024 미만의 포트 번호)에 바인딩하려면 슈퍼 사용자 권한이 필요합니다. RPC 엔드포인트 매퍼 프로세스에 대해 루트 권한으로 SQL Server를 시작하지 않도록 하려면 시스템 관리자가 iptables를 사용하여 포트 135의 트래픽을 SQL Server의 RPC 엔드포인트 매핑 프로세스로 라우팅하기 위한 NAT(Network Address Translation)를 만들어야 합니다.

MSDTC는 mssql-conf 유틸리티의 두 가지 구성 매개 변수를 사용합니다.

| mssql-conf 설정 | 설명 |
|---|---|
| **network.rpcport** | RPC 엔드포인트 매퍼 프로세스가 바인딩되는 TCP 포트입니다. |
| **distributedtransaction.servertcpport** | MSDTC 서버가 수신 대기하는 포트입니다. 이 포트를 설정하지 않으면 MSDTC 서비스는 서비스를 다시 시작할 때 사용 후 삭제되는 임의 포트를 사용하며, MSDTC 서비스가 계속 통신할 수 있도록 방화벽 예외를 다시 구성해야 합니다. |

이 설정 및 기타 관련 MSDTC 설정에 대한 자세한 내용은 [mssql-conf 도구를 사용하여 SQL Server on Linux 구성](sql-server-linux-configure-mssql-conf.md)을 참조하세요.

## <a name="supported-msdtc-configurations"></a>지원되는 MSDTC 구성

다음 MSDTC 구성이 지원됩니다.

- ODBC 공급자를 위한 SQL Server on Linux에 대한 OLE-TX 분산 트랜잭션

- ODBC 공급자를 위한 JDBC를 사용하는 SQL Server on Linux에 대한 OLE-TX 분산 트랜잭션 ODBC 공급자를 사용하여 XA 트랜잭션을 수행하려면 Microsoft ODBC Driver for SQL Server 버전 17.3 이상을 사용해야 합니다. 자세한 내용은 [XA 트랜잭션 이해](../connect/jdbc/understanding-xa-transactions.md#configuration-instructions)를 참조하세요.

- 연결된 서버의 분산 트랜잭션

## <a name="msdtc-configuration-steps"></a>MSDTC 구성 단계

MSDTC 통신 및 기능은 3단계로 구성합니다. 필요한 구성 단계를 수행하지 않으면 SQL Server에서 MSDTC 기능을 사용할 수 없습니다.

- mssql-conf를 사용하여 **network.rpcport** 및 **distributedtransaction.servertcpport**를 구성합니다.
- **distributedtransaction.servertcpport** 및 포트 135에서 통신을 허용하도록 방화벽을 구성합니다.
- 포트 135의 RPC 통신이 SQL Server의 **network.rpcport**로 리디렉션되도록 Linux 서버 라우팅을 구성합니다.

다음 섹션에서는 각 단계에 대한 자세한 지침을 제공합니다.

## <a name="configure-rpc-and-msdtc-ports"></a>RPC 및 MSDTC 포트 구성

먼저 mssql-conf를 사용하여 **network.rpcport** 및 **distributedtransaction.servertcpport**를 구성합니다. 이 단계는 SQL Server에 적용되고 지원되는 모든 배포에서 공통적입니다.

1. mssql-conf를 사용하여 **network.rpcport** 값을 설정합니다. 다음 예제에서는 이 값을 13500으로 설정합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport 13500
   ```

2. **distributedtransaction.servertcpport** 값을 설정합니다. 다음 예제에서는 이 값을 51999로 설정합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport 51999
   ```

3. SQL Server를 다시 시작하십시오.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="configure-the-firewall"></a>방화벽 구성

두 번째 단계에서는 **distributedtransaction.servertcpport** 및 포트 135에서 통신을 허용하도록 방화벽을 구성합니다.  이렇게 하면 RPC 엔드포인트 매핑 프로세스와 MSDTC 프로세스가 외부에서 다른 트랜잭션 관리자 및 코디네이터와 통신할 수 있습니다. 이 구성의 실제 단계는 Linux 배포 및 방화벽에 따라 달라집니다. 

다음 예제에서는 **Ubuntu**에서 이 규칙을 만드는 방법을 보여 줍니다.

```bash
sudo ufw allow from any to any port 51999 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

다음 예제에서는 **RHEL(Red Hat Enterprise Linux)** 에서 이 작업을 수행하는 방법을 보여 줍니다.

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

다음 섹션에서 포트 라우팅을 구성하기 전에 방화벽을 구성해야 합니다. 방화벽을 새로 고치면 경우에 따라 포트 라우팅 규칙이 지워질 수 있습니다.

## <a name="configure-port-routing"></a>포트 라우팅 구성

포트 135의 RPC 통신이 SQL Server의 **network.rpcport**로 리디렉션되도록 Linux 서버 라우팅 테이블을 구성합니다. 다른 배포에서는 포트 전달을 위한 구성 메커니즘이 다를 수 있습니다. 다음 섹션에서는 Ubuntu, SUS Enterprise Linux(SLES) 및 RHEL(Red Hat Enterprise Linux)에 대한 지침을 제공합니다.

### <a name="port-routing-in-ubuntu-and-sles"></a>Ubuntu 및 SLES의 포트 라우팅

Ubuntu 및 SLES는 **firewalld** 서비스를 사용하지 않으므로 **iptable** 규칙은 포트 라우팅을 구현하는 효율적인 메커니즘입니다. **iptable** 규칙은 다시 부팅하는 동안 유지되지 않으므로, 다음 명령은 다시 부팅한 후 규칙을 복원하기 위한 지침도 제공합니다.

1. 포트 135에 대한 라우팅 규칙을 만듭니다. 다음 예제에서 포트 135는 이전 섹션에서 정의한 RPC 포트 13500으로 이동됩니다. `<ipaddress>`를 서버의 IP 주소로 바꿉니다.

   ```bash
   sudo iptables -t nat -A PREROUTING -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL  \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   sudo iptables -t nat -A OUTPUT -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   ```

   이전 명령의 `--comment RpcEndPointMapper` 매개 변수는 이후 명령에서 이 규칙을 관리하는 데 도움이 됩니다.

2. 다음 명령을 사용하여 직접 만든 라우팅 규칙을 확인합니다.

   ```bash
   sudo iptables -S -t nat | grep "RpcEndPointMapper"
   ```

3. 라우팅 규칙을 머신의 파일에 저장합니다.

   ```bash
   sudo iptables-save > /etc/iptables.conf
   ```

4. 다시 부팅한 후 규칙을 다시 로드하려면 `/etc/rc.local`(Ubuntu) 또는 `/etc/init.d/after.local`(SLES)에 다음 명령을 추가합니다.

   ```bash
   iptables-restore < /etc/iptables.conf
   ```

   > [!NOTE]
   > **rc.local** 또는 **after.local** 파일을 편집하려면 슈퍼 사용자(sudo) 권한이 있어야 합니다.

**iptables-save** 및 **iptables-restore** 명령은 `rc.local`/`after.local` 시작 구성과 함께 iptables 항목을 저장하고 복원하기 위한 기본 메커니즘을 제공합니다. Linux 배포에 따라 고급 또는 자동화된 옵션을 사용할 수 있습니다. 예를 들어 Ubuntu의 대체 방법은 항목을 영구적으로 설정하는 **iptables-persistent** 패키지입니다.

> [!IMPORTANT]
> 이전 단계에서는 고정 IP 주소를 가정합니다. SQL Server 인스턴스의 IP 주소가 변경되면(수동 작업 또는 DHCP로 인해) iptables를 사용하여 만들어진 라우팅 규칙을 제거하고 다시 만들어야 합니다. 기존 라우팅 규칙을 다시 만들거나 삭제해야 하는 경우에는 다음 명령을 사용하여 이전 `RpcEndPointMapper` 규칙을 제거할 수 있습니다.
> 
> ```bash
> sudo iptables -S -t nat | grep "RpcEndPointMapper" | sed 's/^-A //' | while read rule; do iptables -t nat -D $rule; done
> ```

### <a name="port-routing-in-rhel"></a>RHEL의 포트 라우팅

Red Hat Enterprise Linux와 같이 **firewalld** 서비스를 사용하는 배포에서는 서버에서 포트 열기 및 내부 포트 전달에 동일한 서비스를 사용할 수 있습니다. 예를 들어 Red Hat Enterprise Linux에서는 **firewalld** 서비스를 사용하여(`-add-forward-port` 또는 비슷한 옵션과 함께 **firewall-cmd** 구성 유틸리티를 통해) iptables를 사용하지 않고 영구적 포트 전달 규칙을 만들고 관리해야 합니다.

```bash
sudo firewall-cmd --permanent --add-forward-port=port=135:proto=tcp:toport=13500
sudo firewall-cmd --reload
```

## <a name="verify"></a>확인

이때 SQL Server는 분산 트랜잭션에 참여할 수 있어야 합니다. SQL Server가 수신 대기 중인지 확인하려면 **netstat** 명령을 실행합니다(RHEL을 사용하는 경우 먼저 **net-tools** 패키지를 설치해야 할 수 있음).

```bash
sudo netstat -tulpn | grep sqlservr
```

다음과 비슷한 내용이 출력됩니다.

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

그러나 다시 시작한 후 SQL Server는 첫 번째 분산 트랜잭션까지 **servertcpport**에서 수신 대기를 시작하지 않습니다. 이 경우 첫 번째 분산 트랜잭션까지 이 예제의 포트 51999에서 수신 대기하는 SQL Server가 표시되지 않습니다.

## <a name="configure-authentication-on-rpc-communication-for-msdtc"></a>MSDTC의 RPC 통신에 대한 인증 구성

SQL Server on Linux용 MSDTC는 기본적으로 RPC 통신에 대한 인증을 사용하지 않습니다. 그러나 호스트 머신이 AD(Active Directory) 도메인에 가입되어 있으면 다음 **mssql-conf** 설정을 통해 인증된 RPC 통신을 사용하도록 MSDTC를 구성할 수 있습니다.

| 설정 | 설명 |
|---|---|
| **distributedtransaction.allowonlysecurerpccalls**          | 분산 트랜잭션에 대한 보안 전용 RPC 호출을 구성합니다. 기본값은 0입니다. |
| **distributedtransaction.fallbacktounsecurerpcifnecessary** | 분산 트랜잭션에 대한 보안 전용 RPC 호출을 구성합니다. 기본값은 0입니다. |
| **distributedtransaction.turnoffrpcsecurity**               | 분산 트랜잭션에 대한 RPC 보안을 사용하거나 사용하지 않도록 설정합니다. 기본값은 0입니다. |

## <a name="additional-guidance"></a>추가 지침

### <a name="active-directory"></a>Active Directory

SQL Server가 AD(Active Directory) 구성에 등록된 경우 RPC를 사용할 수 있는 MSDTC를 사용하는 것이 좋습니다. SQL Server가 AD 인증을 사용하도록 구성된 경우 MSDTC는 기본적으로 상호 인증 RPC 보안을 사용합니다.

### <a name="windows-and-linux"></a>Windows 및 Linux

Windows 운영 체제의 클라이언트가SQL Server on Linux을 사용하여 분산 트랜잭션에 가입해야 하는 경우 다음과 같은 최소 버전의 Windows 운영 체제가 있어야 합니다.

| 운영 체제 | 최소 버전 | OS 빌드 |
|---|---|---|
| [Windows Server](https://docs.microsoft.com/windows-server/get-started/windows-server-release-info) | 1903 | 18362.30.190401-1528 |
| [Windows 10](https://docs.microsoft.com/windows/release-information/) | 1903 | 18362.267 |

## <a name="next-steps"></a>다음 단계

SQL Server on Linux에 대한 자세한 내용은 [SQL Server on Linux](sql-server-linux-overview.md)를 참조하세요.

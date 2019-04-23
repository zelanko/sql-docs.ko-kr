---
title: Linux에서 사용량 및 SQL Server에 대 한 진단 데이터 수집 구성 | Microsoft Docs
description: SQL Server 고객 사용량 및 진단 데이터는 수집 방법과 linux 구성에 대해 설명 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: c94023e89dbdfb784f2b1bc8db8c9842c4455fb1
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59944234"
---
# <a name="configure-usage-and-diagnostic-data-collection-for-sql-server-on-linux"></a>Linux에서 사용량 및 SQL Server에 대 한 진단 데이터 컬렉션 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

기본적으로 Microsoft SQL Server는 고객이 애플리케이션을 사용하는 방법에 대한 정보를 수집합니다. 특히, SQL Server는 설치 환경, 사용 및 성능에 대한 정보를 수집합니다. 이 정보는 Microsoft에서 고객의 요구에 맞게 제품을 향상시키는 데 도움이 됩니다. 예를 들어 Microsoft는 관련 버그를 수정하고, SQL Server 사용 방법에 대한 설명서를 개선하고, 고객에게 더 나은 서비스를 제공하기 위해 제품에 기능을 추가할지 여부를 결정할 수 있도록 고객에게 발생하는 오류 코드 종류에 대한 정보를 수집합니다.

이 문서에서는 세부 정보 수집는 보내도록 Linux의 Microsoft SQL Server를 구성 하는 방법에 대 한 어떤 종류의 정보는 수집에 대 한 정보를 Microsoft입니다. SQL Server 2017에는 수행 하 고 사용자 로부터 수집 하지 않습니다 정보를 설명 하는 개인정보취급방침 포함 됩니다. 자세한 내용은 참조는 [개인정보취급방침](https://go.microsoft.com/fwlink/?LinkID=868444)합니다.

특히 Microsoft는 이러한 메커니즘을 통해 다음과 같은 유형의 정보는 전송하지 않습니다.

- 사용자 테이블 내부의 값
- 로그온 자격 증명 또는 기타 인증 정보
- PII(개인 식별 정보)

SQL Server 2017은 고객이 경험하는 설치 문제를 빠르게 찾아 해결할 수 있도록 하기 위해 항상 설치 프로세스에서 설치 환경에 대한 정보를 수집하고 전송합니다. SQL Server 2017 (서버 인스턴스 기준) 정보를 통해 Microsoft로 보내지 않도록 구성할 수 있습니다 **mssql conf**합니다. mssql conf은 Red Hat Enterprise Linux, SUSE Linux Enterprise Server 및 Ubuntu 용 SQL Server 2017을 사용 하 여 설치 하는 구성 스크립트.

> [!NOTE]
> 유료 버전의 SQL Server에서만 Microsoft로 정보를 보내지 못하게 설정할 수 있습니다.

## <a name="disable-usage-and-diagnostic-data-collection"></a>사용량 및 진단 데이터 수집을 사용 하지 않도록 설정

이 옵션을 통해 SQL Server 사용 및 진단 데이터 수집을 보내면 Microsoft 여부를 변경할 수 있습니다. 기본적으로이 값은 설정을 true로 합니다. 값을 변경 하려면 다음 명령을 실행 합니다.

> [!IMPORTANT]
> 해제할 수 있습니다 하지 진단 데이터 수집 및 사용 현황 무료로 SQL Server, Express 및 Developer 버전입니다.

### <a name="on-red-hat-suse-and-ubuntu"></a>Red Hat, SUSE 및 Ubuntu에서

1. 사용 하 여 루트로 mssql conf 스크립트를 실행 합니다 **설정** 에 대 한 명령을 **telemetry.customerfeedback**합니다. 다음 예제에서는 해제 사용량 및 진단 데이터 수집을 지정 하 여 **false**합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>Docker에서
사용량 및 docker에서 진단 데이터 수집을 사용 하지 않으려면 Docker 있어야 [데이터를 유지](sql-server-linux-configure-docker.md)합니다. 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 추가 된 `mssql.conf` 줄을 사용 하 여 파일 `[telemetry]` 및 `customerfeedback = false` 호스트 디렉터리에서:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. 컨테이너 이미지 실행

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. 추가 된 `mssql.conf` 줄을 사용 하 여 파일 `[telemetry]` 및 `customerfeedback = false` 호스트 디렉터리에서:

   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. 컨테이너 이미지 실행

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

::: moniker-end

## <a name="local-audit-for-sql-server-on-linux-usage-and-diagnostic-data-collection"></a>SQL Server Linux 사용량 및 진단 데이터 수집에 대 한 로컬 감사

Microsoft SQL Server 2017에는 수집 하 고 컴퓨터 또는 장치 ("표준 컴퓨터 정보")에 대 한 정보를 Microsoft에 전송할 수 있는 인터넷 사용 기능이 포함 되어 있습니다. SQL Server 사용 현황 및 진단 데이터 수집의 로컬 감사 구성 요소 서비스에 의해 Microsoft로 전송 될 데이터 (로그)를 나타내는 지정 된 폴더에 수집 된 데이터를 작성할 수 있습니다. 로컬 감사의 목적은 고객들이 규정 준수 또는 개인 정보 유효성 검사의 이유로 이 기능을 사용하여 Microsoft에서 수집하는 모든 데이터를 확인하기 위함입니다.

Linux의 SQL Server에서 로컬 감사는 SQL Server 데이터베이스 엔진에 대 한 인스턴스 수준에서 구성할 수 있습니다. 다른 SQL Server 구성 요소 및 SQL Server 도구 사용 및 진단 데이터 수집에 대 한 로컬 감사 기능을 갖지 않습니다.

### <a name="enable-local-audit"></a>로컬 감사를 사용 하도록 설정

이 옵션 로컬 감사를 사용 하도록 설정 하 고 로컬 감사 로그를 생성 되는 위치에 디렉터리를 설정할 수 있습니다.

1. 새 로컬 감사 로그에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/감사** 디렉터리:

   ```bash
   sudo mkdir /tmp/audit
   ```

2. 소유자 및 디렉터리의 그룹을 변경 합니다 **mssql** 사용자:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

3. 사용 하 여 루트로 mssql conf 스크립트를 실행 합니다 **설정할** 명령에 **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

4. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>Docker에서
Docker에서 로컬 감사를 사용 하려면 Docker 있어야 [데이터를 유지](sql-server-linux-configure-docker.md)합니다. 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 새 로컬 감사 로그에 대 한 대상 디렉터리는 컨테이너에 있게 됩니다. 컴퓨터에서 호스트 디렉터리에 새 로컬 감사 로그에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/감사** 디렉터리:

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. 추가 된 `mssql.conf` 줄을 사용 하 여 파일 `[telemetry]` 및 `userrequestedlocalauditdirectory = <host directory>/audit` 호스트 디렉터리에서:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. 컨테이너 이미지 실행

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. 새 로컬 감사 로그에 대 한 대상 디렉터리는 컨테이너에 있게 됩니다. 컴퓨터에서 호스트 디렉터리에 새 로컬 감사 로그에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/감사** 디렉터리:

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. 추가 된 `mssql.conf` 줄을 사용 하 여 파일 `[telemetry]` 및 `userrequestedlocalauditdirectory = <host directory>/audit` 호스트 디렉터리에서:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. 컨테이너 이미지 실행

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

::: moniker-end

## <a name="next-steps"></a>다음 단계

Linux의 SQL Server에 대 한 자세한 내용은 참조는 [개요 SQL Server on Linux](sql-server-linux-overview.md)합니다.

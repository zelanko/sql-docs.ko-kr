---
title: SQL Server on Linux의 사용량 및 진단 데이터 수집 구성
description: Linux에서 SQL Server 고객 사용량 및 진단 데이터를 수집하고 구성하는 방법을 설명합니다.
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 96c58159a020ba11708b12a4e5732438044b3291
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115739"
---
# <a name="configure-usage--diagnostic-data-collection-for-sql-server-on-linux"></a>SQL Server on Linux의 사용량 및 진단 데이터 수집 구성

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

기본적으로 Microsoft SQL Server는 고객이 애플리케이션을 사용하는 방법에 대한 정보를 수집합니다. 특히, SQL Server는 설치 환경, 사용 및 성능에 대한 정보를 수집합니다. 이 정보는 Microsoft에서 고객의 요구에 맞게 제품을 향상시키는 데 도움이 됩니다. 예를 들어 Microsoft는 관련 버그를 수정하고, SQL Server 사용 방법에 대한 설명서를 개선하고, 고객에게 더 나은 서비스를 제공하기 위해 제품에 기능을 추가할지 여부를 결정할 수 있도록 고객에게 발생하는 오류 코드 종류에 대한 정보를 수집합니다.

이 문서에서는 수집되는 정보 종류와 수집된 정보를 Microsoft에 보내도록 Microsoft SQL Server on Linux를 구성하는 방법을 자세히 설명합니다. SQL Server 2017에는 사용자로부터 수집하는 정보와 수집하지 않는 정보를 설명하는 개인정보처리방침이 포함되어 있습니다. 자세한 내용은 [개인정보처리방침](../sql-server/sql-server-privacy.md)을 참조하세요.

특히 Microsoft는 이러한 메커니즘을 통해 다음과 같은 유형의 정보는 전송하지 않습니다.

- 사용자 테이블 내부의 값
- 로그온 자격 증명 또는 기타 인증 정보
- PII(개인 식별 정보)

SQL Server 2017은 고객이 경험하는 설치 문제를 빠르게 찾아 해결할 수 있도록 하기 위해 항상 설치 프로세스에서 설치 환경에 대한 정보를 수집하고 전송합니다. **mssql-conf**를 통해 Microsoft에 정보를 보내지 않도록 SQL Server 2017을 구성할 수 있습니다(서버 인스턴스 기준). mssql-conf는 Red Hat Enterprise Linux, SUSE Linux Enterprise Server 및 Ubuntu용 SQL Server 2017과 함께 설치되는 구성 스크립트입니다.

> [!NOTE]
> 유료 버전의 SQL Server에서만 Microsoft로 정보를 보내지 못하게 설정할 수 있습니다.

## <a name="disable-usage-and-diagnostic-data-collection"></a>사용량 및 진단 데이터 수집 사용 안 함

이 옵션을 사용하면 SQL Server에서 사용량 및 진단 데이터 컬렉션을 Microsoft로 보낼지 여부를 변경할 수 있습니다. 기본적으로 이 값은 true로 설정되어 있습니다. 값을 변경하려면 다음 명령을 실행합니다.

> [!IMPORTANT]
> SQL Server, Express 및 Developer 체험용 버전에서는 사용량 및 진단 데이터 수집을 끌 수 없습니다.

### <a name="on-red-hat-suse-and-ubuntu"></a>Red Hat, SUSE 및 Ubuntu

1. **telemetry.customerfeedback**에 대해 **set** 명령을 사용하여 mssql-conf 스크립트를 루트 권한으로 실행합니다. 다음 예제에서는 **false**를 지정하여 사용량 및 진단 데이터 수집을 끕니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. SQL Server 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>Docker
docker에서 사용량 및 진단 데이터 수집을 사용하지 않도록 설정하려면 Docker를 통해 [데이터를 유지](./sql-server-linux-docker-container-deployment.md)해야 합니다. 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 호스트 디렉터리에 `[telemetry]` 및 `customerfeedback = false` 줄이 포함된 `mssql.conf` 파일을 추가합니다.
 
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

1. 호스트 디렉터리에 `[telemetry]` 및 `customerfeedback = false` 줄이 포함된 `mssql.conf` 파일을 추가합니다.

   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. 컨테이너 이미지 실행

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

::: moniker-end

## <a name="local-audit-for-sql-server-on-linux-usage-and-diagnostic-data-collection"></a>SQL Server on Linux 사용량 및 진단 데이터 수집의 로컬 감사

Microsoft SQL Server 2017에는 컴퓨터 또는 디바이스에 대한 정보(“표준 컴퓨터 정보”)를 수집하여 Microsoft에 보낼 수 있는 인터넷 사용 기능이 포함되어 있습니다. SQL Server 사용량 및 진단 데이터 수집의 로컬 감사 구성 요소는 서비스에서 수집한 데이터를 지정된 폴더에 기록하여 Microsoft로 보낼 데이터(로그)를 나타낼 수 있습니다. 로컬 감사의 목적은 고객들이 규정 준수 또는 개인 정보 유효성 검사의 이유로 이 기능을 사용하여 Microsoft에서 수집하는 모든 데이터를 확인하기 위함입니다.

SQL Server on Linux에서 로컬 감사는 SQL Server 데이터베이스 엔진의 인스턴스 수준에서 구성할 수 있습니다. 다른 SQL Server 구성 요소 및 SQL Server 도구에는 사용량 및 진단 데이터 수집의 로컬 감사 기능이 없습니다.

### <a name="enable-local-audit"></a>로컬 감사 사용

이 옵션은 로컬 감사를 사용하도록 설정하며, 옵션에서 로컬 감사 로그가 생성되는 디렉터리를 설정할 수 있습니다.

1. 새 로컬 감사 로그의 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/audit** 디렉터리를 만듭니다.

   ```bash
   sudo mkdir /tmp/audit
   ```

2. 디렉터리의 소유자 및 그룹을 **mssql** 사용자로 변경합니다.

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

3. **telemetry.userrequestedlocalauditdirectory**에 대해 **set** 명령을 사용하여 mssql-conf 스크립트를 루트 권한으로 실행합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

4. SQL Server 서비스를 다시 시작합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>Docker
docker에서 로컬 감사를 사용하도록 설정하려면 Docker를 통해 [데이터를 유지](./sql-server-linux-docker-container-deployment.md)해야 합니다. 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 새 로컬 감사 로그의 대상 디렉터리는 컨테이너에 있습니다. 머신의 호스트 디렉터리에 새 로컬 감사 로그의 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/audit** 디렉터리를 만듭니다.

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. 호스트 디렉터리에 `[telemetry]` 및 `userrequestedlocalauditdirectory = <host directory>/audit` 줄이 포함된 `mssql.conf` 파일을 추가합니다.
 
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

1. 새 로컬 감사 로그의 대상 디렉터리는 컨테이너에 있습니다. 머신의 호스트 디렉터리에 새 로컬 감사 로그의 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/audit** 디렉터리를 만듭니다.

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. 호스트 디렉터리에 `[telemetry]` 및 `userrequestedlocalauditdirectory = <host directory>/audit` 줄이 포함된 `mssql.conf` 파일을 추가합니다.
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. 컨테이너 이미지 실행

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

::: moniker-end

## <a name="next-steps"></a>다음 단계

SQL Server on Linux에 대한 자세한 내용은 [SQL Server on Linux 개요](sql-server-linux-overview.md)를 참조하세요.
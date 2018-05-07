---
title: Linux에서 SQL Server에 대 한 고객 의견 | Microsoft Docs
description: SQL Server 사용자 의견 수집 되 고 Linux에 구성 되는 방법을 설명 합니다.
author: annashres
ms.author: anshrest
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: 278b53003fd04ccc8692b205124c85ca366f96f7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="customer-feedback-for-sql-server-on-linux"></a>Linux에서 SQL Server에 대 한 고객 의견

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

기본적으로 Microsoft SQL Server는 고객이 응용 프로그램을 사용하는 방법에 대한 정보를 수집합니다. 특히, SQL Server는 설치 환경, 사용 및 성능에 대한 정보를 수집합니다. 이 정보는 Microsoft에서 고객의 요구에 맞게 제품을 향상시키는 데 도움이 됩니다. 예를 들어 Microsoft는 관련 버그를 수정하고, SQL Server 사용 방법에 대한 설명서를 개선하고, 고객에게 더 나은 서비스를 제공하기 위해 제품에 기능을 추가할지 여부를 결정할 수 있도록 고객에게 발생하는 오류 코드 종류에 대한 정보를 수집합니다.

이 문서에서는 세부 정보는 수집를 보내도록 Linux에서 Microsoft SQL Server를 구성 하는 방법에 대 한 어떤 종류의 정보를 수집 하는 방법에 대 한 정보를 Microsoft 합니다. SQL Server 2017 수행 하 고 사용자 로부터 수집 하지 않는 정보를 설명 하는 개인정보취급방침 포함 되어 있습니다. 개인정보취급방침 읽어 보십시오.

특히 Microsoft는 이러한 메커니즘을 통해 다음과 같은 유형의 정보는 전송하지 않습니다.

- 사용자 테이블 내부의 값
- 로그온 자격 증명 또는 기타 인증 정보
- PII(개인 식별 정보)

SQL Server 2017은 고객이 경험하는 설치 문제를 빠르게 찾아 해결할 수 있도록 하기 위해 항상 설치 프로세스에서 설치 환경에 대한 정보를 수집하고 전송합니다. SQL Server 2017를 (서버 인스턴스 단위로)에 대 한 정보를 통해 보내지 않도록 구성할 수 있습니다 **mssql conf**합니다. mssql conf Red Hat Enterprise Linux, SUSE Linux Enterprise Server 및 Ubuntu에 대 한 SQL Server 2017와 함께 설치 되는 구성 스크립트입니다.

> [!NOTE]
> 유료 버전의 SQL Server에서만 Microsoft로 정보를 보내지 못하게 설정할 수 있습니다.

## <a name="disable-customer-feedback"></a>고객 의견을 사용 하지 않도록 설정

이 옵션에는 SQL Server 여부를 Microsoft로 피드백을 보내는 경우 변경할 수 있습니다. 기본적으로이 값은 설정을 true로 합니다. 값을 변경 하려면 다음 명령을 실행 합니다.

### <a name="on-red-hat-suse-and-ubuntu"></a>Ubuntu, Red Hat 및 SUSE, 등에

1. 루트 및 mssql conf 스크립트를 실행 하는 중는 **설정** 명령을 **telemetry.customerfeedback**합니다. 다음 예에서는 지정 하 여 고객 의견 해제 **false**합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>Docker에서
Docker에 고객의 의견을 사용 하지 않도록 설정 하려면 Docker 있어야 [데이터 유지](sql-server-linux-configure-docker.md)합니다. 

1. 추가 `mssql.conf` 줄이 포함 된 파일 `[telemetry]` 및 `customerfeedback = false` 호스트 디렉터리에 있습니다.
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```
2. 컨테이너 이미지를 실행 합니다.
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```
   
## <a name="local-audit-for-sql-server-on-linux-usage-feedback-collection"></a>Linux 사용 피드백 컬렉션에서 SQL Server에 대 한 로컬 감사

Microsoft SQL Server 2017 수집 하는 컴퓨터 또는 장치 ("표준 컴퓨터 정보")에 대 한 정보를 Microsoft로 보낼 수 있는 인터넷 사용 기능이 포함 되어 있습니다. SQL Server 사용 피드백 컬렉션의 로컬 감사 구성 요소를 Microsoft로 전송 되는 데이터 (로그)를 나타내는 지정 된 폴더로 서비스에 의해 수집 된 데이터를 작성할 수 있습니다. 로컬 감사의 목적은 고객들이 규정 준수 또는 개인 정보 유효성 검사의 이유로 이 기능을 사용하여 Microsoft에서 수집하는 모든 데이터를 확인하기 위함입니다.

Linux에서 SQL Server에서 로컬 감사는 SQL Server 데이터베이스 엔진에 대 한 인스턴스 수준에서 구성할 수 있습니다. 다른 SQL Server 구성 요소 및 SQL Server 도구 사용 피드백 컬렉션에 대 한 로컬 감사 기능을 갖지 않습니다.

### <a name="enable-local-audit"></a>로컬 감사를 사용 하도록 설정

이 옵션 로컬 감사를 사용 하도록 설정 하 고 로컬 감사 로그가 생성 됩니다는 디렉터리를 설정할 수 있습니다.

1. 새 로컬 감사 로그에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/감사** 디렉터리:

   ```bash
   sudo mkdir /tmp/audit
   ```

1. 소유자 및 그룹 디렉터리의 변경 된 **mssql** 사용자:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. 루트 및 mssql conf 스크립트를 실행 하는 중는 **설정** 명령을 **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. SQL Server 서비스를 다시 시작 합니다.

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>Docker에서
Docker에서 로컬 감사를 사용 하도록 설정 하려면 Docker 있어야 [데이터 유지](sql-server-linux-configure-docker.md)합니다. 

1. 새 로컬 감사 로그에 대 한 대상 디렉터리는 컨테이너에 있게 됩니다. 컴퓨터에 호스트 디렉터리에서 새 로컬 감사 로그에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **감사/** 디렉터리:

   ```bash
   sudo mkdir <host directory>/audit
   ```

   
1. 추가 `mssql.conf` 줄이 포함 된 파일 `[telemetry]` 및 `userrequestedlocalauditdirectory = <host directory>/audit` 호스트 디렉터리에 있습니다.
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```
2. 컨테이너 이미지를 실행 합니다.
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```
   
## <a name="next-steps"></a>다음 단계

Linux에서 SQL Server에 대 한 자세한 내용은 참조는 [linux 개요 SQL Server의](sql-server-linux-overview.md)합니다.

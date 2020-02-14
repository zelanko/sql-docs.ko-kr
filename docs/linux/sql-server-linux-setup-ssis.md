---
title: Linux에서 SQL Server Integration Services 설치
description: 이 문서에서는 Linux에서 SSIS(SQL Server Integration Services)를 설치하는 방법을 설명합니다.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 0f400667e73effb73ff41c3c7270e3f89a2ca0da
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76162644"
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Linux에서 SSIS(SQL Server Integration Services) 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Linux에 SQL Server Integration Services(**mssql-server-is**)를 설치하려면 이 아티클의 단계를 수행합니다. 이 Linux용 Integration Services 릴리스에서 지원되는 기능에 대한 자세한 내용은 [릴리스 정보](sql-server-linux-release-notes.md)를 참조하세요.

다음 플랫폼에 SQL Server Integration Services를 설치할 수 있습니다.

- [Ubuntu 16.04](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a> Ubuntu에서 SSIS 설치

Ubuntu에 **mssql-server-is** 패키지를 설치하려면 다음 단계를 수행합니다.

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 공용 리포지토리 GPG 키를 가져옵니다.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. SQL Server Ubuntu 리포지토리를 등록합니다.

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

1. 다음 명령을 실행하여 SQL Server Integration Services를 설치합니다.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

1. Integration Services를 설치한 후에 **ssis-conf**를 실행합니다. 자세한 내용은 [ssis-conf를 사용하여 Linux에서 SSIS 구성](sql-server-linux-configure-ssis.md)을 참조하세요.

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 구성이 완료되면 PATH 환경 변수를 설정합니다.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. 공용 리포지토리 GPG 키를 가져옵니다.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. SQL Server Ubuntu 리포지토리를 등록합니다.

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
   ```

1. 다음 명령을 실행하여 SQL Server Integration Services를 설치합니다.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

1. Integration Services를 설치한 후에 **ssis-conf**를 실행합니다. 자세한 내용은 [ssis-conf를 사용하여 Linux에서 SSIS 구성](sql-server-linux-configure-ssis.md)을 참조하세요.

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 구성이 완료되면 PATH 환경 변수를 설정합니다.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

### <a name="update-ssis"></a>SSIS 업데이트

**mssql-server-is**가 이미 설치된 경우 다음 명령을 통해 최신 버전으로 업데이트합니다.

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>SSIS 제거

**mssql-server-is**를 제거하려면 다음 명령을 실행합니다.

```bash
sudo apt-get remove mssql-server-is
```

## <a name="RHEL"></a> RHEL에서 SSIS 설치
RHEL에 **mssql-server-is** 패키지를 설치하려면 다음 단계를 수행합니다.

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. SQL Server Red Hat 리포지토리 구성 파일을 다운로드합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. 다음 명령을 실행하여 SQL Server Integration Services를 설치합니다.

   ```bash
   sudo yum install -y mssql-server-is
   ```

1. 설치 후에 **ssis-conf**를 실행합니다. 자세한 내용은 [ssis-conf를 사용하여 Linux에서 SSIS 구성](sql-server-linux-configure-ssis.md)을 참조하세요.

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 구성이 완료되면 PATH 환경 변수를 설정합니다.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. SQL Server Red Hat 리포지토리 구성 파일을 다운로드합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   ```

1. 다음 명령을 실행하여 SQL Server Integration Services를 설치합니다.

   ```bash
   sudo yum install -y mssql-server-is
   ```

1. 설치 후에 **ssis-conf**를 실행합니다. 자세한 내용은 [ssis-conf를 사용하여 Linux에서 SSIS 구성](sql-server-linux-configure-ssis.md)을 참조하세요.

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 구성이 완료되면 PATH 환경 변수를 설정합니다.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

### <a name="update-ssis"></a>SSIS 업데이트

**mssql-server-is**가 이미 설치된 경우 다음 명령을 사용하여 최신 버전으로 업데이트합니다.

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>SSIS 제거
**mssql-server-is**를 제거하려면 다음 명령을 실행합니다.

```bash
sudo yum remove mssql-server-is
```

## <a name="unattended-installation"></a>무인 설치

무인 설치로 **ssis-conf setup**을 실행하려면 다음 단계를 수행합니다.

1. **-n**(프롬프트 없음) 옵션을 지정합니다.
1. 환경 변수를 설정하여 필요한 값을 제공합니다.

아래 예제에서는 다음 작업을 수행합니다.

- SSIS 설치
- SSIS_PID 환경 변수의 값을 제공하여 Developer Edition 지정
- ACCEPT_EULA 환경 변수의 값을 제공하여 Microsoft 소프트웨어 사용 조건에 동의
- **-n**(프롬프트 없음) 옵션을 지정하여 무인 설치 실행

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>무인 설치의 환경 변수

| 환경 변수 | Description |
|---|---|
| ACCEPT_EULA | “Y” 등의 임의 값으로 설정된 경우 SQL Server 사용 조건에 동의합니다.|
| SSIS_PID | SQL Server 버전 또는 제품 키를 설정합니다. 가능한 값은 다음과 같습니다.<ul><li>평가</li><li>Developer</li><li>Express</li><li>웹</li><li>Standard</li><li>Enterprise</li><li>제품 키</li></ul>제품 키를 지정하는 경우 제품 키는 *#####* - *#####* - *#####* - *#####* - *#####* 형식이어야 합니다. 여기서 *#* 은 문자 또는 숫자입니다.  |
| | |

## <a name="next-steps"></a>다음 단계

Linux에서 SSIS 패키지를 실행하려면 [SSIS를 사용하여 SQL Server on Linux에 대한 데이터 추출, 변환 및 로드](sql-server-linux-migrate-ssis.md)를 참조하세요.

Linux에서 추가 SSIS 설정을 구성하려면 [ssis-conf를 사용하여 Linux에서 SQL Server Integration Services 구성](sql-server-linux-configure-ssis.md)을 참조하세요.

## <a name="related-content-about-ssis-on-linux"></a>Linux SSIS에 대한 관련 콘텐츠

- [SSIS를 사용하여 Linux에서 데이터 추출, 변환 및 로드](sql-server-linux-migrate-ssis.md)
- [ssis-conf를 사용하여 Linux에서 SQL Server Integration Services 구성](sql-server-linux-configure-ssis.md)
- [Linux SSIS의 제한 사항 및 알려진 문제](sql-server-linux-ssis-known-issues.md)
- [cron을 사용하여 Linux에서 SQL Server Integration Services 패키지 실행 예약](sql-server-linux-schedule-ssis-packages.md)

---
title: Linux에서 SQL Server Integration Services를 설치 합니다. | Microsoft Docs
description: 이 문서에서는 Linux에서 SQL Server Integration Services (SSIS)를 설치 하는 방법을 설명 합니다.
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 01/09/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: 79ea78bc8697c477968f2a1b7dba6e90e689b54d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Linux에서 SQL Server Integration Services (SSIS)를 설치 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server Integration Services를 설치 하려면이 문서의 단계에 따라 (`mssql-server-is`) linux. Linux 용 Integration Services의이 릴리스에서 지원 되는 기능에 대 한 정보에 대 한 참조는 [릴리스 정보](sql-server-linux-release-notes.md)합니다.

플랫폼에 대 한 SQL Server 통합 서버를 설치 합니다.

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a> Ubuntu SSIS를 설치 합니다.
설치 하는 `mssql-server-is` ubuntu 패키지에서 다음이 단계를 수행 합니다.

1. 공용 저장소 GPG 키를 가져옵니다.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Microsoft SQL Server Ubuntu 리포지토리를 등록 합니다.

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

3. SQL Server Integration Services를 설치 하려면 다음 명령을 실행 합니다.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

4. Integration Services를 설치한 후 실행 `ssis-conf`합니다. 자세한 내용은 참조 하십시오. [ssis conf와 Linux에서 SSIS 구성](sql-server-linux-configure-ssis.md)합니다.

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

5. 구성이 완료 된 후에 경로 설정 합니다.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>SSIS를 업데이트 합니다.
이미 있는 경우 `mssql-server-is` 있습니다 다음 명령 사용 하 여 최신 버전으로 업데이트할 수 설치 합니다.

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>SSIS를 제거 합니다.
제거 하려면 `mssql-server-is`, 다음 명령을 실행할 수 있습니다.
```bash
sudo apt-get remove mssql-server-is
```

## <a name="RHEL"></a> RHEL에 SSIS를 설치 합니다.
설치 하는 `mssql-server-is` RHEL에 패키지에서 다음이 단계를 수행 합니다.

1. Microsoft SQL Server Red Hat 저장소 구성 파일을 다운로드 합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. SQL Server Integration Services를 설치 하려면 다음 명령을 실행 합니다.

   ```bash
   sudo yum install -y mssql-server-is
   ```


1. 설치 후 실행 `ssis-conf`합니다. 자세한 내용은 참조 하십시오. [ssis conf와 Linux에서 SSIS 구성](sql-server-linux-configure-ssis.md)합니다.

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 구성 작업이 완료 되 면 경로 설정 합니다.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>SSIS를 업데이트 합니다.
이미 있는 경우 `mssql-server-is` 있습니다 다음 명령 사용 하 여 최신 버전으로 업데이트할 수 설치 합니다.

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>SSIS를 제거 합니다.
제거 하려면 `mssql-server-is`, 다음 명령을 실행할 수 있습니다.
```bash
sudo yum remove mssql-server-is
```

## <a name="unattended-installation"></a>무인된 설치
실행 하면 무인된 설치를 실행 하려면 `ssis-conf setup`, 다음을 수행 합니다.
1.  지정 된 `-n` (메시지 표시) 옵션입니다.
2.  환경 변수를 설정 하 여 필요한 값을 제공 합니다.

다음 예제에서는 다음 작업을 수행합니다.
-   SSIS를 설치합니다.
-   개발자 버전에 대 한 값을 제공 하 여 지정 된 `SSIS_PID` 환경 변수입니다.
-   에 대 한 값을 제공 하 여 EULA 허용는 `ACCEPT_EULA` 환경 변수입니다.
-   무인된 설치를 지정 하 여 실행 된 `-n` (메시지 표시) 옵션입니다.

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>무인된 설치에 대 한 환경 변수

| 환경 변수 | Description |
|---|---|
| **ACCEPT_EULA** | 값으로 설정 된 경우 SQL Server 사용권 계약에 동의 (예를 들어 `Y`).|
| **SSIS_PID** | SQL Server 버전 또는 제품 키를 설정합니다. 가능한 값은 다음과 같습니다.<br/>Evaluation<br/>개발자<br/>Express <br/>Web <br/>Standard<br/>Enterprise <br/>제품 키<br/><br/>제품 키 형식에서 이어야 합니다 제품 키를 지정 하는 경우 `#####-#####-#####-#####-#####`여기서 `#` 문자 또는 숫자 이면 합니다.  |
| | |

## <a name="next-steps"></a>다음 단계

SSIS 패키지에서 Linux를 실행 하려면 참조 [추출, 변환 및 SSIS와 Linux에서 SQL Server에 대 한 데이터 로드](sql-server-linux-migrate-ssis.md)합니다.

Linux에서 추가 SSIS 설정을 구성 하려면 참조 [ssis conf와 Linux에서 SQL Server Integration Services 구성](sql-server-linux-configure-ssis.md)합니다.

## <a name="related-content-about-ssis-on-linux"></a>Linux에서 SSIS에 대 한 관련된 내용
-   [추출, 변환 및 SSIS와 Linux에서 데이터 로드](sql-server-linux-migrate-ssis.md)
-   [Linux에서 SQL Server Integration Services ssis conf 구성](sql-server-linux-configure-ssis.md)
-   [Linux에서 SSIS에 대 한 알려진된 문제 및 제한](sql-server-linux-ssis-known-issues.md)
-   [일정 SQL Server Integration Services 패키지 cron 사용 하 여 Linux에서 실행](sql-server-linux-schedule-ssis-packages.md)

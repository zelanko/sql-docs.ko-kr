---
title: Linux에서 SQL Server Integration Services 설치 | Microsoft Docs
description: 이 문서에서는 Linux의 SQL Server Integration Services (SSIS)를 설치 하는 방법을 설명 합니다.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
manager: craigg
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: d581e3e238ed2d9531b725e59ef4c250d8f155c2
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66015016"
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Linux의 SQL Server Integration Services (SSIS)를 설치 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server Integration Services를 설치 하려면이 문서의 단계에 따라 (`mssql-server-is`) linux. Linux 용 Integration Services의이 릴리스에서 지 원하는 기능에 대 한 정보를 참조 하세요. 합니다 [릴리스](sql-server-linux-release-notes.md)합니다.

플랫폼에 대 한 SQL Server 통합 서버를 설치 합니다.

- [Ubuntu 16.04](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a> Ubuntu에서 SSIS를 설치 합니다.
설치 하는 `mssql-server-is` ubuntu 패키지를 다음이 단계를 수행 합니다.

1. 공용 리포지토리 GPG 키를 가져옵니다.

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

4. Integration Services를 설치한 후 실행 `ssis-conf`합니다. 자세한 내용은 참조 하세요. [conf ssis를 사용 하 여 Linux에서 SSIS 구성](sql-server-linux-configure-ssis.md)합니다.

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

5. 구성이 완료 되 면 경로 설정 합니다.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>SSIS를 업데이트 합니다.
이미 있는 경우 `mssql-server-is` 설치를 업데이트할 수 있습니다 다음 명령 사용 하 여 최신 버전으로 합니다.

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>SSIS를 제거 합니다.
제거할 `mssql-server-is`, 다음 명령을 실행할 수 있습니다.
```bash
sudo apt-get remove mssql-server-is
```

## <a name="RHEL"></a> RHEL에서 SSIS를 설치 합니다.
설치 하는 `mssql-server-is` RHEL에서 패키지를 다음이 단계를 수행 합니다.

1. Microsoft SQL Server, Red Hat 리포지토리 구성 파일을 다운로드 합니다.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. SQL Server Integration Services를 설치 하려면 다음 명령을 실행 합니다.

   ```bash
   sudo yum install -y mssql-server-is
   ```


1. 설치 후 실행 `ssis-conf`합니다. 자세한 내용은 참조 하세요. [conf ssis를 사용 하 여 Linux에서 SSIS 구성](sql-server-linux-configure-ssis.md)합니다.

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 구성이 완료 되 면 경로 설정 합니다.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>SSIS를 업데이트 합니다.
이미 있는 경우 `mssql-server-is` 설치를 업데이트할 수 있습니다 다음 명령 사용 하 여 최신 버전으로 합니다.

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>SSIS를 제거 합니다.
제거할 `mssql-server-is`, 다음 명령을 실행할 수 있습니다.
```bash
sudo yum remove mssql-server-is
```

## <a name="unattended-installation"></a>무인된 설치
실행 하면 무인된 설치를 실행 하려면 `ssis-conf setup`, 다음 작업을 수행 합니다.
1.  지정 된 `-n` (메시지 표시) 옵션입니다.
2.  환경 변수를 설정 하 여 필요한 값을 제공 합니다.

다음 예제에서는 다음 작업을 수행합니다.
-   SSIS를 설치합니다.
-   Developer edition에 대 한 값을 제공 하 여 지정 된 `SSIS_PID` 환경 변수입니다.
-   에 대 한 값을 제공 하 여 EULA를 허용 합니다 `ACCEPT_EULA` 환경 변수입니다.
-   지정 하 여 무인된 설치를 실행 합니다 `-n` (메시지 표시) 옵션입니다.

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>무인된 설치에 대 한 환경 변수

| 환경 변수 | Description |
|---|---|
| **ACCEPT_EULA** | 허용 값으로 설정 된 경우 SQL Server 사용권 계약 (예를 들어 `Y`).|
| **SSIS_PID** | SQL Server 버전 또는 제품 키를 설정합니다. 가능한 값은 다음과 같습니다.<br/>Evaluation<br/>Developer<br/>Express <br/>Web <br/>Standard<br/>Enterprise <br/>제품 키<br/><br/>제품 키 제품 키를 지정 하는 경우 폼 묶어야 `#####-#####-#####-#####-#####`여기서 `#` 문자 또는 숫자입니다.  |
| | |

## <a name="next-steps"></a>다음 단계

Linux에서 SSIS 패키지 실행을 참조 하세요 [추출, 변환 및 SSIS 사용 하 여 Linux에서 SQL Server에 대 한 데이터 로드](sql-server-linux-migrate-ssis.md)합니다.

Linux에서 추가 SSIS 설정을 구성 하려면 [conf ssis를 사용 하 여 Linux에서 SQL Server Integration Services 구성](sql-server-linux-configure-ssis.md)합니다.

## <a name="related-content-about-ssis-on-linux"></a>Linux에서 SSIS에 대 한 관련된 콘텐츠
-   [추출, 변환 및 SSIS와 Linux에서 데이터 로드](sql-server-linux-migrate-ssis.md)
-   [Conf ssis를 사용 하 여 Linux에서 SQL Server Integration Services 구성](sql-server-linux-configure-ssis.md)
-   [제한 사항 및 Linux에서 SSIS에 대 한 알려진된 문제](sql-server-linux-ssis-known-issues.md)
-   [일정 SQL Server Integration Services 패키지 cron 사용 하 여 Linux에서 실행](sql-server-linux-schedule-ssis-packages.md)

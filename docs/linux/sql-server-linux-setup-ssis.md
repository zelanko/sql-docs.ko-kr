---
title: "Linux에서 SQL Server Integration Services를 설치 합니다. | Microsoft Docs"
description: "이 항목에서는 Linux에서 SQL Server Integration Services (SSIS)를 설치 하는 방법에 설명 합니다."
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: d265d1c4fa25f10c58e321cef06cf293fdce5ac5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Linux에서 SQL Server Integration Services (SSIS)를 설치 합니다.

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server Integration Services를 설치 하려면이 문서의 단계에 따라 (`mssql-server-is`) linux. Linux 용 Integration Services의이 릴리스에서 지원 되는 기능에 대 한 정보에 대 한 참조는 [릴리스 정보](sql-server-linux-release-notes.md)합니다.

플랫폼에 대 한 SQL Server 통합 서버를 설치 합니다.

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a>Ubuntu SSIS를 설치 합니다.
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
sudo apt-get remove msssql-server-is
```

## <a name="RHEL"></a>RHEL에 SSIS를 설치 합니다.
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
sudo yum remove msssql-server-is
```




## <a name="run-a-package"></a>패키지 실행
Linux 컴퓨터에 SSIS 패키지를 복사 합니다. 다음 명령을 사용 하 여 다음 패키지를 실행 합니다.

```bash
dtexec /F <package name> /DE <protection password>
```



## <a name="next-steps"></a>다음 단계

Linux에서 SSIS를 사용 하 여를 추출, 변환 및 데이터를 로드 하는 방법에 대 한 자세한 내용은 참조 [추출, 변환 및 SSIS와 Linux에서 SQL Server에 대 한 데이터를 로드](sql-server-linux-migrate-ssis.md)합니다.

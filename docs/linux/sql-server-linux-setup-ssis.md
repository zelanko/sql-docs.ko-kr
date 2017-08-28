---
title: "Linux에서 SQL Server Integration Services를 설치 합니다. | Microsoft Docs"
description: "이 항목에서는 Linux에서 SQL Server Integration Services를 설치 하는 방법에 설명 합니다."
author: leolimsft
ms.author: lle
manager: craigg
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: integration-services
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c3943870ec10b8430ac4819398908c5459a8b03c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Linux에서 SQL Server Integration Services (SSIS)를 설치 합니다.

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server Integration Services를 설치 하려면이 문서의 단계에 따라 (`mssql-server-is`) linux. Linux 용 Integration Services의이 릴리스에서 지원 되는 기능에 대 한 정보에 대 한 참조는 [릴리스 정보](sql-server-linux-release-notes.md)합니다.

플랫폼에 대 한 SQL Server 통합 서버를 설치 합니다.

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)



## <a name="ubuntu"></a>Ubuntu SSIS를 설치 합니다.
설치 하는 `mssql-server-is` ubuntu 패키지에서 다음이 단계를 수행 합니다.


1.  공용 저장소 GPG 키를 가져옵니다.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add –
    ```


2.  Microsoft SQL Server Ubuntu 리포지토리를 등록 합니다.

    ```bash
    curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server.list | sudo tee /etc/apt/sources.list.d/mssql-server.list
    ```


3.  SQL Server Integration Services를 설치 하려면 다음 명령을 실행 합니다.

    ```bash
    sudo apt-get update
    sudo apt-get install -y mssql-server-is
    ```


4.  Integration Services를 설치한 후 실행 `ssis-conf`합니다.

    ```bash
    sudo /opt/ssis/bin/ssis-conf setup
    ```


5.  구성이 완료 된 후에 경로 설정 합니다.

    ```bash
    export PATH=/opt/ssis/bin:$PATH
    ```


이미 있는 경우 `mssql-server-is` 있습니다 다음 명령 사용 하 여 최신 버전으로 업데이트할 수 설치 합니다.

```bash
sudo apt-get install mssql-server-is
```


제거 하려면 `mssql-server-is`, 다음 명령을 실행할 수 있습니다.
```bash
sudo apt-get remove msssql-server-is
```



## <a name="RHEL"></a>RHEL에 SSIS를 설치 합니다.
설치 하는 `mssql-server-is` RHEL에 패키지에서 다음이 단계를 수행 합니다.


1.  Superuser 모드를 입력 합니다.

    ```bash
    sudo su
    ```


2.  Microsoft SQL Server Red Hat 저장소 구성 파일을 다운로드 합니다.

    ```bash
    curl https://packages.microsoft.com/config/rhel/7/mssql-server.repo > /etc/yum.repos.d/mssql-server.repo
    ```


3.  Superuser 모드를 종료 합니다.

    ```bash
    exit
    ```


4.  SQL Server Integration Services를 설치 하려면 다음 명령을 실행 합니다.

    ```bash
    sudo yum install -y mssql-server-is
    ```


5.  설치 후 실행 하십시오 `ssis-conf`합니다.

    ```bash
    sudo /opt/ssis/bin/ssis-conf setup
    ```


6.  구성 작업이 완료 되 면 경로 설정 합니다.

    ```bash
    export PATH=/opt/ssis/bin:$PATH
    ```


이미 있는 경우 `mssql-server-is` 있습니다 다음 명령 사용 하 여 최신 버전으로 업데이트할 수 설치 합니다.

```bash
sudo yum update mssql-server-is
```


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

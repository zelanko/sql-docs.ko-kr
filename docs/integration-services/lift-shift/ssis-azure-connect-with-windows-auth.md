---
title: Windows 인증으로 데이터 및 파일 공유에 연결 | Microsoft Docs
description: Windows 인증을 사용하여 데이터 원본과 파일 공유에 연결하는 패키지를 실행하도록 Azure SQL Database에 SSIS 카탈로그를 구성하는 방법을 알아봅니다.
ms.date: 02/05/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.suite: sql
ms.custom: ''
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cca5deecf90fbbe28399d33ac2038bc2264b1ae6
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35332687"
---
# <a name="connect-to-data-sources-and-file-shares-with-windows-authentication-in-ssis-packages-in-azure"></a>Azure의 SSIS 패키지에서 Windows 인증으로 데이터 원본 및 파일 공유에 연결

이 문서에서는 Windows 인증을 사용하여 데이터 원본과 파일 공유에 연결하는 패키지를 실행하도록 Azure SQL Database에 SSIS 카탈로그를 구성하는 방법을 설명합니다. Windows 인증을 사용하여 Azure 가상 머신에서 온-프레미스 및 Azure Files의 Azure SSIS Integration Runtime과 동일한 가상 네트워크에 있는 데이터 원본에 연결할 수 있습니다.

> [!WARNING]
> 이 문서에 설명된 대로 `catalog`.`set_execution_credential`을 실행하여 Windows 인증에 유효한 도메인 자격 증명을 제공하지 않으면 Windows 인증에 종속된 패키지가 데이터 원본에 연결할 수 없으며 런타임에 실패합니다.

## <a name="you-can-only-use-one-set-of-credentials"></a>자격 증명 집합을 하나만 사용 가능

지금은 패키지의 자격 증명 집합을 하나만 사용할 수 있습니다. 이 문서의 단계를 수행할 때 제공하는 도메인 자격 증명은 자격 증명을 변경하거나 제거할 때까지 SQL Database 인스턴스에서 모든 패키지 실행(대화형 또는 예약된 실행)에 적용됩니다. 여러 자격 증명 집합을 사용하여 패키지를 여러 데이터 원본에 연결해야 하는 경우 패키지를 여러 패키지로 분리해야 할 수도 있습니다.

데이터 원본 중 하나가 Azure 파일인 경우 패키지를 실행할 때 프로세스 실행 태스크에서 `net use` 또는 동일 기능을 사용하여 Azure 파일 공유를 탑재하면 이 제한을 해결할 수 있습니다. 자세한 내용은 [Azure 파일 공유를 탑재하고 Windows에서 공유 액세스](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows)를 참조하세요.

## <a name="provide-domain-credentials-for-windows-authentication"></a>Windows 인증에 대한 도메인 자격 증명 제공
패키지에서 Windows 인증을 사용하여 온-프레미스 데이터 원본에 연결할 수 있는 도메인 자격 증명을 제공하려면 다음을 수행합니다.

1.  SSMS(SQL Server Management Studio) 또는 다른 도구를 사용하여 SSISDB(SSIS Catalog database)를 호스트하는 SQL Database에 연결합니다. 자세한 내용은 [Azure에서 SSIS 카탈로그(SSISDB)에 연결](ssis-azure-connect-to-catalog-database.md)을 참조하세요.

2.  SSISDB를 현재 데이터베이스로 사용하여 쿼리 창을 엽니다.

3.  다음 저장 프로시저를 실행하고 적절한 도메인 자격 증명을 제공합니다.

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```

4.  SSIS 패키지를 실행합니다. 패키지는 Windows 인증을 사용하여 온-프레미스 데이터 원본에 연결하기 위해 제공한 자격 증명을 사용합니다.

### <a name="view-domain-credentials"></a>도메인 자격 증명 보기
활성 도메인 자격 증명을 보려면 다음을 수행합니다.

1.  SSMS(SQL Server Management Studio) 또는 다른 도구를 사용하여 SSISDB(SSIS Catalog database)를 호스트하는 SQL Database에 연결합니다.

2.  SSISDB를 현재 데이터베이스로 사용하여 쿼리 창을 엽니다.

3.  다음 저장 프로시저를 실행하고 출력을 확인합니다.

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

### <a name="clear-domain-credentials"></a>도메인 자격 증명 지우기
이 문서의 설명에 따라 제공한 자격 증명을 지우고 제거하려면 다음을 수행합니다.

1.  SSMS(SQL Server Management Studio) 또는 다른 도구를 사용하여 SSISDB(SSIS Catalog database)를 호스트하는 SQL Database에 연결합니다.

2.  SSISDB를 현재 데이터베이스로 사용하여 쿼리 창을 엽니다.

3.  다음 저장 프로시저를 실행합니다.

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="connect-to-an-on-premises-sql-server"></a>온-프레미스 SQL Server에 연결
온-프레미스 SQL Server에 연결할 수 있는지 확인하려면 다음을 수행합니다.

1.  이 테스트를 실행하려면 도메인에 가입되지 않은 컴퓨터를 찾습니다.

2.  도메인에 가입하지 않은 컴퓨터에서 다음 명령을 실행하여, 사용할 도메인 자격 증명으로 SSMS(SQL Server Management Studio)를 시작합니다.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  SSMS에서 사용할 온-프레미스 SQL Server에 연결할 수 있는지 확인합니다.

### <a name="prerequisites"></a>사전 요구 사항
Azure에서 실행 중인 패키지에서 온-프레미스 SQL Server에 연결하려면 다음과 같은 사전 요구 사항을 구현해야 합니다.

1.  SQL Server 구성 관리자에서 TCP/IP 프로토콜을 설정합니다.
2.  Windows 방화벽을 통한 액세스를 허용합니다. 자세한 내용은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](https://docs.microsoft.com/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access)을 참조하세요.
3.  Windows 인증을 사용하여 연결하려면 Azure-SSIS Integration Runtime이 온-프레미스 SQL Server가 포함되어 있는 가상 네트워크에 속해 있어야 합니다.  자세한 내용은 [Azure SSIS 통합 런타임을 가상 네트워크에 조인](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network)을 참조하세요. 그런 다음 이 아티클에 설명된 대로 `catalog.set_execution_credential`을 사용하여 자격 증명을 제공합니다.

## <a name="connect-to-an-on-premises-file-share"></a>온-프레미스 파일 공유에 연결
온-프레미스 파일 공유에 연결할 수 있는지 확인하려면 다음을 수행합니다.

1.  이 테스트를 실행하려면 도메인에 가입되지 않은 컴퓨터를 찾습니다.

2.  도메인에 가입하지 않은 컴퓨터에서 다음 명령을 실행합니다. 이 명령은 사용할 도메인 자격 증명이 있는 명령 프롬프트 창을 연 다음 디렉터리 목록을 가져 와서 파일 공유에 대한 연결을 테스트합니다.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  사용할 온-프레미스 파일 공유에 대한 디렉터리 목록이 반환되는지 확인합니다.

## <a name="connect-to-a-file-share-on-an-azure-vm"></a>Azure VM의 파일 공유에 연결
Azure 가상 머신의 파일 공유에 연결하려면 다음을 수행합니다.

1.  SSMS(SQL Server Management Studio) 또는 다른 도구를 사용하여 SSISDB(SSIS Catalog database)를 호스트하는 SQL Database에 연결합니다.

2.  SSISDB를 현재 데이터베이스로 사용하여 쿼리 창을 엽니다.

3.  다음 옵션의 설명에 따라 `catalog.set_execution_credential` 저장 프로시저를 실행합니다.

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

## <a name="connect-to-a-file-share-in-azure-files"></a>Azure 파일의 파일 공유에 연결
Azure Files에 대한 자세한 내용은 [Azure Files](https://azure.microsoft.com/services/storage/files/)를 참조하세요.

Azure 파일 공유의 파일 공유에 연결하려면 다음을 수행합니다.

1.  SSMS(SQL Server Management Studio) 또는 다른 도구를 사용하여 SSISDB(SSIS Catalog database)를 호스트하는 SQL Database에 연결합니다.

2.  SSISDB를 현재 데이터베이스로 사용하여 쿼리 창을 엽니다.

3.  다음 옵션의 설명에 따라 `catalog.set_execution_credential` 저장 프로시저를 실행합니다.

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>다음 단계
- 패키지를 배포합니다. 자세한 내용은 [SSMS(SQL Server Management Studio)를 사용하여 SSIS 프로젝트 배포](../ssis-quickstart-deploy-ssms.md)를 참조하세요.
- 패키지를 실행합니다. 자세한 내용은 [SSMS(SQL Server Management Studio)를 사용하여 SSIS 패키지 실행](../ssis-quickstart-run-ssms.md)을 참조하세요.
- 패키지를 예약합니다. 자세한 내용은 [Azure에서 SSIS 패키지 예약](ssis-azure-schedule-packages.md)을 참조하세요.

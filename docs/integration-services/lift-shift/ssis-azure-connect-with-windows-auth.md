---
title: "Windows 인증으로 온-프레미스 데이터 원본 및 Azure 파일 공유에 연결 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9235ffd3225e76ee94067519c72e997c451d9893
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authentication"></a>Windows 인증으로 온-프레미스 데이터 원본 및 Azure 파일 공유에 연결
이 문서에서는 Windows 인증을 사용하여 온-프레미스 데이터 원본과 Azure 파일 공유에 연결하는 패키지를 실행하도록 Azure SQL Database에 SSIS 카탈로그를 구성하는 방법을 설명합니다.

이 문서의 단계를 수행할 때 제공하는 도메인 자격 증명은 자격 증명을 변경하거나 제거할 때까지 SQL Database 인스턴스에서 모든 패키지 실행에 적용됩니다.

## <a name="connect-to-on-premises-data-sources"></a>온-프레미스 데이터 원본에 연결

### <a name="prerequisite"></a>필수 구성 요소
Windows 인증에 대한 도메인 자격 증명을 설정하기 전에 도메인에 가입되지 않은 컴퓨터가 `runas` 모드에서 온-프레미스 데이터 원본에 연결할 수 있는지 확인합니다.

#### <a name="connecting-to-sql-server"></a>SQL Server에 연결
온-프레미스 SQL Server에 연결할 수 있는지 확인하려면 다음을 수행합니다.

1.  이 테스트를 실행하려면 도메인에 가입되지 않은 컴퓨터를 찾습니다.

2.  도메인에 가입하지 않은 컴퓨터에서 다음 명령을 실행하여, 사용할 도메인 자격 증명으로 SSMS(SQL Server Management Studio)를 시작합니다.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  SSMS에서 사용할 온-프레미스 SQL Server에 연결할 수 있는지 확인합니다.

#### <a name="connecting-to-a-file-share"></a>파일 공유에 연결
온-프레미스 파일 공유에 연결할 수 있는지 확인하려면 다음을 수행합니다.

1.  이 테스트를 실행하려면 도메인에 가입되지 않은 컴퓨터를 찾습니다.

2.  도메인에 가입하지 않은 컴퓨터에서 다음 명령을 실행합니다. 이 명령은 사용할 도메인 자격 증명이 있는 명령 프롬프트 창을 연 다음 디렉터리 목록을 가져 와서 파일 공유에 대한 연결을 테스트합니다.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  사용할 온-프레미스 파일 공유에 대한 디렉터리 목록이 반환되는지 확인합니다.

### <a name="provide-domain-credentials"></a>도메인 자격 증명 제공
패키지에서 Windows 인증을 사용하여 온-프레미스 데이터 원본에 연결할 수 있는 도메인 자격 증명을 제공하려면 다음을 수행합니다.

1.  SSMS(SQL Server Management Studio) 또는 다른 도구를 사용하여 SSISDB(SSIS Catalog database)를 호스트하는 SQL Database에 연결합니다. 자세한 내용은 [Azure에서 SSISDB 카탈로그 데이터베이스에 연결](ssis-azure-connect-to-catalog-database.md)을 참조하세요.

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

## <a name="connect-to-file-shares"></a>파일 공유에 연결
Windows 인증을 사용하여 온-프레미스 및 Azure 가상 머신과 Azure Files의 Azure SSIS Integration Runtime과 동일한 가상 네트워크에 있는 파일 공유에 연결할 수 있습니다. Azure Files에 대한 자세한 내용은 [Azure Files](https://azure.microsoft.com/services/storage/files/)를 참조하세요.

Azure 가상 머신 또는 Azure 파일 공유의 파일 공유에 연결하려면 다음을 수행합니다.

1.  SSMS(SQL Server Management Studio) 또는 다른 도구를 사용하여 SSISDB(SSIS Catalog database)를 호스트하는 SQL Database에 연결합니다.

2.  SSISDB를 현재 데이터베이스로 사용하여 쿼리 창을 엽니다.

3.  다음 옵션의 설명에 따라 `catalog.set_execution_credential` 저장 프로시저를 실행합니다.

    a.  Azure 가상 머신의 파일 공유에 연결하려면 다음을 수행합니다.

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

    b.  Azure 파일 공유(즉, Azure Files에 있는)에 연결하려면 다음 저장 프로시저를 실행합니다.

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>다음 단계
- 패키지를 배포합니다. 자세한 내용은 [SSMS(SQL Server Management Studio)를 사용하여 SSIS 프로젝트 배포](../ssis-quickstart-deploy-ssms.md)를 참조하세요.
- 패키지를 실행합니다. 자세한 내용은 [SSMS(SQL Server Management Studio)를 사용하여 SSIS 패키지 실행](../ssis-quickstart-run-ssms.md)을 참조하세요.
- 패키지를 예약합니다. 자세한 내용은 [Azure에서 SSIS 패키지 실행 예약](ssis-azure-schedule-packages.md)을 참조하세요.

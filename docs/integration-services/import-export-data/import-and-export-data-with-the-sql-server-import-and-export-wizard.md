---
title: "SQL Server 가져오기 및 내보내기 마법사와 데이터 내보내기 및 가져오기 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- exporting data
- mapping files [Integration Services]
- SQL Server Import and Export Wizard
- SSIS packages, creating
- packages [Integration Services], copying
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
- Import and Export Wizard
- copying data [Integration Services]
- importing data, SSIS packages
- sources [Integration Services], copying data
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
caps.latest.revision: 160
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 59c7e1cc3c31f77652acb21d375e1294bdc93397
ms.openlocfilehash: 22419ce21476588f4ff2859185c8b833306fa896
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="import-and-export-data-with-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기

 > 이전 버전의 SQL Server와 관련 된 콘텐츠를 참조 하십시오. [SQL Server 가져오기 및 내보내기 마법사](https://msdn.microsoft.com/en-US/library/ms140052(SQL.120).aspx)합니다.

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사는 원본에서 대상으로 데이터를 복사하는 간단한 방법입니다. 이 개요에서는으로 마법사는 원본 및 대상으로 사용할 수 있는 데이터 원본 마법사를 실행 하려면 필요한 사용 권한을 설명 합니다.

## <a name="get-the-wizard"></a>가져오기 마법사
마법사를 실행하려고 하지만 컴퓨터에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치되지 않은 경우 SSDT(SQL Server Data Tools)를 설치하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 설치할 수 있습니다. 자세한 내용은 [SSDT(SQL Server Data Tools) 다운로드](https://msdn.microsoft.com/library/mt204009.aspx)를 참조하세요.

## <a name="what-happens-when-i-run-the-wizard"></a>마법사를 실행할 때 어떻게 될까요?
-    **단계 목록을 참조 하십시오.** 마법사의 단계에 대 한 참조 [SQL Server 가져오기 및 내보내기 마법사의 단계를](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)합니다. 마법사의 각 페이지에 대 한 설명서의 개별 페이지 이기도합니다.  
    \-또는\-
-   **간단한 예를 참조 하십시오.** 일반적인 세션에서 여러 화면을 빠르게 확인에 대 한 살펴보세요이 간단한 종단 간 예제를 한 페이지- [가져오기 및 내보내기 마법사의이 간단한 예제 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)합니다.  

##  <a name="wizardSources"></a>어떤 원본 및 대상을 사용할 수 있습니까?  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사는 다음 표에 나열 된 데이터 원본에서 데이터를 복사할 수 있습니다. 이러한 데이터 원본 중 일부에 연결할를 다운로드 하 여 추가 파일을 설치 해야 합니다.
 
| 데이터 원본 | 추가 파일을 다운로드해야 하나요? |
|-------------|-----------------------------------------|
|**엔터프라이즈 데이터베이스**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Oracle, DB2, 등입니다.|SQL Server 또는 SQL Server Data Tools (SSDT)에 연결 해야 하는 파일을 설치 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 하지만 SSDT Oracle 또는 IBM DB2 등 다른 엔터프라이즈 데이터베이스에 연결 해야 하는 모든 파일을 설치 하지는 않습니다.<br/><br/>일반적으로 엔터프라이즈 데이터베이스에 연결 하려면 다음 두 가지 해야 할:<br/><br/>1. **클라이언트 소프트웨어**합니다. 엔터프라이즈 데이터베이스 시스템용으로 클라이언트 소프트웨어가 이미 설치된 경우 일반적으로 연결해야 합니다. 클라이언트 소프트웨어를 설치하지 않은 경우 데이터베이스 관리자에게 사용이 허가된 복사본 설치 방법을 문의하세요.<br/><br/>2. **공급자 또는 드라이버**합니다. Microsoft은 Oracle에 연결 하는 공급자 및 드라이버를 설치 합니다. 를 IBM d b 2에 연결 하려면 Microsoft® OLEDB Provider for DB2 v 5.0에서 Microsoft SQL Server에 대 한 가져오기는 [Microsoft SQL Server 2016 기능 팩](https://www.microsoft.com/download/details.aspx?id=52676)합니다.|
|**텍스트 파일** (플랫 파일)|추가 파일이 필요 없습니다.|
|**Microsoft Excel 및 Microsoft Access 파일**|Microsoft Office는 데이터 원본으로 Excel 및 Access 파일에 연결해야 하는 모든 파일을 설치하지 않습니다. 다음 다운로드-가져오기 [Microsoft Access 데이터베이스 엔진 2016 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=54920)합니다.<br/><br/>자세한 내용은 참조 하십시오. [Excel 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md) 또는 [Access 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)합니다.|
|**Azure 데이터 원본**<br/>현재 Azure Blob Storage만 해당합니다.|SQL Server Data Tools는 데이터 원본으로 Azure Blob 저장소에 연결 해야 하는 파일을 설치 하지 마세요. 다운로드 [Azure용 Microsoft SQL Server 2016 Integration Services Feature Pack](https://www.microsoft.com/download/details.aspx?id=49492)을 가져옵니다.<br/><br/>자세한 내용은 참조 하십시오. [Azure 블로그 저장소에 연결](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)합니다.|
|**오픈 소스 데이터베이스**<br/>PostgreSQL, MySql, 등입니다.|이러한 데이터 원본에 연결할 추가 파일을 다운로드해야 합니다.<br/><br/>- **PostgreSQL**, 참조 [PostgreSQL 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)합니다.<br/>- **MySql**, 참조 [MySQL 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)합니다.|
|**다른 데이터 소스를 드라이버 또는 공급자를 사용할 수**|일반적으로 다음 데이터 원본에 연결할 추가 파일을 다운로드해야 합니다.<br/><br/>- **ODBC 드라이버** 를 사용할 수 있는 모든 원본 자세한 내용은 참조 하십시오. [ODBC 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)합니다.<br/>- **.Net Framework 데이터 공급자** 를 사용할 수 있는 모든 원본<br/>- **OLE DB 공급자** 를 사용할 수 있는 모든 원본<br/><br/>다른 데이터 원본에 대 한 원본 및 대상 기능을 제공 하는 타사 구성 요소는 경우에 따라 판매 되 플랫폼 추가 기능 제품으로 SQL Server Integration Services (SSIS)에 대 한 합니다.|

## <a name="how-do-i-connect-to-my-data"></a>내 데이터에 연결 어떻게 합니까?
자주 사용 되는 데이터 원본에 연결 하는 방법에 대 한 내용은 다음 페이지 중 하나를 참조 합니다.
-   [SQL Server에 연결](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Oracle에 연결](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [플랫 파일 (텍스트 파일)에 연결](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Excel에 연결](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Access에 연결](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Azure Blob 저장소에 연결](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [ODBC를 사용 하 여 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [PostgreSQL에 연결](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [MySQL에 연결](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)


여기에 나열 되어 있지 않은 데이터 원본에 연결 하는 방법에 대 한 정보를 참조 하십시오. [연결 문자열 Reference](https://www.connectionstrings.com/)합니다. 이 다른 공급 업체 사이트 샘플 연결 문자열 및 데이터 공급자에 대 한 자세한 내용 및 필요한 연결 정보를 포함 합니다.

## <a name="what-permissions-do-i-need"></a>어떤 권한이 필요 합니까?  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 성공적으로 실행하려면 적어도 다음 권한이 있어야 합니다. 현재 데이터 원본과 대상으로 작업하는 경우 이미 필요한 권한이 있을 수 있습니다.
  
|수행할 작업|이러한 특정 사용 권한이 필요한 SQL Server에 연결 하는 경우 |  
|-------------------------|----------------------------------------------------|  
|원본 및 대상 데이터베이스나 파일 공유에 연결합니다.|서버 및 데이터베이스 로그인 권한|  
|원본 데이터베이스 또는 파일에서 데이터 내보내기 또는 읽기|원본 테이블 및 뷰에 대한 SELECT 권한|  
|대상 데이터베이스 또는 파일에 데이터 가져오기 또는 쓰기|대상 테이블에 대한 INSERT 권한|  
|대상 데이터베이스 또는 파일 만들기(해당하는 경우)|CREATE DATABASE 또는 CREATE TABLE 권한|  
|마법사가 만든 SSIS 패키지(해당하는 경우)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 패키지를 저장하려는 경우 **msdb** 데이터베이스에 패키지를 저장할 수 있는 권한|  
  
## <a name="get-help-while-the-wizard-is-running"></a>마법사를 실행하는 동안 도움말 보기
> [!TIP]
> 마법사의 모든 페이지 또는 대화 상자에서 F1 키를 누르면 현재 페이지에 대한 설명서를 볼 수 있습니다.   
  
##  <a name="wizardSSIS"></a> 마법사에서 SSIS(SQL Server Integration Services) 사용  
 마법사에서는 SSIS(SQL Server Integration Services)를 사용하여 데이터를 복사합니다. SSIS는 데이터를 ETL(추출, 변환 및 로드)하는 도구입니다. 마법사 페이지에서는 SSIS 언어 일부를 사용합니다.
  
 SSIS에서 기본 단위는 **패키지**입니다. 마법사는 사용자가 마법사 페이지를 진행하고 옵션을 지정하면 메모리 내에 SSIS 패키지를 만듭니다.    
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition 이상이 설치된 경우 마법사의 마지막 단계에서 필요에 따라 SSIS 패키지를 저장할 수 있습니다. 나중에 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하여 패키지를 다시 실행하고 태스크, 변환 및 이벤트 기반 논리를 추가하여 패키지를 확장할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사는 원본의 데이터를 대상으로 복사하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 만드는 가장 간단한 방법을 제공합니다.

SSIS에 대한 자세한 내용은 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)를 참조하세요.

## <a name="whats-next"></a>다음 단계  
 마법사를 시작합니다. 자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)을 참조하세요.  

## <a name="see-also"></a>참고 항목
[가져오기 및 내보내기 마법사의 이 간단한 예제로 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[SQL Server 가져오기 및 내보내기 마법사에서 데이터 형식 매핑](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)




---
title: SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기 | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f3327f4026d7830c28e6651ff596741093146d95
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782193"
---
# <a name="import-and-export-data-with-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기

 > 이전 버전의 SQL Server와 관련된 내용은 [SQL Server 가져오기 및 내보내기 마법사 실행](start-the-sql-server-import-and-export-wizard.md)을 참조하세요.

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사는 원본에서 대상으로 데이터를 복사하는 간단한 방법입니다. 이 개요에서는 마법사에서 원본 및 대상으로 사용할 수 있는 데이터 원본과 마법사를 실행하는 데 필요한 권한에 대해 설명합니다.

## <a name="get-the-wizard"></a>마법사 가져오기
마법사를 실행하려고 하지만 컴퓨터에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치되지 않은 경우 SSDT(SQL Server Data Tools)를 설치하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 설치할 수 있습니다. 자세한 내용은 [SSDT(SQL Server Data Tools) 다운로드](https://msdn.microsoft.com/library/mt204009.aspx)를 참조하세요.

## <a name="what-happens-when-i-run-the-wizard"></a>마법사를 실행하면 어떻게 될까요?
-    **단계 목록을 참조하세요.** 마법사의 단계에 대한 설명은 [SQL Server 가져오기 및 내보내기 마법사의 단계](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)를 참조하세요. 또한 마법사의 각 페이지마다 별도의 설명서 페이지가 있습니다.  
    \- 또는 \-
-   **예제를 참조하세요.** 일반적인 세션에서 볼 수 있는 몇 가지 화면을 간략히 보려면 [가져오기 및 내보내기 마법사의 간단한 예제 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md) 단일 페이지에 있는 간단한 예제를 살펴봅니다.  

##  <a name="wizardSources"></a> 어떤 원본 및 대상을 사용할 수 있나요?  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사는 다음 표에 나와 있는 데이터 원본 간에 데이터를 복사할 수 있습니다. 이러한 데이터 원본 중 일부에 연결하려면 추가 파일을 다운로드하여 설치해야 합니다.
 
| 데이터 원본 | 추가 파일을 다운로드해야 하나요? |
|-------------|-----------------------------------------|
|**엔터프라이즈 데이터베이스**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, DB2 및 기타|SQL Server 또는 SSDT(SQL Server Data Tools)는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하는 데 필요한 파일을 설치합니다. 그러나 SSDT는 Oracle 또는 IBM DB2와 같은 다른 엔터프라이즈 데이터베이스에 연결하는 데 필요한 모든 파일을 설치하지 않습니다.<br/><br/>엔터프라이즈 데이터베이스에 연결하려면 일반적으로 다음 두 가지 항목이 있어야 합니다.<br/><br/>1. **클라이언트 소프트웨어** - 엔터프라이즈 데이터베이스 시스템용으로 클라이언트 소프트웨어가 이미 설치된 경우 일반적으로 연결해야 합니다. 클라이언트 소프트웨어를 설치하지 않은 경우 데이터베이스 관리자에게 사용이 허가된 복사본 설치 방법을 문의하세요.<br/><br/>2. **드라이버 또는 공급자** - Microsoft는 Oracle에 연결할 드라이버와 공급자를 설치합니다. IBM DB2에 연결하려면 [Microsoft SQL Server 2016 Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676)에서 Microsoft SQL Server용 Microsoft® OLEDB Provider for DB2 v5.0을 가져옵니다.<br/><br/>자세한 내용은 [SQL Server 데이터 원본에 연결](connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md) 또는 [Oracle 데이터 원본에 연결](connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)을 참조하세요.|
|**텍스트 파일**(플랫 파일)|추가 파일이 필요 없습니다.<br/><br/>자세한 내용은 [플랫 파일 데이터 원본에 연결](connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)을 참조하세요.|
|**Microsoft Excel 및 Microsoft Access 파일**|Microsoft Office는 데이터 원본으로 Excel 및 Access 파일에 연결해야 하는 모든 파일을 설치하지 않습니다. [Microsoft Access 데이터베이스 엔진 2016 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=54920) 다운로드를 가져옵니다.<br/><br/>자세한 내용은 [Excel 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md) 또는 [Access 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)을 참조하세요.|
|**Azure 데이터 원본**<br/>현재 Azure Blob Storage만 해당합니다.|SQL Server Data Tools는 Azure Blob Storage에 연결하는 데 필요한 파일을 데이터 원본으로 설치하지 않습니다. 다운로드 [Azure용 Microsoft SQL Server 2016 Integration Services Feature Pack](https://www.microsoft.com/download/details.aspx?id=49492)을 가져옵니다.<br/><br/>자세한 내용은 [Azure Blob Storage에 연결](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)을 참조하세요.|
|**오픈 소스 데이터베이스**<br/>PostgreSQL, MySQL 및 기타|이러한 데이터 원본에 연결하려면 추가 파일을 다운로드해야 합니다.<br/><br/>- **PostgreSQL**의 경우 [PostgreSQL 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)을 참조하세요.<br/>- **MySQL**의 경우 [MySQL 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)을 참조하세요.|
|**드라이버 또는 공급자를 사용할 수 있는 기타 모든 데이터 원본**|일반적으로 다음 데이터 원본에 연결할 추가 파일을 다운로드해야 합니다.<br/><br/>- **ODBC 드라이버** 를 사용할 수 있는 모든 원본 자세한 내용은 [ODBC 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)을 참조하세요.<br/>- **.Net Framework 데이터 공급자** 를 사용할 수 있는 모든 원본<br/>- **OLE DB 공급자** 를 사용할 수 있는 모든 원본<br/><br/>다른 데이터 원본에 대한 원본 및 대상 기능을 제공하는 타사 구성 요소는 SSIS(SQL Server Integration Services)용 추가 기능 제품으로 판매되는 경우가 있습니다.|

## <a name="how-do-i-connect-to-my-data"></a>내 데이터에 연결하려면 어떻게 할까요?
일반적으로 사용되는 데이터 원본에 연결하는 방법에 대한 자세한 내용은 다음 페이지 중 하나를 참조하세요.
-   [SQL Server에 연결](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Oracle에 연결](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [플랫 파일(텍스트 파일)에 연결](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Excel에 연결](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Access에 연결](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Azure Blob Storage에 연결](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [ODBC를 사용하여 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [PostgreSQL에 연결](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [MySQL에 연결](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)


여기에 나열되지 않은 데이터 원본에 연결하는 방법에 대한 자세한 내용은 [연결 문자열 참조](https://www.connectionstrings.com/)를 참조하세요. 이 타사 사이트에는 샘플 연결 문자열과 필요한 데이터 공급자 및 연결 정보에 대한 추가 정보가 포함되어 있습니다.

## <a name="what-permissions-do-i-need"></a>어떤 권한이 필요한가요?  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 성공적으로 실행하려면 적어도 다음 권한이 있어야 합니다. 현재 데이터 원본과 대상으로 작업하는 경우 이미 필요한 권한이 있을 수 있습니다.
  
|수행할 작업|SQL Server에 연결하는 경우 필요한 특정 권한 |  
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

## <a name="see-also"></a>관련 항목:
[가져오기 및 내보내기 마법사의 이 간단한 예제로 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[SQL Server 가져오기 및 내보내기 마법사에서 데이터 형식 매핑](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)



---
title: "SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "데이터 내보내기"
  - "매핑 파일 [Integration Services]"
  - "SQL Server 가져오기 및 내보내기 마법사"
  - "SSIS 패키지, 만들기"
  - "패키지 [Integration Services], 복사"
  - "Integration Services 패키지, 만들기"
  - "패키지 [Integration Services], 만들기"
  - "SQL Server Integration Services 패키지, 만들기"
  - "가져오기 및 내보내기 마법사"
  - "데이터 복사 [Integration Services]"
  - "데이터 가져오기, SSIS 패키지"
  - "원본 [Integration Services], 데이터 복사"
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
caps.latest.revision: 160
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 134
---
# SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사는 원본에서 대상으로 데이터를 복사하는 간단한 방법입니다. 마법사를 실행하기 위해 SQL Server를 설치할 필요가 없습니다. 이 개요에서는 마법사를 사용하여 데이터를 가져오거나 내보낼 수 있는 데이터 원본과 마법사를 실행하기 위해 필요한 권한에 대해 설명합니다.

이 항목에서는 마법사에 대한 대략적인 **개요**를 제공합니다.
-   마법사 실행 준비를 마치고 시작하는 방법을 알고 싶으면 [SQL Server 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)을 참조하세요.
-   마법사의 단계에 대한 정보를 살펴보려면 콘텐츠 탐색 메뉴에서 원하는 페이지를 선택합니다. 마법사의 각 페이지에 대한 개별 설명서 페이지가 있습니다. 또는 마법사의 모든 페이지 또는 대화 상자에서 F1 키를 누르면 현재 페이지에 대한 설명서를 볼 수 있습니다.

**마법사를 가져옵니다.** 마법사를 실행하려고 하지만 컴퓨터에 [!INCLUDE[msCoName] (../Token/msCoName_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치되지 않은 경우 SSDT(SQL Server Data Tools)를 설치하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 설치할 수 있습니다. 자세한 내용은 [SSDT(SQL Server Data Tools) 다운로드](https://msdn.microsoft.com/library/mt204009.aspx)를 참조하세요.

> [!TIP] 둘 이상의 데이터베이스나 테이블 및 뷰 이외의 다른 데이터베이스 개체를 복사해야 하는 경우 가져오기 및 내보내기 마법사 대신 데이터베이스 복사 마법사를 사용합니다. 자세한 내용은 [데이터베이스 복사 마법사 사용](../../relational-databases/databases/use-the-copy-database-wizard.md)을 참조하세요.

## <a name="example-of-a-common-use-case---exporting-data-to-excel-video"></a>일반적인 사용 사례의 예 - 데이터를 Excel로 내보내기(동영상)  
데이터를 Excel로 내보내는 마법사의 일반적인 용도입니다. 다음은 마법사에서 이 작업을 수행하는 방법을 이해하기 쉽고 간단한 지침과 함께 설명하는 4분 길이의 YouTube 동영상 [Using the SQL Server Import and Export Wizard to Export to Excel](https://go.microsoft.com/fwlink/?linkid=829049)(SQL Server 가져오기 및 내보내기 마법사를 사용하여 Excel로 내보내기)입니다.

##  <a name="a-namewizardsourcesa-what-data-sources-and-destinations-can-i-use"></a><a name="wizardSources"></a> 어떤 데이터 원본 및 대상을 사용할 수 있나요?  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사는 다음 데이터 원본에서 또는 다음 데이터 원본으로 데이터를 복사할 수 있습니다. 이러한 데이터 원본 중 일부를 사용하려면 추가 파일을 다운로드 및 설치해야 합니다.

| 데이터 원본 | 추가 파일을 다운로드해야 하나요? |
|-------------|-----------------------------------------|
|**엔터프라이즈 데이터베이스**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle 및 기타.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Oracle에 연결할 파일을 설치하지만 IBM DB2 또는 Informix 등 다른 엔터프라이즈 데이터베이스에 연결해야 하는 파일은 설치하지 않습니다.<br/>- 엔터프라이즈 데이터베이스 시스템용으로 클라이언트 소프트웨어가 이미 설치된 경우 일반적으로 연결해야 합니다.<br/>- 클라이언트 소프트웨어를 설치하지 않은 경우 데이터베이스 관리자에게 사용이 허가된 복사본 설치 방법을 문의하세요.|
|**오픈 소스 데이터베이스**<br/>MySql, PostgreSQL, SQLite 및 기타.|이러한 데이터 원본에 연결할 추가 파일을 다운로드해야 합니다.<br/><br/>- **MySql**의 경우 [MySQL Connectors](http://dev.mysql.com/downloads/connector/)를 참조하세요.<br/>- **PostgreSQL**의 경우 [psqlODBC - PostgreSQL ODBC 드라이버](https://odbc.postgresql.org/) 및 [Npgsql - .NET Data Provider for PostgreSQL](http://www.npgsql.org/) 등의 타사 제품을 참조하세요.<br/>- **SQLite**의 경우 온라인에서 사용 가능한 여러 가지 오픈 소스 공급자 및 드라이버를 선택합니다.|
|**텍스트 파일**(플랫 파일)|추가 파일이 필요 없습니다.|
|**Microsoft Excel 및 Microsoft Access 파일**|Microsoft Office는 데이터 원본으로 Excel 및 Access 파일에 연결해야 하는 모든 파일을 설치하지 않습니다. 다운로드 [Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)을 가져옵니다.|
|**Azure 데이터 원본**<br/>현재 Azure Blob Storage만 해당합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 데이터 원본으로 Azure Blob 저장소에 연결해야 하는 파일을 설치하지 않습니다. 다운로드 [Azure용 Microsoft SQL Server 2016 Integration Services Feature Pack](https://www.microsoft.com/download/details.aspx?id=49492)을 가져옵니다.|
|**커넥터를 사용할 수 있는 다른 모든 데이터 원본**|일반적으로 다음 데이터 원본에 연결할 추가 파일을 다운로드해야 합니다.<br/><br/>- **ODBC 드라이버**를 사용할 수 있는 모든 원본 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 .Net Framework Provider for ODBC를 선택하여 ODBC(Open Database Connectivity)를 연결한 다음 ODBC 드라이버를 참조하는 연결 문자열 또는 기존 DSN(데이터 원본 이름)을 제공합니다.<br/>- **OLE DB 공급자**를 사용할 수 있는 모든 원본<br/>- **.Net Framework 데이터 공급자**를 사용할 수 있는 모든 원본<br/>- **타사 구성 요소**에서 원본 및 대상 기능을 제공하는 기타 데이터 원본 일반적으로 이러한 타사 제품은 SSIS(SQL Server Integration Services)용 추가 기능 제품으로 출시됩니다.|
  
> [!TIP] 데이터 원본에 연결 문자열이 필요한 경우 타사 사이트인 [연결 문자열 참조](https://www.connectionstrings.com/)에서 예제를 찾을 수 있습니다.  
  
## <a name="what-permissions-do-i-need-to-run-the-wizard"></a>마법사를 실행하려면 어떤 권한이 필요한가요?  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 성공적으로 실행하려면 적어도 다음 권한이 있어야 합니다. 현재 데이터 원본과 대상으로 작업하는 경우 이미 필요한 권한이 있을 수 있습니다.
  
|수행할 작업|SQL Server에 연결되어 있는 경우 필요한 권한 |  
|-------------------------|----------------------------------------------------|  
|원본 및 대상 데이터베이스나 파일 공유에 연결합니다.|서버 및 데이터베이스 로그인 권한|  
|원본 데이터베이스 또는 파일에서 데이터 내보내기 또는 읽기|원본 테이블 및 뷰에 대한 SELECT 권한|  
|대상 데이터베이스 또는 파일에 데이터 가져오기 또는 쓰기|대상 테이블에 대한 INSERT 권한|  
|대상 데이터베이스 또는 파일 만들기(해당하는 경우)|CREATE DATABASE 또는 CREATE TABLE 권한|  
|마법사가 만든 SSIS 패키지(해당하는 경우)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 패키지를 저장하려는 경우 **msdb** 데이터베이스에 패키지를 저장할 수 있는 권한|  
  
##  <a name="a-namewizardssisa-the-wizard-uses-sql-server-integration-services-ssis"></a><a name="wizardSSIS"></a> 마법사에서 SSIS(SQL Server Integration Services) 사용  
 마법사에서는 SSIS(SQL Server Integration Services)를 사용하여 데이터를 복사합니다. SSIS는 데이터를 ETL(추출, 변환 및 로드)하는 도구입니다. 마법사 페이지에서는 SSIS 언어 일부를 사용합니다.
  
 SSIS에서 기본 단위는 **패키지**입니다. 마법사는 사용자가 마법사 페이지를 진행하고 옵션을 지정하면 메모리 내에 SSIS 패키지를 만듭니다.    
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition 이상이 설치된 경우 마법사의 마지막 단계에서 필요에 따라 SSIS 패키지를 저장할 수 있습니다. 나중에 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하여 패키지를 다시 실행하고 태스크, 변환 및 이벤트 기반 논리를 추가하여 패키지를 확장할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사는 원본의 데이터를 대상으로 복사하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 만드는 가장 간단한 방법을 제공합니다.

SSIS에 대한 자세한 내용은 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)를 참조하세요.

## <a name="get-help-while-the-wizard-is-running"></a>마법사를 실행하는 동안 도움말 보기
> [!TIP] 마법사의 모든 페이지 또는 대화 상자에서 F1 키를 누르면 현재 페이지에 대한 설명서를 볼 수 있습니다.   
  
## <a name="whats-next"></a>다음 단계  
 마법사를 시작합니다. 자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목
[SQL Server 가져오기 및 내보내기 마법사에서 데이터 형식 매핑](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)

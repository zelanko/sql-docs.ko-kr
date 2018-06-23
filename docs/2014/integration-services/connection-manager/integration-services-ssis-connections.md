---
title: Integration Services(SSIS) 연결 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- sources [Integration Services], connections
- packages [Integration Services], connections
- destinations [Integration Services], connections
- tasks [Integration Services], connections
- connections [Integration Services], about connections
- connections [Integration Services]
- SQL Server Integration Services packages, connections
ms.assetid: 72f5afa3-d636-410b-9e81-2ffa27772a8c
caps.latest.revision: 90
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: aa0a870cd1a5e48849b81d392f3d34bdeb7d308e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082729"
---
# <a name="integration-services-ssis-connections"></a>Integration Services(SSIS) 연결
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지는 연결을 사용하여 다음과 같은 다양한 태스크와 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 기능을 수행하거나 구현합니다.  
  
-   텍스트, XML, Excel 통합 문서 및 관계형 데이터베이스와 같은 원본 및 대상 데이터 저장소에 연결하여 데이터 추출 및 로드  
  
-   참조 데이터가 포함된 관계형 데이터베이스에 연결하여 정확히 조회 또는 유사 항목 조회 수행  
  
-   관계형 데이터베이스에 연결하여 SELECT, DELETE, INSERT 명령과 같은 SQL 문 및 저장 프로시저 실행  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하여 유지 관리 수행 및 태스크 전송(예: 데이터베이스 백업 및 로그인 전송)  
  
-   텍스트 및 XML 파일과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 및 패키지 구성의 로그 항목을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 쓰기  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하여 일부 변환에서 해당 작업을 수행하는 데 필요한 임시 작업 테이블 만들기  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 및 데이터베이스에 연결하여 데이터 마이닝 모델 액세스, 큐브 및 차원 처리, DDL 코드 실행  
  
-   Foreach 루프 열거자 및 태스크에 사용할 기존 파일과 폴더 지정 또는 새 파일과 폴더 만들기  
  
-   메시지 큐, WMI(Windows Management Instrumentation), SMO( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects), 웹 및 메일 서버에 연결  
  
 이러한 연결을 만들려면 다음 섹션에서 설명한 대로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 연결 관리자를 사용합니다.  
  
## <a name="connection-managers"></a>연결 관리자  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 연결 관리자를 연결의 논리적 표현으로 사용합니다. 연결 관리자의 속성은 디자인 타임에 패키지가 실행될 때 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 만드는 물리적 연결을 기술하기 위한 것입니다. 예를 들어 연결 관리자에 포함 되어는 `ConnectionString` 속성이 런타임 시; 디자인 타임에 설정 하는, 물리적 연결 만들어집니다 연결 문자열 속성의 값을 사용 하 여 합니다.  
  
 패키지에는 하나의 연결 문자열 유형에 대한 여러 항목이 사용될 수 있으며, 각 항목에 대해 속성을 설정할 수 있습니다. 런타임 시 연결 관리자 유형의 각 항목에는 다른 특성을 지닌 연결이 생성됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 패키지에서 여러 데이터 원본 및 서버로 연결할 수 있는 여러 유형의 연결 관리자가 제공됩니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치할 때 설치 프로그램에서 기본적으로 설치하는 연결 관리자가 있습니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 웹 사이트에서 다운로드할 수 있는 연결 관리자가 있습니다.  
  
-   기존 연결 관리자가 사용자 요구에 맞지 않는 경우 자체 사용자 지정 연결 관리자를 만들 수 있습니다.  
  
### <a name="built-in-connection-managers"></a>기본 제공 연결 관리자  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 제공하는 연결 관리자 유형을 보여 줍니다.  
  
|형식|Description|항목|  
|----------|-----------------|-----------|  
|ADO|ADO(ActiveX Data Objects) 개체에 연결합니다.|[ADO 연결 관리자](ado-connection-manager.md)|  
|ADO.NET|.NET 공급자를 사용하여 데이터 원본에 연결합니다.|[ADO.NET 연결 관리자](ado-net-connection-manager.md)|  
|CACHE|데이터 흐름 또는 캐시 파일(.caw)에서 데이터를 읽고 이러한 데이터를 캐시 파일로 저장합니다.|[캐시 연결 관리자](cache-connection-manager.md)|  
|DQS|Data Quality Services 서버 및 서버의 Data Quality Services 데이터베이스에 연결합니다.|[DQS 정리 연결 관리자](dqs-cleansing-connection-manager.md)|  
|EXCEL|Excel 통합 문서 파일에 연결합니다.|[Excel 연결 관리자](excel-connection-manager.md)|  
|FILE|파일 또는 폴더에 연결합니다.|[파일 연결 관리자](file-connection-manager.md)|  
|FLATFILE|단일 플랫 파일의 데이터에 연결합니다.|[플랫 파일 연결 관리자](flat-file-connection-manager.md)|  
|FTP|FTP 서버에 연결합니다.|[FTP 연결 관리자](ftp-connection-manager.md)|  
|HTTP|웹 서버에 연결합니다.|[HTTP 연결 관리자](http-connection-manager.md)|  
|MSMQ|메시지 큐에 연결합니다.|[MSMQ 연결 관리자](msmq-connection-manager.md)|  
|MSOLAP100|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 연결합니다.|[Analysis Services 연결 관리자](analysis-services-connection-manager.md)|  
|MULTIFILE|다중 파일 또는 폴더에 연결합니다.|[다중 파일 연결 관리자](multiple-files-connection-manager.md)|  
|MULTIFLATFILE|다중 데이터 파일 및 폴더에 연결합니다.|[다중 플랫 파일 연결 관리자](multiple-flat-files-connection-manager.md)|  
|OLEDB|OLE DB Provider를 사용하여 데이터 원본에 연결합니다.|[OLE DB 연결 관리자](ole-db-connection-manager.md)|  
|ODBC|ODBC를 사용하여 데이터 원본에 연결합니다.|[ODBC 연결 관리자](odbc-connection-manager.md)|  
|SMOServer|SMO( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects) 서버에 연결합니다.|[SMO 연결 관리자](smo-connection-manager.md)|  
|SMTP|SMTP 메일 서버에 연결합니다.|[SMTP 연결 관리자](smtp-connection-manager.md)|  
|SQLMOBILE|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스에 연결합니다.|[SQL Server Compact Edition 연결 관리자](sql-server-compact-edition-connection-manager.md)|  
|WMI|서버에 연결하고 해당 서버에서 WMI(Windows Management Instrumentation)의 범위를 지정합니다.|[WMI 연결 관리자](wmi-connection-manager.md)|  
  
### <a name="connection-managers-available-for-download"></a>다운로드할 수 있는 연결 관리자  
 다음 표에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 웹 사이트에서 다운로드할 수 있는 추가 연결 관리자 유형을 나열합니다.  
  
> [!IMPORTANT]  
>  다음 표에 나열된 연결 관리자는 [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] 및 [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)]에서만 작동합니다.  
  
|형식|Description|항목|  
|----------|-----------------|-----------|  
|ORACLE|Oracle에 연결 \<버전 정보 > 서버입니다.|Oracle 연결 관리자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Oracle by Attunity의 연결 관리자 구성 요소입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Oracle by Attunity에는 원본 및 대상도 포함되어 있습니다. 자세한 내용은 [Microsoft Connectors for Oracle by Attunity 및 Microsoft Connectors for Teradata by Attunity(Microsoft Connectors for Oracle and Teradata by Attunity)](http://go.microsoft.com/fwlink/?LinkId=251526)다운로드 페이지를 참조하십시오.|  
|SAPBI|SAP NetWeaver BI 버전 7 시스템에 연결합니다.|SAP BI 연결 관리자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for SAP BI의 연결 관리자 구성 요소입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for SAP BI에는 원본 및 대상도 포함되어 있습니다. 자세한 내용은 [Microsoft SQL Server 2008 기능 팩](http://go.microsoft.com/fwlink/?LinkId=262016)다운로드 페이지를 참조하십시오.|  
|TERADATA|에 Teradata 연결 \<버전 정보 > 서버입니다.|Teradata 연결 관리자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Teradata by Attunity의 연결 관리자 구성 요소입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Teradata by Attunity에는 원본 및 대상도 포함되어 있습니다. 자세한 내용은 [Microsoft Connectors for Oracle by Attunity 및 Microsoft Connectors for Teradata by Attunity(Microsoft Connectors for Oracle and Teradata by Attunity)](http://go.microsoft.com/fwlink/?LinkId=251526)다운로드 페이지를 참조하십시오.|  
  
### <a name="custom-connection-managers"></a>사용자 지정 연결 관리자  
 사용자 지정 연결 관리자를 작성할 수도 있습니다. 자세한 내용은 [Developing a Custom Connection Manager](../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 패키지에서 연결 관리자를 추가하거나 삭제하는 방법에 대한 자세한 내용은 [패키지에서 연결 관리자 추가, 삭제 또는 공유](../add-delete-or-share-a-connection-manager-in-a-package.md)를 참조하세요.  
  
 패키지에서 연결 관리자 속성을 설정하는 방법에 대한 자세한 내용은 [연결 관리자의 속성 설정](../set-the-properties-of-a-connection-manager.md)을 참조하세요.  
  
## <a name="related-content"></a>관련 내용  
  
-   technet.microsoft.com의 비디오 - [패키지 성능 향상을 위해 Microsoft Attunity Connector for Oracle 활용](http://technet.microsoft.com/sqlserver/gg598963.aspx)  
  
-   social.technet.microsoft.com의 Wiki 문서 - [SSIS 연결](http://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity)   
  
-   blogs.msdn.com의 블로그 항목 - [SSIS에서 MySQL에 연결](http://go.microsoft.com/fwlink/?LinkId=217669)  
  
-   msdn.microsoft.com의 기술 문서 - [SQL Server Integration Services의 SharePoint 데이터 추출 및 로드](http://go.microsoft.com/fwlink/?LinkId=247826)  
  
-   support.microsoft.com의 기술 자료 - [You get "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" error message when using Oracle connection manager in SSIS](http://go.microsoft.com/fwlink/?LinkId=233696)(SSIS에서 Oracle 연결 관리자를 사용하는 경우 "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" 오류 메시지가 발생합니다.)  
  
  
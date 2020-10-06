---
description: Integration Services(SSIS) 연결
title: Integration Services(SSIS) 연결 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.asvs.connectionmanager.f1
- sql13.dts.designer.adddtsconnection.f1
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3b101ac6ab904543ab3e5a558ce2d50030df5adf
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91720844"
---
# <a name="integration-services-ssis-connections"></a>Integration Services(SSIS) 연결

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


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
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 연결 관리자를 연결의 논리적 표현으로 사용합니다. 연결 관리자의 속성은 디자인 타임에 패키지가 실행될 때 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 만드는 물리적 연결을 기술하기 위한 것입니다. 예를 들어 연결 관리자에는 디자인 타임에 설정하는 **ConnectionString** 속성이 포함되며, 런타임에는 연결 문자열 속성의 값을 사용하여 물리적 연결이 생성됩니다.  
  
 패키지에는 하나의 연결 문자열 유형에 대한 여러 항목이 사용될 수 있으며, 각 항목에 대해 속성을 설정할 수 있습니다. 런타임 시 연결 관리자 유형의 각 항목에는 다른 특성을 지닌 연결이 생성됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에는 패키지에서 여러 데이터 원본 및 서버로 연결할 수 있는 여러 유형의 연결 관리자가 제공됩니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치할 때 설치 프로그램에서 기본적으로 설치하는 연결 관리자가 있습니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 웹 사이트에서 다운로드할 수 있는 연결 관리자가 있습니다.  
  
-   기존 연결 관리자가 사용자 요구에 맞지 않는 경우 자체 사용자 지정 연결 관리자를 만들 수 있습니다.  

### <a name="package-level-and-project-level-connection-managers"></a>패키지 수준 및 프로젝트 수준 연결 관리자
패키지 수준 또는 프로젝트 수준에서 연결 관리자를 만들 수 있습니다. 프로젝트 수준에서 만든 연결 관리자는 프로젝트의 모든 패키지에 사용할 수 있습니다. 반면, 패키지 수준에서 만든 연결 관리자는 해당하는 특정 패키지에 사용할 수 있습니다.  
  
 데이터 원본 대신 프로젝트 수준에서 만든 연결 관리자를 사용하여 원본에 대한 연결을 공유합니다. 프로젝트 수준에서 연결 관리자를 추가하려면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트에 프로젝트 배포 모델을 사용해야 합니다. 프로젝트가 이 모델을 사용하도록 구성된 경우 **연결 관리자** 폴더가 **솔루션 탐색기**에 표시되고 **데이터 원본** 폴더가 **솔루션 탐색기**에서 제거됩니다.  
  
> [!NOTE]  
>  패키지에 데이터 원본을 사용하려면 프로젝트를 패키지 배포 모델로 변환해야 합니다.  
>   
>  두 모델 및 프로젝트를 프로젝트 배포 모델로 변환에 대한 자세한 내용은 [Integration Services(SSIS) 프로젝트 및 패키지 배포](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)를 참조하세요.

### <a name="built-in-connection-managers"></a>기본 제공 연결 관리자  
 다음 테이블에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 제공하는 연결 관리자 유형을 보여 줍니다.  
  
|Type|Description|항목|  
|----------|-----------------|-----------|  
|ADO|ADO(ActiveX Data Objects) 개체에 연결합니다.|[ADO 연결 관리자](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|.NET 공급자를 사용하여 데이터 원본에 연결합니다.|[ADO.NET 연결 관리자](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|CACHE|데이터 흐름 또는 캐시 파일(.caw)에서 데이터를 읽고 이러한 데이터를 캐시 파일로 저장합니다.|[캐시 연결 관리자](../../integration-services/connection-manager/cache-connection-manager.md)|  
|DQS|Data Quality Services 서버 및 서버의 Data Quality Services 데이터베이스에 연결합니다.|[DQS 정리 연결 관리자](../../integration-services/connection-manager/dqs-cleansing-connection-manager.md)|  
|EXCEL|Excel 통합 문서 파일에 연결합니다.|[Excel 연결 관리자](../../integration-services/connection-manager/excel-connection-manager.md)|  
|FILE|파일 또는 폴더에 연결합니다.|[파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md)|  
|FLATFILE|단일 플랫 파일의 데이터에 연결합니다.|[플랫 파일 연결 관리자](../../integration-services/connection-manager/flat-file-connection-manager.md)|  
|FTP|FTP 서버에 연결합니다.|[FTP 연결 관리자](../../integration-services/connection-manager/ftp-connection-manager.md)|  
|HTTP|웹 서버에 연결합니다.|[HTTP 연결 관리자](../../integration-services/connection-manager/http-connection-manager.md)|  
|MSMQ|메시지 큐에 연결합니다.|[MSMQ 연결 관리자](../../integration-services/connection-manager/msmq-connection-manager.md)|  
|MSOLAP100|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 연결합니다.|[Analysis Services 연결 관리자](../../integration-services/connection-manager/analysis-services-connection-manager.md)|  
|MULTIFILE|다중 파일 또는 폴더에 연결합니다.|[다중 파일 연결 관리자](../../integration-services/connection-manager/multiple-files-connection-manager.md)|  
|MULTIFLATFILE|다중 데이터 파일 및 폴더에 연결합니다.|[다중 플랫 파일 연결 관리자](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|  
|OLEDB|OLE DB Provider를 사용하여 데이터 원본에 연결합니다.|[OLE DB 연결 관리자](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|ODBC를 사용하여 데이터 원본에 연결합니다.|[ODBC 연결 관리자](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|SMOServer|SMO( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects) 서버에 연결합니다.|[SMO 연결 관리자](../../integration-services/connection-manager/smo-connection-manager.md)|  
|SMTP|SMTP 메일 서버에 연결합니다.|[SMTP 연결 관리자](../../integration-services/connection-manager/smtp-connection-manager.md)|  
|SQLMOBILE|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스에 연결합니다.|[SQL Server Compact Edition 연결 관리자](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
|WMI|서버에 연결하고 해당 서버에서 WMI(Windows Management Instrumentation)의 범위를 지정합니다.|[WMI 연결 관리자](../../integration-services/connection-manager/wmi-connection-manager.md)|  
  
### <a name="connection-managers-available-for-download"></a>다운로드할 수 있는 연결 관리자  
 다음 표에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 웹 사이트에서 다운로드할 수 있는 추가 연결 관리자 유형을 나열합니다.  
  
> [!IMPORTANT]  
>  다음 표에 나열된 연결 관리자는 [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] 및 [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)]에서만 작동합니다.  
  
|Type|Description|항목|  
|----------|-----------------|-----------|  
|ORACLE|Oracle \<version info\> 서버에 연결합니다.|Oracle 연결 관리자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Oracle by Attunity의 연결 관리자 구성 요소입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Oracle by Attunity에는 원본 및 대상도 포함되어 있습니다. 자세한 내용은 [Microsoft Connectors for Oracle by Attunity 및 Microsoft Connectors for Teradata by Attunity(Microsoft Connectors for Oracle and Teradata by Attunity)](https://www.microsoft.com/download/details.aspx?id=55179)다운로드 페이지를 참조하십시오.|  
|SAPBI|SAP NetWeaver BI 버전 7 시스템에 연결합니다.|SAP BI 연결 관리자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for SAP BI의 연결 관리자 구성 요소입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for SAP BI에는 원본 및 대상도 포함되어 있습니다. 자세한 내용은 [Microsoft SQL Server 2008 기능 팩](https://www.microsoft.com/download/details.aspx?id=30440)다운로드 페이지를 참조하십시오.|  
|TERADATA|Teradata \<version info\> 서버에 연결합니다.|Teradata 연결 관리자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Teradata by Attunity의 연결 관리자 구성 요소입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Teradata by Attunity에는 원본 및 대상도 포함되어 있습니다. 자세한 내용은 [Microsoft Connectors for Oracle by Attunity 및 Microsoft Connectors for Teradata by Attunity(Microsoft Connectors for Oracle and Teradata by Attunity)](https://www.microsoft.com/download/details.aspx?id=55179)다운로드 페이지를 참조하십시오.|  
  
### <a name="custom-connection-managers"></a>사용자 지정 연결 관리자  
 사용자 지정 연결 관리자를 작성할 수도 있습니다. 자세한 내용은 [Developing a Custom Connection Manager](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)을 참조하세요.  
  
## <a name="create-connection-managers"></a>연결 관리자 만들기
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에는 태스크를 여러 유형의 서버 및 데이터 원본에 연결하기 위한 다양한 연결 관리자가 포함됩니다. 연결 관리자는 여러 유형의 데이터 저장소에서 데이터를 추출하고 로드하는 데이터 흐름 구성 요소와 서버, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 또는 파일에 로그를 기록하는 로그 공급자에서 사용됩니다. 예를 들어 메일 보내기 태스크가 포함된 패키지에서는 SMTP 연결 관리자 유형을 사용하여 SMTP(Simple Mail Transfer Protocol) 서버에 연결합니다. SQL 실행 태스크가 포함된 패키지에서는 OLE DB 연결 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)을 참조하세요.  
  
 새 연결 관리자를 만들 때 연결 관리자를 자동으로 만들고 구성하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 사용할 수 있습니다. 또한 마법사는 연결 관리자를 사용하는 원본과 대상을 만들고 구성할 수 있도록 도와줍니다. 자세한 내용은 [Create Packages in SQL Server Data Tools](../../integration-services/create-packages-in-sql-server-data-tools.md)을 참조하세요.  
  
 수동으로 새 연결 관리자를 만들고 기존 패키지에 이 연결 관리자를 추가하려면 **디자이너의** 제어 흐름 **,** 데이터 흐름 **및**이벤트 처리기 **탭에 나타나는** 연결 관리자 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 영역을 사용합니다. **연결 관리자** 영역에서 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너가 제공하는 대화 상자를 사용하여 만들 연결 관리자 유형을 선택한 다음 해당 연결 관리자의 속성을 설정합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "연결 관리자 영역 사용" 섹션을 참조하십시오.  
  
 패키지에 연결 관리자를 추가한 다음에는 태스크, Foreach 루프 컨테이너, 원본, 변환 및 대상에서 연결 관리자를 사용할 수 있습니다. 자세한 내용은 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md), [Foreach 루프 컨테이너](../../integration-services/control-flow/foreach-loop-container.md) 및 [데이터 흐름](../../integration-services/data-flow/data-flow.md)을 참조하세요.  
  
### <a name="using-the-connection-managers-area"></a>연결 관리자 영역 사용  
 **디자이너의**제어 흐름 **,** 데이터 흐름 **또는** 이벤트 처리기 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 탭이 활성화된 상태에서 연결 관리자를 만들 수 있습니다.  
  
 다음 다이어그램은 **디자이너의** 제어 흐름 **탭에 표시된** 연결 관리자 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 영역을 보여 줍니다.  
  
 ![패키지가 포함된 제어 흐름 디자이너의 스크린샷](../../integration-services/connection-manager/media/samplecontrolflow.gif "패키지가 포함된 제어 흐름 디자이너의 스크린샷")    
  
### <a name="32-bit-and-64-bit-providers-for-connection-managers"></a>연결 관리자의 32비트 및 64비트 공급자  
 연결 관리자에서 사용하는 공급자는 대부분 32비트 및 64비트 버전에서 사용할 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 디자인 환경은 32비트 환경이므로 패키지를 디자인하는 동안 32비트 공급자만 표시됩니다. 따라서 특정 공급자의 32비트 버전과 64비트 버전이 모두 설치되어 있는 경우 연결 관리자에서 64비트 버전을 사용하도록 구성할 수 있습니다.  
  
 런타임 시 올바른 버전이 사용되므로 디자인 타임에 32비트 버전의 공급자를 지정했어도 문제가 되지 않습니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지가 실행될 경우에도 64비트 버전의 공급자를 실행할 수 있습니다.  
  
  두 버전의 공급자는 동일한 ID를 갖습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 런타임에서 사용 가능한 64비트 버전의 공급자를 사용하도록 할지 여부를 지정하려면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트의 Run64BitRuntime 속성을 설정합니다. Run64BitRuntime 속성이 **true**로 설정되면 런타임에 64비트 공급자를 찾아 사용합니다. Run64BitRuntime 속성이 **false**로 설정되면 런타임에 32비트 공급자를 찾아 사용합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트에서 설정할 수 있는 속성에 대한 자세한 내용은 [SSIS(Integration Services) 및 Studio 환경](../integration-services-ssis-development-and-management-tools.md)을 참조하세요.   

## <a name="add-a-connection-manager"></a>연결 관리자 추가
###  <a name="add-a-connection-manager-when-you-create-a-package"></a><a name="wizard"></a> 패키지를 만들 때 연결 관리자 추가  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 사용합니다.  
  
     이 마법사는 연결 관리자를 만들고 구성하는 것 외에도 연결 관리자를 사용하는 원본과 대상을 만들고 구성하는 것을 도와줍니다. 자세한 내용은 [Create Packages in SQL Server Data Tools](../../integration-services/create-packages-in-sql-server-data-tools.md)을 참조하세요.  
  
###  <a name="add-a-connection-manager-to-an-existing-package"></a><a name="package"></a> 기존 패키지에 연결 관리자 추가  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 **제어 흐름** 탭, **데이터 흐름** 탭 또는 **이벤트 처리기** 탭을 클릭하여 **연결 관리자** 영역을 표시합니다.  
  
4.  **연결 관리자** 영역의 아무 곳이나 마우스 오른쪽 단추로 클릭하고 다음 중 하나를 수행합니다.  
  
    -   패키지에 추가할 연결 관리자 유형을 클릭합니다.  
  
         또는  
  
    -   추가할 유형이 목록에 없는 경우 **새 연결** 을 클릭하여 **SSIS 연결 관리자 추가** 대화 상자를 열고 연결 관리자 유형을 선택한 다음 **확인**을 클릭합니다.  
  
     선택한 연결 관리자 유형의 사용자 지정 대화 상자가 열립니다. 사용 가능한 옵션 및 연결 관리자 유형에 대한 자세한 내용은 다음 옵션 표를 참조하십시오.  
  
    |ODBC 대상 편집기|옵션|  
    |------------------------|-------------|  
    |[ADO 연결 관리자](../../integration-services/connection-manager/ado-connection-manager.md)|[OLE DB 연결 관리자 구성](./ole-db-connection-manager.md)|  
    |[ADO.NET 연결 관리자](../../integration-services/connection-manager/ado-net-connection-manager.md)|[ADO.NET 연결 관리자 구성](./ado-net-connection-manager.md)|  
    |[Analysis Services 연결 관리자](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Analysis Services 연결 관리자 추가 대화 상자 UI 참조](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 연결 관리자](../../integration-services/connection-manager/excel-connection-manager.md)|[Excel 연결 관리자 편집기](./excel-connection-manager.md)|  
    |[파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md)|[파일 연결 관리자 편집기](./file-connection-manager.md)|  
    |[다중 파일 연결 관리자](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[파일 연결 관리자 추가 대화 상자 UI 참조](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[플랫 파일 연결 관리자](../../integration-services/connection-manager/flat-file-connection-manager.md)|[플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](./flat-file-connection-manager.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;열 페이지&#41;](./flat-file-connection-manager.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;고급 페이지&#41;](./flat-file-connection-manager.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](./flat-file-connection-manager.md)|  
    |[다중 플랫 파일 연결 관리자](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[다중 플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](./multiple-flat-files-connection-manager.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기&#40;열 페이지&#41;](./multiple-flat-files-connection-manager.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기&#40;고급 페이지&#41;](./multiple-flat-files-connection-manager.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](./multiple-flat-files-connection-manager.md)|  
    |[FTP 연결 관리자](../../integration-services/connection-manager/ftp-connection-manager.md)|[FTP 연결 관리자 편집기](./ftp-connection-manager.md)|  
    |[HTTP 연결 관리자](../../integration-services/connection-manager/http-connection-manager.md)|[HTTP 연결 관리자 편집기&#40;서버 페이지&#41;](./http-connection-manager.md)<br /><br /> [HTTP 연결 관리자 편집기&#40;프록시 페이지&#41;](./http-connection-manager.md)|  
    |[MSMQ 연결 관리자](../../integration-services/connection-manager/msmq-connection-manager.md)|[MSMQ 연결 관리자 편집기](./msmq-connection-manager.md)|  
    |[ODBC 연결 관리자](../../integration-services/connection-manager/odbc-connection-manager.md)|[ODBC 연결 관리자 UI 참조](./odbc-connection-manager.md)|  
    |[OLE DB 연결 관리자](../../integration-services/connection-manager/ole-db-connection-manager.md)|[OLE DB 연결 관리자 구성](./ole-db-connection-manager.md)|  
    |[SMO 연결 관리자](../../integration-services/connection-manager/smo-connection-manager.md)|[SMO 연결 관리자 편집기](./smo-connection-manager.md)|  
    |[SMTP 연결 관리자](../../integration-services/connection-manager/smtp-connection-manager.md)|[SMTP 연결 관리자 편집기](./smtp-connection-manager.md)|  
    |[SQL Server Compact Edition 연결 관리자](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[SQL Server Compact Edition 연결 관리자 편집기&#40;연결 페이지&#41;](./sql-server-compact-edition-connection-manager.md)<br /><br /> [SQL Server Compact Edition 연결 관리자 편집기&#40;모든 페이지&#41;](./sql-server-compact-edition-connection-manager.md)|  
    |[WMI 연결 관리자](../../integration-services/connection-manager/wmi-connection-manager.md)|[WMI 연결 관리자 편집기](./wmi-connection-manager.md)|  
  
     **연결 관리자** 영역에 추가된 연결 관리자가 나열됩니다.  
  
5.  필요에 따라 연결 관리자를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 클릭하여 연결 관리자의 기본 이름을 수정합니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
###  <a name="add-a-connection-manager-at-the-project-level"></a><a name="project"></a> 프로젝트 수준에서 연결 관리자 추가  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  **솔루션 탐색기**에서 **연결 관리자**를 마우스 오른쪽 단추로 클릭하고 **새 연결 관리자**를 클릭합니다.  
  
3.  **SSIS 연결 관리자 추가** 대화 상자에서 연결 관리자 유형을 선택한 다음 **추가**를 클릭합니다.  
  
     선택한 연결 관리자 유형의 사용자 지정 대화 상자가 열립니다. 사용 가능한 옵션 및 연결 관리자 유형에 대한 자세한 내용은 다음 옵션 표를 참조하십시오.  
  
    |ODBC 대상 편집기|옵션|  
    |------------------------|-------------|  
    |[ADO 연결 관리자](../../integration-services/connection-manager/ado-connection-manager.md)|[OLE DB 연결 관리자 구성](./ole-db-connection-manager.md)|  
    |[ADO.NET 연결 관리자](../../integration-services/connection-manager/ado-net-connection-manager.md)|[ADO.NET 연결 관리자 구성](./ado-net-connection-manager.md)|  
    |[Analysis Services 연결 관리자](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Analysis Services 연결 관리자 추가 대화 상자 UI 참조](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 연결 관리자](../../integration-services/connection-manager/excel-connection-manager.md)|[Excel 연결 관리자 편집기](./excel-connection-manager.md)|  
    |[파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md)|[파일 연결 관리자 편집기](./file-connection-manager.md)|  
    |[다중 파일 연결 관리자](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[파일 연결 관리자 추가 대화 상자 UI 참조](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[플랫 파일 연결 관리자](../../integration-services/connection-manager/flat-file-connection-manager.md)|[플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](./flat-file-connection-manager.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;열 페이지&#41;](./flat-file-connection-manager.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;고급 페이지&#41;](./flat-file-connection-manager.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](./flat-file-connection-manager.md)|  
    |[다중 플랫 파일 연결 관리자](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[다중 플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](./multiple-flat-files-connection-manager.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기&#40;열 페이지&#41;](./multiple-flat-files-connection-manager.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기&#40;고급 페이지&#41;](./multiple-flat-files-connection-manager.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](./multiple-flat-files-connection-manager.md)|  
    |[FTP 연결 관리자](../../integration-services/connection-manager/ftp-connection-manager.md)|[FTP 연결 관리자 편집기](./ftp-connection-manager.md)|  
    |[HTTP 연결 관리자](../../integration-services/connection-manager/http-connection-manager.md)|[HTTP 연결 관리자 편집기&#40;서버 페이지&#41;](./http-connection-manager.md)<br /><br /> [HTTP 연결 관리자 편집기&#40;프록시 페이지&#41;](./http-connection-manager.md)|  
    |[MSMQ 연결 관리자](../../integration-services/connection-manager/msmq-connection-manager.md)|[MSMQ 연결 관리자 편집기](./msmq-connection-manager.md)|  
    |[ODBC 연결 관리자](../../integration-services/connection-manager/odbc-connection-manager.md)|[ODBC 연결 관리자 UI 참조](./odbc-connection-manager.md)|  
    |[OLE DB 연결 관리자](../../integration-services/connection-manager/ole-db-connection-manager.md)|[OLE DB 연결 관리자 구성](./ole-db-connection-manager.md)|  
    |[SMO 연결 관리자](../../integration-services/connection-manager/smo-connection-manager.md)|[SMO 연결 관리자 편집기](./smo-connection-manager.md)|  
    |[SMTP 연결 관리자](../../integration-services/connection-manager/smtp-connection-manager.md)|[SMTP 연결 관리자 편집기](./smtp-connection-manager.md)|  
    |[SQL Server Compact Edition 연결 관리자](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[SQL Server Compact Edition 연결 관리자 편집기&#40;연결 페이지&#41;](./sql-server-compact-edition-connection-manager.md)<br /><br /> [SQL Server Compact Edition 연결 관리자 편집기&#40;모든 페이지&#41;](./sql-server-compact-edition-connection-manager.md)|  
    |[WMI 연결 관리자](../../integration-services/connection-manager/wmi-connection-manager.md)|[WMI 연결 관리자 편집기](./wmi-connection-manager.md)|  
  
     추가한 연결 관리자가 **솔루션 탐색기** 의 **연결 관리자**노드에 표시됩니다. 이 연결 관리자는 프로젝트의 모든 패키지에 대한 **SSIS 디자이너** 창의 **연결 관리자** 탭에도 나타납니다. 이 프로젝트 수준 연결 관리자를 패키지 수준 연결 관리자와 구별하기 위해 이 탭의 연결 관리자 이름에는 **(프로젝트)** 라는 접두사가 붙습니다.  
  
4.  선택적으로 **SSIS 디자이너** 창의 **연결 관리자** 탭 또는 **연결 관리자** 노드 아래에 있는 **솔루션 탐색기** 창에서 연결 관리자를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 클릭한 다음 연결 관리자의 기본 이름을 수정합니다.  
  
    > [!NOTE]  
    >  **SSIS 디자이너** 창의 **연결 관리자** 탭에서는 연결 관리자 이름의 **(프로젝트)** 접두사를 덮어쓸 수 없습니다. 이것은 의도적인 것입니다.  

### <a name="add-ssis-connection-manager-dialog-box"></a>SSIS 연결 관리자 추가 대화 상자
**SSIS 연결 관리자 추가** 대화 상자를 사용하여 패키지에 추가할 연결 형식을 선택할 수 있습니다.  
  
 연결 관리자에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)을 참조하세요.  
  
#### <a name="options"></a>옵션  
 **연결 관리자 유형**  
 각 연결 형식에 대해 편집기를 사용하여 연결 속성을 지정하려면 연결 형식을 선택한 다음 **추가**를 클릭하거나 연결 형식을 두 번 클릭합니다.  
  
 **추가**  
 각 연결 형식에 대해 편집기를 사용하여 연결 속성을 지정합니다.  
   
##  <a name="create-a-parameter-for-a-connection-manager-property"></a><a name="parameter"></a> 연결 관리자 속성에 대한 매개 변수 만들기  
  
1.  **연결 관리자** 영역에서 매개 변수를 만들려는 연결 관리자를 마우스 오른쪽 단추로 클릭한 후 **매개 변수화**를 클릭합니다.  
  
2.  **매개 변수화** 대화 상자에서 매개 변수 설정을 구성합니다. 자세한 내용은 [Parameterize Dialog Box](../integration-services-ssis-package-and-project-parameters.md)을 참조하세요.  

## <a name="delete-a-connection-manager"></a>연결 관리자 삭제 
###  <a name="delete-a-connection-manager-from-a-package"></a><a name="DeletePackageLevel"></a> 패키지에서 연결 관리자 삭제  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 **제어 흐름** 탭, **데이터 흐름** 탭 또는 **이벤트 처리기** 탭을 클릭하여 **연결 관리자** 영역을 표시합니다.  
  
4.  삭제할 연결 관리자를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
     SQL 실행 태스크 또는 OLE DB 원본과 같은 패키지 요소가 사용하는 연결 관리자를 삭제하면 다음과 같은 결과가 나타납니다.  
  
    -   삭제된 연결 관리자를 사용하던 패키지 요소에 오류 아이콘이 나타납니다.  
  
    -   패키지의 유효성 검사가 실패합니다.  
  
    -   패키지를 실행할 수 없습니다.  
  
5.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
###  <a name="delete-a-shared-connection-manager-project-level-connection-manager"></a><a name="DeleteProjectLevel"></a> 공유 연결 관리자(프로젝트 수준 연결 관리자) 삭제  
  
1.  프로젝트 수준 연결 관리자를 삭제하려면 **솔루션 탐색기** 창의 **연결 관리자** 노드 아래에 있는 연결 관리자를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에 다음과 같은 경고 메시지가 표시됩니다.  
  
    > [!WARNING]  
    >  프로젝트 연결 관리자를 삭제하면 연결 관리자를 사용하는 패키지가 실행되지 않을 수 있습니다. 이 동작은 실행 취소할 수 없습니다. 연결 관리자를 삭제하시겠습니까?  
  
2.  확인을 클릭하여 연결 관리자를 삭제하거나 취소를 클릭하여 연결 관리자를 그대로 둡니다.  
  
    > [!NOTE]  
    >  프로젝트의 특정 패키지에 대해 열려 있는 **SSIS 디자이너** 창의 **연결 관리자** 탭에서 프로젝트 수준 연결 관리자를 삭제할 수도 있습니다. 탭에서 연결 관리자를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭하면 됩니다. 
    
## <a name="set-the-properties-of-a-connection-manager"></a>연결 관리자의 속성 설정
**속성** 창을 사용하여 모든 연결 관리자를 구성할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 여러 유형의 연결 관리자를 수정하기 위한 사용자 지정 대화 상자도 제공합니다. 대화 상자는 연결 관리자 유형에 따라 다른 옵션들을 포함합니다.  
  
### <a name="modify-a-connection-manager-using-the-properties-window"></a>속성 창을 사용하여 연결 관리자 수정  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  SSIS 디자이너에서 **제어 흐름** 탭, **데이터 흐름** 탭 또는 **이벤트 처리기** 탭을 클릭하여 **연결 관리자** 영역을 표시합니다.  
  
4.  연결 관리자를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
5.  **속성** 창에서 속성 값을 편집합니다. **속성** 창은 연결 관리자의 표준 편집기에서 구성할 수 없는 일부 속성에 대한 액세스를 제공합니다.  
  
6.  **확인**을 클릭합니다.  
  
7.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
### <a name="modify-a-connection-manager-using-a-connection-manager-dialog-box"></a>연결 관리자 대화 상자를 사용하여 연결 관리자 수정  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 **제어 흐름** 탭, **데이터 흐름** 탭 또는 **이벤트 처리기** 탭을 클릭하여 **연결 관리자** 영역을 표시합니다.  
  
4.  **연결 관리자** 영역에서 연결 관리자를 두 번 클릭하여 **연결 관리자** 대화 상자를 엽니다. 특정 연결 관리자 유형에 대한 설명과 각 유형에 사용할 수 있는 옵션에 대한 자세한 내용은 다음 표를 참조하십시오.  
  
    |ODBC 대상 편집기|옵션|  
    |------------------------|-------------|  
    |[ADO 연결 관리자](../../integration-services/connection-manager/ado-connection-manager.md)|[OLE DB 연결 관리자 구성](./ole-db-connection-manager.md)|  
    |[ADO.NET 연결 관리자](../../integration-services/connection-manager/ado-net-connection-manager.md)|[ADO.NET 연결 관리자 구성](./ado-net-connection-manager.md)|  
    |[Analysis Services 연결 관리자](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Analysis Services 연결 관리자 추가 대화 상자 UI 참조](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 연결 관리자](../../integration-services/connection-manager/excel-connection-manager.md)|[Excel 연결 관리자 편집기](./excel-connection-manager.md)|  
    |[파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md)|[파일 연결 관리자 편집기](./file-connection-manager.md)|  
    |[다중 파일 연결 관리자](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[파일 연결 관리자 추가 대화 상자 UI 참조](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[플랫 파일 연결 관리자](../../integration-services/connection-manager/flat-file-connection-manager.md)|[플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](./flat-file-connection-manager.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;열 페이지&#41;](./flat-file-connection-manager.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;고급 페이지&#41;](./flat-file-connection-manager.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](./flat-file-connection-manager.md)|  
    |[다중 플랫 파일 연결 관리자](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[다중 플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](./multiple-flat-files-connection-manager.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기&#40;열 페이지&#41;](./multiple-flat-files-connection-manager.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기&#40;고급 페이지&#41;](./multiple-flat-files-connection-manager.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](./multiple-flat-files-connection-manager.md)|  
    |[FTP 연결 관리자](../../integration-services/connection-manager/ftp-connection-manager.md)|[FTP 연결 관리자 편집기](./ftp-connection-manager.md)|  
    |[HTTP 연결 관리자](../../integration-services/connection-manager/http-connection-manager.md)|[HTTP 연결 관리자 편집기&#40;서버 페이지&#41;](./http-connection-manager.md)<br /><br /> [HTTP 연결 관리자 편집기&#40;프록시 페이지&#41;](./http-connection-manager.md)|  
    |[MSMQ 연결 관리자](../../integration-services/connection-manager/msmq-connection-manager.md)|[MSMQ 연결 관리자 편집기](./msmq-connection-manager.md)|  
    |[ODBC 연결 관리자](../../integration-services/connection-manager/odbc-connection-manager.md)|[ODBC 연결 관리자 UI 참조](./odbc-connection-manager.md)|  
    |[OLE DB 연결 관리자](../../integration-services/connection-manager/ole-db-connection-manager.md)|[OLE DB 연결 관리자 구성](./ole-db-connection-manager.md)|  
    |[SMO 연결 관리자](../../integration-services/connection-manager/smo-connection-manager.md)|[SMO 연결 관리자 편집기](./smo-connection-manager.md)|  
    |[SMTP 연결 관리자](../../integration-services/connection-manager/smtp-connection-manager.md)|[SMTP 연결 관리자 편집기](./smtp-connection-manager.md)|  
    |[SQL Server Compact Edition 연결 관리자](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[SQL Server Compact Edition 연결 관리자 편집기&#40;연결 페이지&#41;](./sql-server-compact-edition-connection-manager.md)<br /><br /> [SQL Server Compact Edition 연결 관리자 편집기&#40;모든 페이지&#41;](./sql-server-compact-edition-connection-manager.md)|  
    |[WMI 연결 관리자](../../integration-services/connection-manager/wmi-connection-manager.md)|[WMI 연결 관리자 편집기](./wmi-connection-manager.md)|  
  
5.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  

## <a name="related-content"></a>관련 내용  
  
-   technet.microsoft.com의 비디오 - [패키지 성능 향상을 위해 Microsoft Attunity Connector for Oracle 활용](/previous-versions/dn912438(v=msdn.10))  
  
-   social.technet.microsoft.com의 Wiki 문서 - [SSIS 연결](https://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity)  
  
-   blogs.msdn.com의 블로그 항목 - [SSIS에서 MySQL에 연결](https://techcommunity.microsoft.com/t5/sql-server-integration-services/connecting-to-mysql-from-ssis/ba-p/387400)  
  
-   msdn.microsoft.com의 기술 문서 - [SQL Server Integration Services의 SharePoint 데이터 추출 및 로드](/previous-versions/sql/sql-server-2012/hh368261(v=msdn.10))  
  
-   support.microsoft.com의 기술 자료 - [You get "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" error message when using Oracle connection manager in SSIS](https://go.microsoft.com/fwlink/?LinkId=233696)(SSIS에서 Oracle 연결 관리자를 사용하는 경우 "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" 오류 메시지가 발생합니다.)  
  

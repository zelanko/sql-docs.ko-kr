---
title: 데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], data sources
- reports [Reporting Services], data
- expressions [Reporting Services], data sources
- data sources [Reporting Services], connections
- connection strings [Reporting Services]
- shared data sources [Reporting Services]
- Reporting Services, data sources
- logins [Reporting Services]
ms.assetid: 4d8f0ae1-102b-4b3d-9155-fa584c962c9e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a89cb1d06b60d086c139b4d618b7bd716c04616e
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63462040"
---
# <a name="data-connections-data-sources-and-connection-strings-in-reporting-services"></a>Data Connections, Data Sources, and Connection Strings in Reporting Services
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서에 데이터를 포함하려면 먼저 *데이터 원본* 및 *데이터 집합*을 만들어야 합니다. 이 항목에서는 데이터 원본의 유형, 데이터 원본을 만드는 방법 및 데이터 원본 자격 증명과 관련된 중요 정보를 설명합니다. 데이터 원본에는 데이터 원본 유형, 연결 정보 및 사용할 자격 증명의 유형이 포함됩니다. 데이터 원본에는 포함된 데이터 원본과 공유 데이터 원본의 두 가지 유형이 있습니다. 포함된 데이터 원본은 보고서에서 정의되고 해당 보고서에서만 사용됩니다. 공유 데이터 원본은 보고서와 독립적으로 정의되며 여러 보고서에서 사용될 수 있습니다. 자세한 내용은 [포함된 데이터 연결 및 공유 데이터 연결 또는 데이터 원본&#40;보고서 작성기 및 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md) 및 [포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)을 참조하세요.  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기본 모드 &#124; [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드|  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  

  
##  <a name="bkmk_data_sources"></a> 포함된 데이터 원본 또는 공유 데이터 원본  
 포함된 데이터 원본과 공유 데이터 원본은 작성,  저장 및 관리되는 방법이 다릅니다.  
  
-   보고서 디자이너에서 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 프로젝트의 일부분으로 포함된 데이터 원본 또는 공유 데이터 원본을 만듭니다. 이러한 데이터 원본을 미리 보기용으로 로컬에서 사용할지 아니면 프로젝트의 일부분으로 보고서 서버 또는 SharePoint 사이트에 배포할지를 제어할 수 있습니다. 보고서를 배포하는 보고서 서버 또는 SharePoint 사이트와 사용 중인 컴퓨터에 설치한 사용자 지정 데이터 확장 프로그램을 사용할 수 있습니다.  
  
     시스템 관리자는 추가적인 데이터 처리 확장 프로그램 및 .NET Framework 데이터 공급자를 설치하고 구성할 수 있습니다. 자세한 내용은 [데이터 처리 확장 프로그램과 .NET Framework 데이터 공급자&#40;SSRS&#41;](report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)를 참조하세요.  
  
     개발자는 <xref:Microsoft.ReportingServices.DataProcessing> API를 사용하여 다른 유형의 데이터 원본을 지원하는 데이터 처리 확장을 만들 수 있습니다.  
  
-   보고서 작성기에서 보고서 서버 또는 SharePoint 사이트를 찾은 다음 보고서에서 포함된 데이터 원본을 만들거나 공유 데이터 원본을 선택합니다. 보고서 작성기에서는 공유 데이터 원본을 만들 수 없습니다. 또한 보고서 작성기에서는 사용자 지정 데이터 확장 프로그램을 사용할 수 없습니다.  
  
##  <a name="bkmk_DataConnections"></a> 기본 제공 데이터 확장  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 의 기본 데이터 확장에는 다음과 같은 데이터 연결 형식이 포함됩니다.  
  
-   Microsoft SQL Server  
  
-   Microsoft SQL Server Analysis Services  
  
-   Microsoft SharePoint 목록  
  
-   [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]  
  
-   Microsoft SQL Server 병렬 데이터 웨어하우스  
  
-   OLE DB  
  
-   Oracle  
  
-   SAP NetWeaver BI  
  
-   Hyperion Essbase  
  
-   Teradata  
  
-   XML  
  
-   ODBC  
  
-   Power View 용 Microsoft BI 의미 체계 모델: PowerPivot 갤러리에 대 한 구성 된 SharePoint 사이트에서 및 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)],이 데이터 원본 유형에 사용할 수 있습니다. 이 데이터 원본 유형은 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 프레젠테이션에 대해서만 사용됩니다. 자세한 내용은 [파워 뷰용의 완벽한 표 형식 BI 의미 체계 모델 구성](https://technet.microsoft.com/video/building-the-perfect-bi-semantic-tabular-models-for-power-view.aspx)(영문)을 참조하세요.  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 지원하는 데이터 원본 및 버전의 전체 목록은 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](create-deploy-and-manage-mobile-and-paginated-reports.md)을 참조하세요.  
  
##  <a name="bkmk_create_data_source"></a> 데이터 원본 만들기  
 데이터 원본을 만들려면 다음 정보가 있어야 합니다.  
  
-   **데이터 원본 유형** 예를 들어, 연결 유형 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다. 연결 유형 드롭다운 목록에서 이 값을 선택합니다.  
  
-   **연결 정보** 연결 정보에는 데이터 원본의 이름과 위치 및 각 데이터 공급자마다 다른 연결 속성이 포함됩니다. *연결 문자열* 연결 정보는 텍스트 표현입니다. 예를 들어 데이터 원본이 SQL Server 데이터베이스인 경우에는 데이터베이스 이름을 지정할 수 있습니다. 포함된 데이터 원본의 경우에는 런타임에 평가되는 식 기반 연결 문자열을 작성할 수도 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [식 기반 연결 문자열](#bkmk_Expressions_in_connection_strings) 을 참조하세요.  
  
-   **자격 증명** 데이터에 액세스하는 데 필요한 자격 증명을 제공합니다. 데이터 원본 및 데이터 원본의 특정 데이터에 모두 액세스할 수 있는 적절한 사용 권한을 데이터 원본 소유자가 부여해야 합니다. 예를 들어 네트워크 서버에 설치된 [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] 예제 데이터베이스에 연결하려면 서버에 연결할 수 있는 권한과 데이터베이스에 액세스할 수 있는 읽기 전용 권한이 모두 있어야 합니다.  
  
    > [!NOTE]  
    >  기본적으로 자격 증명은 데이터 원본과 독립적으로 관리됩니다. 로컬 시스템에서 보고서를 미리 볼 때 사용하는 자격 증명은 게시된 보고서를 보는 데 필요한 자격 증명과 다를 수 있습니다. 보고서 서버 또는 SharePoint 사이트에 데이터 원본을 저장한 후 해당 위치에서 작업을 하려면 자격 증명을 변경해야 할 수 있습니다. 자세한 내용은 [데이터 원본에 대한 자격 증명](#bkmk_credentials)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 보고서에 대한 포함된 데이터 원본을 만들 때는 서버 탐색기가 아니라 보고서 디자이너의 솔루션 탐색기 또는 보고서 데이터 창에서 데이터 원본을 만들어야 합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 보고서 디자이너에서는 서버 탐색기에서 만든 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 데이터 원본이 지원되지 않습니다.  
  
 보고서 데이터 창에는 보고서에 추가된 공유 데이터 원본에 대한 참조 및 포함된 데이터 원본이 표시됩니다. 보고서 작성기에서 공유 데이터 원본 참조는 보고서 서버 또는 SharePoint 사이트의 공유 데이터 원본을 가리킵니다. 보고서 디자이너에서 공유 데이터 원본 참조는 솔루션 탐색기의 공유 데이터 원본 폴더에 있는 공유 데이터 원본을 가리킵니다.  
  
##  <a name="bkmk_credentials"></a> 데이터 원본에 대 한 자격 증명  
 기본적으로 자격 증명은 연결 정보와 독립적으로 저장 및 관리할 수 있습니다. 자격 증명은 데이터 원본을 만들고 데이터 세트 쿼리를 실행하고 보고서를 미리 보는 데 사용됩니다.  
  
> [!NOTE]  
>  로그인 이름, 암호 등의 로그인 정보를 데이터 원본의 연결 속성에 포함하지 않는 것이 좋습니다. 가능한 경우에는 항상 저장된 자격 증명과 함께 공유 데이터 원본을 사용하세요. 제작 환경에서는 데이터 연결을 만들거나 데이터 세트 쿼리를 실행할 때 **데이터 원본** 대화 상자의 자격 증명 페이지를 통해 자격 증명을 입력합니다.  
  
 컴퓨터에서 데이터 액세스용으로 입력하는 자격 증명은 로컬 프로젝트 구성 파일에 안전하게 저장되며, 해당 컴퓨터에서만 사용할 수 있습니다. 프로젝트 파일을 다른 컴퓨터에 복사하면 데이터 원본에 대해 자격 증명을 다시 정의해야 합니다.  
  
 보고서 서버 또는 SharePoint 사이트에 보고서를 배포하면 보고서의 포함된 데이터 원본 및 공유 데이터 원본은 독립적으로 관리됩니다. 컴퓨터에서 데이터에 액세스하기 위해 필요한 데이터 원본 자격 증명은 데이터에 액세스하기 위해 보고서 서버에 필요한 자격 증명과 다를 수 있습니다.  
  
 ![참고](media/rs-fyinote.png "참고")계속 작동 하는지 확인 데이터 원본 연결은 보고서를 게시 하면 성공적으로 연결 하는 것이 좋습니다. 자격 증명을 변경해야 하는 경우에는 보고서 서버에서 직접 수정할 수 있습니다.  
  
 보고서를 사용 하는 데이터 소스를 변경 하려면 기본 모드 보고서 관리자 또는 SharePoint 모드에서 문서 라이브러리에서 보고서 속성을 수정할 수 있습니다. 자세한 내용은 다음 항목을 참조하세요.  
  
-   [Reporting Services 데이터 원본에 자격 증명 저장](report-data/store-credentials-in-a-reporting-services-data-source.md) [Reporting Services 데이터 원본에 자격 증명을 저장 합니다.](report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
-   [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
-   [사용자 지정 데이터 처리 확장 프로그램에 대한 연결 지정](report-data/specify-connections-for-custom-data-processing-extensions.md)  
  
-   [보고서 작성기에 자격 증명 지정](../../2014/reporting-services/specify-credentials-in-report-builder.md)  
  
-   [데이터 연결이 나 데이터 원본 추가 및 확인 &#40;보고서 작성기 및 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
##  <a name="bkmk_connection_examples"></a> 자주 사용하는 연결 문자열 예  
 연결 문자열은 데이터 공급자에 대한 연결 속성의 텍스트 표현입니다. 다음 표에서는 다양한 데이터 연결 형식에 대한 연결 문자열의 예를 보여 줍니다.  
  
|**데이터 원본**|**예제**|**설명**|  
|---------------------|-----------------|---------------------|  
|로컬 서버의 SQL Server 데이터베이스|`data source="(local)";initial catalog=AdventureWorks`|데이터 원본 유형을 `Microsoft SQL Server`로 설정합니다. 자세한 내용은 [SQL Server 연결 형식&#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md)을 참조하세요.|  
|로컬 서버의 SQL Server 데이터베이스|`data source="(local)";initial catalog=AdventureWorks`|데이터 원본 유형을 `Microsoft SQL Server`로 설정합니다.|  
|SQL Server 인스턴스<br /><br /> database|`Data Source=localhost\MSSQL10_50.InstanceName; Initial Catalog=AdventureWorks`|데이터 원본 유형을 `Microsoft SQL Server`로 설정합니다.|  
|SQL Server Express 데이터베이스|`Data Source=localhost\MSSQL10_50.SQLEXPRESS; Initial Catalog=AdventureWorks`|데이터 원본 유형을 `Microsoft SQL Server`로 설정합니다.|  
|클라우드의 [!INCLUDE[ssSDS](../includes/sssds-md.md)]|`Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True`|데이터 원본 유형을 `Windows Azure SQL Database`로 설정합니다. 자세한 내용은 [SQL Azure 연결 형식&#40;SSRS&#41;](report-data/sql-azure-connection-type-ssrs.md)을 참조하세요.|  
|SQL Server 병렬 데이터 웨어하우스|`HOST=<IP address>;database= AdventureWorks; port=<port>`|데이터 원본 유형을 `Microsoft SQL Server Parallel Data Warehouse`로 설정합니다. 자세한 내용은 [SQL Server 병렬 데이터 웨어하우스 연결 형식&#40;SSRS&#41;](report-data/sql-server-parallel-data-warehouse-connection-type-ssrs.md)을 참조하세요.|  
|로컬 서버의 Analysis Services 데이터베이스|`data source=localhost;initial catalog=Adventure Works DW`|데이터 원본 유형을 `Microsoft SQL Server Analysis Services`로 설정합니다. 자세한 내용은 [MDX용 Analysis Services 연결 형식&#40;SSRS&#41;](report-data/analysis-services-connection-type-for-mdx-ssrs.md) 또는 [DMX용 Analysis Services 연결 형식&#40;SSRS&#41;](report-data/analysis-services-connection-type-for-dmx-ssrs.md)을 참조하세요.|  
|Sales 큐브 뷰가 있는 Analysis Services 테이블 형식 model 데이터베이스|`Data source=<servername>;initial catalog= Adventure Works DW;cube='Sales'`|데이터 원본 유형을 `Microsoft SQL Server Analysis Services`로 설정합니다. cube= 설정에 큐브 뷰 이름을 지정합니다. 자세한 내용은 [큐브 뷰&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/perspectives-ssas-tabular.md)를 참조하세요.|  
|기본 모드에서 구성된 보고서 서버의 보고서 모델 데이터 원본|`Server=http://myreportservername/reportserver; datasource=/models/Adventure Works`|보고서 서버 또는 문서 라이브러리 URL과 보고서 서버 폴더 또는 문서 라이브러리 폴더 네임스페이스에 게시된 모델의 경로를 지정합니다.
|SharePoint 통합 모드에서 구성된 보고서 서버의 보고서 모델 데이터 원본|`Server=http://server; datasource=http://server/site/documents/models/Adventure Works.smdl`|보고서 서버 또는 문서 라이브러리 URL과 보고서 서버 폴더 또는 문서 라이브러리 폴더 네임스페이스에 게시된 모델의 경로를 지정합니다.|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버|`provider=MSOLAP.2;data source=<remote server name>;initial catalog=FoodMart 2000`|데이터 원본 유형을 `OLE DB Provider for OLAP Services 8.0`로 설정합니다.<br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 속성을 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]으로 설정하면 `ConnectTo` 2000 `8.0` 데이터 원본에 보다 빠르게 연결할 수 있습니다. 이 속성을 설정하려면 **연결 속성** 대화 상자의 **고급 속성** 탭을 사용합니다.|  
|Oracle 서버|`data source=myserver`|데이터 원본 유형을 `Oracle`로 설정합니다. Oracle 클라이언트 도구는 보고서 디자이너 컴퓨터와 보고서 서버에 설치해야 합니다. 자세한 내용은 [Oracle 연결 형식&#40;SSRS&#41;](report-data/oracle-connection-type-ssrs.md)을 참조하세요.|  
|SAP NetWeaver BI 데이터 원본|`DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|데이터 원본 유형을 `SAP NetWeaver BI`로 설정합니다. 자세한 내용은 [SAP NetWeaver BI 연결 형식&#40;SSRS&#41;](report-data/sap-netweaver-bi-connection-type-ssrs.md)을 참조하세요.|  
|Hyperion Essbase 데이터 원본|`Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample`|데이터 원본 유형을 `Hyperion Essbase`로 설정합니다. 자세한 내용은 [Hyperion Essbase 연결 형식&#40;SSRS&#41;](report-data/hyperion-essbase-connection-type-ssrs.md)을 참조하세요.|  
|Teradata 데이터 원본|`data source=`\<NNN>.\<NNN>.\<NNN>.\<NNN>`;`|데이터 원본 유형을 `Teradata`로 설정합니다. 연결 문자열은 1자리부터 3자리 숫자까지 허용되는 필드 네 개로 구성된 형식의 IP(인터넷 프로토콜) 주소입니다. 자세한 내용은 [Teradata 연결 형식&#40;SSRS&#41;](report-data/teradata-connection-type-ssrs.md)을 참조하세요.|  
|XML 데이터 원본, 웹 서비스|`data source=http://adventure-works.com/results.aspx`|데이터 원본 유형을 `XML`로 설정합니다. 연결 문자열은 WSDL(Web Services Definition Language)을 지원하는 웹 서비스의 URL입니다. 자세한 내용은 [XML 연결 형식&#40;SSRS&#41;](report-data/xml-connection-type-ssrs.md)을 참조하세요.|  
|XML 데이터 원본, XML 문서|`http://localhost/XML/Customers.xml`|데이터 원본 유형을 `XML`로 설정합니다. 연결 문자열은 XML 문서의 URL입니다.|  
|XML 데이터 원본, 포함된 XML 문서|*비어 있음*|데이터 원본 유형을 `XML`로 설정합니다. XML 데이터는 보고서 정의에 포함됩니다.|  
  
`localhost`를 사용하여 보고서 서버에 연결하지 못하는 경우 TCP/IP 프로토콜에 대한 네트워크 프로토콜이 설정되어 있는지 확인합니다. 자세한 내용은 [Configure Client Protocols](../database-engine/configure-windows/configure-client-protocols.md)을 참조하세요.  
  
##  <a name="bkmk_special_password_characters"></a> 암호의 특수 문자  
 암호를 입력하라는 메시지를 표시하거나 연결 문자열에 암호를 포함하도록 ODBC 또는 SQL 데이터 원본을 구성한 경우 사용자가 문장 부호와 같은 특수 문자가 포함된 암호를 입력하면 일부 기본 데이터 원본 드라이버가 해당 특수 문자의 유효성을 검사할 수 없습니다. 보고서 처리 시 "올바른 암호가 아닙니다" 메시지가 나타나면 이 문제 때문일 수 있습니다. 암호를 변경하는 것이 불가능한 경우 데이터베이스 관리자와 협력하여 서버에서 해당 자격 증명을 시스템 ODBC DSN(데이터 원본 이름)의 일부로 저장합니다. 자세한 내용은 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK 설명서의 "OdbcConnection.ConnectionString"을 참조하세요.  
  
##  <a name="bkmk_Expressions_in_connection_strings"></a> 식 기반 연결 문자열  
 식 기반 연결 문자열은 런타임에 평가됩니다. 예를 들어 데이터 원본을 매개 변수로 지정하고 연결 문자열에 매개 변수 참조를 포함하여 사용자가 보고서의 데이터 원본을 선택할 수 있도록 할 수 있습니다. 예를 들어 여러 국가에 데이터 서버를 보유하고 있는 다국적 기업의 경우 식 기반 연결 문자열을 사용하면 판매 보고서를 실행하는 사용자가 보고서를 실행하기 전에 특정 국가의 데이터 원본을 선택할 수 있습니다.  
  
 다음 예에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 연결 문자열에 데이터 원본 식을 사용하는 작업을 보여 줍니다. 이 예에서는 `ServerName`이라는 보고서 매개 변수를 만들었다고 가정합니다.  
  
```  
="data source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks"  
```  
  
 데이터 원본 식은 런타임에 또는 보고서를 미리 볼 때 처리됩니다. 식은 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]으로 작성해야 합니다. 다음 지침에 따라 데이터 원본 식을 정의합니다.  
  
-   정적 연결 문자열을 사용하여 보고서를 디자인합니다. 정적 연결 문자열이란 식을 통해 설정되지 않은 연결 문자열을 말합니다. 예를 들어 보고서별 데이터 원본 또는 공유 데이터 원본을 만드는 단계를 따르는 경우 정적 연결 문자열을 정의하게 됩니다. 정적 연결 문자열을 사용하면 보고서를 만드는 데 필요한 쿼리 결과를 가져올 수 있도록 보고서 디자이너의 데이터 원본에 연결할 수 있습니다.  
  
-   데이터 원본 연결을 정의할 때는 공유 데이터 원본을 사용하지 마세요. 공유 데이터 원본에서는 데이터 원본 식을 사용할 수 없습니다. 보고서에 대한 포함된 데이터 원본을 정의해야 합니다.  
  
-   연결 문자열과 별도로 자격 증명을 지정합니다. 저장된 자격 증명, 입력 정보를 요청하는 자격 증명 또는 통합 보안을 사용할 수 있습니다.  
  
-   보고서 매개 변수를 추가하여 데이터 원본을 지정합니다. 매개 변수 값으로는 사용 가능한 값(이 경우 사용 가능한 값은 보고서에 사용할 수 있는 데이터 원본이어야 함)의 정적 목록을 제공하거나 런타임에 데이터 원본 목록을 검색하는 쿼리를 정의할 수 있습니다.  
  
-   데이터 원본 목록에서 동일한 데이터베이스 스키마를 공유하는지 확인합니다. 모든 보고서 디자인은 스키마 정보로 시작됩니다. 보고서 정의에 사용되는 스키마와 런타임 시 보고서에 사용되는 실제 스키마가 일치하지 않으면 보고서가 실행되지 않을 수 있습니다.  
  
-   보고서를 게시하기 전에 정적 연결 문자열을 식으로 바꿉니다. 이때 정적 연결 문자열은 보고서 디자인을 완료한 다음에 식으로 바꿔야 합니다. 식을 사용한 다음에는 보고서 디자이너에서 쿼리를 실행할 수 없습니다. 또한 보고서 데이터 창의 필드 목록과 매개 변수 목록이 자동으로 업데이트되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [포함된 데이터 연결 및 공유 데이터 연결 또는 데이터 원본&#40;보고서 작성기 및 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [보고서 데이터 원본 관리](report-data/manage-report-data-sources.md)   
 [데이터 원본 속성 대화 상자, 자격 증명](../../2014/reporting-services/data-source-properties-dialog-box-credentials.md)   
 [공유 데이터 원본 속성 대화 상자, 자격 증명](../../2014/reporting-services/shared-data-source-properties-dialog-box-credentials.md)   
 [공유 데이터 원본 만들기, 수정 및 삭제&#40;SSRS&#41;](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [배포 속성 설정&#40;Reporting Services&#41;](tools/set-deployment-properties-reporting-services.md)   
 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [데이터 연결이 나 데이터 원본 추가 및 확인 &#40;보고서 작성기 및 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  

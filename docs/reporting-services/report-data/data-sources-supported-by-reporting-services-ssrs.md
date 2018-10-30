---
title: Reporting Services에서 지원하는 데이터 원본(SSRS) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- SQL Server data processing extension [Reporting Services]
- XML data processing extension [Reporting Services]
- reports [Reporting Services], data
- data processing extensions [Reporting Services], data sources
- Oracle [Reporting Services]
- OLE DB data processing extension
- data sources [Reporting Services], about data sources
- ODBC data processing extension
- Reporting Services, data sources
ms.assetid: 9d11d055-a3be-45aa-99a7-46447a94ed42
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7348463fe7fb9f3871ecba06a2be8e768f8e3d51
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50029171"
---
# <a name="data-sources-supported-by-reporting-services-ssrs"></a>Reporting Services에서 지원하는 데이터 원본(SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 데이터 처리 확장 프로그램을 사용하는 확장 가능한 모듈식 데이터 계층을 통해 데이터 원본에서 보고서 데이터를 검색합니다. 데이터 원본에서 보고서 데이터를 검색하려면 데이터 원본 유형, 데이터 원본에서 실행 중인 소프트웨어 버전 및 데이터 원본 플랫폼(32비트 또는 64비트 [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)])을 지원하는 데이터 처리 확장 프로그램을 선택해야 합니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 배포하면 다양한 데이터 원본 유형에 대한 액세스를 제공하는 데이터 처리 확장 프로그램 집합이 자동으로 보고서 제작 클라이언트와 보고서 서버에 설치되고 등록됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 다음과 같은 데이터 원본 유형을 설치합니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] - MDX, DMX, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]및 테이블 형식 모델용  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]  
  
-   Oracle  
  
-   SAP BW 
  
-   [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 목록  
  
-   Teradata  
  
-   OLE DB  
  
-   ODBC  
  
-   XML  
  
 또한 시스템 관리자로 사용자 지정 데이터 처리 확장 프로그램과 표준 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 설치하고 등록할 수 있습니다. 보고서를 처리하고 보려면 보고서 서버에 데이터 처리 확장 프로그램과 데이터 공급자를 설치하고 등록해야 합니다. 보고서를 미리 보려면 보고서 제작 클라이언트에 DPE와 데이터 공급자를 설치하고 등록해야 합니다. 데이터 처리 확장 프로그램과 데이터 공급자는 설치되는 플랫폼에 대해 기본적으로 컴파일되어야 합니다. SOAP 웹 서비스를 사용하여 데이터 원본을 프로그래밍 방식으로 배포할 경우 데이터 원본 확장 프로그램을 정의해야 합니다. **RSReportDesigner.config** 파일의 데이터 확장 프로그램 값을 사용합니다. 기본적으로 이 파일은 다음 폴더에 있습니다.  
  
```  
<drive letter>\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies  
```  
  
 예를 들어 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 확장 프로그램은 OLEDB-MD입니다.  
  
 많은 타사 표준 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?linkid=51456) 와 타사 사이트에서 다운로드할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 공개 포럼에서 타사 데이터 공급자에 대한 정보를 검색할 수도 있습니다.  
  
> [!NOTE]  
>  표준 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램이 제공하는 기능 중 일부를 지원하지 않을 수 있습니다. 또한 일부 OLE DB 데이터 공급자 및 ODBC 드라이버의 경우 보고서를 제작하고 미리 보는 데 사용할 수 있지만 보고서 서버에 게시된 보고서를 지원하지 않을 수 있습니다. 예를 들어 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet은 보고서 서버에서 지원되지 않습니다. 자세한 내용은 [데이터 처리 확장 프로그램과 .NET Framework 데이터 공급자&#40;SSRS&#41;](../../reporting-services/report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)를 참조하세요.  
  
 사용자 지정 데이터 처리 확장 프로그램에 대한 자세한 내용은 [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)을 참조하십시오. 표준 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자에 대한 자세한 내용은 <xref:System.Data> 네임스페이스를 참조하세요.   
  
## <a name="platform-support-for-report-data-sources"></a>보고서 데이터 원본에 대한 플랫폼 지원  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 배포에서 사용할 수 있는 데이터 원본은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 버전 및 플랫폼에 따라 달라집니다. 기능에 대한 자세한 내용은 [SQL Server 2016 버전에서 지원하는 Reporting Services 기능](../../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요. 버전 및 플랫폼별로 지원되는 데이터 원본에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 표를 참조하십시오.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 원본에 대한 플랫폼 고려 사항은 보고서 제작 클라이언트와 보고서 서버에 대해 각각 다릅니다.  
  
### <a name="on-the-report-authoring-client"></a>보고서 제작 클라이언트  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] 는 32비트 응용 프로그램입니다. [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] 는 Itanium 기반 플랫폼에서 지원되지 않습니다. x64 플랫폼에서 보고서 디자이너를 통해 보고서를 편집 및 미리 보려면 x86 플랫폼 디렉터리에 32비트 데이터 공급자가 설치되어 있어야 합니다.  
  
### <a name="on-the-report-server"></a>보고서 서버  
 64비트 보고서 서버에 보고서를 배포하는 경우 보고서 서버에 기본적으로 컴파일된 64비트 데이터 공급자가 설치되어 있어야 합니다. 64비트 인터페이스에 32비트 데이터 공급자를 래핑하는 기능은 지원되지 않습니다. 자세한 내용은 데이터 공급자에 대한 설명서를 참조하십시오.  
  
## <a name="supported-data-sources"></a>지원되는 데이터 원본  
 다음 표에서는 보고서 데이터 집합 및 보고서 모델에 대해 데이터를 검색하는 데 사용할 수 있는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 데이터 처리 확장 프로그램 및 데이터 공급자를 보여 줍니다. 확장 프로그램이나 데이터 공급자에 대한 자세한 내용을 보려면 두 번째 열의 링크를 클릭하십시오. 표 열은 다음과 같습니다.  
  
-   보고서 데이터 원본: 액세스하는 데이터의 유형(예: 관계형 데이터베이스, 다차원 데이터베이스, 플랫 파일 또는 XML)입니다. 이 열을 통해 " [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 보고서에 사용할 수 있는 데이터 형식은 무엇인가?"라는 질문에 대한 답을 얻을 수 있습니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 원본 유형: [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 데이터 원본을 정의할 때 드롭다운 목록에 표시되는 데이터 원본 유형 중 하나입니다. 이 목록은 설치 및 등록된 DPE와 데이터 공급자를 통해 채워집니다. 이 열을 통해 "보고서 데이터 원본을 만들 때 드롭다운 목록에서 어떤 데이터 원본 유형을 선택할 것인가?"라는 질문에 대한 답을 얻을 수 있습니다.  
  
-   데이터 처리 확장 프로그램/데이터 공급자의 이름: [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램이나 선택한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 원본 유형에 해당하는 다른 데이터 공급자입니다. 이 열을 통해 "데이터 원본 유형을 선택할 때 사용되는 해당 데이터 처리 확장 프로그램이나 데이터 공급자는 무엇인가?"라는 질문에 대한 답을 얻을 수 있습니다.  
  
-   기본 데이터 공급자 버전(옵션): 일부 데이터 원본 유형은 두 개 이상의 데이터 공급자를 지원합니다. 이는 같은 공급자의 다른 버전일 수도 있고 데이터 공급자 유형에 대한 타사의 다른 구현일 수도 있습니다. 공급자 이름은 데이터 원본을 구성한 후 연결 문자열에 자주 나타납니다. 이 열을 통해 "데이터 원본 유형을 선택한 후 **연결 속성** 대화 상자에서 어떤 데이터 공급자를 선택할 것인가?"라는 질문에 대한 답을 얻을 수 있습니다.  
  
-   데이터 원본 *\<platform>*: 데이터 처리 확장 프로그램이나 데이터 공급자가 대상 데이터 원본에 대해 지원하는 데이터 원본 플랫폼입니다. 이 열을 통해 "이 데이터 처리 확장 프로그램이나 데이터 공급자가 이 플랫폼 유형의 데이터 원본에서 데이터를 검색할 수 있는가?"라는 질문에 대한 답을 얻을 수 있습니다.  
  
-   데이터 원본 버전: DPE 또는 데이터 공급자가 지원하는 대상 데이터 원본의 버전입니다. 이 열을 통해 "이 데이터 처리 확장 프로그램이나 데이터 공급자가 이 버전의 데이터 원본에서 데이터를 검색할 수 있는가?"라는 질문에 대한 답을 얻을 수 있습니다.  
  
-   RS *\<platform>*: 사용자 지정 DPE 또는 데이터 공급자를 설치할 수 있는 보고서 서버 및 보고서 제작 클라이언트의 플랫폼입니다. 기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램은 모든 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]설치에 포함되어 있습니다. 사용자 지정 데이터 처리 확장 프로그램이나 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자는 특정 플랫폼에 대해 기본적으로 컴파일되어야 합니다. 이 열을 통해 "이 데이터 처리 확장 프로그램이나 데이터 공급자를 이 플랫폼 유형에 설치할 수 있는가?"라는 질문에 대한 답을 얻을 수 있습니다.  
  
###  <a name="DataSourcesTable"></a> 데이터 원본 유형  
  
|보고서 데이터<br /><br /> 원본|Reporting Services 데이터 원본 유형|데이터 처리 확장 프로그램/데이터 공급자의 이름|기본 데이터 공급자 버전<br /><br /> (옵션)|data<br /><br /> 원본<br /><br /> 플랫폼 x86|데이터<br /><br /> 원본<br /><br /> 플랫폼 x64|데이터 원본 버전|RS<br /><br /> 플랫폼 x86|RS<br /><br /> 플랫폼 x64|  
|-------------------------------|-----------------------------------------|------------------------------------------------------|-------------------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|-------------------------|-------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 데이터베이스|[Microsoft SQL Server](#MicrosoftSQLServer)|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|System.Data.SqlClient 확장|Y|Y|SQL Server 2008 이상|Y|Y|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 데이터베이스|OLEDB|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|System.Data.OledbClient 확장|Y|Y|SQL Server 2008 이상|Y|Y|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 데이터베이스|[ODBC](#ODBC)|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|System.Data.OdbcClient 확장|Y|Y|SQL Server 2008 이상|Y|Y|  
|[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|[Microsoft Azure SQL Database](#Azure)|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|System.Data.SqlClient 확장|해당 사항 없음|해당 사항 없음|[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|Y|Y|
|SQL 데이터 웨어하우스|[Microsoft Azure SQL Database](#Azure)|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|System.Data.SqlClient 확장|해당 사항 없음|해당 사항 없음|SQL 데이터 웨어하우스|Y|Y| 
|[!INCLUDE[ssDW](../../includes/ssdw-md.md)] 어플라이언스|[Microsoft 병렬 데이터 웨어하우스](#PWD)|사용되지 않는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|해당 사항 없음|해당 사항 없음|해당 사항 없음|[!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|N|N|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 다차원 데이터베이스|[Microsoft SQL Server Analysis Services](#AnalysisServices)|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|ADOMD.NET 사용|Y|Y|SQL Server 2008 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 이상|Y|Y|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 다차원 데이터베이스|OLEDB|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|System.Data.OledbClient 확장<br /><br /> 버전 10.0|Y|Y|SQL Server 2008 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Y|Y|   
|SharePoint 목록|[Microsoft SharePoint 목록](#SharePointList)|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|Lists.asmx 또는 SharePoint 개체 모델 API 인터페이스에서 데이터 가져오기<br /><br /> [참고](#SharePointList)를 참조하십시오.|N|Y|SharePoint 2013 제품 이상|Y|Y|   
|XML|[XML](#XML)|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|XML 데이터 원본에는 플랫폼 종속성이 없음|해당 사항 없음|해당 사항 없음|[!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)] 또는 문서|Y|Y|  
|보고서 서버 모델|보고서 모델|게시된 SMDL 파일에 대한 사용되지 않는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|모델의 데이터 원본에서 기본 제공 데이터 처리 확장 프로그램을 사용합니다.<br /><br /> Oracle 기반 모델을 사용하려면 Oracle 클라이언트 구성 요소가 있어야 합니다.<br /><br /> Teradata 기반 모델을 사용하려면 Teradata의 .NET Data Provider for Teradata 필요<br /><br /> 플랫폼 지원에 대한 자세한 내용은 Teradata 설명서를 참조하십시오.|해당 사항 없음|해당 사항 없음|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상에서 모델을 만들 수 있습니다.<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]<br /><br /> Oracle 9.2.0.3 이상<br /><br /> Teradata V14, v13, v12 및 v6.2|N|N|  
|SAP 다차원 데이터베이스|SAP BW|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|플랫폼 지원에 대한 자세한 내용은 SAP 설명서를 참조하십시오.|해당 사항 없음|해당 사항 없음|SAP BW 7.0-7.5|Y|해당 사항 없음|  
|[!INCLUDE[extEssbase](../../includes/extessbase-md.md)]|[Hyperion Essbase](#Hyperion)|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|플랫폼 지원에 대한 자세한 내용은 Hyperion 설명서를 참조하십시오.|Y|해당 사항 없음|[!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 9.3.1|Y|해당 사항 없음|  
|Oracle 관계형 데이터베이스|[Oracle](#OracleClient)|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|Oracle 클라이언트 구성 요소 12c 이상 필요|Y|해당 사항 없음|Oracle 11g, 11g R2, 12c|Y|Y|  
|Teradata 관계형 데이터베이스|[Teradata](#Teradata)|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|Teradata의 .NET Data Provider for Teradata 확장<br /><br /> Teradata의 .NET Data Provider for Teradata 필요<br /><br /> 플랫폼 지원에 대한 자세한 내용은 Teradata 설명서를 참조하십시오.|Y|해당 사항 없음|Teradata v15<br /><br />Teradata v14<br /><br /> Teradata v13|Y|N|  
|DB2 관계형 데이터베이스|사용자 지정 및 등록된 데이터 확장 프로그램 이름||2004 Host Integration (HI) Server<br /><br /> [HI Server 설명서](https://msdn.microsoft.com/library/gg241192\(v=bts.10\).aspx)(영문)를 참조하세요.|Y|해당 사항 없음|해당 사항 없음|Y|N|  
|일반 OLE DB 데이터 원본|OLEDB|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|OLE DB를 지원하는 모든 데이터 원본<br /><br /> 플랫폼 지원에 대한 자세한 내용은 데이터 원본 설명서를 참조하십시오.|Y|해당 사항 없음|OLE DB를 지원하는 모든 데이터 원본 [참고](#OLEDBStandard)를 참조하십시오.|Y|해당 사항 없음|  
|일반 ODBC 데이터 원본|[ODBC](#ODBCGeneric)|기본 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램|ODBC를 지원하는 모든 데이터 원본.<br /><br /> 플랫폼 지원에 대한 자세한 내용은 데이터 원본 설명서를 참조하십시오.|Y|해당 사항 없음|ODBC를 지원하는 모든 데이터 원본. [참고](#ODBCGeneric)를 참조하십시오.|Y|Y|  
  
 외부 데이터 원본 사용에 대한 자세한 내용은 [외부 데이터 원본의 데이터 추가&#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)를 참조하세요.  
  
 타사를 통해 사용할 수 있는 많은 표준 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자가 있습니다. 자세한 내용을 보려면 타사 웹 사이트나 포럼을 검색하십시오.  
  
 사용자 지정 데이터 처리 확장 프로그램이나 표준 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 설치하고 등록하려면 데이터 공급자 참조 설명서를 참조해야 합니다. 자세한 내용은 [표준 .NET Framework 데이터 공급자 등록&#40;SSRS&#41;](../../reporting-services/report-data/register-a-standard-net-framework-data-provider-ssrs.md)을 참조하세요.  
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
## <a name="reporting-services-data-processing-extensions"></a>Reporting Services 데이터 처리 확장 프로그램  
 다음 데이터 처리 확장 프로그램은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]와 함께 자동으로 설치됩니다. 자세한 내용을 보고 설치를 확인하려면 [RSReportDesigner 구성 파일](../../reporting-services/report-server/rsreportdesigner-configuration-file.md) 및 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 처리 확장 프로그램은 현재 지원되지 않습니다.  
  
 보고서 작성기에서 지원하는 데이터 처리 확장 프로그램에 대한 자세한 내용은 msdn.microsoft.com의 [보고서 작성기 설명서](https://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34) 에서 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](https://go.microsoft.com/fwlink/?LinkId=154494) 을 참조하세요.  
  
###  <a name="MicrosoftSQLServer"></a> Microsoft SQL Server 데이터 처리 확장 프로그램  
 데이터 원본 유형 **Microsoft SQL Server** 는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 래핑하고 확장합니다. 이 데이터 처리 확장 프로그램은 x86 및 [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]기반 플랫폼에 대해 기본적으로 컴파일되고 실행됩니다.  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]에서 이 데이터 확장 프로그램과 연결된 쿼리 디자이너는 Visual Database Tool 디자이너입니다. 그래픽 모드에서 이 쿼리 디자이너를 사용하면 쿼리가 분석되고 다시 작성될 수 있습니다. 쿼리에 사용되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문을 정확히 제어하려면 텍스트 기반 쿼리 디자이너를 사용합니다. 자세한 내용은 [Graphical Query Designer User Interface](../../reporting-services/report-data/graphical-query-designer-user-interface.md)을 참조하세요.  
  
 자세한 내용은 [SQL Server 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)을 참조하세요.  
  
 보고서 작성기에서 이 데이터 확장 프로그램과 연결된 쿼리 디자이너는 관계형 쿼리 디자이너입니다. 
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
###  <a name="Azure"></a> Microsoft Azure SQL Database 처리 확장 프로그램  
 데이터 원본 유형 **Microsoft Azure[!INCLUDE[ssSDS](../../includes/sssds-md.md)]** 는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 래핑하고 확장합니다.  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]에서 이 데이터 확장 프로그램과 연결된 그래픽 쿼리 디자이너는 **Microsoft SQL Server**데이터 원본 유형과 함께 사용하는 Visual Database Tool 디자이너가 아닌 관계형 쿼리 디자이너입니다.  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]는 **Microsoft Azure[!INCLUDE[ssSDS](../../includes/sssds-md.md)]** 와 **Microsoft SQL Server** 데이터 원본 유형을 자동으로 구별하여 해당 데이터 원본 유형과 연결된 그래픽 쿼리 디자이너를 엽니다.  
  
 그래픽 모드에서 이 쿼리 디자이너를 사용하면 쿼리가 분석되고 다시 작성될 수 있습니다. 텍스트 기반 쿼리 디자이너를 사용하여 쿼리를 작성할 수도 있습니다. 쿼리에 사용되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문을 정확히 제어하려면 텍스트 기반 쿼리 디자이너를 사용합니다.   
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서의 데이터 검색은 SQL Data Warehouse 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 비슷하지만 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에는 몇 가지 요구 사항이 적용됩니다. 자세한 내용은 [SQL Azure 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/sql-azure-connection-type-ssrs.md)을 참조하세요.  
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
###  <a name="PWD"></a> Microsoft SQL Server 병렬 데이터 웨어하우스 처리 확장 프로그램  
이 데이터 원본은 더 이상 사용되지 않습니다. SQL Server 데이터 원본 유형을 사용하여 Microsoft APS(분석 플랫폼)에 연결합니다.
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
###  <a name="AnalysisServices"></a> Microsoft SQL Server Analysis Services 데이터 처리 확장 프로그램  
 데이터 원본 유형 **Microsoft SQL Server Analysis Services**를 선택하면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. 이 데이터 처리 확장 프로그램은 x86 및 x64 기반 플랫폼에 대해 기본적으로 컴파일되고 실행됩니다.  
  
 이 데이터 공급자는 ADOMD.NET 개체 모델을 사용하여 XMLA(XML for Analysis) 버전 1.1을 사용하는 쿼리를 만듭니다. 결과는 일반 행 집합으로 반환됩니다. 자세한 내용은 [MDX용 Analysis Services 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md), [DMX용 Analysis Services 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md), [Analysis Services MDX 쿼리 디자이너 사용자 인터페이스](../../reporting-services/report-data/analysis-services-mdx-query-designer-user-interface.md) 및 [Analysis Services DMX 쿼리 디자이너 사용자 인터페이스](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)를 참조하세요.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본에 연결할 때 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 처리 확장 프로그램은 다중값 매개 변수를 지원하고 셀 및 멤버 속성을 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 지원되는 확장 속성에 매핑합니다. 자세한 내용은 [Analysis Services 데이터베이스에 대한 확장 필드 속성 &#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본의 모델도 만들 수 있습니다.  
  
###  <a name="OLEDBAll"></a> OLE DB Data Processing Extension  
 OLE DB 데이터 처리 확장 프로그램을 사용하려면 보고서에 사용할 데이터 원본의 버전을 기반으로 추가 데이터 공급자 계층을 선택해야 합니다. 특정 데이터 공급자를 선택하지 않으면 기본값이 제공됩니다. 데이터 원본 또는 공유 데이터 원본 대화 상자의 **편집** 단추를 통해 액세스하는 **연결 속성** 대화 상자를 사용하여 특정 데이터 공급자를 선택합니다.  
  
 OLE DB 연결된 쿼리 디자이너에 대한 자세한 내용은 [그래픽 쿼리 디자이너 사용자 인터페이스](../../reporting-services/report-data/graphical-query-designer-user-interface.md)를 참조하세요. 특정 OLE DB 공급자 지원에 대한 자세한 내용은 [기술 자료의](http://support.microsoft.com/default.aspx/kb/811241) 특정 OLE DB 공급자에 대한 Visual Studio .NET 디자이너 도구의 지원(Visual Studio .NET Designer Tool Supports Specific OLE DB Providers) [!INCLUDE[msCoName](../../includes/msconame-md.md)] 을 참조하십시오.  
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
####  <a name="OLEDBSQL"></a> SQL Server용 OLE DB  
 데이터 원본 유형 **OLE DB**를 선택하면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Data Provider for OLE DB를 확장하는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 처리 확장 프로그램이 선택됩니다. 이 데이터 처리 확장 프로그램은 x86 및 x64 플랫폼에 대해 기본적으로 컴파일되고 실행됩니다.  
  
 자세한 내용은 [OLE DB 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)을 참조하세요.  
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
#### <a name="ole-db-for-olap-70"></a>OLAP 7.0용 OLE DB  
 OLE DB Provider for OLAP Services 7.0은 지원되지 않습니다.  
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
####  <a name="OracleOLEDB"></a> Oracle용 OLE DB  
 데이터 처리 확장 프로그램인 Oracle용 OLE DB는 Oracle 데이터 형식 중 BLOB, CLOB, NCLOB, BFILE, UROWID를 지원하지 않습니다.  
  
 이 확장 프로그램은 위치에 종속적인 명명되지 않은 매개 변수를 지원하지만 명명된 매개 변수는 지원하지 않습니다. 명명된 매개 변수를 사용하려면 [Oracle](#OracleClient) 데이터 처리 확장 프로그램을 사용합니다.  
  
 Oracle을 데이터 원본으로 구성하는 방법은 [Reporting Services를 사용하여 Oracle 데이터 원본을 구성하고 액세스하는 방법(How to use Reporting Services to configure and to access an Oracle data source)](http://support.microsoft.com/kb/834305)을 참조하십시오. 추가 사용 권한 구성에 대한 자세한 내용은 [기술 자료에서](http://support.microsoft.com/kb/870668) NETWORK SERVICE 보안 주체에 대한 사용 권한을 추가하는 방법 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 을 참조하세요.  
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
####  <a name="OLEDBStandard"></a> OLE DB 표준 .NET Framework 데이터 공급자  
 OLE DB [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 지원하는 데이터 원본에서 데이터를 검색하려면 **OLE DB** 데이터 원본 유형을 사용하고 기본 데이터 공급자를 선택하거나 **연결 문자열** 대화 상자의 설치된 데이터 공급자에서 선택합니다.  
  
> [!NOTE]  
>  데이터 공급자가 보고서 제작 클라이언트에서 보고서 미리 보기 작업을 지원할 수 있지만 모든 OLE DB 데이터 공급자가 보고서 서버에 게시된 보고서를 지원하는 것은 아닙니다.  
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
###  <a name="ODBC"></a> ODBC Data Processing Extension  
 데이터 원본 유형 **ODBC**를 선택하면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Data Provider for ODBC를 확장하는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 처리 확장 프로그램이 선택됩니다. 이 데이터 처리 확장 프로그램은 x86, 및 [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)] 플랫폼에 대해 기본적으로 컴파일되고 실행됩니다. 이 확장 프로그램을 사용하여 ODBC 공급자가 있는 모든 데이터 원본에 연결하고 이 데이터 원본에서 데이터를 검색할 수 있습니다.  
  
> [!NOTE]  
>  데이터 공급자가 보고서 제작 클라이언트에서 보고서 미리 보기 작업을 지원할 수 있지만 모든 ODBC 데이터 공급자가 보고서 서버에 게시된 보고서를 지원하는 것은 아닙니다.  
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
####  <a name="ODBCGeneric"></a> ODBC 표준 .NET Framework 데이터 공급자  
 표준 ODBC [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 지원하는 데이터 원본에서 데이터를 검색하려면 **ODBC** 데이터 원본 유형을 사용하고 기본 데이터 공급자를 선택하거나 **연결 문자열** 대화 상자의 설치된 데이터 공급자에서 선택합니다.  
  
> [!NOTE]  
>  데이터 공급자가 보고서 제작 클라이언트에서 보고서 미리 보기 작업을 지원할 수 있지만 모든 ODBC 데이터 공급자가 보고서 서버에 게시된 보고서를 지원하는 것은 아닙니다.  
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
###  <a name="OracleClient"></a> Oracle 데이터 처리 확장 프로그램  
 데이터 원본 형식 **Oracle**을 선택하는 경우 Oracle Data Provider를 직접 사용하고 System.Data.OracleClient를 통해 더 이상 가지 않는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램을 선택합니다. Oracle 데이터베이스에서 보고서 데이터를 검색하려면 관리자가 Oracle 클라이언트 도구를 설치해야 합니다. 클라이언트 응용 프로그램 버전은 11g 이상이어야 합니다. 이러한 도구는 보고서를 미리 보려는 경우 보고서 제작 클라이언트에 설치되어 있어야 하고 게시된 보고서를 보려는 경우 보고서 서버에 설치되어 있어야 합니다.  
 
Oracle 클라이언트 도구를 설치하기 위해 다음을 수행할 수 있습니다.
 
1.  [Oracle의 다운로드 사이트](http://www.oracle.com/us/products/tools/index-090165.html)로 이동
2.  Windows(서버에 대해 64비트, 도구에 대해 32비트)용 ODAC 12c 릴리스 4(12.1.0.2.4) 다운로드
3.  Data Provider for .NET 4 설치
  
 이 확장 프로그램은 명명된 매개 변수를 지원합니다. Oracle 버전 11g 이상의 경우 다중값 매개 변수가 지원됩니다. 위치에 종속적인 명명되지 않은 매개 변수의 경우 데이터 공급자 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Oracle과 함께 OLE DB 데이터 처리 확장 프로그램을 사용합니다. Oracle을 데이터 원본으로 구성하는 방법은 [Reporting Services를 사용하여 Oracle 데이터 원본을 구성하고 액세스하는 방법(How to use Reporting Services to configure and to access an Oracle data source)](http://support.microsoft.com/kb/834305)을 참조하십시오. 추가 사용 권한 구성에 대한 자세한 내용은 [기술 자료에서](http://support.microsoft.com/kb/870668) NETWORK SERVICE 보안 주체에 대한 사용 권한을 추가하는 방법 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 을 참조하세요.  
  
 다중 입력 매개 변수를 사용하여 저장 프로시저에서 데이터를 검색할 수 있지만 저장 프로시저는 하나의 출력 커서만 반환해야 합니다. 자세한 내용은 [DataReader를 사용하여 데이터 검색(Retrieving Data Using the DataReader)](https://go.microsoft.com/fwlink/?LinkId=81758)의 Oracle 섹션을 참조하십시오.  
  
 자세한 내용은 [Oracle 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/oracle-connection-type-ssrs.md)을 참조하세요. 연결된 쿼리 디자이너에 대한 자세한 내용은 [그래픽 쿼리 디자이너 사용자 인터페이스](../../reporting-services/report-data/graphical-query-designer-user-interface.md)를 참조하세요.  
  
 Oracle 데이터베이스를 기반으로 모델을 만들 수도 있습니다.  
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
###  <a name="Teradata"></a> Teradata 데이터 처리 확장 프로그램  
 데이터 원본 유형 **Teradata**를 선택하면 .NET Framework Data Provider for Teradata를 확장하는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램이 선택됩니다. Teradata 데이터베이스에서 보고서 데이터를 검색하려면 시스템 관리자가 클라이언트에서 보고서를 편집 및 미리 보기 위한 보고서 제작 클라이언트와 게시된 보고서를 보기 위한 보고서 서버에 .NET Framework Data Provider for Teradata를 설치해야 합니다.  
  
 보고서 서버 프로젝트의 경우 이 확장 프로그램에 대해 그래픽 쿼리 디자이너를 사용할 수 없습니다. 쿼리를 만들려면 텍스트 기반 쿼리 디자이너를 사용해야 합니다.  
  
 다음 표에서는 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]의 보고서 정의에서 데이터 원본을 정의하기 위해 지원되는 .NET Data Provider for Teradata 버전을 보여 줍니다.  
  
|[!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] 버전|Teradata 데이터베이스 버전|.NET Framework Data Provider for Teradata 버전|  
|-----------------------------------|-------------------------------|-------------------------------------------------------|    
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|14.00|14.00.01| 
|SQL Server 2016|13.00|13.0.0.1|  
|SQL Server 2016|14.00|14.00.01|
|SQL Server 2016|15.00|15.00.01| 
  
 이 확장 프로그램은 다중값 매개 변수를 지원하지 않습니다. TEXT 쿼리 모드에서 EXECUTE 명령을 사용하여 쿼리에 매크로를 지정할 수 있습니다.  
  
 자세한 내용은 [Teradata 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/teradata-connection-type-ssrs.md)을 참조하세요.  
  
 Teradata 데이터베이스를 기반으로 모델을 만들 수도 있습니다. 자세한 내용은 Teradata 사이트의 [Microsoft SQL Server 2012 Reporting Services 및 Teradata Corporation](http://www.teradata.com/white-papers/Microsoft-SQL-Server-2012-Reporting-Services-and-Teradata-Corporation/?type=WP)백서를 참조하세요.  
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
###  <a name="SharePointList"></a> SharePoint 목록 데이터 확장 프로그램  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 목록 데이터 확장 프로그램이 포함되어 있으므로 보고서에서 SharePoint 목록을 데이터 원본으로 사용할 수 있습니다. 다음에서 목록 데이터를 검색할 수 있습니다.  
  
-   SharePoint Server 2016  

-   [!INCLUDE[SPS2013](../../includes/sps2013-md.md)]  
  
 SharePoint 목록 데이터 공급자 구현에는 세 가지가 있습니다.  
  
1.  [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]의 보고서 디자이너 또는 보고서 작성기와 같은 보고서 작성 환경에서 또는 기본 모드에서 구성된 보고서 서버의 경우 목록 데이터는 SharePoint 사이트의 Lists.asmx 웹 서비스에서 제공됩니다.  
  
2.  SharePoint 통합 모드에서 구성된 보고서 서버에서 목록 데이터는 해당하는 Lists.asmx 웹 서비스 또는 SharePoint API에 대한 프로그래밍 방식 호출에서 제공됩니다. 이 모드에서는 SharePoint 팜의 목록 데이터를 검색할 수 있습니다.  
  
3.  [!INCLUDE[SPS2013](../../includes/sps2013-md.md)] 및 SharePoint Server 2016의 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 기술용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 사용하면 SharePoint 사이트의 Lists.asmx 웹 서비스 또는 SharePoint 팜의 일부분인 SharePoint 사이트에서 목록 데이터를 검색할 수 있습니다. 이 시나리오는 보고서 서버가 필요하지 않으므로 *로컬 모드* 라고도 합니다.  
  
 지정할 수 있는 자격 증명은 클라이언트 응용 프로그램에서 사용하는 구현에 따라 다릅니다. 자세한 내용은 [SharePoint 목록 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/sharepoint-list-connection-type-ssrs.md)을 참조하세요.  
  
###  <a name="XML"></a> XML 데이터 처리 확장 프로그램  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에 포함된 XML 데이터 처리 확장 프로그램을 사용하여 보고서에 XML 데이터를 사용할 수 있습니다. URL로 액세스할 수 있는 웹 기반의 응용 프로그램, 웹 서비스 또는 XML 문서에서 데이터를 검색할 수 있습니다. 자세한 내용은 [XML 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)을 참조하세요. 연결된 쿼리 디자이너에 대한 자세한 내용은 [그래픽 쿼리 디자이너 사용자 인터페이스](../../reporting-services/report-data/graphical-query-designer-user-interface.md)의 텍스트 기반 쿼리 디자이너 섹션을 참조하세요. 예를 보려면 [Reporting Services: XML 및 웹 서비스 데이터 원본 사용(Reporting Services: Using XML and Web Service Data Sources)](https://go.microsoft.com/fwlink/?LinkId=81654)을 참조하십시오.  
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
###  <a name="SAPBW"></a> SAP BW 데이터 처리 확장 프로그램  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 보고서의 SAP BW 데이터 원본에서 데이터를 사용할 수 있도록 하는 데이터 처리 확장 프로그램을 포함합니다.
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
###  <a name="Hyperion"></a> Hyperion Essbase Business Intelligence 데이터 처리 확장 프로그램  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 보고서의 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 데이터 원본에서 데이터를 사용할 수 있도록 하는 데이터 처리 확장 프로그램을 포함합니다.  
  
 자세한 내용은 [Hyperion Essbase 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/hyperion-essbase-connection-type-ssrs.md)을 참조하세요. 연결된 쿼리 디자이너에 대한 자세한 내용은 [Hyperion Essbase Query Designer User Interface](../../reporting-services/report-data/hyperion-essbase-query-designer-user-interface.md)를 참조하십시오.  
  
 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]에 대한 자세한 내용은 [Hyperion Essbase와 함께 SQL Server 2005 Reporting Services 사용](https://go.microsoft.com/fwlink/?LinkId=81970)을 참조하십시오.  
  
 [데이터 원본 표로 돌아가기](#DataSourcesTable)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [보고서 데이터 집합&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 추가 질문이 있으신가요? [Reporting Services 포럼을 이용해 보세요.](https://go.microsoft.com/fwlink/?LinkId=620231)
  
  

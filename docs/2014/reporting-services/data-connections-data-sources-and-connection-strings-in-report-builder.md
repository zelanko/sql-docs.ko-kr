---
title: 데이터 연결, 데이터 원본 및 보고서 작성기에서 연결 문자열 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10421"
ms.assetid: 7e103637-4371-43d7-821c-d269c2cc1b34
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 13edc28a739af6a40ab47766c1909be3a8105ee5
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56288871"
---
# <a name="data-connections-data-sources-and-connection-strings-in-report-builder"></a>보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열
  보고서에 데이터를 포함하려면 데이터 연결 및 데이터 집합을 만듭니다. 데이터 연결에는 외부 데이터 원본에 액세스하는 방법에 대한 정보가 포함됩니다. 데이터 집합에는 데이터 연결을 사용하여 포함할 데이터를 지정하는 쿼리 명령이 포함됩니다.  
  
1.  **보고서 데이터 창의 데이터 원본** 포함된 데이터 원본을 만들거나 공유 데이터 원본을 추가하면 데이터 원본이 보고서 데이터 창에 표시됩니다.  
  
2.  **연결 대화 상자** 연결 대화 상자를 사용하여 연결 문자열을 작성하거나 붙여 넣습니다.  
  
3.  **데이터 연결 정보** 연결 문자열은 데이터 확장 프로그램에 전달됩니다.  
  
4.  **자격 증명** 자격 증명은 연결 문자열과 별도로 관리됩니다.  
  
5.  **데이터 확장 프로그램/데이터 공급자** 여러 데이터 액세스 계층을 통해 데이터에 연결할 수 있습니다.  
  
6.  **외부 데이터 원본** 관계형 데이터베이스,  다차원 데이터베이스,  SharePoint  목록,  웹 서비스 또는 보고서 모델에서 데이터를 검색합니다.  
  
 자세한 내용은 [포함 및 공유 데이터 연결 또는 데이터 원본 &#40;보고서 작성기 및 SSRS&#41; ](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md) 하 고 [데이터 연결, 데이터 원본 및 Reporting Services의에서연결문자열](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 데이터는 미리 정의된 공유 데이터 원본, 공유 데이터 집합 및 보고서 파트를 사용하여 보고서에 포함될 수도 있습니다. 이러한 항목에는 이미 필요한 데이터 연결 정보가 있습니다. 자세한 내용은 [보고서에 데이터 추가 &#40;보고서 작성기 및 SSRS&#41;](report-data/report-datasets-ssrs.md)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
 ![rs_DataSourcesStory](media/rs-datasourcesstory.gif "rs_DataSourcesStory")  
  
##  <a name="ConnectionString"></a> 연결 문자열 예  
 데이터 연결에는 일반적으로 외부 데이터 원본의 소유자가 제공하는 연결 문자열이 포함되어 있습니다. 다음 표에는 여러 유형의 외부 데이터 원본에 대한 연결 문자열의 예가 나와 있습니다.  
  
|**데이터 원본**|**예제**|**설명**|  
|---------------------|-----------------|---------------------|  
|로컬 서버의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스|`data source="(local)";initial catalog=AdventureWorks2012`|데이터 원본 유형을 `SQL Server`로 설정합니다.|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 데이터베이스|`Data Source=localhost\MSSQL12.InstanceName; Initial Catalog= AdventureWorks2012`|데이터 원본 유형을 `SQL Server`로 설정합니다.|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express 데이터베이스|`Data Source=localhost\MSSQL12.SQLEXPRESS; Initial Catalog= AdventureWorks2012`|데이터 원본 유형을 `SQL Server`로 설정합니다.|  
|로컬 서버의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스|`data source=localhost;initial catalog=Adventure Works DW 2012`|데이터 원본 유형을 `SQL Server Analysis Services`로 설정합니다.|  
|SharePoint 목록|`data source=http://MySharePointWeb/MySharePointSite/`|데이터 원본 유형을 `SharePoint List`로 설정합니다.|  
||||  
|보고서 모델|이 오류에는 이 작업을 적용할 수 없습니다.|보고서 모델에 대한 연결 문자열은 필요하지 않습니다. 보고서 작성기에서 보고서 서버로 이동하고 보고서 모델인 .smdl 파일을 선택합니다.|  
|Oracle 서버|`data source=myserver`|데이터 원본 유형을 `Oracle`로 설정합니다. Oracle 클라이언트 도구는 보고서 작성기 컴퓨터와 보고서 서버에 설치되어야 합니다.|  
|SAP NetWeaver BI 데이터 원본|`DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|데이터 원본 유형을 `SAP NetWeaver BI`로 설정합니다.|  
|Hyperion Essbase 데이터 원본|`Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample`|데이터 원본 유형을 `Hyperion Essbase`로 설정합니다.|  
|Teradata 데이터 원본|`data source=` *\<NN>.\<NNN>.\<NNN>.\<N>* `;`|데이터 원본 유형을 `Teradata`로 설정합니다. 연결 문자열은 1자리부터 3자리 숫자까지 허용되는 필드 네 개로 구성된 형식의 IP(인터넷 프로토콜) 주소입니다.|  
|Teradata 데이터 원본|`Database=` *\<데이터베이스 이름>* `; data source=` *\<NN*N *>.\<NNN>.\<NNN>.\<N*NN*>*`;Use X Views=False;Restrict to Default Database=True`|앞의 예와 마찬가지로 데이터 원본 유형을 `Teradata`로 설정합니다. Database 태그에 지정된 기본 데이터베이스만 사용하고 데이터 관계를 자동으로 검색하지 마십시오.|  
|XML 데이터 원본, 웹 서비스|`data source=http://adventure-works.com/results.aspx`|데이터 원본 유형을 `XML`로 설정합니다. 연결 문자열은 WSDL(Web Services Definition Language)을 지원하는 웹 서비스의 URL입니다.|  
|XML 데이터 원본, XML 문서|`http://localhost/XML/Customers.xml`|데이터 원본 유형을 `XML`로 설정합니다. 연결 문자열은 XML 문서의 URL입니다.|  
|XML 데이터 원본, 포함된 XML 문서|*비어 있음*|데이터 원본 유형을 `XML`로 설정합니다. XML 데이터는 보고서 정의에 포함됩니다.|  
  
 각 연결 형식에 대 한 자세한 내용은 참조 하세요. [외부 데이터 원본의 데이터 추가 &#40;SSRS&#41; ](report-data/add-data-from-external-data-sources-ssrs.md) 하 고 [Data Sources Supported by Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md).  
  

  
##  <a name="Creating"></a> 데이터 원본 만들기  
 포함된 데이터 원본을 만들려면 데이터에 액세스하는 데 필요한 자격 증명과 연결 문자열이 있어야 합니다. 이 정보는 대개 데이터 원본의 소유자가 제공합니다. 데이터 연결은 데이터 원본의 일부로 보고서 정의에 저장됩니다. 자격 증명은 연결과 독립적으로 관리됩니다. 단계별 지침은 [데이터 연결이 나 데이터 원본 추가 및 확인 &#40;보고서 작성기 및 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)합니다.  
  
> [!NOTE]  
>  몇 가지 유형의 자격 증명 보고서 작성기를 사용 하는 모든 시나리오를 지원 하지 않을 수 있습니다: 쿼리 디자이너에서 쿼리를 실행 하려면 보고서 서버에 연결 되어 있지 컴퓨터에서 보고서를 미리 보고 보고서 서버에서 보고서를 실행 합니다. 가능한 경우 항상 공유 데이터 원본을 사용하는 것이 좋습니다. 보고서 서버에 공유 데이터 원본에 대한 자격 증명을 저장할 수 있습니다. 자세한 내용은 [보고서 작성기에 자격 증명 지정](../../2014/reporting-services/specify-credentials-in-report-builder.md)을 참조하세요.  
  
 공유 데이터 원본을 만들려면 보고서 서버에서 직접 데이터 소스를 만들려면 보고서 관리자를 사용 하거나 등의 보고서 디자이너 제작 환경을 사용 해야 합니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]합니다. 자세한 내용은 [포함 또는 공유 데이터 원본 만들기 &#40;SSRS&#41;](../../2014/reporting-services/create-an-embedded-or-shared-data-source-ssrs.md)합니다.  
  

  
## <a name="see-also"></a>관련 항목  
 [보고서에 데이터 추가 &#40;보고서 작성기 및 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [보고서 파트&#40;보고서 작성기 및 SSRS&#41;](report-parts-report-builder-and-ssrs.md)  
  
  

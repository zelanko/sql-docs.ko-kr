---
title: 데이터 연결 문자열 만들기 - 보고서 작성기 및 SSRS | Microsoft Docs
ms.date: 11/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 73bf9e24ffb42ef93547097c53b5838a22292fda
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74190920"
---
# <a name="create-data-connection-strings---report-builder--ssrs"></a>데이터 연결 문자열 만들기 - 보고서 작성기 및 SSRS

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 페이지가 매겨진 보고서에 데이터를 포함하려면 먼저 *데이터 원본*에 *연결 문자열*을 만들어야 합니다. 이 문서에서는 데이터 연결 문자열을 만드는 방법 및 데이터 원본 자격 증명과 관련된 중요 정보를 설명합니다. 데이터 원본에는 데이터 원본 유형, 연결 정보 및 사용할 자격 증명의 유형이 포함됩니다. 자세한 배경 정보는 [SSRS(SQL Server Reporting Services)의 보고서 데이터 소개](report-data-ssrs.md)를 참조하세요.
  
##  <a name="bkmk_DataConnections"></a> 기본 제공 데이터 확장  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 기본 데이터 확장에는 Microsoft SQL Server, Microsoft Azure SQL Database 및 Microsoft SQL Server Analysis Services가 포함됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 지원하는 데이터 원본 및 버전의 전체 목록은 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)을 참조하세요.  
  
##  <a name="bkmk_connection_examples"></a> 자주 사용하는 연결 문자열 예  
 연결 문자열은 데이터 공급자에 대한 연결 속성의 텍스트 표현입니다. 다음 표에서는 다양한 데이터 연결 형식에 대한 연결 문자열의 예를 보여 줍니다.  
 
 > [!NOTE]  
>  [Connectionstrings.com](https://www.connectionstrings.com/) 은 연결 문자열에 대한 예제를 가져올 수 있는 다른 리소스입니다. 
  
|**데이터 원본**|**예제**|**설명**|  
|---------------------|-----------------|---------------------|  
|로컬 서버의 SQL Server 데이터베이스|`data source="(local)";initial catalog=AdventureWorks`|데이터 원본 유형을 **Microsoft SQL Server**로 설정합니다. 자세한 내용은 [SQL Server 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)을 참조하세요.|  
|SQL Server 인스턴스<br /><br /> 데이터베이스|`Data Source=localhost\MSSQL13.<InstanceName>; Initial Catalog=AdventureWorks`|데이터 원본 유형을 **Microsoft SQL Server**로 설정합니다.|  
|Azure SQL Database|`Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True`|데이터 원본 유형을 **Microsoft Azure SQL Database**로 설정합니다. 자세한 내용은 [SQL Azure 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/sql-azure-connection-type-ssrs.md)을 참조하세요.|  
|SQL Server 병렬 데이터 웨어하우스|`HOST=<IP address>;database= AdventureWorks; port=<port>`|데이터 원본 유형을 **Microsoft SQL Server Parallel Data Warehouse**로 설정합니다. 자세한 내용은 [SQL Server 병렬 데이터 웨어하우스 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/sql-server-parallel-data-warehouse-connection-type-ssrs.md)을 참조하세요.|  
|로컬 서버의 Analysis Services 데이터베이스|`data source=localhost;initial catalog=Adventure Works DW`|데이터 원본 유형을 **Microsoft SQL Server Analysis Services**로 설정합니다. 자세한 내용은 [MDX용 Analysis Services 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md) 또는 [DMX용 Analysis Services 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)을 참조하세요.|  
|Sales 큐브 뷰가 있는 Analysis Services 테이블 형식 model 데이터베이스|`Data source=<servername>;initial catalog= Adventure Works DW;cube='Sales'`|데이터 원본 유형을 **Microsoft SQL Server Analysis Services**로 설정합니다. cube= 설정에 큐브 뷰 이름을 지정합니다. 자세한 내용은 [큐브 뷰&#40;SSAS 테이블 형식&#41;](https://docs.microsoft.com/analysis-services/tabular-models/perspectives-ssas-tabular)를 참조하세요.|  
|Oracle 서버|`data source=myserver`|데이터 원본 유형을 **Oracle**로 설정합니다. Oracle 클라이언트 도구는 보고서 디자이너 컴퓨터와 보고서 서버에 설치해야 합니다. 자세한 내용은 [Oracle 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/oracle-connection-type-ssrs.md)을 참조하세요.|  
|SAP NetWeaver BI 데이터 원본|`DataSource=https://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|데이터 원본 유형을 **SAP NetWeaver BI**로 설정합니다. 자세한 내용은 [SAP NetWeaver BI 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/sap-netweaver-bi-connection-type-ssrs.md)을 참조하세요.|  
|Hyperion Essbase 데이터 원본|`Data Source=https://localhost:13080/aps/XMLA; Initial Catalog=Sample`|데이터 원본 유형을 **Hyperion Essbase**로 설정합니다. 자세한 내용은 [Hyperion Essbase 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/hyperion-essbase-connection-type-ssrs.md)을 참조하세요.|  
|Teradata 데이터 원본|`data source=`\<NNN>.\<NNN>.\<NNN>.\<NNN>`;`|데이터 원본 유형을 **Teradata**로 설정합니다. 연결 문자열은 1자리부터 3자리 숫자까지 허용되는 필드 네 개로 구성된 형식의 IP(인터넷 프로토콜) 주소입니다. 자세한 내용은 [Teradata 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/teradata-connection-type-ssrs.md)을 참조하세요.|  
|Teradata 데이터 원본|`Database=` *\<데이터베이스 이름>* `; data source=` *\<NN*N *>.\<NNN>.\<NNN>.\<N*NN *>* `;Use X Views=False;Restrict to Default Database=True`|앞의 예와 마찬가지로 데이터 원본 유형을 **Teradata**로 설정합니다. Database 태그에 지정된 기본 데이터베이스만 사용하고 데이터 관계를 자동으로 검색하지 마십시오.|  
|XML 데이터 원본, 웹 서비스|`data source=https://adventure-works.com/results.aspx`|데이터 원본 유형을 **XML**로 설정합니다. 연결 문자열은 WSDL(Web Services Definition Language)을 지원하는 웹 서비스의 URL입니다. 자세한 내용은 [XML 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)을 참조하세요.|  
|XML 데이터 원본, XML 문서|`https://localhost/XML/Customers.xml`|데이터 원본 유형을 **XML**로 설정합니다. 연결 문자열은 XML 문서의 URL입니다. 
|XML 데이터 원본, 포함된 XML 문서|*비어 있음*|데이터 원본 유형을 **XML**로 설정합니다. XML 데이터는 보고서 정의에 포함됩니다.|  
|SharePoint 목록|`data source=https://MySharePointWeb/MySharePointSite/`|데이터 원본 유형을 **SharePoint List**로 설정합니다.|  
| Power BI Premium 데이터 세트(Reporting Services 2019부터) | Server=powerbi://api.powerbi.com/v1.0/myorg/<workspacename>;initial catalog = <YourDatasetName> | 데이터 원본 유형을 **Microsoft SQL Server Analysis Services**로 설정합니다. |

  
 **localhost**를 사용하여 보고서 서버에 연결하지 못하는 경우 TCP/IP 프로토콜에 대한 네트워크 프로토콜이 설정되어 있는지 확인합니다. 자세한 내용은 [Configure Client Protocols](../../database-engine/configure-windows/configure-client-protocols.md)을 참조하세요.  
  
 각각의 데이터 원본 유형에 연결하는 데 필요한 구성에 대한 자세한 내용은 [외부 데이터 원본의 데이터 추가 &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) 또는 [Reporting Services에서 지원하는 데이터 원본 &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)의 해당 데이터 연결 문서를 참조하세요.  
  
##  <a name="bkmk_special_password_characters"></a> 암호의 특수 문자  
 암호를 입력하라는 메시지를 표시하거나 연결 문자열에 암호를 포함하도록 ODBC 또는 SQL 데이터 원본을 구성한 경우 사용자가 문장 부호와 같은 특수 문자가 포함된 암호를 입력하면 일부 기본 데이터 원본 드라이버가 해당 특수 문자의 유효성을 검사할 수 없습니다. 보고서 처리 시 "올바른 암호가 아닙니다" 메시지가 나타나면 이 문제 때문일 수 있습니다. 암호를 변경하는 것이 불가능한 경우 데이터베이스 관리자와 협력하여 서버에서 해당 자격 증명을 시스템 ODBC DSN(데이터 원본 이름)의 일부로 저장합니다. 자세한 내용은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 설명서의 [OdbcConnection.ConnectionString](https://docs.microsoft.com/dotnet/api/system.data.odbc.odbcconnection.connectionstring)을 참조하세요.  
  
##  <a name="bkmk_Expressions_in_connection_strings"></a> 식 기반 연결 문자열  
 식 기반 연결 문자열은 런타임에 평가됩니다. 예를 들어 데이터 원본을 매개 변수로 지정하고 연결 문자열에 매개 변수 참조를 포함하여 사용자가 보고서의 데이터 원본을 선택할 수 있도록 할 수 있습니다. 예를 들어 여러 국가에 데이터 서버를 보유하고 있는 다국적 기업의 경우 식 기반 연결 문자열을 사용하면 판매 보고서를 실행하는 사용자가 보고서를 실행하기 전에 특정 국가의 데이터 원본을 선택할 수 있습니다.  
  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 문자열에 데이터 원본 식을 사용하는 작업을 보여 줍니다. 이 예에서는 `ServerName`이라는 보고서 매개 변수를 만들었다고 가정합니다.  
  
```  
="data source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks"  
```  
  
 데이터 원본 식은 런타임에 또는 보고서를 미리 볼 때 처리됩니다. 식은 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]으로 작성해야 합니다. 다음 지침에 따라 데이터 원본 식을 정의합니다.  
  
-   정적 연결 문자열을 사용하여 보고서를 디자인합니다. 정적 연결 문자열이란 식을 통해 설정되지 않은 연결 문자열을 말합니다. 예를 들어 보고서별 데이터 원본 또는 공유 데이터 원본을 만드는 단계를 따르는 경우 정적 연결 문자열을 정의하게 됩니다. 정적 연결 문자열을 사용하면 보고서를 만드는 데 필요한 쿼리 결과를 가져올 수 있도록 보고서 디자이너의 데이터 원본에 연결할 수 있습니다.  
  
-   데이터 원본 연결을 정의할 때는 공유 데이터 원본을 사용하지 마세요. 공유 데이터 원본에서는 데이터 원본 식을 사용할 수 없습니다. 보고서에 대한 포함된 데이터 원본을 정의해야 합니다.  
  
-   연결 문자열과 별도로 자격 증명을 지정합니다. 저장된 자격 증명, 입력 정보를 요청하는 자격 증명 또는 통합 보안을 사용할 수 있습니다.  
  
-   보고서 매개 변수를 추가하여 데이터 원본을 지정합니다. 매개 변수 값으로는 사용 가능한 값(이 경우 사용 가능한 값은 보고서에 사용할 수 있는 데이터 원본이어야 함)의 정적 목록을 제공하거나 런타임에 데이터 원본 목록을 검색하는 쿼리를 정의할 수 있습니다.  
  
-   데이터 원본 목록에서 동일한 데이터베이스 스키마를 공유하는지 확인합니다. 모든 보고서 디자인은 스키마 정보로 시작됩니다. 보고서 정의에 사용되는 스키마와 런타임 시 보고서에 사용되는 실제 스키마가 일치하지 않으면 보고서가 실행되지 않을 수 있습니다.  
  
-   보고서를 게시하기 전에 정적 연결 문자열을 식으로 바꿉니다. 이때 정적 연결 문자열은 보고서 디자인을 완료한 다음에 식으로 바꿔야 합니다. 식을 사용한 다음에는 보고서 디자이너에서 쿼리를 실행할 수 없습니다. 또한 보고서 데이터 창의 필드 목록과 매개 변수 목록이 자동으로 업데이트되지 않습니다.  

## <a name="next-steps"></a>다음 단계

[SSRS(SQL Server Reporting Services)의 보고서 데이터 소개](report-data-ssrs.md)
[공유 데이터 원본 만들기 및 수정](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
[포함된 데이터 원본 만들기 및 수정](../../reporting-services/report-data/create-and-modify-embedded-data-sources.md)   
[배포 속성 설정](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
[보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)

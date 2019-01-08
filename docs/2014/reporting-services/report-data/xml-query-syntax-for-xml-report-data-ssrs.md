---
title: XML 보고서 데이터를 위한 XML 쿼리 구문(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- namespaces [Reporting Services]
- data processing extensions [Reporting Services], data sources
- xmldp [Reporting Services]
- XML [Reporting Services], data retrieval
ms.assetid: d203886f-faa1-4a02-88f5-dd4c217181ef
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4c8a1a3b41bd30702a04ce6cbb49b70bc561e508
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369895"
---
# <a name="xml-query-syntax-for-xml-report-data-ssrs"></a>XML 보고서 데이터를 위한 XML 쿼리 구문(SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 XML 데이터 원본에 대한 데이터 집합을 만들 수 있습니다. 데이터 원본을 정의한 후 데이터 세트에 대한 쿼리를 만듭니다. 데이터 원본이 가리키는 XML 데이터의 형식에 따라 XML `Query`나 요소 경로를 포함하여 데이터 집합 쿼리를 만듭니다. XML `Query` 로 시작 하는  **\<쿼리 >** 태그 및 네임 스페이스와 데이터 원본에 따라 달라 지는 XML 요소를 포함 합니다. 요소 경로는 네임스페이스로부터 독립적이며 기본 XML 데이터에서 사용할 노드 및 노드 특성을 XPath 형식 구문으로 지정합니다. 요소 경로에 대한 자세한 내용은 [XML 보고서 데이터를 위한 요소 경로 구문&#40;SSRS&#41;](report-data-ssrs.md)을 참조하세요.  
  
 다음과 같은 형식의 XML 데이터에 대한 XML 데이터 원본을 만들 수 있습니다.  
  
-   http 프로토콜을 사용하는 URL이 가리키는 XML 문서  
  
-   XML 데이터를 반환하는 웹 서비스 엔드포인트  
  
-   포함 XML 데이터  
  
 XML `Query`나 요소 경로를 지정하는 방법은 XML 데이터 형식에 따라 달라집니다.  
  
 XML 문서의 경우 XML `Query`는 선택 사항입니다. 이 쿼리가 포함되어 있지 않으면 선택적 XML `ElementPath`를 포함할 수 있습니다. XML `ElementPath` 값에는 요소 경로 구문이 사용됩니다. 데이터 원본의 XML 데이터에 필요한 경우 XML `Query` 및 XML `ElementPath`를 포함하여 네임스페이스를 올바르게 처리할 수 있습니다.  
  
 연결 문자열 URL이 가리키는 웹 서비스 엔드포인트의 경우 XML `Query`는 웹 서비스 메서드나 SOAP 동작 또는 둘 모두를 정의합니다. XML 데이터 공급자는 보고서에 사용할 XML 데이터를 검색하는 웹 서비스 요청을 만듭니다.  
  
> [!NOTE]  
>  웹 서비스 네임스페이스에 슬래시(`/)` 문자가 포함되어 있으면 XML 데이터 처리 확장 프로그램에서 해당 네임스페이스를 올바르게 가져올 수 있도록 웹 서비스 메서드와 SOAP 동작을 모두 포함하십시오.  
  
 포함 XML 문서의 경우 XML `Query`는 사용할 포함 XML 데이터를 정의하고 선택적 네임스페이스와 선택적 XML `ElementPath`를 포함합니다.  
  
## <a name="specifying-query-parameters-for-xml-data"></a>XML 데이터의 쿼리 매개 변수 지정  
 XML 문서의 쿼리 매개 변수를 지정할 수 있습니다.  
  
-   URL 요청의 경우 쿼리 매개 변수는 표준 URL 매개 변수로 포함됩니다.  
  
-   웹 서비스 요청의 경우 쿼리 매개 변수는 웹 서비스 메서드에 전달됩니다. 쿼리 매개 변수를 정의하려면 **데이터 세트 속성** 대화 상자의 **매개 변수** 페이지를 사용합니다. 자세한 내용은 [데이터 세트 속성 대화 상자, 매개 변수](dataset-properties-dialog-box-parameters.md)를 참조하세요.  
  
### <a name="example"></a>예제  
 다음 표의 예에서는 보고서 서버 웹 서비스, XML 문서 및 포함 XML 데이터에서 데이터를 검색하는 방법을 보여 줍니다.  
  
|XML 데이터 원본|쿼리 예|  
|---------------------|-------------------|  
|ListChildren 메서드에서 웹 서비스 XML 데이터입니다.|`<Query>`<br /><br /> `<Method Name="ListChildren" Namespace="https://schemas.microsoft.com/sqlserver/2005/06/30/reporting/reportingservices" />`<br /><br /> `</Query>`|  
|웹 서비스 XML 데이터(SoapAction 사용)|`<Query xmlns=namespace>`<br /><br /> `<SoapAction>http://schemas/microsoft.com/sqlserver/2005/03/23/reporting/reportingservices/ListChildren</SoapAction>`<br /><br /> `</Query>`|  
|네임스페이스를 사용하는 XML 문서 또는 포함 XML 데이터<br /><br /> 요소 경로의 네임스페이스를 지정하는 쿼리 요소|`<Query xmlns:es="https://schemas.microsoft.com/StandardSchemas/ExtendedSales">`<br /><br /> `<ElementPath>/Customers/Customer/Orders/Order/es:LineItems/es:LineItem</ElementPath>`<br /><br /> `</Query>`|  
|포함 XML 문서|`<Query>`<br /><br /> `<XmlData>`<br /><br /> `<Customers>`<br /><br /> `<Customer ID="1">Bobby</Customer>`<br /><br /> `</Customers>`<br /><br /> `</XmlData>`<br /><br /> `<ElementPath>Customer {@}</ElementPath>`<br /><br /> `</Query>`|  
|기본값을 사용하는 XML 문서|*No query*입니다.<br /><br /> 요소 경로는 XML 문서 자체에서 파생되며 네임스페이스로부터 독립적입니다.|  
  
> [!NOTE]  
>  첫 번째 웹 서비스 예에서는 <xref:ReportService2006.ReportingService2006.ListChildren%2A> 메서드 사용) 이 쿼리를 실행하려면 새 데이터 원본을 만들고 연결 문자열을 http://localhost/reportserver/reportservice2006.asmx로 설정해야 합니다. <xref:ReportService2006.ReportingService2006.ListChildren%2A> 메서드는 `Item` 및 `Recursive`의 두 매개 변수를 사용합니다. `Item`의 기본값은 `/`로 설정하고 `Recursive`의 기본값은 `1`로 설정합니다.  
  
## <a name="specifying-namespaces"></a>네임스페이스 지정  
 XML `Query` 요소를 사용하여 데이터 원본의 XML 데이터에 사용된 네임스페이스를 지정할 수 있습니다. 다음 XML 쿼리에서는 `sales` 네임스페이스를 사용합니다. `sales:LineItems` 및 `sales:LineItem`의 XML `ElementPath` 노드는 `sales` 네임스페이스를 사용합니다.  
  
```  
<Query xmlns:sales=  
"https://schemas.microsoft.com/StandardSchemas/ExtendedSales">  
   <SoapAction>  
      https://schemas.microsoft.com/SalesWebService/ListOrders   
   </SoapAction>  
   <ElementPath>  
      Customers/Customer/Orders/Order/sales:LineItems/sales:LineItem  
   </ElementPath>  
</Query>  
```  
  
 기본 네임스페이스가 빈 상태로 유지되도록 데이터 공급자 네임스페이스를 지정하려면 `xmldp`를 사용합니다. 이는 다음 예에서 확인할 수 있습니다.  
  
### <a name="example"></a>예제  
 다음 예에서는 XML 문서 DPNamespace.xml을 사용하며 이 문서는 표 아래에 제공되어 있습니다. 이 표에서는 네임스페이스 접두사가 포함된 XML ElementPath 구문의 두 가지 예를 보여 줍니다.  
  
|XML 쿼리 요소|데이터 세트의 결과 필드|  
|-----------------------|-------------------------------------|  
|\<Query/>|A: 값 https://schemas.microsoft.com/..합니다.<br /><br /> 값 b: https://schemas.microsoft.com/..합니다.<br /><br /> C: 값 https://schemas.microsoft.com/..합니다.|  
|\<xmldp:Query xmlns:xmldp = "https://schemas.microsoft.com/sqlserver/2005/02/reporting/XmlDPQuery" xmlns:ns = "https://schemas.microsoft.com/..." ><br /><br /> \<xmldp:ElementPath > 루트 {}/ns:Element2 / 노드\</xmldp:ElementPath ><br /><br /> \</xmldp:Query >|Value D<br /><br /> Value E<br /><br /> Value F|  
  
#### <a name="xml-document-dpnamespacexml"></a>XML 문서: DPNamespace.xml  
 이 XML을 복사한 후 보고서 디자이너에서 XML 데이터 원본으로 사용할 수 있는 URL에 저장할 수 있습니다(예: http://localhost/DPNamespace.xml).  
  
```  
<Root xmlns:ns="https://schemas.microsoft.com/...">  
   <ns:Element1>  
      <Node>Value A</Node>  
      <Node>Value B</Node>  
      <Node>Value C</Node>  
   </ns:Element1>  
   <ns:Element2>  
      <Node>Value D</Node>  
      <Node>Value E</Node>  
      <Node>Value F</Node>  
   </ns:Element2>  
</Root>  
```  
  
## <a name="see-also"></a>관련 항목  
 [XML 연결 형식&#40;SSRS&#41;](xml-connection-type-ssrs.md)   
 [Reporting Services&#40;SSRS&#41; 자습서](../reporting-services-tutorials-ssrs.md)  
  
  

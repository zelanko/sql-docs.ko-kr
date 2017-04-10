---
title: "OData 원본 | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.DTS.DESIGNER.ODATASOURCE.F1"
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# OData 원본
  SSIS 패키지의 OData 원본 구성 요소를 사용하여 Open Data Protocol(OData) 서비스에서 데이터를 사용할 수 있습니다. 구성 요소는 OData v3 및 v4 프로토콜을 지원합니다.  
  
-   OData V3 프로토콜의 경우 구성 요소는 ATOM 및 JSON 데이터 형식을 지원합니다.  
  
-   OData V4 프로토콜의 경우 구성 요소는 JSON 데이터 형식을 지원합니다.  
  
> [!NOTE]  
>  OData 원본을 사용하여 SharePoint 목록에서 읽을 수도 있습니다. SharePoint 서버의 모든 목록을 보려면 다음 URL을 사용합니다. http://\<server>/_vti_bin/ListData.svc. SharePoint URL 규칙에 대한 자세한 내용은 [SharePoint Foundation REST 인터페이스](http://msdn.microsoft.com/library/ff521587.aspx)를 참조하십시오.  이제 OData 원본은 Microsoft Dynamics AX Online 및 Microsoft Dynamics CRM Online 제품을 지원합니다.
  
## <a name="odata-format"></a>OData 형식  
 대부분의 OData 서비스는 여러 형식으로 결과를 반환합니다. $format 쿼리 옵션을 사용하여 결과 집합의 형식을 지정할 수 있습니다. JSON 및 JSON Light와 같은 형식은 ATOM 또는 XML보다 효율적이며 많은 양의 데이터를 전송하는 경우 더 나은 성능을 제공할 수 있습니다. 다음 표에서는 샘플 테스트의 결과를 제공합니다. 표에 나와 있듯이 ATOM에서 JSON으로 전환하는 경우 성능이 30-53% 향상되었고, ATOM에서 새로운 JSON Light 형식(WCF Data Services 5.1에서 사용 가능)으로 전환하는 경우에는 성능이 67% 향상되었습니다.  
  
|||||  
|-|-|-|-|  
|행|ATOM|JSON|JSON(Light)|  
|10000|113초|74초|68초|  
|1000000|1110초|853초|665초|  
  
> [!NOTE]  
>  SSIS OData 원본은 5.6.1을 사용하여 OData V3 피드를 구문 분석하고 ODataLib 6.12.0을 사용하여 OData V4 피드를 구문 분석합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [자습서: OData 원본 사용](../../integration-services/data-flow/tutorial-using-the-odata-source.md)  
  
-   [런타임에 OData 원본 쿼리 수정](../../integration-services/data-flow/modify-odata-source-query-at-runtime.md)  
  
-   [OData 원본 편집기&#40;연결 페이지&#41;](../../integration-services/data-flow/odata-source-editor-connection-page.md)  
  
-   [OData 원본 편집기&#40;열 페이지&#41;](../../integration-services/data-flow/odata-source-editor-columns-page.md)  
  
-   [OData 원본 편집기&#40;오류 출력 페이지&#41;](../../integration-services/data-flow/odata-source-editor-error-output-page.md)  
  
-   [OData 원본 속성](../../integration-services/data-flow/odata-source-properties.md)  
  
## <a name="see-also"></a>관련 항목:  
 [OData 연결 관리자](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  
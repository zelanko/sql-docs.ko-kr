---
title: OData 원본 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.ODATASOURCE.F1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4b6b4aeb4059ba659a3188712b1ce76f10efd030
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62771039"
---
# <a name="odata-source"></a>OData 원본
  SSIS 패키지의 OData 원본 구성 요소를 사용하여 Open Data Protocol(OData) 서비스에서 데이터를 사용할 수 있습니다. 이 구성 요소는 OData v2 및 v3 프로토콜뿐만 아니라 ATOM 및 JSON 데이터 형식을 지원합니다.  
  
> [!NOTE]  
>  OData 원본을 사용하여 SharePoint 목록에서 읽을 수 있습니다. SharePoint 서버의 모든 목록을 보려면 다음 URL을 사용 합니다. http://\<server>/_vti_bin/listdata.svc. SharePoint URL 규칙에 대한 자세한 내용은 [SharePoint Foundation REST 인터페이스](https://msdn.microsoft.com/library/ff521587.aspx)를 참조하십시오.  
  
## <a name="odata-format"></a>OData 형식  
 대부분의 OData 서비스는 여러 형식으로 결과를 반환합니다. $format 쿼리 옵션을 사용하여 결과 집합의 형식을 지정할 수 있습니다. JSON 및 JSON Light와 같은 형식은 ATOM/XML보다 효율적이며 많은 양의 데이터를 전송하는 경우 더 나은 성능을 제공할 수 있습니다. 다음 표에서는 샘플 테스트의 결과를 제공합니다. 표에 나와 있듯이 ATOM에서 JSON으로 전환하는 경우 성능이 30-53% 향상되었고, ATOM에서 새로운 JSON Light 형식(WCF Data Services 5.1에서 사용 가능)으로 전환하는 경우에는 성능이 67% 향상되었습니다.  
  
|||||  
|-|-|-|-|  
|행|ATOM|JSON|JSON(Light)|  
|10000|113초|74초|68초|  
|1000000|1110초|853초|665초|  
  
> [!NOTE]  
>  SSIS OData 원본은 ODataLib 5.5.0을 사용하여 OData 피드를 구문 분석하며 이 라이브러리에서 지원하는 모든 형식을 읽을 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [OData 원본 구성 요소 설치 및 제거](../install-and-uninstall-odata-source-component.md)  
  
-   [자습서: OData 원본 &#91;SSIS&#93;사용](tutorial-using-the-odata-source.md)  
  
-   [런타임에 OData 원본 쿼리 수정](modify-odata-source-query-at-runtime.md)  
  
-   [OData 원본 편집기&#40;연결 페이지&#41;](../odata-source-editor-connection-page.md)  
  
-   [OData 원본 편집기&#40;열 페이지&#41;](../odata-source-editor-columns-page.md)  
  
-   [OData 원본 편집기&#40;오류 출력 페이지&#41;](../odata-source-editor-error-output-page.md)  
  
-   [OData 원본 속성](odata-source-properties.md)  
  
## <a name="see-also"></a>참고 항목  
 [OData 연결 관리자](../connection-manager/odata-connection-manager.md)  
  
  

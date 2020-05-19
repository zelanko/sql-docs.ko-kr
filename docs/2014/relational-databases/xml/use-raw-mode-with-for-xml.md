---
title: FOR XML에서 RAW 모드 사용 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML RAW mode
- XMLSCHEMA option
- FOR XML clause, RAW mode
- RAW FOR XML mode
- ELEMENTS directive
- RAW mode
- XMLDATA option
ms.assetid: 02c1bc0b-760c-4589-9ab1-6927c6d9c734
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 06054f9a107e2aaf9fea83cb3879ef672a8520b6
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702350"
---
# <a name="use-raw-mode-with-for-xml"></a>FOR XML에서 RAW 모드 사용
  RAW 모드는 쿼리 결과 집합의 각 행을 일반 식별자 \<row>가 있는 XML 요소 또는 선택적으로 제공된 요소 이름으로 변환합니다. 기본적으로 행 집합에서 NULL이 아닌 각 열 값은 \<row> 요소의 특성으로 매핑됩니다. ELEMENTS 지시어가 FOR XML 절에 추가된 경우 각 열 값은 \<row> 요소의 하위 요소로 매핑됩니다. ELEMENTS 지시어와 함께 선택적으로 XSINIL 옵션을 지정하여 결과 집합의 NULL 열 값을 xsi:nil=`"`true`"`특성이 있는 요소로 매핑할 수 있습니다.  
  
 결과 XML에 대한 스키마를 요청할 수 있습니다. XMLDATA 옵션을 지정하면 인라인 XDR 스키마가 반환됩니다. XMLSCHEMA 옵션을 지정하면 인라인 XSD 스키마가 반환됩니다. 스키마는 데이터 시작 부분에 표시됩니다. 결국 모든 최상위 요소에 대해 스키마 네임스페이스 참조가 반복됩니다.  
  
 이진 데이터를 base64 인코딩 형식으로 반환하기 위해 FOR XML 절에서 BINARY BASE64 옵션을 지정해야 합니다. RAW 모드에서 BINARY BASE64 옵션을 지정하지 않고 이진 데이터를 검색하면 오류가 발생합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 이 섹션에는 다음 예제가 포함되어 있습니다.  
  
-   [예제: 제품 모델 정보를 XML로 검색](example-retrieving-product-model-information-as-xml.md)  
  
-   [예제: ELEMENTS 지시어를 사용하여 XSINIL 지정](example-specifying-xsinil-with-the-elements-directive.md)  
  
-   [예제: XMLDATA 및 XMLSCHEMA 옵션을 사용하여 결과로 스키마 요청](example-requesting-schemas-as-results-with-the-xmldata-and-xmlschema-options.md)  
  
-   [예제: 이진 데이터 검색](example-retrieving-binary-data.md)  
  
-   [예제: &#60;행&#62; 요소 이름 바꾸기](example-renaming-the-row-element.md)  
  
-   [예제: FOR XML로 생성된 XML에 대한 루트 요소 지정](example-specifying-a-root-element-for-the-xml-generated-by-for-xml.md)  
  
-   [예제: XMLType 열 쿼리](example-querying-xmltype-columns.md)  
  
## <a name="see-also"></a>참고 항목  
 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [FOR XML에서 AUTO 모드 사용](use-auto-mode-with-for-xml.md)   
 [FOR XML에서 EXPLICIT 모드 사용](use-explicit-mode-with-for-xml.md)   
 [FOR XML에서 PATH 모드 사용](use-path-mode-with-for-xml.md)   
 [SELECT&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML&#40;SQL Server&#41;](../xml/for-xml-sql-server.md)  
  
  

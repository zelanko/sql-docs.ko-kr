---
title: "FOR XML에서 PATH 모드 사용 | Microsoft 문서"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PATH FOR XML mode
- characters [SQL Server], XML
- aliases [SQL Server], XML
- FOR XML clause, PATH mode
- FOR XML PATH mode
- column names [SQL Server]
- XPath queries [SQL Server]
ms.assetid: a685a9ad-3d28-4596-aa72-119202df3976
caps.latest.revision: "45"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: dce5f60b6224cfcb2904244a5d84a6a997abe49d
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="use-path-mode-with-for-xml"></a>FOR XML에서 PATH 모드 사용
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] [FOR XML을 사용하는 XML 생성](../../relational-databases/xml/for-xml-sql-server.md) 항목에 설명된 대로 PATH 모드를 사용하면 요소와 특성을 간단하게 혼합할 수 있고 추가 중첩을 간단하게 도입하여 복잡한 속성을 표시할 수 있습니다. FOR XML EXPLICIT 모드 쿼리를 사용하여 행 집합에서 해당 XML을 생성할 수 있지만 PATH 모드를 사용할 경우 복잡해지기 쉬운 EXPLICIT 모드 쿼리의 대안을 찾을 수 있습니다. **XML** 유형 인스턴스를 반환하는 중첩 FOR XML 쿼리 및 TYPE 지시어 작성 기능과 함께 PATH 모드를 사용하면 보다 간편하게 쿼리를 작성할 수 있습니다.  
  
 PATH 모드에서는 열 이름이나 열 별칭이 XPath 식으로 처리됩니다. 이러한 식은 값이 XML에 매핑되는 방법을 나타냅니다. 각 XPath 식은 특성, 요소와 스칼라 값 및 행 요소에 대해 생성되는 노드의 이름과 계층 등의 항목 유형을 제공하는 상대 XPath입니다.  
  
 이 섹션에서는 다양한 조건에서 행 집합의 열을 매핑하는 방법에 대해 설명하고 예를 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [이름이 없는 열](../../relational-databases/xml/columns-without-a-name.md)  
  
-   [이름이 있는 열](../../relational-databases/xml/columns-with-a-name.md)  
  
-   [이름이 와일드카드 문자로 지정된 열](../../relational-databases/xml/columns-with-a-name-specified-as-a-wildcard-character.md)  
  
-   [이름이 XPath 노드 테스트인 열](../../relational-databases/xml/columns-with-the-name-of-an-xpath-node-test.md)  
  
-   [경로가 data&#40;&#41;로 지정된 열 이름](../../relational-databases/xml/column-names-with-the-path-specified-as-data.md)  
  
-   [기본적으로 Null 값을 포함하는 열](../../relational-databases/xml/columns-that-contain-a-null-value-by-default.md)  
  
-   [PATH 모드에서의 네임스페이스 지원](../../relational-databases/xml/namespace-support-in-path-mode.md)  
  
-   [예제: PATH 모드 사용](../../relational-databases/xml/examples-using-path-mode.md)  
  
## <a name="see-also"></a>참고 항목  
 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML&#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  

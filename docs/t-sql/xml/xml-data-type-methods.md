---
title: "xml 데이터 형식 메서드 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: d112b9c9-be9f-435c-a9e6-d21b65778fb7
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fcf16bd9b71f27ab91fb02bbfd7bb7625185b44e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="xml-data-type-methods"></a>xml 데이터 형식 메서드
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  사용할 수는 **xml** 데이터 형식 변수 또는 열에 저장 된 XML 인스턴스를 쿼리 하는 메서드 **xml** 유형입니다. 이 섹션의 항목 사용 하는 방법에 설명 된 **xml** 데이터 형식 메서드.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[쿼리 &#40; &#41; 방법 &#40; xml 데이터 형식 &#41;](../../t-sql/xml/query-method-xml-data-type.md)|query() 메서드를 사용하여 XML 인스턴스에 대해 쿼리하는 방법에 대해 설명합니다.|  
|[값 &#40; &#41; 방법 &#40; xml 데이터 형식 &#41;](../../t-sql/xml/value-method-xml-data-type.md)|value() 메서드를 사용하여 XML 인스턴스에서 SQL 형식의 값을 검색하는 방법에 대해 설명합니다.|  
|[존재 &#40; &#41; 방법 &#40; xml 데이터 형식 &#41;](../../t-sql/xml/exist-method-xml-data-type.md)|exist() 메서드를 사용하여 쿼리가 비어 있지 않은 결과를 반환하는지 여부를 확인하는 방법에 대해 설명합니다.|  
|[수정 &#40; &#41; 방법 &#40; xml 데이터 형식 &#41;](../../t-sql/xml/modify-method-xml-data-type.md)|Modify () 메서드를 사용 하 여 지정 하는 방법을 설명 [XML 데이터 수정 언어 &#40; XML DML &#41; ](../../t-sql/xml/xml-data-modification-language-xml-dml.md)업데이트를 수행 하는 문입니다.|  
|[노드 &#40; &#41; 방법 &#40; xml 데이터 형식 &#41;](../../t-sql/xml/nodes-method-xml-data-type.md)|nodes() 메서드를 사용하여 XML을 여러 행으로 나누어 XML 문서 부분을 행 집합으로 분할하는 방법에 대해 설명합니다.|  
|[XML 데이터 내 관계형 데이터 바인딩](../../t-sql/xml/binding-relational-data-inside-xml-data.md)|XML 내에 XML이 아닌 데이터를 바인딩하는 방법에 대해 설명합니다.|  
|[xml 데이터 형식 메서드를 사용하기 위한 지침](../../t-sql/xml/guidelines-for-using-xml-data-type-methods.md)|사용 하기 위한 지침을 설명는 **xml** 데이터 형식 메서드.|  
  
 사용자 정의 형식 메서드 호출 구문을 사용하여 이러한 메서드를 호출할 수 있습니다. 예를 들어  
  
```  
SELECT XmlCol.query(' ... ')  
FROM   Table  
```  
  
> [!NOTE]  
>  **xml** 데이터 형식 메서드 **query ()**, **value ()**, 및 **exist ()** NULL XML 인스턴스에 대해 실행 된 경우 NULL을 반환 합니다. 또한 **modify ()** 아무것도 반환 하지 않는 있지만 **nodes ()** NULL 입력 된 행 집합 및 빈 행 집합을 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  


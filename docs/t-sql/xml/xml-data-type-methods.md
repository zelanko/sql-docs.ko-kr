---
title: xml 데이터 형식 메서드 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: d112b9c9-be9f-435c-a9e6-d21b65778fb7
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b788282072088b4c9ee98b27b6f4ce3fb2b923c6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="xml-data-type-methods"></a>xml 데이터 형식 메서드
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **xml** 데이터 형식 메서드를 사용하여 **xml** 형식의 변수 또는 열에 저장된 XML 인스턴스를 쿼리할 수 있습니다. 이 섹션에서는 **xml** 데이터 형식 메서드를 사용하는 방법에 대해 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[query&#40;&#41; 메서드&#40;xml 데이터 형식&#41;](../../t-sql/xml/query-method-xml-data-type.md)|query() 메서드를 사용하여 XML 인스턴스에 대해 쿼리하는 방법에 대해 설명합니다.|  
|[value&#40;&#41; 메서드&#40;xml 데이터 형식&#41;](../../t-sql/xml/value-method-xml-data-type.md)|value() 메서드를 사용하여 XML 인스턴스에서 SQL 형식의 값을 검색하는 방법에 대해 설명합니다.|  
|[exist&#40;&#41; 메서드&#40;xml 데이터 형식&#41;](../../t-sql/xml/exist-method-xml-data-type.md)|exist() 메서드를 사용하여 쿼리가 비어 있지 않은 결과를 반환하는지 여부를 확인하는 방법에 대해 설명합니다.|  
|[modify&#40;&#41; 메서드&#40;xml 데이터 형식&#41;](../../t-sql/xml/modify-method-xml-data-type.md)|modify() 메서드를 사용하여 [XML 데이터 수정 언어&#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md) 문이 업데이트를 수행하도록 지정하는 방법에 대해 설명합니다.|  
|[nodes&#40;&#41; 메서드&#40;xml 데이터 형식&#41;](../../t-sql/xml/nodes-method-xml-data-type.md)|nodes() 메서드를 사용하여 XML을 여러 행으로 나누어 XML 문서 부분을 행 집합으로 분할하는 방법에 대해 설명합니다.|  
|[XML 데이터 내 관계형 데이터 바인딩](../../t-sql/xml/binding-relational-data-inside-xml-data.md)|XML 내에 XML이 아닌 데이터를 바인딩하는 방법에 대해 설명합니다.|  
|[xml 데이터 형식 메서드를 사용하기 위한 지침](../../t-sql/xml/guidelines-for-using-xml-data-type-methods.md)|**xml** 데이터 형식 메서드 사용에 대한 지침을 설명합니다.|  
  
 사용자 정의 형식 메서드 호출 구문을 사용하여 이러한 메서드를 호출할 수 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
SELECT XmlCol.query(' ... ')  
FROM   Table  
```  
  
> [!NOTE]  
>  **xml** 데이터 형식 메서드 **query()**, **value()** 및 **exist()** 는 NULL XML 인스턴스에 대해 실행된 경우 NULL을 반환합니다. 또한 **modify()** 는 아무 것도 반환하지 않지만 **nodes()** 는 행 집합과 NULL 입력 사항이 있는 빈 행 집합을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  

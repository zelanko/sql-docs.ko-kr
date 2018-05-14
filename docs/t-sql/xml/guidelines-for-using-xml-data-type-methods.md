---
title: xml 데이터 형식 메서드를 사용하기 위한 지침 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
ms.assetid: 1a483aa1-42de-4c88-a4b8-c518def3d496
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4ea4da8b314d5f7a55c8a3ca2a5913440f5c9268
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="guidelines-for-using-xml-data-type-methods"></a>xml 데이터 형식 메서드를 사용하기 위한 지침
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 **xml** 데이터 형식 메서드를 사용하기 위한 지침을 설명합니다.  
  
## <a name="the-print-statement"></a>PRINT 문  
 **xml** 데이터 형식 메서드는 다음 예에 표시된 것과 같이 PRINT 문에서 사용할 수 없습니다. **xml** 데이터 형식 메서드는 하위 쿼리로 취급되며 하위 쿼리는 PRINT 문에 허용되지 않습니다. 따라서 다음 예는 오류를 반환합니다.  
  
```  
DECLARE @x xml  
SET @x = '<root>Hello</root>'  
PRINT @x.value('/root[1]', 'varchar(20)') -- will not work because this is treated as a subquery (select top 1 col from table)   
```  
  
 이에 대한 해결 방법은 먼저 **value()** 메서드의 결과를 **xml** 형식의 변수에 할당한 다음, 쿼리에서 변수를 지정하는 것입니다.  
  
```  
DECLARE @x xml  
DECLARE @c varchar(max)  
SET @x = '<root>Hello</root>'  
SET @c = @x.value('/root[1]', 'varchar(11)')  
PRINT @c                                                        
```  
  
## <a name="the-group-by-clause"></a>GROUP BY 절  
 **xml** 데이터 형식 메서드는 내부적으로 하위 쿼리로 취급됩니다. GROUP BY에는 스칼라가 필요하고 집계 및 하위 쿼리가 허용되지 않기 때문에 GROUP BY 절에 **xml** 데이터 형식 메서드를 지정할 수 없습니다. 이에 대한 해결 방법은 절 내에서 XML 메서드를 사용하는 사용자 정의 함수를 호출하는 것입니다.  
  
## <a name="reporting-errors"></a>오류 보고  
 오류를 보고할 때 **xml** 데이터 형식 메서드는 다음 형식의 단일 오류를 발생시킵니다.  
  
```  
Msg errorNumber, Level levelNumber, State stateNumber:  
XQuery [database.table.method]: description_of_error  
```  
  
 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
Msg 2396, Level 16, State 1:  
XQuery [xmldb_test.xmlcol.query()]: Attribute may not appear outside of an element  
```  
  
## <a name="singleton-checks"></a>단일 항목 검사  
 단일 항목이 필요한 위치 단계, 함수 매개 변수 및 연산자는 컴파일러가 런타임 시 단일 항목이 보장되는지 여부를 확인할 수 없는 경우 오류를 반환합니다. 이 문제는 형식화되지 않은 데이터에서 자주 발생합니다. 예를 들어 특성 조회에는 단일 부모 요소가 필요합니다. 이를 위해서는 단일 부모 노드를 선택하는 서수만으로도 충분합니다. 특성 값 추출을 위한 **node()**-**value()** 조합의 평가에는 서수 사양이 필요하지 않을 수 있습니다. 이러한 내용은 다음 예에 표시되어 있습니다.  
  
### <a name="example-known-singleton"></a>예: 알려진 단일 항목  
 이 예에서 **nodes()** 메서드는 각 <`book`> 요소에 대해 별개의 행을 생성합니다. <`book`> 노드에서 평가되는 **value()** 메서드는 @genre의 값을 추출하고 단일 항목 특성이 됩니다.  
  
```  
SELECT nref.value('@genre', 'varchar(max)') LastName  
FROM   T CROSS APPLY xCol.nodes('//book') AS R(nref)  
```  
  
 형식화된 XML의 유형 검사에는 XML 스키마가 사용됩니다. XML 스키마의 단일 항목으로 노드가 지정된 경우 컴파일러는 이 정보를 사용하며 오류가 발생하지 않습니다. 그렇지 않으면 단일 노드를 선택하는 서수가 필요합니다. 특히 /book//title에서와 같이 하위 항목 또는 자체 축(//)을 사용하면 XML 스키마에 지정되어 있더라도 \<title> 요소에 대한 단일 항목 카디널리티 추론이 손실됩니다. 따라서 이를 (/book//title)[1]과 같이 다시 작성해야 합니다.  
  
 유형 검사를 위해서는 //first-name[1] 및 (//first-name)[1] 간의 차이점을 인식해야 합니다. 전자는 각 노드가 해당 형제 간의 가장 왼쪽에 있는 \<first-name> 노드인 \<first-name> 노드의 시퀀스를 반환합니다. 후자는 XML 인스턴스에서 문서 순서의 첫 번째 단일 \<first-name> 노드를 반환합니다.  
  
### <a name="example-using-value"></a>예: value() 사용  
 형식화되지 않은 XML 열에서 다음 쿼리를 실행하면 정적 컴파일 오류가 발생합니다. 그 이유는 **value()** 에 첫 번째 인수로 단일 노드가 필요한데 런타임 시 하나의 \<last-name> 노드만 발생하는지 여부를 컴파일러에서 확인할 수 없기 때문입니다.  
  
```  
SELECT xCol.value('//author/last-name', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 다음은 고려할 수 있는 해결 방법입니다.  
  
```  
SELECT xCol.value('//author/last-name[1]', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 하지만 이 해결 방법은 각 XML 인스턴스에 여러 <`author`> 노드가 발생할 수 있기 때문에 오류를 해결하지 않습니다. 다음과 같이 쿼리를 다시 작성하면 도움이 됩니다.  
  
```  
SELECT xCol.value('(//author/last-name/text())[1]', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 이 쿼리는 각 XML 인스턴스에서 첫 번째 `<last-name>` 요소의 값을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)  
  
  

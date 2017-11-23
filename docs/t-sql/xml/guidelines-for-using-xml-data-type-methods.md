---
title: "Xml 데이터 형식 메서드를 사용 하기 위한 지침 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: 1a483aa1-42de-4c88-a4b8-c518def3d496
caps.latest.revision: "34"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f22c3535c66663979009d1e760ecf8c2164bc765
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="guidelines-for-using-xml-data-type-methods"></a>xml 데이터 형식 메서드를 사용하기 위한 지침
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  사용 하기 위한 지침을 설명 하는이 항목의 **xml** 데이터 형식 메서드.  
  
## <a name="the-print-statement"></a>PRINT 문  
 **xml** 데이터 형식 메서드는 다음 예제와 같이 PRINT 문에서 사용할 수 없습니다. **xml** 데이터 형식 메서드는 하위 쿼리로 취급 되 고 PRINT 문에서 하위 쿼리를 사용할 수 없습니다. 따라서 다음 예는 오류를 반환합니다.  
  
```  
DECLARE @x xml  
SET @x = '<root>Hello</root>'  
PRINT @x.value('/root[1]', 'varchar(20)') -- will not work because this is treated as a subquery (select top 1 col from table)   
```  
  
 솔루션은 먼저의 결과 할당 하는 **value ()** 변수에 메서드 **xml** 입력 한 다음 쿼리에서 변수를 지정 합니다.  
  
```  
DECLARE @x xml  
DECLARE @c varchar(max)  
SET @x = '<root>Hello</root>'  
SET @c = @x.value('/root[1]', 'varchar(11)')  
PRINT @c                                                        
```  
  
## <a name="the-group-by-clause"></a>GROUP BY 절  
 **xml** 데이터 형식 메서드는 내부적으로 하위 쿼리로 취급 됩니다. GROUP BY는 스칼라가 필요 하 고 집계 및 하위 쿼리를 허용 하지 않습니다, 때문에 지정할 수 없습니다는 **xml** GROUP BY 절에 데이터 형식 메서드. 이에 대한 해결 방법은 절 내에서 XML 메서드를 사용하는 사용자 정의 함수를 호출하는 것입니다.  
  
## <a name="reporting-errors"></a>오류 보고  
 오류를 보고할 때 **xml** 데이터 형식 메서드는 다음과 같은 형식의 단일 오류를 발생 시킵니다.  
  
```  
Msg errorNumber, Level levelNumber, State stateNumber:  
XQuery [database.table.method]: description_of_error  
```  
  
 예를 들어  
  
```  
Msg 2396, Level 16, State 1:  
XQuery [xmldb_test.xmlcol.query()]: Attribute may not appear outside of an element  
```  
  
## <a name="singleton-checks"></a>단일 항목 검사  
 단일 항목이 필요한 위치 단계, 함수 매개 변수 및 연산자는 컴파일러가 런타임 시 단일 항목이 보장되는지 여부를 확인할 수 없는 경우 오류를 반환합니다. 이 문제는 형식화되지 않은 데이터에서 자주 발생합니다. 예를 들어 특성 조회에는 단일 부모 요소가 필요합니다. 이를 위해서는 단일 부모 노드를 선택하는 서수만으로도 충분합니다. 평가 **node ()**-**value ()** 특성 값을 추출 하는 서 수 사양이 필요 하지 않을 수 있습니다. 이러한 내용은 다음 예에 표시되어 있습니다.  
  
### <a name="example-known-singleton"></a>예: 알려진된 단일 항목  
 이 예제는 **nodes ()** 메서드 각각에 대해 별도 행을 생성 <`book`> 요소입니다. **value ()** 에서 계산 되는 메서드는 <`book`>의 값을 추출 하는 노드 @genre 및 특성에는 단일 항목입니다.  
  
```  
SELECT nref.value('@genre', 'varchar(max)') LastName  
FROM   T CROSS APPLY xCol.nodes('//book') AS R(nref)  
```  
  
 형식화된 XML의 유형 검사에는 XML 스키마가 사용됩니다. XML 스키마의 단일 항목으로 노드가 지정된 경우 컴파일러는 이 정보를 사용하며 오류가 발생하지 않습니다. 그렇지 않으면 단일 노드를 선택하는 서수가 필요합니다. 특히, 하위 또는 자체 축 사용 (/ /) / 책/와 같이 축 / 제목에 대 한 단일 항목 카디널리티 유추를 잃을 \<제목 > 요소를 XML 스키마 그렇게 지정 하는 경우에 합니다. 따라서 이를 (/book//title)[1]과 같이 다시 작성해야 합니다.  
  
 유형 검사를 위해서는 //first-name[1] 및 (//first-name)[1] 간의 차이점을 인식해야 합니다. 앞의 시퀀스를 반환 \<-이름 > 각 노드는 가장 왼쪽에 있는 노드 \<-이름 > 노드를 형제 중입니다. 첫 번째 단일 후자 반환 \<-이름 > XML 인스턴스에서 문서 순서로 노드.  
  
### <a name="example-using-value"></a>예: value () 사용  
 다음 쿼리는 형식화 되지 않은 XML 열에는 정적 컴파일 오류가 발생합니다. ¿¡´ **Value ()** 하나만 있는지 여부를 확인할 수 없습니다 첫 번째 인수와 컴파일러 처럼 단일 노드가 필요한 \<마지막 이름 > 노드는 런타임에 발생 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)  
  
  

---
title: XML 데이터 내 관계형 데이터 바인딩 | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- relational data binding [SQL Server]
- XML [SQL Server], binding relational data
- xml data type [SQL Server], relational data binding
- binding relational data [XML in SQL Server]
- variables [XML in SQL Server], relational data binding
- columns [XML in SQL Server], relational data binding
ms.assetid: 03d013a9-b53f-46c3-9628-da77f099c74a
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: db924e662687ab79d207fe3e1e33ccc75aecd059
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="binding-relational-data-inside-xml-data"></a>XML 데이터 내 관계형 데이터 바인딩
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **xml** 데이터 형식 변수 또는 열에 대해 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)를 지정할 수 있습니다. 예를 들어 [query&#40;&#41; 메서드&#40;xml 데이터 형식&#41;](../../t-sql/xml/query-method-xml-data-type.md)는 XML 인스턴스에 대해 지정된 XQuery를 실행합니다. 이 방식으로 XML을 구성하면 비-XML 유형의 열이나 Transact-SQL 변수로부터 값을 가져올 수 있습니다. 이러한 과정을 XML 내 관계형 데이터 바인딩이라고 합니다.  
  
 XML 내 비-XML 관계형 데이터를 바인딩하기 위해 SQL Server 데이터베이스 엔진은 다음과 같은 의사 함수를 제공합니다.  
  
-   [sql:column&#40;&#41; 함수 &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-column.md)를 사용하면 XQuery 또는 XML DML 식의 관계형 열에 있는 값을 사용할 수 있습니다.  
  
-   [sql:variable&#40;&#41; 함수 &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-variable.md) . XQuery 또는 XML DML 식에 있는 SQL 변수 값을 사용할 수 있습니다.  
  
 이러한 함수는 XML 내 관계형 값을 제공할 때마다 **xml** 데이터 형식 메서드와 함께 사용할 수 있습니다.  
  
 **xml**, CLR 사용자 정의 형식, datetime, smalldatetime, **text**, **ntext**, **sql_variant** 및 **image** 형식의 열 또는 변수에 있는 데이터를 참조하는 데는 이러한 함수를 사용할 수 없습니다.  
  
 또한 이 바인딩은 읽기 전용으로만 사용됩니다. 즉, 이러한 함수를 사용하는 열에는 데이터를 기록할 수 없습니다. 예를 들어 sql:variable(“@x”)=“*some expression”* 은 허용되지 않습니다.  
  
## <a name="example-cross-domain-query-using-sqlvariable"></a>예: sql:variable()을 사용한 도메인 간 쿼리  
 이 예에서는 응용 프로그램에서 **sql:variable()** 을 사용하여 쿼리를 매개 변수화하는 방법을 보여 줍니다. ISBN은 SQL 변수 @isbn을 사용하여 전달됩니다. 상수를 **sql:variable()** 로 바꿈으로써 0-7356-1588-2인 ISBN뿐만 아니라 다른 모든 ISBN을 검색하는 데 쿼리를 사용할 수 있습니다.  
  
```  
DECLARE @isbn varchar(20)  
SET     @isbn = '0-7356-1588-2'  
SELECT  xCol  
FROM    T  
WHERE   xCol.exist ('/book/@ISBN[. = sql:variable("@isbn")]') = 1  
```  
  
 **sql:column()** 을 비슷한 방식으로 사용하면 추가 이점이 있습니다. 비용 기반 쿼리 최적화 프로그램에서 결정되는 것과 같이 효율성을 위해 열에 대해 인덱스를 사용할 수 있습니다. 또한 계산 열에서 승격된 속성을 저장할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)  
  
  

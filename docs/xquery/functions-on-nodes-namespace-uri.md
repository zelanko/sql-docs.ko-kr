---
title: namespace-uri 함수 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri function
- namespace-uri function
ms.assetid: 9b48d216-26c8-431d-9ab4-20ab187917f4
caps.latest.revision: 14
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e93e74bc8198876c3bf5d364e72eb2775515d020
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="functions-on-nodes---namespace-uri"></a>노드-네임 스페이스 uri 함수
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  URI에 지정 된 QName의 네임 스페이스를 반환 *$arg* 는 xs: string으로 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
fn:namespace-uri() as xs:string  
fn:namespace-uri($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 네임스페이스 URI 부분이 검색되는 노드 이름입니다.  
  
## <a name="remarks"></a>주의  
  
-   인수가 생략된 경우 기본값은 컨텍스트 노드입니다.  
  
-   SQL Server에서 **fn:namespace-uri()** 상황별 조건자의 컨텍스트에서 인수만 사용할 수 있습니다. 특히 사용 시 대괄호([])로 묶어야 합니다.  
  
-   경우 *$arg* 이 빈 시퀀스인 경우 길이가 0 인 문자열이 반환 됩니다.  
  
-   경우 *$arg* 는 요소 또는 특성 노드에 있는 Expanded-qname 함수 네임 스페이스에 없는 길이가 0 인 문자열을 반환 합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-retrieve-namespace-uri-of-a-specific-node"></a>1. 특정 노드의 네임스페이스 URI 검색  
 다음은 형식화되지 않은 XML 인스턴스에 대해 지정된 쿼리입니다. 쿼리 식 `namespace-uri(/ROOT[1])`은 지정된 노드의 네임스페이스 URI 부분을 검색합니다.  
  
```  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('namespace-uri(/ROOT[1])')  
```  
  
 지정된 QName에 네임스페이스 URI 부분이 없고 로컬 이름 부분만 있는 경우 결과는 길이가 0인 문자열입니다.  
  
 다음 쿼리는 형식화 된 Instructions에 대해 지정 **xml** 열입니다. `namespace-uri(/AWMI:root[1]/AWMI:Location[1])` 식은 <`root`> 요소에 대한 첫 번째 <`Location`> 요소 자식의 네임스페이스 URI를 반환합니다.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     namespace-uri(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 다음은 결과입니다.  
  
```  
http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions  
```  
  
### <a name="b-using-namespace-uri-without-argument-in-a-predicate"></a>2. 조건자의 인수 없이 namespace-uri() 사용  
 다음 쿼리는 형식화된 CatalogDescription xml 열에 대해 지정되었습니다. 이 식은 네임스페이스 URI가 `http://www.adventure-works.com/schemas/OtherFeatures`인 모든 요소 노드를 반환합니다. 네임 스페이스-**uri()** 함수는 인수 없이 지정 하 고 컨텍스트 노드를 사용 합니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   /p1:ProductDescription//*[namespace-uri() = "http://www.adventure-works.com/schemas/OtherFeatures"]  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 다음은 결과 중 일부입니다.  
  
```  
<p1:wheel xmlns:p1="http://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p1:wheel>  
<p2:saddle xmlns:p2="http://www.adventure-works.com/schemas/OtherFeatures">  
  <p3:i xmlns:p3="http://www.w3.org/1999/xhtml">Anatomic design</p3:i> and made from durable leather for a full-day of riding in comfort.</p2:saddle>  
…  
```  
  
 이전 쿼리의 네임스페이스 URI를 `http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`으로 바꿀 수 있습니다. 그런 다음 확장 QName의 네임스페이스 URI 부분이 `http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`인 <`ProductDescription`> 요소의 모든 요소 노드 자식을 검색합니다.  
  
### <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **namespace-uri ()** 함수는 xs: anyuri 대신 xs: string 유형의 인스턴스를 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [노드 함수](http://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [local-name 함수 &#40;XQuery&#41;](../xquery/functions-on-nodes-local-name.md)  
  
  

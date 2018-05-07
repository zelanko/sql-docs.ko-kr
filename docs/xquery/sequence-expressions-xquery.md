---
title: 시퀀스 식 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- expressions [XQuery], sequence
- filtering sequences [XQuery]
ms.assetid: 41e18b20-526b-45d2-9bd9-e3b7d7fbce4e
caps.latest.revision: 22
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 34c26b529aeaee5e9f80ecc0a1a07d3cb8cedbf4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sequence-expressions-xquery"></a>시퀀스 식(XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 항목의 시퀀스를 생성, 필터링 및 조합하는 데 사용되는 XQuery 연산자를 지원합니다. 항목은 원자 값이거나 노드일 수 있습니다.  
  
## <a name="constructing-sequences"></a>시퀀스 생성  
 쉼표 연산자를 사용하여 항목을 단일 시퀀스로 연결하는 시퀀스를 생성할 수 있습니다.  
  
 시퀀스에는 중복된 값이 포함될 수 있습니다. 시퀀스 내에 포함된 시퀀스와 같은 중첩된 시퀀스는 축소되어 표시됩니다. 예를 들어 시퀀스 (1, 2, (3, 4, (5)))는 (1, 2, 3, 4, 5)가 됩니다. 다음은 시퀀스를 생성하는 예입니다.  
  
### <a name="example-a"></a>예 1  
 다음 쿼리는 5개의 원자 값에 대한 하나의 시퀀스를 반환합니다.  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2,3,4,5)')  
go  
-- result 1 2 3 4 5  
```  
  
 다음 쿼리는 두 개의 노드에 대한 하나의 시퀀스를 반환합니다.  
  
```  
-- sequence of 2 nodes  
declare @x xml  
set @x=''  
select @x.query('(<a/>, <b/>)')  
go  
-- result  
<a />  
<b />  
```  
  
 다음 쿼리는 원자 값 및 노드에 대한 하나의 시퀀스를 생성하기 때문에 오류를 반환합니다. 이러한 시퀀스는 유형이 다르며 지원되지 않습니다.  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1, 2, <a/>, <b/>)')  
go  
```  
  
### <a name="example-b"></a>예 2  
 다음 쿼리는 길이가 다른 4개의 시퀀스를 단일 시퀀스로 조합하여 원자 값에 대한 하나의 시퀀스를 생성합니다.  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2),10,(),(4, 5, 6)')  
go  
-- result = 1 2 10 4 5 6  
```  
  
 이 시퀀스는 FLOWR 및 ORDER BY를 사용하여 정렬할 수 있습니다.  
  
```  
declare @x xml  
set @x=''  
select @x.query('for $i in ((1,2),10,(),(4, 5, 6))  
                  order by $i  
                  return $i')  
go  
```  
  
 사용 하 여 시퀀스에서 항목을 계산할 수는 **fn:count()** 함수입니다.  
  
```  
declare @x xml  
set @x=''  
select @x.query('count( (1,2,3,(),4) )')  
go  
-- result = 4  
```  
  
### <a name="example-c"></a>예 3  
 다음 쿼리는 AdditionalContactInfo 열에 대해 지정 된는 **xml** Contact 테이블에서 유형입니다. 이 열에는 하나 이상의 추가 전화 번호, 호출기 번호 및 주소와 같은 추가 연락 정보가 저장됩니다. \<telephoneNumber >, \<호출기 >, 다른 노드는 문서에 아무 곳 이나 나타날 수 있습니다. 모두 포함 하는 시퀀스를 생성 하는 쿼리는 \<telephoneNumber > 뒤에 여는 컨텍스트 노드에서 자식은 \<호출기 > 자식입니다. `($a//act:telephoneNumber, $a//act:pager)` 반환 식에서 사용된 쉼표 시퀀스 연산자에 유의하십시오.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
 'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo   
   return ($a//act:telephoneNumber, $a//act:pager)  
') As Result  
FROM Person.Contact  
WHERE ContactID=3  
```  
  
 다음은 결과입니다.  
  
```  
<act:telephoneNumber xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:pager xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>999-555-1244</act:number>  
  <act:SpecialInstructions>  
Page only in case of emergencies.  
</act:SpecialInstructions>  
</act:pager>  
```  
  
## <a name="filtering-sequences"></a>시퀀스 필터링  
 식에 조건자를 추가하여 식에 의해 반환된 시퀀스를 필터링할 수 있습니다. 자세한 내용은 참조 [경로 식 &#40;XQuery&#41;](../xquery/path-expressions-xquery.md)합니다. 예를 들어 다음 쿼리는 3개의 <`a`> 요소 노드에 대한 하나의 시퀀스를 반환합니다.  
  
```  
declare @x xml  
set @x = '<root>  
<a attrA="1">111</a>  
<a></a>  
<a></a>  
</root>'  
SELECT @x.query('/root/a')  
```  
  
 다음은 결과입니다.  
  
```  
<a attrA="1">111</a>  
<a />  
<a />  
```  
  
 특성 attrA가 포함된 <`a`> 요소만 검색하려면 조건자에서 필터를 지정하면 됩니다. 결과 시퀀스에는 하나의 <`a`> 요소만 포함됩니다.  
  
```  
declare @x xml  
set @x = '<root>  
<a attrA="1">111</a>  
<a></a>  
<a></a>  
</root>'  
SELECT @x.query('/root/a[@attrA]')  
```  
  
 다음은 결과입니다.  
  
```  
<a attrA="1">111</a>  
```  
  
 경로 식에서 조건자를 지정 하는 방법에 대 한 자세한 내용은 참조 [경로 식 단계에서 조건자 지정](../xquery/path-expressions-specifying-predicates.md)합니다.  
  
 다음 예에서는 하위 트리의 시퀀스 식을 작성한 다음 시퀀스에 필터를 적용합니다.  
  
```  
declare @x xml  
set @x = '  
<a>  
  <c>C under a</c>  
</a>  
<b>    
   <c>C under b</c>  
</b>  
<c>top level c</c>  
<d></d>  
'  
```  
  
 `(/a, /b)`의 식은 하위 트리 `/a` 및 `/b`가 포함되어 있고 식이 `<c>` 요소를 필터링한 결과 시퀀스로부터 가져온 시퀀스를 생성합니다.  
  
```  
SELECT @x.query('  
  (/a, /b)/c  
')  
```  
  
 다음은 결과입니다.  
  
```  
<c>C under a</c>  
<c>C under b</c>  
```  
  
 다음 예에서는 조건자 필터가 적용됩니다. 이 식은 <`c`> 요소가 포함된 <`a`> 및 <`b`> 요소를 검색합니다.  
  
```  
declare @x xml  
set @x = '  
<a>  
  <c>C under a</c>  
</a>  
<b>    
   <c>C under b</c>  
</b>  
  
<c>top level c</c>  
<d></d>  
'  
SELECT @x.query('  
  (/a, /b)[c]  
')  
```  
  
 다음은 결과입니다.  
  
```  
<a>  
  <c>C under a</c>  
</a>  
<b>  
  <c>C under b</c>  
</b>  
```  
  
### <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   XQuery 범위 식은 지원되지 않습니다.  
  
-   시퀀스는 유형이 같아야 합니다. 특히 한 시퀀스의 모든 항목은 노드 값이나 원자 값 중 하나여야 합니다. 이 제한은 정적으로 확인됩니다.  
  
-   union, intersect 또는 except 연산자를 사용하여 노드 시퀀스를 조합하는 기능은 지원되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XQuery 식](../xquery/xquery-expressions.md)  
  
  

---
title: data 함수 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:data function
- data function [XQuery]
ms.assetid: 511b5d7d-c679-4cb2-a3dd-170cc126f49d
author: rothja
ms.author: jroth
ms.openlocfilehash: 7376c57f809fa97168b27b158678d931a696b5df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038973"
---
# <a name="data-accessor-functions---data-xquery"></a>데이터 접근자 함수 - data(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  지정 된 각 항목에 대 한 형식화 된 값을 반환 합니다 *$arg*합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:data ($arg as item()*) as xdt:untypedAtomic*  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 형식화된 값이 반환되는 항목의 시퀀스입니다.  
  
## <a name="remarks"></a>설명  
 형식화된 값에는 다음이 적용됩니다.  
  
-   원자 값의 형식화된 값은 원자 값입니다.  
  
-   텍스트 노드의 형식화된 값은 텍스트 노드의 문자열 값입니다.  
  
-   주석의 형식화된 값은 주석의 문자열 값입니다.  
  
-   처리 명령의 형식화된 값은 처리 명령 대상 이름이 없는 처리 명령의 내용입니다.  
  
-   문서 노드의 형식화된 값은 해당 문자열 값입니다.  
  
 특성 및 요소 노드에는 다음이 적용됩니다.  
  
-   특성 노드가 XML 스키마 유형으로 형식화된 경우 해당 형식화된 값은 그에 따라 형식화된 값입니다.  
  
-   특성 노드가 형식화 되지 하는 경우 해당 형식화 된 값은 인스턴스가 반환 되는 문자열 값과 동일 **xdt: untypedatomic**합니다.  
  
-   요소 노드가 형식화 되지 않은, 하는 경우 해당 형식화 된 값은 인스턴스의 반환 되는 문자열 값과 동일 **xdt: untypedatomic**합니다.  
  
 형식화된 요소 노드에는 다음이 적용됩니다.  
  
-   요소에 간단한 내용 유형을 **data ()** 요소의 형식화 된 값을 반환 합니다.  
  
-   노드가 xs: anytype과 포함 하는 복합 형식의 경우 **data ()** 정적 오류를 반환 합니다.  
  
 사용 합니다 **data ()** 함수는 지정 하는 다음 예와에서 같이 자주 선택적 합니다 **data ()** 함수에는 명시적으로 쿼리 가독성이 향상. 자세한 내용은 [XQuery 기초](../xquery/xquery-basics.md)합니다.  
  
 지정할 수 없습니다 **data ()** 에서 생성 된 XML에 다음과에서 같이 합니다.  
  
```  
declare @x xml  
set @x = ''  
select @x.query('data(<SomeNode>value</SomeNode>)')  
```  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예를 제공 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-data-xquery-function-to-extract-typed-value-of-a-node"></a>A. data() XQuery 함수를 사용하여 노드의 형식화된 값 추출  
 다음 쿼리를 보여 줍니다 하는 방법을 **data ()** 함수를 사용 하는 특성, 요소 및 텍스트 노드는 값을 검색 합니다.  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query(N'  
 for $pd in //p1:ProductDescription  
 return   
    <Root   
      ProductID = "{ data( ($pd//@ProductModelID)[1] ) }"   
      Feature =   "{ data( ($pd/p1:Features/wm:Warranty/wm:Description)[1] ) }" >  
    </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 다음은 결과입니다.  
  
```  
<Root ProductID="19" Feature="parts and labor"/>  
```  
  
 언급 했 듯이 합니다 **data ()** 함수는 특성을 생성 하는 경우 선택 사항입니다. 지정 하지 않으면 경우는 **data ()** 함수를 암시적으로 가정 합니다. 다음 쿼리에서는 이전 쿼리와 동일한 결과를 생성합니다.  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for $pd in //p1:ProductDescription  
         return   
          <Root    
                ProductID = "{ ($pd/@ProductModelID)[1] }"    
                Feature =   "{ ($pd/p1:Features/wm:Warranty/wm:Description)[1] }" >  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 다음 예에서는 인스턴스를 보여 줍니다.는 **data ()** 함수는 필요 합니다.  
  
 다음 쿼리에서 **$pd / p1:Specifications 자재 /** 반환 된 <`Material`> 요소. 또한 **데이터 ($pd/p1:Specifications 자재 /)** 때문에 문자 xdt: untypedatomic로 형식화 된 데이터를 반환 <`Material`>은 형식화 되지 않습니다. 입력이 형식화 된 경우, 결과 **data ()** 로 형식화 됩니다 **xdt: untypedatomic**합니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in //p1:ProductDescription  
         return   
          <Root>  
             { $pd/p1:Specifications/Material }  
             { data($pd/p1:Specifications/Material) }  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 다음은 결과입니다.  
  
```  
<Root>  
  <Material>Almuminum Alloy</Material>Almuminum Alloy  
</Root>  
```  
  
 다음 쿼리에서 **data($pd/p1:Features/wm:Warranty)** 때문에 정적 오류를 반환 합니다 <`Warranty`> 복합 형식 요소입니다.  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
 <Root>  
   {     /p1:ProductDescription/p1:Features/wm:Warranty }  
   { data(/p1:ProductDescription/p1:Features/wm:Warranty) }  
 </Root>  
 ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID = 23  
```  
  
## <a name="see-also"></a>관련 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

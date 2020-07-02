---
title: data 함수 (XQuery) | Microsoft Docs
description: XQuery 함수 data ()를 사용 하 여 지정 된 항목 시퀀스의 각 항목에 대해 형식화 된 값을 반환 하는 방법에 대해 알아봅니다.
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
ms.openlocfilehash: a5d0940f6e182d477d2c0660f4c93aaa9fedeb6f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85643546"
---
# <a name="data-accessor-functions---data-xquery"></a>데이터 접근자 함수 - data(XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  *$Arg*에 지정 된 각 항목에 대해 형식화 된 값을 반환 합니다.  
  
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
  
-   Attribute 노드가 형식화 되지 않은 경우 해당 형식화 된 값은 **xdt: untypedAtomic**인스턴스로 반환 된 문자열 값과 동일 합니다.  
  
-   요소 노드가 형식화 되지 않은 경우 해당 형식화 된 값은 **xdt: untypedAtomic**인스턴스로 반환 된 문자열 값과 동일 합니다.  
  
 형식화된 요소 노드에는 다음이 적용됩니다.  
  
-   요소에 단순 콘텐츠 형식이 있는 경우 **data ()** 는 요소의 형식화 된 값을 반환 합니다.  
  
-   노드가 xs: anyType을 포함 하는 복합 유형인 경우 **data ()** 는 정적 오류를 반환 합니다.  
  
 다음 예제와 같이 **data ()** 함수를 사용 하는 것은 대개 선택 사항 이지만 **data ()** 함수를 지정 하면 쿼리 가독성을 명시적으로 높일 수 있습니다. 자세한 내용은 [XQuery 기본 사항](../xquery/xquery-basics.md)을 참조 하세요.  
  
 다음과 같이 생성 된 XML에서는 **data ()** 를 지정할 수 없습니다.  
  
```  
declare @x xml  
set @x = ''  
select @x.query('data(<SomeNode>value</SomeNode>)')  
```  
  
## <a name="examples"></a>예제  
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
### <a name="a-using-the-data-xquery-function-to-extract-typed-value-of-a-node"></a>A. data() XQuery 함수를 사용하여 노드의 형식화된 값 추출  
 다음 쿼리에서는 **data ()** 함수를 사용 하 여 특성, 요소 및 텍스트 노드의 값을 검색 하는 방법을 보여 줍니다.  
  
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
  
 앞에서 설명한 것 처럼 **data ()** 함수는 특성을 생성할 때 선택 사항입니다. **Data ()** 함수를 지정 하지 않으면 암시적으로 가정 됩니다. 다음 쿼리에서는 이전 쿼리와 동일한 결과를 생성합니다.  
  
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
  
 다음 예에서는 **data ()** 함수가 필요한 인스턴스를 보여 줍니다.  
  
 다음 쿼리에서 **$pd/p1: 사양/자료** 는 <> 요소를 반환 합니다 `Material` . 또한 <>는 형식화 되지 않았기 때문에 **데이터 ($pd/p1: 사양/재질)** 는 Xdt: untypedAtomic로 형식화 된 문자 데이터를 반환 합니다. `Material` 입력이 형식화 되지 않은 경우 **data ()** 의 결과는 **xdt: untypedAtomic**로 형식화 됩니다.  
  
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
  
 다음 쿼리에서는 <> 복합 형식 요소 이기 때문에 **데이터 ($pd/p1: Features/wm: 보증)** 에서 정적 오류를 반환 합니다 `Warranty` .  
  
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
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

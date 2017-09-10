---
title: "숫자 함수 (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- number function
- fn:number function
ms.assetid: dff6d19b-765c-4df9-afff-9a0e7be9b91b
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dc0ea3abeb06377819bfae2486b5ddd44734123b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="functions-on-nodes---number"></a>노드-숫자 함수
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  표시 된 노드의 숫자 값을 반환 *$arg*합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:number() as xs:double?   
fn:number($arg as node()?) as xs:double?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 값이 숫자로 반환되는 노드입니다.  
  
## <a name="remarks"></a>주의  
 경우 *$arg* 은 지정 하지 않으면 double로 변환 하는 컨텍스트 노드의 숫자 값이 반환 됩니다. SQL Server에서 **fn:number()** 상황별 조건자의 컨텍스트에서 인수만 사용할 수 있습니다. 특히 사용 시 대괄호([])로 묶어야 합니다. 예를 들어 다음 식은 <`ROOT`> 요소를 반환합니다.  
  
```  
declare @x xml  
set @x='<ROOT>111</ROOT>'  
select @x.query('/ROOT[number()=111]')  
```  
  
 에 정의 된 노드의 값이 숫자는 단순 유형의 올바른 어휘 표현이 하지 **XML 스키마 파트 2: datatypes, W3C Recommendation**, 함수는 빈 시퀀스를 반환 합니다. NaN은 지원되지 않습니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-number-xquery-function-to-retrieve-the-numeric-value-of-an-attribute"></a>1. number() XQuery 함수를 사용하여 특성의 숫자 값 검색  
 다음 쿼리는 제품 모델 7의 제조 과정에 있는 첫 번째 업무 센터 위치에서 부지 크기 특성의 숫자 값을 검색합니다.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in (//AWMI:root//AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"   
                   LotSizeA="{  $i/@LotSize }"  
                   LotSizeB="{  number($i/@LotSize) }"  
                   LotSizeC="{ number($i/@LotSize) + 1 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   **number ()** 에 대 한 쿼리에 의해 표시 된 것 처럼 함수는 필요 하지는 **LotSizeA** 특성입니다. 이 함수는 XPath 1.0 함수이며 주로 이전 버전과의 호환성을 위해 사용됩니다.  
  
-   에 대 한 XQuery **LotSizeB** 숫자 함수를 지정 하 고 중복 됩니다.  
  
-   에 대 한 쿼리 **LotSizeD** 산술 연산에서 숫자 값의 사용을 보여 줍니다.  
  
 다음은 결과입니다.  
  
```  
ProductModelID   Result  
----------------------------------------------  
7              <Location LocationID="10"   
                         LotSizeA="100"   
                         LotSizeB="100"   
                         LotSizeC="101" />  
```  
  
### <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **number ()** 함수는 노드만 합니다. 원자 값을 사용하지 않습니다.  
  
-   숫자 값을 반환할 수 없는 경우는 **number ()** 함수는 NaN 대신 빈 시퀀스를 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

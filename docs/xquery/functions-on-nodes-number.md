---
title: number 함수 (XQuery) | Microsoft Docs
description: 지정 된 인수의 숫자 값을 반환 하는 XQuery 함수 번호 ()에 대해 알아봅니다.
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
- number function
- fn:number function
ms.assetid: dff6d19b-765c-4df9-afff-9a0e7be9b91b
author: rothja
ms.author: jroth
ms.openlocfilehash: c1a4d3014286618639b045f5028935368321a3a0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85753579"
---
# <a name="functions-on-nodes---number"></a>노드 함수 - number
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  *$Arg*표시 되는 노드의 숫자 값을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:number() as xs:double?   
fn:number($arg as node()?) as xs:double?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 값이 숫자로 반환되는 노드입니다.  
  
## <a name="remarks"></a>설명  
 *$Arg* 지정 하지 않으면 double로 변환 된 컨텍스트 노드의 숫자 값이 반환 됩니다. SQL Server에서 인수가 없는 **fn: number ()** 는 컨텍스트 종속 조건자의 컨텍스트에서만 사용할 수 있습니다. 특히 사용 시 대괄호([])로 묶어야 합니다. 예를 들어 다음 식은 <> 요소를 반환 합니다 `ROOT` .  
  
```  
declare @x xml  
set @x='<ROOT>111</ROOT>'  
select @x.query('/ROOT[number()=111]')  
```  
  
 **XML 스키마 파트 2: 데이터 형식 W3C 권장 사항**에 정의 된 대로 노드 값이 숫자 단순 형식의 올바른 어휘 표현이 아닌 경우 함수는 빈 시퀀스를 반환 합니다. NaN은 지원되지 않습니다.  
  
## <a name="examples"></a>예제  
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
### <a name="a-using-the-number-xquery-function-to-retrieve-the-numeric-value-of-an-attribute"></a>A. number() XQuery 함수를 사용하여 특성의 숫자 값 검색  
 다음 쿼리는 제품 모델 7의 제조 과정에 있는 첫 번째 업무 센터 위치에서 부지 크기 특성의 숫자 값을 검색합니다.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
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
  
-   **LotSizeA** 특성에 대 한 쿼리에 표시 된 것 처럼 **number ()** 함수는 필요 하지 않습니다. 이 함수는 XPath 1.0 함수이며 주로 이전 버전과의 호환성을 위해 사용됩니다.  
  
-   **LotSizeB** 에 대 한 XQuery는 number 함수를 지정 하며 중복 됩니다.  
  
-   **LotSizeD** 에 대 한 쿼리는 산술 연산에 숫자 값을 사용 하는 방법을 보여 줍니다.  
  
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
  
-   **Number ()** 함수는 노드만 허용 합니다. 원자 값을 사용하지 않습니다.  
  
-   값을 숫자로 반환할 수 없는 경우 **number ()** 함수는 NaN 대신 빈 시퀀스를 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

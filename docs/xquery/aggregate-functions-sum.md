---
title: sum 함수 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sum function [XQuery]
- fn:sum function
ms.assetid: 12288f37-b54c-4237-b75e-eedc5fe8f96d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 802c870f2ea22d24d8dfa80144a44f8805a14c96
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619961"
---
# <a name="aggregate-functions---sum"></a>집계 함수 - sum
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  일련의 숫자의 합계를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:sum($arg as xdt:anyAtomicType*) as xdt:anyAtomicType  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 합계가 계산되는 일련의 원자 값입니다.  
  
## <a name="remarks"></a>Remarks  
 에 전달 되는 세분화 된 값의 유형도 **sum ()** 동일한 기본 유형의 하위 유형 이어야 합니다. 허용된 기준 유형은 3가지 기본 제공 숫자 기준 유형이거나 xdt:untypedAtomic입니다. xdt:untypedAtomic 유형의 값이 xs:double로 캐스팅됩니다. 이러한 종류의 혼합 없거나 다른 형식의 다른 값을 전달 하는 경우 정적 오류가 발생 합니다.  
  
 결과인 **sum ()** 입력이 필요에 따라 빈 시퀀스인 경우에 xdt: untypedatomic의 경우 xs: double 처럼 전달 된 유형의 기본 유형을 받습니다. 입력이 정적으로 빈 경우 결과는 정적 및 동적 xs:integer 유형의 0입니다.  
  
 합니다 **sum ()** 함수는 숫자 값의 합계를 반환 합니다. 입력된 시퀀스에서 값을 xdt: untypedatomic 값을 xs: double로 캐스팅할 수 없습니다, 하는 경우 무시 됩니다 *$arg*합니다. 입력이 동적으로 계산된 빈 시퀀스인 경우 사용된 기준 유형의 값 0이 반환됩니다.  
  
 이 함수는 오버플로 또는 범위 초과 예외가 발생하는 경우 런타임 오류를 반환합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예를 제공 **xml** 유형 열에는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스입니다.  
  
### <a name="a-using-the-sum-xquery-function-to-find-the-total-combined-number-of-labor-hours-for-all-work-center-locations-in-the-manufacturing-process"></a>1. sum() XQuery 함수를 사용하여 제조 프로세스의 모든 작업 센터 위치에 대한 총 근로 시간 검색  
 다음 쿼리에서는 제조 지침이 저장된 모든 제품 모델에 대해 제조 프로세스에 포함된 모든 작업 센터 위치에 대한 총 근로 시간을 검색합니다.  
  
```  
SELECT Instructions.query('         
   declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
  <ProductModel PMID= "{ sql:column("Production.ProductModel.ProductModelID") }"         
  ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >         
   <TotalLaborHrs>         
     { sum(//AWMI:Location/@LaborHours) }         
   </TotalLaborHrs>         
 </ProductModel>         
    ') as Result         
FROM Production.ProductModel         
WHERE Instructions is not NULL         
```  
  
 다음은 결과의 일부입니다.  
  
```  
<ProductModel PMID="7" ProductModelName="HL Touring Frame">  
   <TotalLaborHrs>12.75</TotalLaborHrs>  
</ProductModel>  
<ProductModel PMID="10" ProductModelName="LL Touring Frame">  
  <TotalLaborHrs>13</TotalLaborHrs>  
</ProductModel>  
...  
```  
  
 결과를 XML로 반환하는 대신 다음 쿼리에서와 같이 관계형 결과를 생성하는 쿼리를 작성할 수 있습니다.  
  
```  
SELECT ProductModelID,         
        Name,         
        Instructions.value('declare namespace   
      AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
    sum(//AWMI:Location/@LaborHours)', 'float') as TotalLaborHours         
FROM Production.ProductModel         
WHERE Instructions is not NULL          
```  
  
 다음은 결과의 일부입니다.  
  
```  
ProductModelID Name                 TotalLaborHours         
-------------- -------------------------------------------------  
7              HL Touring Frame           12.75                   
10             LL Touring Frame           13                      
43             Touring Rear Wheel         3                       
...  
```  
  
### <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   단일 인수 버전만 **sum ()** 지원 됩니다.  
  
-   입력이 동적으로 계산된 빈 시퀀스인 경우 사용된 기준 유형의 값 0이 xs:integer 유형 대신 반환됩니다.  
  
-   합니다 **sum ()** 함수 모든 정수를 xs: decimal로 매핑합니다.  
  
-   합니다 **sum ()** xs: duration 유형의 값에는 함수가 지원 되지 않습니다.  
  
-   여러 기본 유형 범위의 유형이 혼합된 시퀀스는 지원되지 않습니다.  
  
-   sum((xs:double(“INF”), xs:double(“-INF”)))는 도메인 오류를 발생시킵니다.  
  
## <a name="see-also"></a>관련 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

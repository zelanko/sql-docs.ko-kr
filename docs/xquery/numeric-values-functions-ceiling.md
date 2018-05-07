---
title: ceiling 함수 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
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
- fn:ceiling function
- ceiling function [XQuery]
ms.assetid: 594f1dd0-3c27-41b3-b809-9ce6714c5a97
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1399fd20bf4d7af3fed85730fc397e1400347ad2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="numeric-values-functions---ceiling"></a>Ceiling-숫자 값 함수 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  소수점 부분이 없이 해당 인수의 값보다 작지 않은 가장 작은 수를 반환합니다. 인수가 빈 시퀀스이면 빈 시퀀스가 반환됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:ceiling ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 함수가 적용되는 번호입니다.  
  
## <a name="remarks"></a>주의  
 경우 유형의 *$arg* 세 가지 숫자 기본 형식 중 하나인 **xs: float**, **xs: double**, 또는 **xs: decimal**, 반환 형식이 동일 *$arg* 유형입니다.  
  
 경우 유형의 *$arg* 숫자 형식 중 하나에서 파생 된 형식이 반환 형식은 기본 숫자 형식입니다.  
  
 Fn: floor, fn: ceiling 또는 fn: round 함수에 대 한 입력 이면 **xdt: untypedatomic**, 암시적으로 캐스팅 된 **xs: double**합니다.  
  
 다른 유형을 사용하면 정적 오류가 발생합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-ceiling-xquery-function"></a>1. ceiling() XQuery 함수 사용  
 제품 모델 7에 대해 이 쿼리는 제품 모델의 제조 프로세스에 있는 작업 센터 위치 목록을 반환합니다. 각 작업 센터 위치에 대해 다음 쿼리는 문서화된 경우 위치 ID, 근무 시간 및 부지 크기를 반환합니다. 쿼리에서 사용 하 여는 **ceiling** 형식의 값으로 근무 시간을 반환 하도록 함수 **10 진수**합니다.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
     for $i in /AWMI:root/AWMI:Location  
     return   
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ ceiling($i/@LaborHours) }" >  
                    {   
                      $i/@LotSize  
                    }    
       </Location>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   AWMI 네임스페이스 접두사는 Adventure Works Manufacturing Instructions를 나타냅니다. 이 접두사는 쿼리되는 문서에 사용된 같은 네임스페이스를 참조합니다.  
  
-   **지침** 는 **xml** 유형 열입니다. 따라서는 [query () 메서드 (XML 데이터 형식)](../t-sql/xml/query-method-xml-data-type.md) XQuery를 지정 하는 데 사용 됩니다. XQuery 문은 쿼리 메서드에 대한 인수로 지정됩니다.  
  
-   **에 대 한... 반환** 은 루프 구성 합니다. 쿼리에서 **에 대 한** 루프의 목록을 확인 \<위치 > 요소입니다. 각 작업 센터 위치에 대 한는 **반환** 의 문에서 **에 대 한** 루프 설명 하는 XML을 생성할 수:  
  
    -   A \<위치 > LocationID 및 LaborHrs 특성이 있는 요소입니다. 중괄호({ }) 안에 있는 해당 식은 문서에서 필요한 값을 검색합니다.  
  
    -   {$i/@LotSize } 있는 경우 식은 문서에서 LotSize 특성을 검색 합니다.  
  
    -   다음은 결과입니다.  
  
```  
ProductModelID Result    
-------------- ------------------------------------------------------  
7      <Location LocationID="10" LaborHrs="3" LotSize="100"/>  
       <Location LocationID="20" LaborHrs="2" LotSize="1"/>     
       <Location LocationID="30" LaborHrs="1" LotSize="1"/>     
       <Location LocationID="45" LaborHrs="1" LotSize="20"/>  
       <Location LocationID="60" LaborHrs="3" LotSize="1"/>     
       <Location LocationID="60" LaborHrs="4" LotSize="1"/>  
```  
  
### <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **ceiling ()** 함수 모든 정수 값을 xs: decimal에 매핑합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [floor 함수 &#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [round 함수 &#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)  
  
  

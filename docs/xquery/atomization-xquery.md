---
title: 원자화 (XQuery) | Microsoft Docs
description: 항목의 형식화 된 값이 추출 되는 XQuery의 원자화 프로세스에 대해 알아봅니다.
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, atomization
- atomization [XQuery]
ms.assetid: e3d7cf2f-c6fb-43c2-8538-4470a6375af5
author: rothja
ms.author: jroth
ms.openlocfilehash: 24840ac01f448270e43065887746fd7230be4d35
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914665"
---
# <a name="atomization-xquery"></a>원자화(XQuery)
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  원자화는 항목의 유형 값을 추출하는 프로세스입니다. 이 프로세스는 특정 상황에서 적용됩니다. 산술 및 비교 연산자와 같은 일부 XQuery 연산자는 이 프로세스에 따라 달라집니다. 예를 들어 산술 연산자를 노드에 직접 적용 하면 [데이터 함수](../xquery/data-accessor-functions-data-xquery.md)를 암시적으로 호출 하 여 노드의 형식화 된 값이 먼저 검색 됩니다. 이렇게 하면 원자 값이 피연산자로 산술 연산자에 전달됩니다.  
  
 예를 들어 다음 쿼리는 LaborHours 특성의 합계를 반환합니다. 이 경우 **data ()** 는 특성 노드에 암시적으로 적용 됩니다.  
  
```  
declare @x xml  
set @x='<ROOT><Location LID="1" SetupTime="1.1" LaborHours="3.3" />  
<Location LID="2" SetupTime="1.0" LaborHours="5" />  
<Location LID="3" SetupTime="2.1" LaborHours="4" />  
</ROOT>'  
-- data() implicitly applied to the attribute node sequence.  
SELECT @x.query('sum(/ROOT/Location/@LaborHours)')  
```  
  
 필수는 아니지만 **data ()** 함수를 명시적으로 지정할 수도 있습니다.  
  
```  
SELECT @x.query('sum(data(ROOT/Location/@LaborHours))')  
```  
  
 암시적 원자화의 다른 예는 산술 연산자를 사용할 경우입니다. 연산자에는 **+** 원자 값이 필요 하며, **데이터 ()** 가 암시적으로 적용 되어 LaborHours 특성의 원자성 값을 검색 합니다. 이 쿼리는 제품 모델 테이블에서 **xml** 유형의 명령 열에 대해 지정 됩니다. 다음 쿼리는 LaborHours 특성을 3번 반환합니다. 쿼리에서 다음에 유의하십시오.  
  
-   OrignialLaborHours 특성을 구성할 때 원자화는 (`$WC/@LaborHours`)에서 반환된 단일 시퀀스에 암시적으로 적용됩니다. LaborHours 특성의 유형 값은 OrignialLaborHours에 할당됩니다.  
  
-   UpdatedLaborHoursV1 특성을 구성할 때 산술 연산자에 원자 값이 필요합니다. 따라서 **data ()** 는 ()에 의해 반환 되는 LaborHours 특성에 암시적으로 적용 됩니다 `$WC/@LaborHours` . 그런 다음 원자 값 1이 추가됩니다. UpdatedLaborHoursV2 특성을 생성 하면 데이터의 명시적 응용 프로그램 **()** 이 표시 되지만 반드시 필요한 것은 아닙니다.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location[1]  
        return  
            <WC OriginalLaborHours = "{ $WC/@LaborHours }"  
                UpdatedLaborHoursV1 = "{ $WC/@LaborHours + 1 }"   
                UpdatedLaborHoursV2 = "{ data($WC/@LaborHours) + 1 }" >  
            </WC>') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 다음은 결과입니다.  
  
```  
<WC OriginalLaborHours="2.5"   
    UpdatedLaborHoursV1="3.5"   
    UpdatedLaborHoursV2="3.5" />  
```  
  
 원자화 결과 단순 유형 인스턴스, 빈 집합 또는 정적 유형 오류가 생성됩니다.  
  
 원자화는 함수에 전달 된 비교 식 매개 변수, 함수에서 반환 된 값, **cast ()** 식 및 order by 절에 전달 된 정렬 식 에서도 발생 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [XQuery 기본 사항](../xquery/xquery-basics.md)   
 [XQuery &#40;비교 식&#41;](../xquery/comparison-expressions-xquery.md)   
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

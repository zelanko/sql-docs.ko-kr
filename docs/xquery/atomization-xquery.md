---
title: 원자화 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, atomization
- atomization [XQuery]
ms.assetid: e3d7cf2f-c6fb-43c2-8538-4470a6375af5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7cdedffaee342d389c4455b1d0441cca1226789e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47800421"
---
# <a name="atomization-xquery"></a>원자화(XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  원자화는 항목의 유형 값을 추출하는 프로세스입니다. 이 프로세스는 특정 상황에서 적용됩니다. 산술 및 비교 연산자와 같은 일부 XQuery 연산자는 이 프로세스에 따라 달라집니다. 예를 들어 노드로 직접 산술 연산자를 적용 하면 노드의 형식화 된 값은 먼저 검색 암시적으로 호출 하 여 합니다 [데이터 함수](../xquery/data-accessor-functions-data-xquery.md)합니다. 이렇게 하면 원자 값이 피연산자로 산술 연산자에 전달됩니다.  
  
 예를 들어 다음 쿼리는 LaborHours 특성의 합계를 반환합니다. 이 예에서 **data ()** 는 암시적으로 특성 노드에 적용 됩니다.  
  
```  
declare @x xml  
set @x='<ROOT><Location LID="1" SetupTime="1.1" LaborHours="3.3" />  
<Location LID="2" SetupTime="1.0" LaborHours="5" />  
<Location LID="3" SetupTime="2.1" LaborHours="4" />  
</ROOT>'  
-- data() implicitly applied to the attribute node sequence.  
SELECT @x.query('sum(/ROOT/Location/@LaborHours)')  
```  
  
 또한 명시적으로 지정할 수 필요 하지는 않지만 합니다 **data ()** 함수:  
  
```  
SELECT @x.query('sum(data(ROOT/Location/@LaborHours))')  
```  
  
 암시적 원자화의 다른 예는 산술 연산자를 사용할 경우입니다. 합니다 **+** 연산자에 원자 값이 필요 하 고 **data ()** LaborHours 특성의 원자 값을 검색에 암시적으로 적용 됩니다. 쿼리는 Instructions 열에 대해 지정 됩니다 합니다 **xml** ProductModel 테이블의 형식입니다. 다음 쿼리는 LaborHours 특성을 3번 반환합니다. 쿼리에서 다음에 유의하십시오.  
  
-   OrignialLaborHours 특성을 구성할 때 원자화는 (`$WC/@LaborHours`)에서 반환된 단일 시퀀스에 암시적으로 적용됩니다. LaborHours 특성의 유형 값은 OrignialLaborHours에 할당됩니다.  
  
-   UpdatedLaborHoursV1 특성을 구성할 때 산술 연산자에 원자 값이 필요합니다. 따라서 **data ()** 에서 반환 된 LaborHours 특성에 암시적으로 적용 됩니다 (`$WC/@LaborHours`). 그런 다음 원자 값 1이 추가됩니다. UpdatedLaborHoursV2 특성의 명시적 응용 프로그램을 보여 줍니다 **data ()**, 필수는 아닙니다.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
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
  
 원자화는 함수, 함수에서 반환 되는 값을 전달 하는 비교 식 매개 변수의 발생 **캐스팅할** 식 및 by 절 순서 대로 전달 된 순서 식입니다.  
  
## <a name="see-also"></a>관련 항목  
 [XQuery 기초](../xquery/xquery-basics.md)   
 [비교 식 &#40;XQuery&#41;](../xquery/comparison-expressions-xquery.md)   
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

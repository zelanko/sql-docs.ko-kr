---
title: last 함수 (XQuery) | Microsoft Docs
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
- last function [XQuery]
- fn:last function
ms.assetid: dc92086e-3b01-4b0b-9f54-3bbf306cf7ae
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7220b0fe10f88ec9ba78d31a8507d12eba7aafff
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51674072"
---
# <a name="context-functions---last-xquery"></a>컨텍스트 함수 - last(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  현재 처리 중인 시퀀스의 항목 수를 반환합니다. 특히 시퀀스에서 마지막 항목의 정수 인덱스를 반환합니다. 시퀀스의 첫 번째 항목에는 인덱스 값 1이 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:last() as xs:integer  
```  
  
## <a name="remarks"></a>Remarks  
 SQL server에서 **fn:last()** 상황별 조건자의 경우에만 사용할 수 있습니다. 특히 사용 시 대괄호(`[ ]`)로 묶어야 합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예를 제공 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-last-xquery-function-to-retrieve-the-last-two-manufacturing-steps"></a>1. last() XQuery 함수를 사용하여 마지막 두 제조 단계 검색  
 다음 쿼리는 특정 제품 모델의 마지막 두 제조 단계를 검색합니다. 값이 고, 반환한 제조 단계 수를 **last ()** 함수는이 쿼리에서 마지막 두 제조 단계 검색 하는 데 사용 됩니다.  
  
```  
SELECT ProductModelID, Instructions.query('   
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  <LastTwoManuSteps>  
   <Last-1Step>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[(last()-1)]/text() }  
   </Last-1Step>  
   <LastStep>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[last()]/text() }  
   </LastStep>  
  </LastTwoManuSteps>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 이전 쿼리에서 **last ()** 함수 /`/AWMI:root//AWMI:Location)[1]/AWMI:step[last()]` 제조 단계 수를 반환 합니다. 이 값은 업무 센터 위치에서 마지막 제조 단계를 검색하는 데 사용됩니다.  
  
 다음은 결과입니다.  
  
```  
ProductModelID Result    
-------------- -------------------------------------  
7      <LastTwoManuSteps>  
         <Last-1Step>  
            When finished, inspect the forms for defects per   
            Inspection Specification .  
         </Last-1Step>  
         <LastStep>Remove the frames from the tool and place them   
            in the Completed or Rejected bin as appropriate.  
         </LastStep>  
       </LastTwoManuSteps>  
```  
  
## <a name="see-also"></a>관련 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

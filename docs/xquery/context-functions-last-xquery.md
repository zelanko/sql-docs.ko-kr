---
title: last 함수 (XQuery) | Microsoft Docs
description: 시퀀스에서 마지막 항목의 정수 인덱스를 반환 하는 XQuery last () 함수에 대해 알아봅니다.
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
ms.openlocfilehash: 3713f0fadfe186c31a26f2f19adea88da2f28384
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729517"
---
# <a name="context-functions---last-xquery"></a>컨텍스트 함수 - last(XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  현재 처리 중인 시퀀스의 항목 수를 반환합니다. 특히 시퀀스에서 마지막 항목의 정수 인덱스를 반환합니다. 시퀀스의 첫 번째 항목에는 인덱스 값 1이 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:last() as xs:integer  
```  
  
## <a name="remarks"></a>설명  
 SQL Server에서 **fn: last ()** 는 컨텍스트 종속 조건자의 컨텍스트에서만 사용할 수 있습니다. 특히 사용 시 대괄호(`[ ]`)로 묶어야 합니다.  
  
## <a name="examples"></a>예제  
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
### <a name="a-using-the-last-xquery-function-to-retrieve-the-last-two-manufacturing-steps"></a>A. last() XQuery 함수를 사용하여 마지막 두 제조 단계 검색  
 다음 쿼리는 특정 제품 모델의 마지막 두 제조 단계를 검색합니다. Last **()** 함수에서 반환 되는 제조 단계 수 값은 마지막 두 제조 단계를 검색 하기 위해이 쿼리에서 사용 됩니다.  
  
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
  
 위의 쿼리에서 **last ()** 함수는 `/AWMI:root//AWMI:Location)[1]/AWMI:step[last()]` 제조 단계 수를 반환 합니다. 이 값은 업무 센터 위치에서 마지막 제조 단계를 검색하는 데 사용됩니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

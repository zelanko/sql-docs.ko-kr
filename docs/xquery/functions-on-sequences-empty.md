---
title: "빈 함수 (XQuery) | Microsoft Docs"
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
- empty function
- fn:empty function
ms.assetid: 46da89a8-0cd9-4913-8521-4087589a04ba
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1ca580d89bf60046aaf2d02315f18b12772e0bea
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="functions-on-sequences---empty"></a>시퀀스-빈 함수
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이면 True를 반환 값 *$arg* 빈 시퀀스는 합니다. 그렇지 않으면 함수에서 False를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:empty($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 항목의 시퀀스입니다. 시퀀스가 비어 있으면 함수에서 True를 반환합니다. 그렇지 않으면 함수에서 False를 반환합니다.  
  
## <a name="remarks"></a>주의  
 **fn:exists()** 함수가 지원 되지 않습니다. 대신는 **not ()** 함수를 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-empty-xquery-function-to-determine-if-an-attribute-is-present"></a>1. empty() XQuery 함수를 사용하여 특성이 있는지 확인  
 제품 모델 7의 제조 프로세스에서이 쿼리는 반환 되지 않은 모든 작업 센터 위치는 **MachineHours** 특성입니다.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     for $i in /AWMI:root/AWMI:Location[empty(@MachineHours)]  
     return  
       <Location  
            LocationID="{ ($i/@LocationID) }"  
            LaborHrs="{ ($i/@LaborHours) }" >  
            {   
              $i/@MachineHours  
            }    
       </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 다음은 결과입니다.  
  
```  
ProductModelID      Result          
-------------- ------------------------------------------  
7              <Location LocationID="30" LaborHrs="1"/>  
               <Location LocationID="50" LaborHrs="3"/>  
               <Location LocationID="60" LaborHrs="4"/>  
```  
  
 다음의 약간 수정 된 쿼리 하는 경우 "NotFound" 반환 된 **MachineHour** 특성이 없으면:  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace p14="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     for $i in /p14:root/p14:Location  
     return  
       <Location  
            LocationID="{ ($i/@LocationID) }"  
            LaborHrs="{ ($i/@LaborHours) }" >  
            {   
                 if (empty($i/@MachineHours)) then  
                    attribute MachineHours { "NotFound" }  
                 else  
                    attribute MachineHours { data($i/@MachineHours) }  
            }    
       </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 다음은 결과입니다.  
  
```  
ProductModelID Result                         
-------------- -----------------------------------  
7                
  <Location LocationID="10" LaborHrs="2.5" MachineHours="3"/>  
  <Location LocationID="20" LaborHrs="1.75" MachineHours="2"/>  
  <Location LocationID="30" LaborHrs="1" MachineHours="NotFound"/>  
  <Location LocationID="45" LaborHrs="0.5" MachineHours="0.65"/>  
  <Location LocationID="50" LaborHrs="3" MachineHours="NotFound"/>  
  <Location LocationID="60" LaborHrs="4" MachineHours="NotFound"/>  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Xml 데이터 형식에 대 한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)   
 [존재 &#40; &#41; 방법 &#40; xml 데이터 형식 &#41;](../t-sql/xml/exist-method-xml-data-type.md)  
  
  


---
title: '예: XMLTEXT 지시어 지정 | Microsoft 문서'
ms.custom: ''
ms.date: 04/05/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- XMLTEXT directive
ms.assetid: e78008ec-51e8-4fd1-b86f-1058a781de17
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2019e547dca2415c3b40f5e14c5286e0cd05682c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="example-specifying-the-xmltext-directive"></a>예: XMLTEXT 지시어 지정
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  이 예에서는 EXPLICIT 모드를 사용하는 **문에서** XMLTEXT `SELECT` 지시어를 사용하여 오버플로 열의 데이터 주소를 지정하는 방법을 보여 줍니다.  
  
 `Person` 테이블을 검토해 보면 이 테이블에는 XML 문서 중 사용되지 않은 부분을 저장하는 `Overflow` 열이 있는 것을 볼 수 있습니다.  
  
```  
USE tempdb;  
GO  
CREATE TABLE Person(PersonID varchar(5), PersonName varchar(20), Overflow nvarchar(200));  
GO  
INSERT INTO Person VALUES   
    ('P1','Joe',N'<SomeTag attr1="data">content</SomeTag>')  
   ,('P2','Joe',N'<SomeTag attr2="data"/>')  
   ,('P3','Joe',N'<SomeTag attr3="data" PersonID="P">content</SomeTag>');  
```  
  
 이 쿼리는 `Person` 테이블로부터 열을 검색합니다. `Overflow` 열에 대해 *AttributeName* 은 지정되어 있지 않지만 범용 테이블 열 이름을 제공하는 중에 *directive* 가 `XMLTEXT` 로 설정됩니다.  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!!XMLTEXT] -- No AttributeName; XMLTEXT directive  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 결과 XML 문서에서 다음에 유의하십시오.  
  
-   *AttributeName*이 `Overflow` 열에 대해 지정되어 있지 않고 `xmltext` 지시어가 지정되어 있기 때문에 <`Parent`> 요소의 특성이 묶는 <`overflow`> 요소의 특성 목록에 첨부됩니다.  
  
-   <`xmltext`> 요소의 `PersonID` 특성은 동일 요소 수준에서 검색된 `PersonID` 특성과 충돌하기 때문에 <`xmltext`> 요소의 특성은 `PersonID`가 NULL인 경우에도 무시됩니다. 특성은 일반적으로 오버플로의 동일한 이름의 특성에 우선합니다.  
  
 다음은 결과입니다.  
  
 ```   
 <Parent PersonID="P1" PersonName="Joe" attr1="data">content</Parent>  
 <Parent PersonID="P2" PersonName="Joe" attr2="data"></Parent>  
 <Parent PersonID="P3" PersonName="Joe" attr3="data">content</Parent>
 ```  
  
 오버플로 데이터에 하위 요소가 있고 동일한 쿼리가 지정되는 경우에는 `Overflow` 열의 하위 요소들이 묶는 <`Parent`> 요소의 하위 요소로 추가됩니다.  
  
 예를 들어 `Person` 열에 하위 요소가 있게 되도록 `Overflow` 테이블의 데이터를 변경합니다.  
  
```  
USE tempdb;  
GO  
TRUNCATE TABLE Person;  
GO  
INSERT INTO Person VALUES   
    ('P1','Joe',N'<SomeTag attr1="data">content</SomeTag>')  
   ,('P2','Joe',N'<SomeTag attr2="data"/>')  
    ,('P3','Joe',N'<SomeTag attr3="data" PersonID="P"><name>PersonName</name></SomeTag>');  
```  
  
 동일한 쿼리가 실행되는 경우에는 <`xmltext`> 요소의 하위 요소가, 묶는 <`Parent`> 요소의 하위 요소로 추가됩니다.  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!!XMLTEXT] -- no AttributeName, XMLTEXT directive  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 다음은 결과입니다.  
  
 ```   
 <Parent PersonID="P1" PersonName="Joe" attr1="data">content</Parent>  
 <Parent PersonID="P2" PersonName="Joe" attr2="data"></Parent>  
 <Parent PersonID="P3" PersonName="Joe" attr3="data">  
 <name>PersonName</name>  
 </Parent>
 ```  
  
 *AttributeName*이 `xmltext` 지시어와 함께 지정된 경우 <`overflow`> 요소의 특성이 묶는 <`Parent`> 요소의 하위 요소에 대한 특성으로 추가됩니다. *AttributeName* 에 대해 지정된 이름은 하위 요소의 이름이 됩니다.  
  
 이 쿼리에서 *AttributeName*인 <`overflow`>는 `xmltext` 지시어와 함께 지정됩니다.  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!overflow!XMLTEXT] -- Overflow is AttributeName  
                      -- XMLTEXT is a directive  
FROM Person  
FOR XML EXPLICIT  
```  
  
 다음은 결과입니다.  
  
 ```   
 <Parent PersonID="P1" PersonName="Joe">  
 <overflow attr1="data">content</overflow>  
 </Parent>  
 <Parent PersonID="P2" PersonName="Joe">  
 <overflow attr2="data" />  
 </Parent>  
 <Parent PersonID="P3" PersonName="Joe">  
 <overflow attr3="data" PersonID="P">  
 <name>PersonName</name>  
 </overflow>  
 </Parent>
 ```  
  
 이 쿼리 요소에서는 *지시어와 함께 지정됩니다.* 가 `PersonName` 특성에 대해 지정됩니다. 그 결과 `PersonName`이 묶는 <`Parent`> 요소의 하위 요소로 추가됩니다. <`xmltext`>의 특성은 계속해서 묶는 <`Parent`> 요소에 첨부됩니다. <`overflow`> 요소인 하위 요소의 내용은 묶는 <`Parent`> 요소의 다른 하위 요소 앞에 놓입니다.  
  
```  
SELECT 1      AS Tag, NULL as parent,  
       PersonID   AS [Parent!1!PersonID],  
       PersonName AS [Parent!1!PersonName!element], -- element directive  
       Overflow   AS [Parent!1!!XMLTEXT]  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 다음은 결과입니다.  
  
 ```   
 <Parent PersonID="P1" attr1="data">content<PersonName>Joe</PersonName>  
 </Parent>  
 <Parent PersonID="P2" attr2="data">  
 <PersonName>Joe</PersonName>  
 </Parent>  
 <Parent PersonID="P3" attr3="data">  
 <name>PersonName</name>  
 <PersonName>Joe</PersonName>  
 </Parent>
 ```  
  
 `XMLTEXT` 열 데이터의 경우 루트 요소에 특성이 있으면 이 특성은 XML 데이터 스키마에 표시되지 않고 MSXML 파서는 결과 XML 문서 조각의 유효성을 검사하지 않습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
SELECT 1 AS Tag,  
       0 ASParent,  
       N'<overflow a="1"/>' AS 'overflow!1!!xmltext'  
FOR XML EXPLICIT, xmldata;  
```  
  
 다음은 결과입니다. 반환된 스키마에서는 오버플로 특성 `a` 가 스키마에서 손실됩니다.  
  
 ```   
 <Schema name="Schema2"  
 xmlns="urn:schemas-microsoft-com:xml-data"  
 xmlns:dt="urn:schemas-microsoft-com:datatypes">  
 <ElementType name="overflow" content="mixed" model="open">`  
 </ElementType>`  
 </Schema>`  
 <overflow xmlns="x-schema:#Schema2" a="1">  
 </overflow>
 ```  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 EXPLICIT 모드 사용](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  

---
title: "(XML DML)의 값을 대체 | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- XML DML [SQL Server]
- update keyword
- replacement values [XML DML]
- updating node values
- replace value of XML DML statement
ms.assetid: c310f6df-7adf-493b-b56b-8e3143b13ae7
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2ac4a0a7f1e2dc5d5f268c306c0e1a92316c99da
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="replace-value-of-xml-dml"></a>replace value of(XML DML)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  문서의 노드 값을 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
replace value of Expression1   
with Expression2  
```  
  
## <a name="arguments"></a>인수  
 *Expression1*  
 업데이트할 값이 있는 노드를 식별합니다. 하나의 노드만 식별해야 합니다. 즉, *Expression1* 정적 단일 항목 이어야 합니다. XML이 형식화되는 경우 노드 유형은 단순 유형이어야 합니다. 노드를 여러 개 선택하면 오류가 발생합니다. 경우 *Expression1* 빈 시퀀스 이면 값이 대체 되지 발생을 반환 하 고 오류가 반환 됩니다. *Expression1* 단순히 유형의 콘텐츠 (목록 또는 원자성 유형), 텍스트 노드 또는 특성 노드에 있는 단일 요소를 반환 해야 합니다. *Expression1* 공용 구조체 유형, 복합 유형, 처리 명령, 문서 노드 또는 주석 노드 수 없습니다. 이들 중 하나인 경우 오류가 반환됩니다.  
  
 *Expression2*  
 노드의 새 값을 식별합니다. 때문에 단순 유형의 노드를 반환 하는 식이 될 수 있습니다이 **data ()** 암시적으로 사용 됩니다. 값이 값의 목록에서 **업데이트** 문은 이전 값을 목록으로 대체 합니다. 형식화 된 XML 인스턴스를 수정 하는 *Expression2* 의 하위 형식 이거나 같은 형식 이어야 합니다 *식*1입니다. 그렇지 않으면 오류가 반환됩니다. 형식화 되지 않은 XML 인스턴스를 수정 하는 *Expression2* 원자화 될 수 있는 식 이어야 합니다. 그렇지 않으면 오류가 반환됩니다.  
  
## <a name="examples"></a>예  
 다음 예제는 **replace value o f** XML DML 문은 XML 문서에서 노드를 업데이트 하는 방법을 보여 줍니다.  
  
### <a name="a-replacing-values-in-an-xml-instance"></a>1. XML 인스턴스에서 값 바꾸기  
 다음 예제에서는 문서 인스턴스를 먼저 변수에 할당 됩니다 **xml** 유형입니다. 그런 다음 **replace value o f** XML DML 문이 문서의 값을 업데이트 합니다.  
  
```  
DECLARE @myDoc xml;  
SET @myDoc = '<Root>  
<Location LocationID="10"   
            LaborHours="1.1"  
            MachineHours=".2" >Manufacturing steps are described here.  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>';  
SELECT @myDoc;  
  
-- update text in the first manufacturing step  
SET @myDoc.modify('  
  replace value of (/Root/Location/step[1]/text())[1]  
  with     "new text describing the manu step"  
');  
SELECT @myDoc;  
-- update attribute value  
SET @myDoc.modify('  
  replace value of (/Root/Location/@LaborHours)[1]  
  with     "100.0"  
');  
SELECT @myDoc;  
```  
  
 업데이트될 대상은 경로 식에서 식 끝에 "[1]"을 추가하여 명시적으로 지정된 최대 하나의 노드여야 합니다.  
  
### <a name="b-using-the-if-expression-to-determine-replacement-value"></a>2. if 식을 사용하여 대체 값 결정  
 지정할 수는 **경우** 식의 Expression2에는 **XML DML의 값을 대체** 다음 예제와 같이 문을 합니다. Expression1은 첫 번째 작업 센터의 LaborHours 특성이 업데이트될 것임을 확인합니다. 사용 하 여 Expression2는 **경우** LaborHours 특성의 새 값을 확인 하는 식입니다.  
  
```  
DECLARE @myDoc xml  
SET @myDoc = '<Root>  
<Location LocationID="10"   
            LaborHours=".1"  
            MachineHours=".2" >Manu steps are described here.  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>'  
--SELECT @myDoc  
  
SET @myDoc.modify('  
  replace value of (/Root/Location[1]/@LaborHours)[1]  
  with (  
       if (count(/Root/Location[1]/step) > 3) then  
         "3.0"  
       else  
          "1.0"  
      )  
')  
SELECT @myDoc  
```  
  
### <a name="c-updating-xml-stored-in-an-untyped-xml-column"></a>3. 형식화되지 않은 XML 열에 저장된 XML 업데이트  
 다음 예에서는 열에 저장되어 있는 XML을 업데이트합니다.  
  
```  
drop table T  
go  
CREATE TABLE T (i int, x xml)  
go  
INSERT INTO T VALUES(1,'<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>')  
go  
-- verify the current <ProductDescription> element  
SELECT x.query(' /Root/ProductDescription')  
FROM T  
-- update the ProductName attribute value  
UPDATE T  
SET x.modify('  
  replace value of (/Root/ProductDescription/@ProductName)[1]  
  with "New Road Bike" ')  
-- verify the update  
SELECT x.query(' /Root/ProductDescription')  
FROM T  
```  
  
### <a name="d-updating-xml-stored-in-a-typed-xml-column"></a>4. 형식화된 XML 열에 저장되어 있는 XML 업데이트  
 다음 예에서는 형식화된 XML 열에 저장되어 있는 제조 지침 문서의 값을 대체합니다.  
  
 이 예에서는 먼저 AdventureWorks 데이터베이스에서 형식화된 XML 열을 가진 테이블(T)을 만듭니다. 그런 다음 ProductModel 테이블의 Instructions 열의 제조 지침 XML 인스턴스를 테이블 T로 복사합니다. 그러면 테이블 T의 XML에 삽입 내용이 적용됩니다.  
  
```  
use AdventureWorks  
go  
drop table T  
go  
create table T(ProductModelID int primary key,   
Instructions xml (Production.ManuInstructionsSchemaCollection))  
go  
insert  T   
select ProductModelID, Instructions  
from Production.ProductModel  
where ProductModelID=7  
go  
--insert a new location - <Location 1000/>.   
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
insert <MI:Location LocationID="1000"  LaborHours="1000"  LotSize="1000" >  
           <MI:step>Do something using <MI:tool>hammer</MI:tool></MI:step>  
         </MI:Location>  
  as first  
  into   (/MI:root)[1]  
')  
go  
select Instructions  
from T  
go  
-- Now replace manu. tool in location 1000  
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  replace value of (/MI:root/MI:Location/MI:step/MI:tool)[1]   
  with   "screwdriver"  
')  
go  
select Instructions  
from T  
-- Now replace value of lot size  
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  replace value of (/MI:root/MI:Location/@LotSize)[1]   
  with   500 cast as xs:decimal ?  
')  
go  
select Instructions  
from T  
```  
  
 사용 하 여 **캐스트** LotSize 값을 대체할 때. 값이 특정 유형인 경우 이렇게 해야 합니다. 이 예에서 값이 500인 경우 명시적 캐스트가 필요하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 데이터 수정 언어 &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

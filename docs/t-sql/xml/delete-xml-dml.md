---
title: delete(XML DML) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- XML DML [SQL Server]
- delete keyword
- delete statement [XML DML]
- deleting nodes
ms.assetid: b22c93a4-b84d-4356-af4c-6013322a4b71
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6c2fd2c71c5272b8104eaf5b24fa8e7c0a9fc8c
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56038554"
---
# <a name="delete-xml-dml"></a>delete(XML DML)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  XML 인스턴스에서 노드를 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
delete Expression  
```  
  
## <a name="arguments"></a>인수  
 *식*  
 삭제할 노드를 식별하는 XQuery 식입니다. 식에서 선택한 모든 노드 및 선택한 노드에 포함된 모든 노드와 값이 삭제됩니다. [insert(XML DML)](../../t-sql/xml/insert-xml-dml.md)에서 설명한 대로 이 식은 문서에 있는 기존 노드에 대한 참조여야 합니다. 생성된 노드여서는 안 됩니다. 식은 루트(/) 노드일 수 없습니다. 식이 빈 시퀀스를 반환할 경우 아무것도 삭제되지 않으며 오류가 반환되지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-deleting-nodes-from-a-document-stored-in-an-untyped-xml-variable"></a>1. 형식화되지 않은 xml 변수에 저장된 문서에서 노드 삭제  
 다음 예에서는 문서에서 여러 노드를 삭제하는 방법을 보여 줍니다. 먼저 **xml** 형식의 변수에 XML 인스턴스가 할당됩니다. 그런 다음 이후의 delete XML DML 문이 문서에서 여러 노드를 삭제합니다.  
  
```  
DECLARE @myDoc xml  
SET @myDoc = '<?Instructions for=TheWC.exe ?>   
<Root>  
 <!-- instructions for the 1st work center -->  
<Location LocationID="10"   
            LaborHours="1.1"  
            MachineHours=".2" >Some text 1  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>'  
SELECT @myDoc  
  
-- delete an attribute  
SET @myDoc.modify('  
  delete /Root/Location/@MachineHours  
')  
SELECT @myDoc  
  
-- delete an element  
SET @myDoc.modify('  
  delete /Root/Location/step[2]  
')  
SELECT @myDoc  
  
-- delete text node (in <Location>  
SET @myDoc.modify('  
  delete /Root/Location/text()  
')  
SELECT @myDoc  
  
-- delete all processing instructions  
SET @myDoc.modify('  
  delete //processing-instruction()  
')  
SELECT @myDoc  
```  
  
### <a name="b-deleting-nodes-from-a-document-stored-in-an-untyped-xml-column"></a>2. 형식화되지 않은 xml 열에 저장된 문서에서 노드 삭제  
 다음 예에서 **delete** XML DML 문은 열에 저장된 문서에서 <`Features`>의 두 번째 자식 요소를 제거합니다.  
  
```  
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
-- verify the contents before delete  
SELECT x.query(' //ProductDescription/Features')  
FROM T  
-- delete the second feature  
UPDATE T  
SET x.modify('delete /Root/ProductDescription/Features/*[2]')  
-- verify the deletion  
SELECT x.query(' //ProductDescription/Features')  
FROM T  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   [modify() 메서드(xml 데이터 형식)](../../t-sql/xml/modify-method-xml-data-type.md)는 **delete** XML DML 키워드를 지정하는 데 사용됩니다.  
  
-   [query() 메서드(xml 데이터 형식)](../../t-sql/xml/query-method-xml-data-type.md)는 문서를 쿼리하는 데 사용됩니다.  
  
### <a name="c-deleting-nodes-from-a-typed-xml-column"></a>C. 형식화된 xml 열에서 노드 삭제  
 이 예에서는 형식화된 **xml** 열에 저장된 제조 지침 XML 문서에서 노드를 삭제합니다.  
  
 이 예에서는 먼저 AdventureWorks 데이터베이스에서 형식화된 **xml** 열을 가진 테이블(T)을 만듭니다. 그런 다음 ProductModel 테이블의 Instructions 열에 있는 제조 지침 XML 인스턴스를 T 테이블로 복사하고 문서에서 하나 이상의 노드를 삭제합니다.  
  
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
select Instructions  
from T  
--1) insert <Location 1000/>. Note: <Root> must be singleton in the query  
update T  
set Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  insert <MI:Location LocationID="1000"  LaborHours="1000" >  
           These are manu steps at location 1000.   
           <MI:step>New step1 instructions</MI:step>  
           Instructions for step 2 are here  
           <MI:step>New step 2 instructions</MI:step>  
         </MI:Location>  
  as first  
  into   (/MI:root)[1]  
')  
go  
select Instructions  
from T  
  
-- delete an attribute  
update T  
set Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/@LaborHours)   
')  
go  
select Instructions  
from T  
-- delete text in <location>  
update T  
set Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/text())   
')  
go  
select Instructions  
from T  
-- delete 2nd manu step at location 1000  
update T  
set Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/MI:step[2])   
')  
go  
select Instructions  
from T  
-- cleanup  
drop table T  
go  
```  
  
## <a name="see-also"></a>참고 항목  
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML&#40;XML 데이터 수정 언어&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

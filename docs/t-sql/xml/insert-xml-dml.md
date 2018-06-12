---
title: insert(XML DML) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- XML DML [SQL Server]
- inserting nodes
- insert keyword [XML DML]
- insert XML DML statement
ms.assetid: 0c95c2b3-5cc2-4c38-9e25-86493096c442
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 22bc1b365e04c5e06e6278974346b1626434a24b
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34744072"
---
# <a name="insert-xml-dml"></a>insert(XML DML)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  *Expression1*에 의해 식별된 하나 이상의 노드를 *Expression2*에 의해 식별된 자식 노드 또는 노드의 형제로 삽입합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
insert   
      Expression1 (  
                 {as first | as last} into | after | before  
                                    Expression2  
                )  
```  
  
## <a name="arguments"></a>인수  
 *Expression1*  
 삽입할 하나 이상의 노드를 식별합니다. 이는 상수 XML 인스턴스, 수정 메서드가 적용되고 있는 XML 스키마 컬렉션과 동일하게 형식화된 XML 데이터 형식 인스턴스에 대한 참조, 독립 실행형 **sql:column()**/**sql:variable()** 함수를 사용하는 형식화되지 않은 XML 데이터 형식 인스턴스 또는 XQuery 식일 수 있습니다. 식 결과는 노드, 텍스트 노드 또는 노드의 정렬된 시퀀스일 수 있습니다. 루트(/) 노드로는 확인될 수 없습니다. 식 결과가 값이나 값의 시퀀스인 경우 해당 값은 시퀀스의 각 값을 구분하기 위한 공백이 포함된 단일 텍스트 노드로 삽입됩니다. 여러 노드를 상수로 지정하는 경우 괄호 안에 노드가 포함되고 쉼표로 구분됩니다. 요소, 특성 또는 값의 시퀀스와 같은 유형이 다른 시퀀스는 삽입할 수 없습니다. *Expression1*이 빈 시퀀스로 확인되는 경우 삽입이 수행되지 않고 오류가 반환되지 않습니다.  
  
 into  
 *Expression1*에 의해 식별된 노드는 *Expression2*에 의해 식별된 노드의 직접 하위 항목(자식 노드)으로 삽입됩니다. *Expression2*의 노드에 이미 하나 이상의 자식 노드가 있는 경우 **as first** 또는 **as last**를 사용하여 새 노드를 추가할 위치를 지정해야 합니다. 예를 들어 자식 목록의 시작이나 끝에 노드를 각각 추가합니다. **as first** 및 **as last** 키워드는 특성이 삽입된 경우 무시됩니다.  
  
 after  
 *Expression1*에 의해 식별된 노드는 *Expression2*에 의해 식별된 노드 바로 다음에 형제로 삽입됩니다. **after** 키워드는 특성을 삽입하는 데 사용할 수 없습니다. 예를 들어 이 키워드를 사용하여 특성 생성자를 삽입하거나 XQuery에서 특성을 반환할 수 없습니다.  
  
 before  
 *Expression1*에 의해 식별된 노드는 *Expression2*에 의해 식별된 노드 바로 앞에 형제로 삽입됩니다. **before** 키워드는 특성이 삽입되는 경우 사용될 수 없습니다. 예를 들어 이 키워드를 사용하여 특성 생성자를 삽입하거나 XQuery에서 특성을 반환할 수 없습니다.  
  
 *Expression2*  
 노드를 식별합니다. *Expression1*에 식별된 노드는 *Expression2*에 의해 식별된 노드에 상대적으로 삽입됩니다. 이 식은 현재 참조되는 문서에 있는 노드에 대해 참조를 반환하는 XQuery 식일 수 있습니다. 두 개 이상의 노드가 반환되면 삽입이 실패합니다. *Expression2*가 빈 시퀀스를 반환하는 경우 삽입이 수행되지 않고 오류가 반환되지 않습니다. *Expression2*가 정적으로 단일 항목이 아닌 경우 정적 오류가 반환됩니다. *Expression2*는 처리 지침, 주석 또는 특성일 수 없습니다. *Expression2*는 구성된 노드가 아닌 문서에 있는 기존 노드에 대한 참조여야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-inserting-element-nodes-into-the-document"></a>1. 문서에 요소 노드 삽입  
 다음 예에서는 문서에 요소를 삽입하는 방법을 보여 줍니다. 먼저 XML 문서가 **xml** 형식의 변수에 할당됩니다. 그런 다음, 여러 **insert** XML DML 문을 통해 예에서 요소 노드가 문서에 삽입되는 방법을 보여 줍니다. 각 삽입 이후 SELECT 문으로 결과를 표시합니다.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;         
SET @myDoc = '<Root>         
    <ProductDescription ProductID="1" ProductName="Road Bike">         
        <Features>         
        </Features>         
    </ProductDescription>         
</Root>'  ;       
SELECT @myDoc;     
-- insert first feature child (no need to specify as first or as last)         
SET @myDoc.modify('         
insert <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>   
into (/Root/ProductDescription/Features)[1]') ;  
SELECT @myDoc ;        
-- insert second feature. We want this to be the first in sequence so use 'as first'         
set @myDoc.modify('         
insert <Warranty>1 year parts and labor</Warranty>          
as first         
into (/Root/ProductDescription/Features)[1]         
')  ;       
SELECT @myDoc  ;       
-- insert third feature child. This one is the last child of <Features> so use 'as last'         
SELECT @myDoc         
SET @myDoc.modify('         
insert <Material>Aluminium</Material>          
as last         
into (/Root/ProductDescription/Features)[1]         
')         
SELECT @myDoc ;        
-- Add fourth feature - this time as a sibling (and not a child)         
-- 'after' keyword is used (instead of as first or as last child)         
SELECT @myDoc  ;       
set @myDoc.modify('         
insert <BikeFrame>Strong long lasting</BikeFrame>   
after (/Root/ProductDescription/Features/Material)[1]         
')  ;       
SELECT @myDoc;  
GO  
```  
  
 이 예의 여러 경로 식은 정적 입력별 요구 사항으로 "[1]"을 지정합니다. 이렇게 하면 단일 대상 노드가 보장됩니다.  
  
### <a name="b-inserting-multiple-elements-into-the-document"></a>2. 문서에 여러 요소 삽입  
 다음 예에서는 문서를 **xml** 형식의 변수에 먼저 할당합니다. 그런 다음, 제품 기능을 나타내는 두 요소의 시퀀스를 **xml** 형식의 두 번째 변수에 할당하고, 이를 다시 첫 번째 변수에 삽입합니다.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc = N'<Root>             
<ProductDescription ProductID="1" ProductName="Road Bike">             
    <Features> </Features>             
</ProductDescription>             
</Root>';  
DECLARE @newFeatures xml;  
SET @newFeatures = N'<Warranty>1 year parts and labor</Warranty>            
<Maintenance>3 year parts and labor extended maintenance is available</Maintenance>';           
-- insert new features from specified variable            
SET @myDoc.modify('             
insert sql:variable("@newFeatures")             
into (/Root/ProductDescription/Features)[1] ')             
SELECT @myDoc;  
GO  
```  
  
### <a name="c-inserting-attributes-into-a-document"></a>3. 문서에 특성 삽입  
 다음 예에서는 문서에 특성을 삽입하는 방법을 보여 줍니다. 먼저 문서가 **xml** 형식 변수에 할당됩니다. 그런 다음, 일련의 **insert** XML DML 문을 사용하여 특성을 문서에 삽입합니다. 각 특성 삽입 이후 SELECT 문으로 결과를 표시합니다.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml ;            
SET @myDoc =   
'<Root>             
    <Location LocationID="10" >             
        <step>Manufacturing step 1 at this work center</step>             
        <step>Manufacturing step 2 at this work center</step>             
    </Location>             
</Root>' ;  
SELECT @myDoc  ;          
-- insert LaborHours attribute             
SET @myDoc.modify('             
insert attribute LaborHours {".5" }             
into (/Root/Location[@LocationID=10])[1] ') ;           
SELECT @myDoc  ;          
-- insert MachineHours attribute but its value is retrived from a sql variable @Hrs             
DECLARE @Hrs float ;            
SET @Hrs =.2   ;          
SET @myDoc.modify('             
insert attribute MachineHours {sql:variable("@Hrs") }             
into   (/Root/Location[@LocationID=10])[1] ');            
SELECT @myDoc;             
-- insert sequence of attribute nodes (note the use of ',' and ()              
-- around the attributes.             
SET @myDoc.modify('             
insert (              
           attribute SetupHours {".5" },             
           attribute SomeOtherAtt {".2"}             
        )             
into (/Root/Location[@LocationID=10])[1] ');             
SELECT @myDoc;  
GO  
```  
  
### <a name="d-inserting-a-comment-node"></a>4. 주석 노드 삽입  
 이 쿼리에서는 먼저 XML 문서가 **xml** 형식의 변수에 할당됩니다. 그런 다음 XML DML을 사용하여 첫 번째 <`step`> 요소 다음에 주석 노드를 삽입합니다.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;             
SET @myDoc =   
'<Root>             
    <Location LocationID="10" >             
        <step>Manufacturing step 1 at this work center</step>             
        <step>Manufacturing step 2 at this work center</step>             
    </Location>             
</Root>' ;           
SELECT @myDoc;             
SET @myDoc.modify('             
insert <!-- some comment -->             
after (/Root/Location[@LocationID=10]/step[1])[1] ');            
SELECT @myDoc;  
GO  
```  
  
### <a name="e-inserting-a-processing-instruction"></a>5. 처리 명령 삽입  
 다음 쿼리에서는 먼저 XML 문서가 **xml** 형식의 변수에 할당됩니다. 그런 다음 XML DML 키워드를 사용하여 문서 시작 부분에 처리 명령을 삽입합니다.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>   
    <Location LocationID="10" >   
        <step>Manufacturing step 1 at this work center</step>   
        <step>Manufacturing step 2 at this work center</step>   
    </Location>   
</Root>' ;  
SELECT @myDoc ;  
SET @myDoc.modify('   
insert <?Program = "Instructions.exe" ?>   
before (/Root)[1] ') ;  
SELECT @myDoc ;  
GO  
```  
  
### <a name="f-inserting-data-using-a-cdata-section"></a>6. CDATA 섹션을 사용하여 데이터 삽입  
 < 또는 >와 같이 XML에서 유효하지 않은 문자가 포함된 텍스트를 삽입하는 경우 다음 쿼리에서와 같이 CDATA 섹션을 사용하여 데이터를 삽입할 수 있습니다. 이 쿼리에서는 CDATA 섹션을 지정하지만 엔터티로 변환된 유효하지 않은 문자가 포함된 텍스트 노드로 추가됩니다. 예를 들어 ‘<’는 &lt;로 저장됩니다.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;             
SET @myDoc =   
'<Root>             
    <ProductDescription ProductID="1" ProductName="Road Bike">             
        <Features> </Features>             
    </ProductDescription>             
</Root>' ;            
SELECT @myDoc ;            
SET @myDoc.modify('             
insert <![CDATA[ <notxml> as text </notxml> or cdata ]]>   
into  (/Root/ProductDescription/Features)[1] ') ;   
SELECT @myDoc ;  
GO  
```  
  
 이 쿼리는 <`Features`> 요소에 텍스트 노드를 삽입합니다.  
  
```  
<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features> <notxml> as text </notxml> or cdata </Features>  
</ProductDescription>  
</Root>       
```  
  
### <a name="g-inserting-text-node"></a>7. 텍스트 노드 삽입  
 이 쿼리에서는 먼저 XML 문서가 **xml** 형식의 변수에 할당됩니다. 그런 다음 XML DML을 사용하여 <`Root`> 요소의 첫 번째 자식으로 텍스트 노드를 삽입합니다. 텍스트 생성자는 텍스트를 지정하는 데 사용됩니다.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  
</Features>  
</ProductDescription>  
</Root>'  
SELECT @myDoc;  
set @myDoc.modify('  
 insert text{"Product Catalog Description"}   
 as first into (/Root)[1]  
');  
SELECT @myDoc;  
```  
  
### <a name="h-inserting-a-new-element-into-an-untyped-xml-column"></a>8. 형식화되지 않은 xml 열에 새 요소 삽입  
 다음 예에서는 XML DML을 적용하여 **xml** 형식의 열에 저장된 XML 인스턴스를 업데이트합니다.  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE T (i int, x xml);  
go  
INSERT INTO T VALUES(1,'<Root>  
    <ProductDescription ProductID="1" ProductName="Road Bike">  
        <Features>  
            <Warranty>1 year parts and labor</Warranty>  
            <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
        </Features>  
    </ProductDescription>  
</Root>');  
go  
-- insert a new element  
UPDATE T  
SET x.modify('insert <Material>Aluminium</Material> as first  
  into   (/Root/ProductDescription/Features)[1]  
');  
GO  
```  
  
 마찬가지로 <`Material`> 요소가 삽입되는 경우 경로 식이 단일 대상을 반환해야 합니다. 이것은 식의 끝에 [1]을 추가하여 명시적으로 지정됩니다.  
  
```  
-- check the update  
SELECT x.query(' //ProductDescription/Features')  
FROM T;  
GO  
```  
  
### <a name="i-inserting-based-on-an-if-condition-statement"></a>9. if 조건 문을 기준으로 삽입  
 다음 예에서는 **insert** XML DML 문에서 Expression1의 일부로 IF 조건이 지정됩니다. 조건이 True이면 특성이 <`WorkCenter`> 요소에 추가됩니다.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>  
    <Location LocationID="10" LaborHours="1.2" >  
        <step>Manufacturing step 1 at this work center</step>  
    <step>Manufacturing step 2 at this work center</step>  
    </Location>  
</Root>';  
SELECT @myDoc  
SET @myDoc.modify('  
insert  
if (/Root/Location[@LocationID=10])  
then attribute MachineHours {".5"}  
else ()  
    as first into   (/Root/Location[@LocationID=10])[1] ');  
SELECT @myDoc;  
GO  
```  
  
 다음 예도 이와 비슷하지만 조건이 True인 경우 **insert** XML DML 문은 요소를 문서에 삽입합니다. 즉, <`WorkCenter`> 요소가 두 개의 <`step`> 자식 요소보다 작거나 같은 경우입니다.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>  
    <Location LocationID="10" LaborHours="1.2" >  
        <step>Manufacturing step 1 at this work center</step>  
        <step>Manufacturing step 2 at this work center</step>  
    </Location>  
</Root>';  
SELECT @myDoc;  
SET @myDoc.modify('  
insert  
if (count(/Root/Location/step) <= 2)  
then element step { "This is a new step" }  
else ()  
    as last into   (/Root/Location[@LocationID=10])[1] ');  
SELECT @myDoc;  
GO  
```  
  
 다음은 결과입니다.  
  
```  
<Root>  
 <WorkCenter WorkCenterID="10" LaborHours="1.2">  
  <step>Manufacturing step 1 at this work center</step>  
  <step>Manufacturing step 2 at this work center</step>  
  <step>This is a new step</step>  
 </WorkCenter>  
```  
  
### <a name="j-inserting-nodes-in-a-typed-xml-column"></a>10. 형식화된 xml 열에 노드 삽입  
 이 예에서는 형식화된 **xml** 열에 저장된 제조 명령 XML에 요소와 특성을 삽입합니다.  
  
 이 예에서는 먼저 AdventureWorks 데이터베이스에서 형식화된 **xml** 열을 가진 테이블(T)을 만듭니다. 그런 다음 ProductModel 테이블의 Instructions 열의 제조 지침 XML 인스턴스를 테이블 T로 복사합니다. 그러면 테이블 T의 XML에 삽입 내용이 적용됩니다.  
  
```  
USE AdventureWorks;  
GO            
DROP TABLE T;  
GO             
CREATE TABLE T(ProductModelID int primary key,    
Instructions xml (Production.ManuInstructionsSchemaCollection));  
GO  
INSERT T              
    SELECT ProductModelID, Instructions             
    FROM Production.ProductModel             
    WHERE ProductModelID=7;  
GO             
SELECT Instructions             
FROM T;  
-- now insertion begins             
--1) insert a new manu. Location. The <Root> specified as              
-- expression 2 in the insert() must be singleton.      
UPDATE T   
set Instructions.modify('   
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
insert <MI:Location LocationID="1000" >   
           <MI:step>New instructions go here</MI:step>   
         </MI:Location>   
as first   
into   (/MI:root)[1]   
') ;  
  
SELECT Instructions             
FROM T ;  
-- 2) insert attributes in the new <Location>             
UPDATE T             
SET Instructions.modify('             
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";             
insert attribute LaborHours { "1000" }             
into (/MI:root/MI:Location[@LocationID=1000])[1] ');   
GO             
SELECT Instructions             
FROM T ;  
GO             
--cleanup             
DROP TABLE T ;  
GO             
```  
  
## <a name="see-also"></a>참고 항목  
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML&#40;XML 데이터 수정 언어&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

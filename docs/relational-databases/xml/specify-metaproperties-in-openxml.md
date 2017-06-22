---
title: "OPENXML에 메타 속성 지정 | Microsoft 문서"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- overflow in XML document [SQL Server]
- metaproperties [XML in SQL Server]
- unconsumed data
- extracting information of XML nodes [SQL Server]
- OPENXML statement, metaproperties
ms.assetid: 29bfd1c6-3f9a-43c4-924a-53d438e442f4
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6bc6d9b3e482869bd82daa13c167d0221639a95f
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="specify-metaproperties-in-openxml"></a>OPENXML에 메타 속성 지정
  XML 문서의 메타 속성 특성은 요소, 특성, 그 밖의 모든 DOM 노드와 같은 XML 항목의 속성을 설명하는 특성입니다. 이러한 특성은 물리적으로 XML 문서 텍스트에 존재하지 않습니다. 하지만 OPENXML은 모든 XML 항목에 대해 이러한 메타 속성을 제공합니다. 이러한 메타 속성을 사용하면 로컬 위치 및 네임스페이스 정보와 같은 XML 노드 정보를 추출할 수 있습니다. 이 정보는 텍스트에 명시적으로 표현된 것보다 자세한 정보를 제공합니다.  
  
 *ColPattern* 매개 변수를 사용하여 이러한 메타 속성을 OPENXML 문의 행 집합 열에 매핑할 수 있습니다. 열에는 매핑될 메타 속성 값이 포함됩니다. OPENXML 구문에 대한 자세한 내용은 [OPENXML&#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)을 참조하세요.  
  
 메타 속성 특성에 액세스하기 위해 SQL Server와 관련된 네임스페이스가 제공됩니다. 이 네임스페이스 **urn:schemas-microsoft-com:xml-metaprop** 를 사용하면 메타 속성 특성에 액세스할 수 있습니다. OPENXML 쿼리의 결과가 Edge 테이블 형식으로 반환되는 경우에는 Edge 테이블에 각 메타 속성 특성( **xmltext** 메타 속성 제외)에 대한 열이 한 개씩 포함됩니다.  
  
 메타 속성 특성 중 일부는 처리 용도로 사용됩니다. 예를 들어 **xmltext** 메타 속성 특성은 오버플로 처리를 위해 사용됩니다. 오버플로 처리란 문서에서 소비되지 않고 처리되지 않은 데이터를 의미합니다. OPENXML에 의해 생성된 행 집합에 있는 열 중 하나는 오버플로 열로 식별될 수 있습니다. 이렇게 하려면 **ColPattern** 매개 변수를 사용하여 열을 *xmltext* 메타 속성으로 매핑합니다. 그러면 열이 오버플로 데이터를 수신합니다. *flags* 매개 변수는 해당 열에 모든 데이터 또는 소비되지 않은 데이터만 포함되는지 여부를 확인합니다.  
  
 다음 표는 구문 분석된 각각의 XML 요소가 처리하는 메타 속성 특성의 목록입니다. 이러한 메타 속성 특성은 네임스페이스 **urn:schemas-microsoft-com:xml-metaprop**를 사용하여 액세스할 수 있습니다. XML 문서에서 이러한 메타 속성을 사용하여 사용자가 직접 설정한 값은 모두 무시됩니다.  
  
> [!NOTE]  
>  XPath 탐색에서는 이러한 메타 속성을 참조할 수 없습니다.  
  
|메타 속성 특성|설명|  
|----------------------------|-----------------|  
|**@mp:id**|DOM 노드에 대해 시스템에서 생성된 문서 차원의 식별자를 제공합니다. 문서가 다시 구문 분석되지 않는 한 이 ID는 동일한 XML 노드를 참조합니다.<br /><br /> XML ID가 **0** 이면 해당 요소가 루트 요소임을 나타냅니다. 해당 부모 XML ID는 NULL입니다.|  
|**@mp:localname**|노드 이름의 로컬 부분을 저장합니다. 이 특성은 접두사 및 네임스페이스 URI와 함께 사용되어 요소 또는 특성 노드 이름을 지정합니다.|  
|**@mp:namespaceuri**|현재 요소의 네임스페이스 URI를 제공합니다. 이 특성의 값이 NULL이면 네임스페이스가 없는 것입니다.|  
|**@mp:prefix**|현재 요소 이름의 네임스페이스 접두사를 저장합니다.<br /><br /> 접두사가 없는 상태(NULL)에서 URI가 주어진 경우는 지정된 네임스페이스가 기본 네임스페이스임을 나타냅니다. URI가 주어지지 않은 경우에는 네임스페이스가 연결되지 않습니다.|  
|**@mp:prev**|노드와 관련된 이전 형제를 저장합니다. 이 특성은 문서에 있는 요소의 순서 정보를 제공합니다.<br /><br /> **@mp:prev** 에는 동일한 부모 요소를 가진 이전 형제의 XML ID가 포함됩니다. 요소가 형제 목록의 시작 부분에 있으면 **@mp:prev** 는 NULL입니다.|  
|**@mp:xmltext**|처리 목적으로 사용됩니다. OPENXML의 오버플로 처리에 사용되는 방식의 요소 및 해당 특성의 텍스트 직렬화와 하위 요소입니다.|  
  
 이 표에서는 계층 구조 정보를 검색할 수 있도록 허용하기 위해 제공되는 추가 부모 속성을 보여 줍니다.  
  
|부모 메타 속성 특성|Description|  
|-----------------------------------|-----------------|  
|**@mp:parentid**|**../@mp:id**에 해당합니다.|  
|**@mp:parentlocalname**|**../@mp:localname**에 해당합니다.|  
|**@mp:parentnamespacerui**|**../@mp:namespaceuri**에 해당합니다.|  
|**@mp:parentprefix**|**../@mp:prefix**에 해당합니다.|  
  
## <a name="examples"></a>예  
 다음 예에서는 OPENXML을 사용하여 여러 행 집합 뷰를 만드는 방법을 보여 줍니다.  
  
### <a name="a-mapping-the-openxml-rowset-columns-to-the-metaproperties"></a>1. OPENXML 행 집합 열을 메타 속성에 매핑  
 이 예에서는 OPENXML을 사용하여 예제 XML 문서의 행 집합 뷰를 만듭니다. 특히 OPENXML 문에서 *ColPattern* 매개 변수를 사용하여 여러 가지 메타 속성 특성을 행 집합 열에 매핑할 수 있는 방법을 보여 줍니다.  
  
 OPENXML 문에서는 다음을 보여 줍니다.  
  
-   **id** 열은 **@mp:id** 메타 속성 특성에 매핑됩니다. 즉, 열에는 요소에 대해 시스템에서 생성된 고유 XML ID가 포함됩니다.  
  
-   **parent** 열은 **@mp:parentid**에 매핑됩니다. 즉, 열에는 요소의 부모에 대한 XML ID가 포함됩니다.  
  
-   **parentLocalName** 열은 **@mp:parentlocalname**에 매핑됩니다. 즉, 열에는 부모의 로컬 이름이 포함됩니다.  
  
 그런 다음 SELECT 문은 OPENXML에 의해 제공되는 행 집합을 반환합니다.  
  
```  
DECLARE @idoc int  
DECLARE @doc nvarchar(1000)  
-- Sample XML document  
SET @doc = N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@idoc, '/root/Customer/Order', 9)  
      WITH (id int '@mp:id',   
            oid char(5),   
            date datetime,   
            amount real,   
            parentIDNo int '@mp:parentid',   
            parentLocalName varchar(40) '@mp:parentlocalname')  
EXEC sp_xml_removedocument @idoc  
```  
  
 다음은 결과입니다.  
  
```  
id   oid         date                amount    parentIDNo  parentLocalName    
--- ------- ---------------------- ---------- ------------ ---------------  
6    O1    1996-01-20 00:00:00.000     3.5         2        Customer  
10   O2    1997-04-30 00:00:00.000     13.4        2        Customer  
19   O3    1999-07-14 00:00:00.000     100.0       15       Customer  
25   O4    1996-01-20 00:00:00.000     10000.0     15       Customer  
```  
  
### <a name="b-retrieving-the-whole-xml-document"></a>2. 전체 XML 문서 검색  
 이 예에서는 OPENXML을 사용하여 예제 XML 문서를 하나의 열로 된 행 집합 뷰로 만듭니다. 이 열 **Col1**은 **xmltext** 메타 속성에 매핑되며 오버플로 열이 됩니다. 그 결과 열이 소비되지 않은 데이터를 수신합니다. 이 경우에는 전체 문서입니다.  
  
 그런 다음 SELECT 문은 완전한 행 집합을 반환합니다.  
  
```  
DECLARE @idoc int  
DECLARE @doc nvarchar(1000)  
SET @doc = N'<?xml version="1.0"?>  
<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very   
             satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
     <MyTag>Testing to see if all the subelements are returned</MyTag>  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@idoc, '/')  
   WITH (Col1 ntext '@mp:xmltext')  
```  
  
 XML을 선언하지 않고 전체 문서를 검색하기 위해서는 쿼리를 다음과 같이 지정할 수 있습니다.  
  
```  
SELECT *  
FROM OPENXML (@idoc, '/root')  
   WITH (Col1 ntext '@mp:xmltext')  
EXEC sp_xml_removedocument @idoc  
```  
  
 쿼리는 이름 루트가 포함된 루트 요소와 해당 루트 요소에 포함된 데이터를 반환합니다.  
  
### <a name="c-specifying-the-xmltext-metaproperty-to-retrieve-the-unconsumed-data-in-a-column"></a>3. xmltext 메타 속성을 지정하여 열에서 소비되지 않은 데이터 검색  
 이 예에서는 OPENXML을 사용하여 예제 XML 문서의 행 집합 뷰를 만듭니다. **xmltext** 메타 속성 특성을 OPENXML의 행 집합 열에 매핑하여 소비되지 않은 XML 데이터를 검색하는 방법을 설명합니다.  
  
 **comment** 열은**@mp:xmltext** 메타 속성에 매핑됨으로써 오버플로 열로 식별됩니다. *flags* 매개 변수는 **9** (XML_ATTRIBUTE 및 XML_NOCOPY)로 설정됩니다. 이는 **특성 중심** 매핑을 나타내며 소비되지 않은 데이터만 오버플로 열에 복사되어야 함을 나타냅니다.  
  
 그런 다음 SELECT 문은 OPENXML이 제공하는 행 집합을 반환합니다.  
  
 이 예에서는 OPENXML이 생성한 행 집합의 열 **@mp:parentlocalname** 에 대해 **ParentLocalName**메타 속성이 설정됩니다. 결과적으로 이 열에는 부모 요소의 로컬 이름이 포함됩니다.  
  
 두 개의 추가 열 **parent** 및 **comment**가 행 집합에 지정됩니다. **parent** 열은 **@mp:parentid**에 매핑됩니다. 즉, 이 열에는 요소의 부모 요소에 대한 XML ID가 포함됩니다. comment 열은 **@mp:xmltext** 메타 속성 제외)에 대한 열이 한 개씩 포함됩니다.  
  
```  
DECLARE @idoc int  
DECLARE @doc nvarchar(1000)  
-- sample XML document  
SET @doc = N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>  
'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@idoc, '/root/Customer/Order', 9)  
      WITH (oid char(5),   
            date datetime,  
            comment ntext '@mp:xmltext')  
EXEC sp_xml_removedocument @idoc  
```  
  
 다음은 결과입니다. oid 열과 date 열은 이미 소비되었으므로 오버플로 열에 나타나지 않습니다.  
  
```  
oid   date                        comment                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            
----- --------------------------- ----------------------------------------  
O1    1996-01-20 00:00:00.000     <Order amount="3.5"/>  
O2    1997-04-30 00:00:00.000     <Order amount="13.4">Customer was very   
                                   satisfied</Order>  
O3    1999-07-14 00:00:00.000     <Order amount="100" note="Wrap it blue   
                                   white red"><Urgency>   
                                   Important</Urgency></Order>  
O4    1996-01-20 00:00:00.000     <Order amount="10000"/>  
```  
  
## <a name="see-also"></a>참고 항목  
 [OPENXML&#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML&#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  

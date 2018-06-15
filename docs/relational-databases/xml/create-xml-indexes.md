---
title: XML 인덱스 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- indexes [XML in SQL Server]
- XML indexes [SQL Server], creating
ms.assetid: 6ecac598-355d-4408-baf7-1b2e8d4cf7c1
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 15c81de1d71da6f0773c53833c2849fd58d1f3ce
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33011786"
---
# <a name="create-xml-indexes"></a>XML 인덱스 만들기
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 기본 및 보조 XML 인덱스를 만드는 방법에 대해 설명합니다.  
  
## <a name="creating-a-primary-xml-index"></a>기본 XML 인덱스 만들기  
 기본 XML 인덱스를 만들려면 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 문을 사용합니다. 비-XML 인덱스에 대해 사용 가능한 옵션이 XML 인덱스에서 모두 지원되는 것은 아닙니다.  
  
 XML 인덱스를 만들 때는 다음 사항을 알아야 합니다.  
  
-   기본 XML 인덱스를 만들려면 기본 테이블이라는 인덱싱되는 XML 열이 포함된 테이블에 기본 키에서 클러스터형 인덱스가 있어야 합니다. 이렇게 하면 기본 테이블이 분할되는 경우 기본 XML 인덱스를 같은 파티션 구성표와 파티션 함수를 사용하여 분할할 수 있습니다.  
  
-   XML 인덱스가 있으면 테이블의 클러스터형 기본 키를 수정할 수 없습니다. 모든 XML 인덱스를 테이블에서 삭제해야 기본 키를 수정할 수 있습니다.  
  
-   기본 XML 인덱스는 단일 **xml** 유형 열에서 만들 수 있습니다. XML 유형 열이 있는 다른 인덱스 유형은 키 열로 만들 수 없습니다. 그러나 비 XML 인덱스에는 **xml** L 유형 열을 포함할 수 있습니다. 테이블의 **xml** 유형 열마다 자신의 기본 XML 인덱스를 지정할 수 있습니다. 그러나 기본 XML 인덱스는 **xml** 유형 열마다 하나씩만 허용됩니다.  
  
-   XML 인덱스는 비-XML 인덱스와 같은 네임스페이스에 있습니다. 따라서 같은 테이블에서 이름이 같은 XML 인덱스와 비-XML 인덱스를 사용할 수 없습니다.  
  
-   IGNORE_DUP_KEY 및 ONLINE 옵션은 XML 인덱스에 대해 항상 OFF로 설정됩니다. 이러한 옵션의 값을 OFF로 지정할 수 있습니다.  
  
-   사용자 테이블의 파일 그룹 또는 분할 정보는 XML 인덱스에 적용됩니다. 사용자는 XML 인덱스에서 이를 별도로 지정할 수 없습니다.  
  
-   DROP_EXISTING 인덱스 옵션은 기본 XML 인덱스를 삭제하고 새 기본 XML 인덱스를 만들거나, 보조 XML 인덱스를 삭제하고 새 보조 XML 인덱스를 만들 수 있습니다. 그러나 이 옵션을 사용하여 보조 XML 인덱스를 삭제하고 새 기본 XML 인덱스를 만들거나 기본 XML 인덱스를 삭제하고 새 보조 XML 인덱스를 만들 수는 없습니다.  
  
-   기본 XML 인덱스 이름에는 뷰 이름과 같은 제한이 있습니다.  
  
 뷰의 **xml** 유형 열이나 **xml** 유형 열 또는 **xml** 유형 변수가 있는 **table** 값 변수에 XML 인덱스를 만들 수 없습니다.  
  
-   ALTER TABLE ALTER COLUMN 옵션을 사용하여 **xml** 유형 열을 형식화되지 않은 XML에서 형식화된 XML로 변경하거나 그 반대로 변경하려면 열에 XML 인덱스가 있으면 안 됩니다. XML 인덱스가 있으면 열 형식 변경을 시도하기 전에 먼저 삭제해야 합니다.  
  
-   ARITHABORT 옵션은 XML 인덱스를 만들 때 ON으로 설정되어야 합니다. XML 데이터 형식 메서드를 사용하여 XML 열의 값을 쿼리, 삽입, 삭제 또는 업데이트하려면 같은 옵션을 연결에 설정해야 합니다. 그렇지 않으면 XML 데이터 형식 메서드가 실패합니다.  
  
    > [!NOTE]  
    >  XML 인덱스에 대한 정보는 카탈로그 뷰에서 찾을 수 있습니다. 그러나 **sp_helpindex** 는 지원되지 않습니다. 이 항목의 후반부에 제공된 예에서는 카탈로그 뷰를 쿼리하여 XML 인덱스 정보를 찾는 방법을 보여 줍니다.  
  
 1년 미만의 값이 있는 XML 스키마 유형 **xs:date** 또는 **xs:dateTime** 이나 그 하위 유형의 값을 포함하는 XML 데이터 형식 열에 기본 XML 인덱스를 만들거나 다시 만들 경우 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 인덱스 만들기에 실패합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 에서는 이러한 값이 허용되었으므로 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 생성된 데이터베이스에 인덱스를 만들 경우 이러한 문제가 발생할 수 있습니다. 자세한 내용은 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)를 참조하세요.  
  
### <a name="example-creating-a-primary-xml-index"></a>예제: 기본 XML 인덱스 만들기  
 대부분의 예에서는 형식화되지 않은 XML 열이 포함된 테이블 T(pk INT PRIMARY KEY, xCol XML)가 사용됩니다. 이러한 예는 직관적인 방식에 따라 형식화된 XML로 확장될 수 있습니다. 간단한 설명을 위해 쿼리는 다음에 표시된 것과 같이 XML 데이터 인스턴스에 대해 기술됩니다.  
  
```  
<book genre="security" publicationdate="2002" ISBN="0-7356-1588-2">  
   <title>Writing Secure Code</title>  
   <author>  
      <first-name>Michael</first-name>  
      <last-name>Howard</last-name>  
   </author>  
   <author>  
      <first-name>David</first-name>  
      <last-name>LeBlanc</last-name>  
   </author>  
   <price>39.99</price>  
</book>  
```  
  
 다음 문은 테이블 T의 XML 열 xCol에서 idx_xCol이라는 XML 인덱스를 만듭니다.  
  
```  
CREATE PRIMARY XML INDEX idx_xCol on T (xCol)  
```  
  
## <a name="creating-a-secondary-xml-index"></a>보조 XML 인덱스 만들기  
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 문을 사용하여 보조 XML 인덱스를 만들고 원하는 보조 XML 인덱스의 유형을 지정할 수 있습니다.  
  
 보조 XML 인덱스를 만들 때는 다음 사항을 알아야 합니다.  
  
-   IGNORE_DUP_KEY 및 ONLINE을 제외하고 비클러스터형 인덱스에 적용되는 모든 인덱싱 옵션을 보조 XML 인덱스에서 사용할 수 있습니다. 두 옵션은 보조 XML 인덱스에 대해 항상 OFF로 설정되어야 합니다.  
  
-   보조 인덱스는 기본 XML 인덱스와 똑같이 분할됩니다.  
  
-   DROP_EXISTING은 사용자 테이블에서 보조 인덱스를 삭제하고 다른 보조 인덱스를 만들 수 있습니다.  
  
 **sys.xml_indexes** 카탈로그 뷰를 쿼리하여 XML 인덱스 정보를 검색할 수 있습니다. **sys.xml_indexes** 카탈로그 뷰의 **secondary_type_desc** 열은 보조 인덱스 유형을 제공합니다.  
  
```  
SELECT  *   
FROM    sys.xml_indexes;  
```  
  
 **secondary_type_desc** 열에 반환된 값은 NULL, PATH, VALUE 또는 PROPERTY가 될 수 있습니다. 기본 XML 인덱스의 경우 반환된 값은 NULL입니다.  
  
### <a name="example-creating-secondary-xml-indexes"></a>예제: 보조 XML 인덱스 만들기  
 다음 예에서는 보조 XML 인덱스가 만들어지는 방법을 설명합니다. 또한 만들어진 XML 인덱스에 대한 정보도 보여 줍니다.  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML);  
GO  
-- Create primary index.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol);  
GO  
-- Create secondary indexes (PATH, VALUE, PROPERTY).  
CREATE XML INDEX PIdx_T_XmlCol_PATH ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR PATH;  
GO  
CREATE XML INDEX PIdx_T_XmlCol_VALUE ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR VALUE;  
GO  
CREATE XML INDEX PIdx_T_XmlCol_PROPERTY ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR PROPERTY;  
GO  
```  
  
 `sys.xml_indexes` 를 쿼리하여 XML 인덱스 정보를 검색할 수 있습니다. `secondary_type_desc` 열은 보조 인덱스 유형을 제공합니다.  
  
```  
SELECT  *   
FROM    sys.xml_indexes;  
```  
  
 카탈로그 뷰에서 인덱스 정보를 쿼리할 수도 있습니다.  
  
```  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T');  
```  
  
 예제 데이터를 추가한 다음 XML 인덱스 정보를 검토할 수 있습니다.  
  
```  
INSERT INTO T VALUES (1,  
'<doc id="123">  
<sections>  
<section num="2">  
<heading>Background</heading>  
</section>  
<section num="3">  
<heading>Sort</heading>  
</section>  
<section num="4">  
<heading>Search</heading>  
</section>  
</sections>  
</doc>');  
GO  
-- Check XML index information.  
SELECT *  
FROM   sys.dm_db_index_physical_stats (db_id(), object_id('T'), NULL, NULL, 'DETAILED');  
GO  
-- Space usage of primary XML index  
DECLARE @index_id int;  
SELECT  @index_id = i.index_id  
FROM    sys.xml_indexes i   
WHERE   i.name = 'PIdx_T_XmlCol' and object_name(i.object_id) = 'T';  
  
SELECT *  
FROM sys.dm_db_index_physical_stats (db_id(), object_id('T') , @index_id, DEFAULT, 'DETAILED');  
go  
--- Space usage of secondary XML index (for example PATH secondary index)  PIdx_T_XmlCol_PATH  
DECLARE @index_id int;  
SELECT  @index_id = i.index_id   
FROM    sys.xml_indexes i   
WHERE  i.name = 'PIdx_T_XmlCol_PATH' and object_name(i.object_id) = 'T';  
  
SELECT *  
FROM sys.dm_db_index_physical_stats (db_id(), object_id('T') , @index_id, DEFAULT, 'DETAILED');  
go  
  
-- Space usage of all secondary XML indexes for a particular table  
SELECT i.name, object_name(i.object_id), stats.*   
FROM   sys.dm_db_index_physical_stats (db_id(), object_id('T'), NULL, DEFAULT, 'DETAILED') stats  
JOIN sys.xml_indexes i ON (stats.object_id = i.object_id and stats.index_id = i.index_id)  
WHERE secondary_type is not null;  
-- Drop secondary indexes.  
DROP INDEX PIdx_T_XmlCol_PATH ON T;  
GO  
DROP INDEX PIdx_T_XmlCol_VALUE ON T;  
GO  
DROP INDEX PIdx_T_XmlCol_PROPERTY ON T;  
GO  
-- Drop primary index.  
DROP INDEX PIdx_T_XmlCol ON T;  
-- Drop table T.  
DROP TABLE T;  
Go  
```  
  
## <a name="see-also"></a>참고 항목  
 [XML 인덱스&#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [XML 데이터&#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  

---
title: XML 인덱스 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- removing indexes
- dropping indexes
- XML indexes [SQL Server], dropping
ms.assetid: 7591ebea-34af-4925-8553-b2adb5b487c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d8162a8eef652a14993f67e4e3931be7362e6f4
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67929661"
---
# <a name="drop-xml-indexes"></a>XML 인덱스 삭제
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [DROP INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 기존 기본 또는 보조 XML 인덱스 및 비 XML 인덱스를 삭제할 수 있습니다. 그러나 DROP INDEX의 옵션은 XML 인덱스에 적용되지 않습니다. 기본 XML 인덱스를 삭제하려면 존재하는 보조 인덱스도 모두 삭제됩니다.  
  
 *TableName.IndexName* 이 있는 DROP 구문은 단계적으로 제거하며 XML 인덱스에 대해서는 지원되지 않습니다.  
  
## <a name="example-creating-and-dropping-a-primary-xml-index"></a>예제: 기본 XML 인덱스 만들기 및 삭제  
 다음 예에서는 XML 인덱스가 **xml** 유형 열에 생성됩니다.  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
-- Create Primary XML index   
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol)  
GO  
-- Verify the index creation.   
-- Note index type is 3 for xml indexes.  
-- Note the type 3 is index on XML type.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'   
-- Drop the index.  
DROP INDEX PIdx_T_XmlCol ON T  
```  
  
 테이블이 삭제될 때 그 테이블의 모든 XML 인덱스도 자동으로 삭제됩니다. 그러나 XML 인덱스가 열에 있는 경우 XML 열은 테이블에서 삭제할 수 없습니다.  
  
 다음 예에서는 XML 인덱스가 **xml** 유형 열에 생성됩니다. 자세한 내용은 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)를 참조하세요.  
  
```  
CREATE TABLE TestTable(  
 Col1 int primary key,   
 Col2 xml (Production.ProductDescriptionSchemaCollection))   
GO  
```  
  
 이제 `Co12`에 기본 XML 인덱스를 만들 수 있습니다.  
  
```  
CREATE PRIMARY XML INDEX PIdx_TestTable_Col2   
ON TestTable(Col2)  
GO  
```  
  
## <a name="example-creating-an-xml-index-by-using-the-drop_existing-index-option"></a>예제: DROP_EXISTING 인덱스 옵션을 사용하여 XML 인덱스 만들기  
 다음 예에서는 XML 인덱스가`XmlColx`열에 생성됩니다. 그런 다음 같은 이름으로 된 다른 XML 인덱스가 다른 열`XmlColy`에 생성됩니다. `DROP_EXISTING` 옵션이 지정되어 있으므로 (`XmlColx)` )의 기존 XML 인덱스가 삭제되고 (`XmlColy`)의 새 XML 인덱스가 생성됩니다.  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T(Col1 int primary key, XmlColx xml, XmlColy xml)  
GO  
-- Create XML index on XmlColx.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColx)  
GO  
-- Create same name XML index on XmlColy.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColy)   
WITH (DROP_EXISTING = ON)  
-- Verify the index is created on XmlColy.d.  
SELECT sc.name   
FROM   sys.xml_indexes si inner join sys.index_columns sic   
ON     sic.object_id=si.object_id and sic.index_id=si.index_id  
INNER  join sys.columns sc on sc.object_id=sic.object_id   
AND    sc.column_id=sic.column_id  
WHERE  si.name='PIdx_T_XmlCol'   
AND    si.object_id=object_id('T')  
```  
  
 이 쿼리에서는 지정된 XML 인덱스가 생성된 열 이름을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 인덱스&#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  

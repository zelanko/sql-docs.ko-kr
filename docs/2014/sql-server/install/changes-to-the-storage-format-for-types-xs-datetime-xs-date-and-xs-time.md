---
title: '형식 xs: datetime, xs: date 및 xs: time에 대 한 저장소 형식 변경 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- xs:date
- xs:time
- storage format
- DateTime
ms.assetid: b9f758df-030c-4aec-8ade-1bf904aa2c61
caps.latest.revision: 10
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1acc25889e693a69e55adc4f5da5ece616bc41a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222523"
---
# <a name="changes-to-the-storage-format-for-types-xsdatetime-xsdate-and-xstime"></a>xs:dateTime, xs:date 및 xs:time 형식의 저장소 형식에 대한 변경 내용입니다.
  XMLDATETIME 규칙은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드한 후 사용할 수 없는 형식화된 XML 데이터가 데이터베이스에 포함되어 있는지 여부를 식별합니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 xs:dateTime, xs:date 및 xs:time 형식에 대한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 의 저장소 형식이 표준 시간대 정보가 있거나 없는 값을 지원하고 표준 시간대를 유지하도록 변경되었습니다.  
  
 XML 스키마 컬렉션이 이러한 형식 중 하나를 참조하는 경우 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드한 이후에 해당 컬렉션에 연결된 모든 열의 XML 인덱스가 비활성화됩니다. SELECT 및/또는 XQUERIES를 사용하면 쿼리할 수 있지만 이러한 XML 인덱스는 사용되지 않습니다. 음수 연도 값이 발견되면 런타임 오류가 발생합니다.  
  
 또한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 은 음수 연도가 있는 값을 지원하지 않습니다.  
  
 XMLDATETIME 규칙은 영향을 받는 형식을 참조하는 XML 스키마 컬렉션이 있는지, 그리고 이러한 컬렉션에 의해 형식화된 XML 열이 있는지 확인합니다.  
  
## <a name="corrective-action"></a>수정 동작  
 XMLDATETIME 규칙을 통해 xs:date, xs:time 또는 xs:dateTime을 참조하는 스키마 컬렉션에 따라 형식화된 XML 열이 있는 것으로 확인되는 경우에는 데이터에 음수 연도가 포함된 값이 있는지 여부를 가장 먼저 점검해야 합니다. 이러한 값이 있는 경우 업그레이드 후 XML 인덱스를 다시 작성할 수 없습니다.  
  
 다음 쿼리는 영향을 받는 형식을 참조하는 XML 스키마 컬렉션, 그리고 형식화된 각 XML 열을 검색합니다. 이 쿼리를 통해 음수 연도 값이 있는 인스턴스의 유무를 확인할 수 있습니다.  
  
```  
CREATE PROCEDURE DateTimeInvestigation(@withdata bit)  
-- @withdata = 0: only get the affected meta data information  
-- @withdata = 1: get the affected meta data and instance information  
AS  
BEGIN  
-- First get XML containing all schema collections containing affected element and attributes  
-- components (model groups????)   
-- and columns that are affected by the schema collections.   
CREATE table #_dt_collector(x xml);   
;with dttypes as  
  (SELECT * FROM sys.xml_schema_components   
   where base_xml_component_id IN   
      (SELECT xml_component_id   
       FROM sys.xml_schema_types   
       where (name='dateTime' or name='date') and kind='P'  
      )   
   union all  
   SELECT * FROM sys.xml_schema_components  
   where xml_component_id IN   
      (SELECT xml_component_id   
       FROM sys.xml_schema_types   
       where (name='dateTime' or name='date') and kind='P'  
       or kind='N' or kind='Z')   
   ),   
dtplaced as  
  (SELECT scp.*   
   FROM sys.xml_schema_component_placements scp   
   JOIN dttypes on scp.placed_xml_component_id=dttypes.xml_component_id  
  )   
insert into #_dt_collector SELECT x FROM (SELECT  
  xsc.xml_collection_id as "@collid"  
, s.name as "@schema"  
, xscol.name as "@name"  
, count(xsc.xml_component_id) as "@affected_elems_and_attrs"  
, (SELECT S.Name as "@schema", T.Name as "@table"  
        , C.Name as "@column"   
   FROM sys.columns C   
   JOIN sys.tables T ON C.object_id = T.object_id  
   JOIN sys.schemas S ON S.schema_id = T.schema_id  
   WHERE C.xml_collection_id = xsc.xml_collection_id  
   FOR XML PATH('Columns'), TYPE  
  )   
FROM sys.xml_schema_components xsc  
JOIN dtplaced on xsc.xml_component_id=dtplaced.xml_component_id  
JOIN sys.xml_schema_collections xscol on xsc.xml_collection_id =xscol.xml_collection_id  
JOIN sys.schemas s on xscol.schema_id=s.schema_id  
group by xsc.xml_collection_id, s.name, xscol.name  
FOR XML PATH('XML_Schema_Collections'), TYPE) as T(x);   
if (@withdata = 0)    
  BEGIN  
  SELECT x as "*" FROM #_dt_collector for xml path(''), root('data');   
  drop table #_dt_collector;   
  return;   
  END;   
-- Declare cursor to find all columns bound to the schema collections  
DECLARE C CURSOR FOR  
SELECT S.Name, T.Name, C.Name   
FROM sys.columns C   
JOIN sys.tables T ON C.object_id = T.object_id  
JOIN sys.schemas S ON S.schema_id = T.schema_id  
WHERE C.xml_collection_id  
IN (SELECT distinct xsc.xml_collection_id  
    FROM sys.xml_schema_components xsc  
    JOIN (SELECT scp.*   
          FROM sys.xml_schema_component_placements scp   
          JOIN (SELECT * FROM sys.xml_schema_components   
                where base_xml_component_id    
                in (SELECT xml_component_id   
                    FROM sys.xml_schema_types   
                    where (name='dateTime' or name='date') and kind='P'  
                   )   
                union all  
                SELECT * FROM sys.xml_schema_components  
                where xml_component_id   
                in (SELECT xml_component_id   
                    FROM sys.xml_schema_types   
                    where (name='dateTime' or name='date') and kind='P'  
                    or kind='N' or kind='Z')   
               ) dttypes on scp.placed_xml_component_id=dttypes.xml_component_id  
          ) dtplaced on xsc.xml_component_id=dtplaced.xml_component_id);   
DECLARE @SchemaName nvarchar(max);   
DECLARE @TableName nvarchar(max);   
DECLARE @ColumnName nvarchar(max);   
DECLARE @strSQL nvarchar(MAX);   
OPEN C;   
FETCH NEXT FROM C INTO @SchemaName, @TableName, @ColumnName;   
WHILE (@@FETCH_STATUS = 0)   
BEGIN  
      SET @strSQL = 'INSERT INTO #_dt_collector SELECT x FROM ( ';   
      SET @strSQL = @strSQL +    
                    'SELECT ''' + @SchemaName + '.' + @TableName + '.' + @ColumnName   
                  + ''' as "@Column", ';   
      SET @strSQL = @strSQL +    
      'sum(' + @ColumnName + '.value(''count(//*[. instance of element(*,xs:dateTime?)])'', ''bigint'')) as "@dT_elements"  
     , sum(' + @ColumnName + '.value(''count(//*[. instance of element(*,xs:dateTime?)][substring(string(.),1,1) ="-"])'', ''bigint'')) as "@neg_dT_elements"  
     , sum(' + @ColumnName + '.value(''count(//*[. instance of element(*,xs:date?)])'', ''bigint'')) as "@date_elements"  
     , sum(' + @ColumnName + '.value(''count(//*[. instance of element(*,xs:date?)][substring(string(.),1,1) ="-"])'', ''bigint'')) as "@neg_date_elements"   
     , sum(' + @ColumnName + '.value(''count(for $d in //@*, $v in data($d)  
                      where $v instance of xs:dateTime?   
                      return 1)'', ''bigint'')) as "@dT_attributes"   
     , sum(' + @ColumnName + '.value(''count(for $d in //@*, $v in data($d)   
                      where $v instance of xs:dateTime?   
                      and substring(string($v),1,1)= "-"  
                      return 1)'', ''bigint'')) as "@neg_dt_attributes"  
     , sum(' + @ColumnName + '.value(''count(for $d in //@*, $v in data($d)   
                      where $v instance of xs:date?   
                      return 1)'', ''bigint'')) as "@date_attributes"   
     , sum('+ @ColumnName + '.value(''count(for $d in //@*, $v in data($d)   
                      where $v instance of xs:date?   
                      and substring(string($v),1,1)= "-"  
                      return 1)'', ''bigint'')) as "@neg_date_attributes"'  
      + ' FROM ' + @SchemaName + '.' + @TableName  
      + ' FOR XML PATH(''data''), type) T(x)';   
      --SELECT @strSQL;   
      EXEC sp_executesql @strSQL;   
      FETCH NEXT FROM C INTO @SchemaName, @TableName, @ColumnName;   
END;   
CLOSE C;   
DEALLOCATE C;   
SELECT x as "*" FROM #_dt_collector for xml path(''), root('data');   
drop table #_dt_collector;   
END;   
go  
-- Get the dependent columns per affected XML Schema Collection and the  
-- number of affected values  
EXECUTE DateTimeInvestigation 1;   
```  
  
 음수 값이 발견될 경우 다음과 같은 여러 가지 해결책을 사용할 수 있습니다.  
  
-   행을 삭제합니다.  
  
-   해당 값을 업데이트합니다.  
  
-   전체 XML 열을 지웁니다.  
  
-   xs:date 또는 xs:dateTime을 사용하지 않는 스키마 컬렉션으로 XML 열을 다시 형식화합니다(예: xs:string 사용).  
  
 음수 연도 문제를 해결하면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드할 수 있습니다.  
  
 업그레이드 후에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 XML 인덱스를 사용하려면 xs:date, xs:time 또는 xs:dateTime을 사용하는 모든 열에 대해 XML 열을 다시 형식화하거나 XML 인덱스를 다시 작성해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
  

---
title: "선택적 XML 인덱스 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1d769f62-f646-4057-b93a-bf5f90e935ed
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 77bbad8b312de3bf5657bebbad834e80bcbe842a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="create-selective-xml-index-transact-sql"></a>CREATE SELECTIVE XML INDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  지정한 테이블 및 XML 열에 새 선택적 XML 인덱스를 만듭니다. 선택적 XML 인덱스는 자주 쿼리하는 노드의 하위 집합만 인덱싱하여 XML 인덱싱 및 쿼리의 성능을 향상시킵니다. 또한 보조 선택적 XML 인덱스를 만들 수도 있습니다. 자세한 내용은 참조 [Create, Alter 및 보조 선택적 XML 인덱스 삭제](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE SELECTIVE XML INDEX index_name  
    ON <table_object> (xml_column_name)  
    [WITH XMLNAMESPACES (<xmlnamespace_list>)]  
    FOR (<promoted_node_path_list>)  
    [WITH (<index_options>)]  
  
<table_object> ::=  
 { [database_name. [schema_name ] . | schema_name. ] table_name }  
  
<promoted_node_path_list> ::=   
<named_promoted_node_path_item> [, <promoted_node_path_list>]  
  
<named_promoted_node_path_item> ::=   
<path_name> = <promoted_node_path_item>  
  
<promoted_node_path_item>::=  
<xquery_node_path_item> | <sql_values_node_path_item>  
  
<xquery_node_path_item> ::=   
<node_path> [AS XQUERY <xsd_type_or_node_hint>] [SINGLETON]  
  
<xsd_type_or_node_hint> ::=   
[<xsd_type>] [MAXLENGTH(x)] | node()  
  
<sql_values_node_path_item> ::=  
<node_path> AS SQL <sql_type> [SINGLETON]  
  
<node_path> ::=   
character_string_literal  
  
<xsd_type> ::=   
character_string_literal  
  
<sql_type> ::=   
identifier  
  
<path_name> ::=   
identifier  
  
<xmlnamespace_list> ::=   
<xmlnamespace_item> [, <xmlnamespace_list>]  
  
<xmlnamespace_item> ::=   
<xmlnamespace_uri> AS <xmlnamespace_prefix>  
  
<xml_namespace_uri> ::=   
character_string_literal  
  
<xml_namespace_prefix> ::=   
identifier  
  
<index_options> ::=   
(   
  | PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
)  
```  
  
##  <a name="Arguments"></a> 인수  
 *index_name*  
 만들 새 인덱스의 이름입니다. 인덱스 이름은 테이블에서 고유해야 하지만 데이터베이스 내에서 고유할 필요는 없습니다. 인덱스 이름은의 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다.  
  
 *\<table_object >* 인덱싱할 XML 열이 포함 된 테이블입니다. 다음 형식 중 하나를 사용합니다.  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
-   `table_name`  
  
 *xml_column_name*  
 인덱싱할 경로가 포함된 XML 열의 이름입니다.  
  
 [WITH XMLNAMESPACES **(**\<xmlnamespace_list >**)**] 인덱싱할 경로에서 사용 하는 네임 스페이스의 목록입니다. WITH XMLNAMESPACES 절의 구문에 대 한 내용은 참조 하세요. [WITH XMLNAMESPACES &#40; Transact SQL &#41; ](../../t-sql/xml/with-xmlnamespaces.md).  
  
 에 대 한 **(**\<promoted_node_path_list >**)** 선택적 최적화 힌트를 사용 하 여 인덱싱할 경로의 목록입니다. CREATE 또는 ALTER 문에 지정할 수 있는 최적화 힌트와 경로 대 한 정보를 참조 하십시오. [지정 경로 및 선택적 XML 인덱스에 대 한 최적화 힌트](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)합니다.  
  
 와  *\<e x _ >* 인덱스 옵션에 대 한 정보를 참조 하세요. [CREATE XML index&#40; 선택적 XML 인덱스 &#41; ](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
## <a name="best-practices"></a>최선의 구현 방법  
 대부분의 경우 더 나은 성능과 더 효율적인 저장소를 위해 일반 XML 인덱스 대신 선택적 XML 인덱스를 만듭니다. 그러나 다음 조건 중 하나에 해당하는 경우에는 선택적 XML 인덱스가 권장되지 않습니다.  
  
-   많은 수의 노드 경로를 매핑해야 하는 경우  
  
-   알 수 없는 위치에 있는 알 수 없는 요소에 대한 쿼리를 지원해야 하는 경우.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 제한 사항에 대 한 정보를 참조 하세요. [선택적 XML 인덱스 &#40; SXI &#41; ](../../relational-databases/xml/selective-xml-indexes-sxi.md).  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다. 사용자는 **sysadmin** 고정 서버 역할의 멤버 또는 **db_ddladmin** 및 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 선택적 XML 인덱스를 만드는 구문을 보여 줍니다. 또한 이 예에서는 선택적 최적화 힌트를 사용하여 인덱싱할 경로를 설명하는 구문의 여러 변형도 보여 줍니다.  
  
```  
CREATE TABLE Tbl ( id INT PRIMARY KEY, xmlcol XML );  
GO  
CREATE SELECTIVE XML INDEX sxi_index  
ON Tbl(xmlcol)  
FOR(  
    pathab   = '/a/b' as XQUERY 'node()',  
    pathabc  = '/a/b/c' as XQUERY 'xs:double',   
    pathdtext = '/a/b/d/text()' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON,  
    pathabe = '/a/b/e' as SQL NVARCHAR(100)  
);  
```  
  
 다음 예에는 WITH XMLNAMESPACES 절이 포함되어 있습니다.  
  
```  
CREATE SELECTIVE XML INDEX on T1(C1)  
WITH XMLNAMESPACES ('http://www.tempuri.org/' as myns)  
FOR ( path1 = '/myns:book/myns:author/text()' );  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SXI&#40;선택적 XML 인덱스&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [만들기, 변경 및 선택적 XML 인덱스 삭제](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)   
 [선택적 XML 인덱스에 대한 경로 및 최적화 힌트 지정](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)  
  
  


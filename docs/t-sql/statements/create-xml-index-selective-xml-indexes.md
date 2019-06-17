---
title: CREATE XML INDEX(선택적 XML 인덱스) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1f510151-41d5-45c2-9cd0-b1ca0246fffe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14e48f3e8af059b0055f9747c5fb1b2e2a53ca6a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65502815"
---
# <a name="create-xml-index-selective-xml-indexes"></a>CREATE XML INDEX(선택적 XML 인덱스)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  기존 선택적 XML 인덱스로 이미 인덱싱된 단일 경로에서 새 보조 선택적 XML 인덱스를 만듭니다. 또한 주 선택적 XML 인덱스를 만들 수도 있습니다. 자세한 내용은 [선택적 XML 인덱스 만들기, 변경 및 삭제](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE XML INDEX index_name  
    ON <table_object> ( xml_column_name )  
    USING XML INDEX sxi_index_name  
    FOR ( <xquery_or_sql_values_path> )  
    [WITH ( <index_options> )]  
  
<table_object> ::=   
{ database_name.schema_name.table_name | schema_name.table_name | table_name }  
  
<xquery_or_sql_values_path>::=   
<path_name>   
  
<path_name> ::=   
character string literal  
  
<xmlnamespace_list> ::=   
<xmlnamespace_item> [, <xmlnamespace_list>]  
  
<xmlnamespace_item> ::=   
xmlnamespace_uri AS xmlnamespace_prefix  
  
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
 만들 새 인덱스의 이름입니다. 인덱스 이름은 테이블에서 고유해야 하지만 데이터베이스 내에서 고유할 필요는 없습니다. 인덱스 이름은 [식별자](../../relational-databases/databases/database-identifiers.md) 규칙을 따라야 합니다.  
  
 ON *\<table_object>* 은 인덱싱할 XML 열이 포함된 테이블입니다. 다음 형식을 사용할 수 있습니다.  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
 *xml_column_name*  
 인덱싱할 경로가 포함된 XML 열의 이름입니다.  
  
 USING XML INDEX *sxi_index_name*  
 기존 선택적 XML 인덱스의 이름입니다.  
  
 FOR **(** \<xquery_or_sql_values_path> **)** 보조 선택적 XML 인덱스를 만드는 인덱싱된 경로의 이름입니다. 인덱싱할 경로는 CREATE SELECTIVE XML INDEX 문에서 할당된 이름입니다. 자세한 내용은 [CREATE SELECTIVE XML INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md)를 참조하세요.  
  
 WITH \<index_options> 인덱스 옵션에 대한 자세한 내용은 [CREATE XML INDEX](../../t-sql/statements/create-xml-index-selective-xml-indexes.md)를 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 기본 테이블의 각 XML 열에는 여러 개의 보조 선택적 XML 인덱스가 있을 수 있습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 XML 열에 선택적 XML 인덱스가 있어야 이 열에 보조 선택적 XML 인덱스를 만들 수 있습니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다. 사용자는 **sysadmin** 고정 서버 역할의 멤버 또는 **db_ddladmin** 및 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `pathabc`경로에서 보조 선택적 XML 인덱스를 만듭니다. 인덱싱할 경로는 [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md)에서 할당된 이름입니다.  
  
```  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR ( pathabc );  
```  
  
## <a name="see-also"></a>참고 항목  
 [SXI&#40;선택적 XML 인덱스&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [보조 선택적 XML 인덱스 만들기, 변경 및 삭제](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md)  
  
  


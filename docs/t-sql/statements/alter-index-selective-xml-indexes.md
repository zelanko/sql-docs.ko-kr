---
title: "ALTER INDEX (선택적 XML 인덱스) | Microsoft Docs"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cca96a8f-7737-42d2-bbcc-03d5f858dcc1
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e7854dd1d9365f97628341c4160c368f97308302
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-index-selective-xml-indexes"></a>ALTER INDEX(선택적 XML 인덱스)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  기존 선택적 XML 인덱스를 수정합니다. ALTER INDEX 문은 다음 항목 중 하나 이상을 변경합니다.  
  
-   인덱싱된 경로 목록(FOR 절)  
  
-   네임스페이스 목록(WITH XMLNAMESPACES 절)  
  
-   인덱스 옵션(WITH 절)  
  
 보조 선택적 XML 인덱스는 변경할 수없습니다. 자세한 내용은 참조 [Create, Alter 및 보조 선택적 XML 인덱스 삭제](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER INDEX index_name  
    ON <table_object>   
    [WITH XMLNAMESPACES ( <xmlnamespace_list> )]  
    FOR ( <promoted_node_path_action_list> )  
    [WITH ( <index_options> )]  
  
<table_object> ::=   
{ [database_name. [schema_name ] . | schema_name. ] table_name }  
<promoted_node_path_action_list> ::=   
<promoted_node_path_action_item> [, <promoted_node_path_action_list>]  
  
<promoted_node_path_action_item>::=   
<add_node_path_item_action> | <remove_node_path_item_action>  
  
<add_node_path_item_action> ::=  
ADD <path_name> = <promoted_node_path_item>  
  
<promoted_node_path_item>::=  
<xquery_node_path_item> | <sql_values_node_path_item>  
  
<remove_node_path_item_action> ::= REMOVE <path_name>   
  
<path_name_or_typed_node_path>::=   
<path_name> | <typed_node_path>  
  
<typed_node_path> ::=   
<node_path> [[AS XQUERY <xsd_type_ext>] | [AS SQL <sql_type>]]  
  
<xquery_node_path_item> ::=   
<node_path> [AS XQUERY <xsd_type_or_node_hint>] [SINGLETON]  
  
<xsd_type_or_node_hint> ::=   
[<xsd_type>] [MAXLENGTH(x)] | 'node()'  
  
<sql_values_node_path_item> ::=   
<node_path> AS SQL <sql_type> [SINGLETON]  
  
<node_path> ::=   
character_string_literal  
  
<xsd_type_ext> ::=   
character_string_literal  
  
<sql_type> ::=   
identifier  
  
<path_name> ::=   
identifier  
  
<xmlnamespace_list> ::=   
<xmlnamespace_item> [, <xmlnamespace_list>]  
  
<xmlnamespace_item> ::=   
<xmlnamespace_uri> AS <xmlnamespace_prefix>  
  
<xml_namespace_uri> ::= character_string_literal  
<xml_namespace_prefix> ::= identifier  
  
<index_options> ::=   
(   
  | PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY =OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE =OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
)  
```  
  
##  <a name="Arguments"></a> 인수  
 *index_name*  
 변경할 기존 인덱스의 이름입니다.  
  
 *\<table_object >*  
 인덱싱할 XML 열이 포함된 테이블입니다. 다음 형식 중 하나를 사용합니다.  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
-   `table_name`  
  
 [WITH XMLNAMESPACES **(** \<xmlnamespace_list > **)**]  
 인덱싱할 경로에서 사용하는 네임스페이스 목록입니다. WITH XMLNAMESPACES 절의 구문에 대 한 내용은 참조 하세요. [WITH XMLNAMESPACES &#40; Transact SQL &#41; ](../../t-sql/xml/with-xmlnamespaces.md).  
  
 에 대 한 **(** \<promoted_node_path_action_list > **)**  
 추가 또는 제거할 인덱싱된 경로의 목록입니다.  
  
-   **경로 추가 합니다.** 경로를 추가할 때는 CREATE SELECTIVE XML INDEX 문과 함께 경로를 만드는 데 사용되는 구문과 동일한 구문을 사용합니다. CREATE 또는 ALTER 문에 지정할 수 있는 경로 대 한 정보를 참조 하십시오. [지정 경로 및 선택적 XML 인덱스에 대 한 최적화 힌트](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)합니다.  
  
-   **경로 제거 합니다.** 경로를 제거할 때는 해당 경로를 만들 때 지정한 경로 이름을 제공합니다.  
  
 [와 **(** \<e x _ > **)**]  
 만 지정할 수 있습니다 \<e x _ > FOR 절 없이 ALTER INDEX를 사용 합니다. ALTER INDEX를 사용하여 인덱스에서 경로를 추가 또는 제거할 때는 인덱스 옵션이 잘못된 인수가 아닙니다. 인덱스 옵션에 대 한 정보를 참조 하세요. [CREATE XML index&#40; 선택적 XML 인덱스 &#41; ](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
## <a name="remarks"></a>주의  
  
> [!IMPORTANT]  
>  ALTER INDEX 문을 실행하면 선택적 XML 인덱스가 항상 다시 작성됩니다. 이 프로세스가 서버 리소스에 미치는 영향을 고려해야 합니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 ALTER INDEX를 실행하려면 테이블 또는 뷰에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 ALTER INDEX 문을 보여 줍니다. 이 문은 인덱스의 XQuery 부분에 `'/a/b/m'` 경로를 추가하고 [CREATE SELECTIVE XML INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md) 항목의 예에서 만든 인덱스의 SQL 부분에서 `'/a/b/e'` 경로를 삭제합니다. 삭제할 경로는 해당 경로를 만들 때 지정한 경로 이름으로 식별됩니다.  
  
```tsql  
ALTER INDEX sxi_index  
ON Tbl  
FOR   
(  
    ADD pathm = '/a/b/m' as XQUERY 'node()' ,  
    REMOVE pathabe  
);  
```  
  
 다음 예에서는 인덱스 옵션을 지정하는 ALTER INDEX 문을 보여 줍니다. 인덱스 옵션이 허용되는 이유는 이 문이 FOR 절을 사용하여 경로를 추가하거나 제거하지 않기 때문입니다.  
  
```tsql  
ALTER INDEX sxi_index  
ON Tbl  
PAD_INDEX = ON;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SXI&#40;선택적 XML 인덱스&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [만들기, 변경 및 선택적 XML 인덱스 삭제](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)   
 [선택적 XML 인덱스에 대한 경로 및 최적화 힌트 지정](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)  
  
  


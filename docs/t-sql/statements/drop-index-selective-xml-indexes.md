---
title: DROP INDEX(선택적 XML 인덱스) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP XML INDEX statement
dev_langs:
- TSQL
ms.assetid: 4779ae84-e5f4-4d04-8fc1-e24a6631b428
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 663dc63894d8356bc9856cba1fca23908e26ef74
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65503646"
---
# <a name="drop-index-selective-xml-indexes"></a>DROP INDEX(선택적 XML 인덱스)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기존 선택적 XML 인덱스 또는 보조 선택적 XML 인덱스를 삭제합니다. 자세한 내용은 [SXI&#40;선택적 XML 인덱스&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DROP INDEX index_name ON <object>  
    [ WITH ( <drop_index_option> [ ,...n ] ) ]  
  
<object> ::=  
{ database_name.schema_name.table_or_view_name | schema_name.table_or_view_name | table_or_view_name }  
  
<drop_index_option> ::=  
{  
    MAXDOP = max_degree_of_parallelism  
    | ONLINE = { ON | OFF }  
}  
```  
  
##  <a name="Arguments"></a> 인수  
 *index_name*  
 삭제할 기존 인덱스의 이름입니다.  
  
 *\< object>* 인덱싱된 XML 열이 포함된 테이블입니다. 다음 형식 중 하나를 사용합니다.  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
-   `table_name`  
  
 *\<drop_index_option >* 인덱스 삭제 옵션에 대한 정보는 [DROP INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)를 참조하세요.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 DROP INDEX를 실행하려면 테이블 또는 뷰에 대한 ALTER 권한이 필요합니다. 이 권한은 기본적으로 sysadmin 고정 서버 역할과 db_ddladmin 및 db_owner 고정 데이터베이스 역할에 부여됩니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 DROP INDEX 문을 보여 줍니다.  
  
```  
DROP INDEX sxi_index ON tbl;  
```  
  
## <a name="see-also"></a>참고 항목  
 [SXI&#40;선택적 XML 인덱스&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [선택적 XML 인덱스 만들기, 변경 및 삭제](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)  
  
  


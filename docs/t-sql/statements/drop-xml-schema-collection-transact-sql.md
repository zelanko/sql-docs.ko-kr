---
title: DROP XML SCHEMA COLLECTION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP XML SCHEMA COLLECTION
- DROP_XML_SCHEMA_COLLECTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting XML schema collections
- XML schema collections [SQL Server], removing
- schema collections [SQL Server], removing
- removing XML schema collections
- dropping XML schema collections
- DROP XML SCHEMA COLLECTION statement
ms.assetid: d686f2f5-e03a-4ffe-a566-6036628f46f1
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 52449a89ac93ea9137e4314c4050573eafb1e28a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37999965"
---
# <a name="drop-xml-schema-collection-transact-sql"></a>DROP XML SCHEMA COLLECTION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  전체 XML 스키마 컬렉션과 모든 해당 구성 요소를 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP XML SCHEMA COLLECTION [ relational_schema. ]sql_identifier  
```  
  
## <a name="arguments"></a>인수  
 *relational_schema*  
 관계형 스키마 이름을 식별합니다. 지정하지 않으면 기본 관계형 스키마가 사용됩니다.  
  
 *sql_identifier*  
 삭제할 XML 스키마 컬렉션의 이름입니다.  
  
## <a name="remarks"></a>Remarks  
 XML 스키마 컬렉션을 삭제하는 것은 트랜잭션 작업입니다. 즉, 트랜잭션 내부에서 XML 스키마 컬렉션을 삭제하고 나중에 트랜잭션을 롤백하는 경우 XML 스키마 컬렉션이 삭제되지 않습니다.  
  
 사용 중인 XML 스키마 컬렉션은 삭제할 수 없습니다. 즉, 다음과 같은 컬렉션은 삭제할 수 없습니다.  
  
-   **xml** 유형 매개 변수 또는 열과 연결된 컬렉션  
  
-   테이블 제약 조건에 지정된 컬렉션  
  
-   스키마 바운드 함수 또는 저장 프로시저에서 참조하는 컬렉션. 예를 들어 다음 함수는 `MyCollection`을 지정하기 때문에 `WITH SCHEMABINDING` XML 스키마 컬렉션을 잠급니다. 이것을 제거하면 XML SCHEMA COLLECTION에 대한 잠금이 사라집니다.  
  
    ```  
    CREATE FUNCTION dbo.MyFunction()  
    RETURNS int  
    WITH SCHEMABINDING  
    AS  
    BEGIN  
       ...  
       DECLARE @x XML(MyCollection)  
       ...  
    END;  
    ```  
  
## <a name="permissions"></a>Permissions  
 XML SCHEMA COLLECTION을 삭제하려면 이 컬렉션에 대한 DROP 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 XML 스키마 컬렉션을 제거하는 것을 보여 줍니다.  
  
```  
DROP XML SCHEMA COLLECTION ManuInstructionsSchemaCollection;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE XML SCHEMA COLLECTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)   
 [ALTER XML SCHEMA COLLECTION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [서버의 XML 스키마 컬렉션에 대한 요구 사항 및 제한 사항](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  

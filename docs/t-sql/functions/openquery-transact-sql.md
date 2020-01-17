---
title: OPENQUERY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPENQUERY_TSQL
- OPENQUERY
dev_langs:
- TSQL
helpviewer_keywords:
- DELETE statement [SQL Server], OPENQUERY function
- OPENQUERY function
- FROM clause, OPENQUERY function
- UPDATE statement [SQL Server], OPENQUERY function
- pass-through queries [SQL Server]
- INSERT statement [SQL Server], OPENQUERY function
ms.assetid: b805e976-f025-4be1-bcb0-3a57b0c57717
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5c2f1a1b1060ff2ce659ed87db9fabb5c6c5346a
ms.sourcegitcommit: 02449abde606892c060ec9e9e9a85a3f49c47c6c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74542276"
---
# <a name="openquery-transact-sql"></a>OPENQUERY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  지정한 연결된 서버에서 지정한 통과 쿼리를 실행합니다. 이 서버는 OLE DB 데이터 원본입니다. OPENQUERY는 테이블 이름처럼 쿼리의 FROM 절에서 참조될 수 있습니다. 또한 OPENQUERY는 INSERT, UPDATE 또는 DELETE 문의 대상 테이블로 참조될 수도 있습니다. 이것은 OLE DB 공급자 기능에 종속됩니다. 쿼리는 여러 결과 집합을 반환할 수 있지만 OPENQUERY는 첫 번째 것만 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
OPENQUERY ( linked_server ,'query' )  
```  
  
## <a name="arguments"></a>인수  
 *linked_server*  
 연결된 서버의 이름을 나타내는 식별자입니다.  
  
 **'** *query* **'**  
 연결된 서버에서 실행된 쿼리 문자열입니다. 문자열의 최대 길이는 8KB입니다.  
  
## <a name="remarks"></a>설명  
 OPENQUERY는 변수를 인수로 받아들이지 않습니다.  
  
 OPENQUERY는 연결된 서버에서 확장 저장 프로시저를 실행하는 데 사용할 수 없습니다. 그러나 확장 저장 프로시저는 네 부분으로 된 이름을 사용하여 연결된 서버에서 실행할 수 있습니다. 다음은 그 예입니다.  
  
```sql  
EXEC SeattleSales.master.dbo.xp_msver  
```  
  
 FROM 절에서 OPENDATASOURCE, OPENQUERY 또는 OPENROWSET에 대한 모든 호출은 두 호출에 동일한 인수가 제공되는 경우에도 업데이트의 대상으로 사용되는 함수에 대한 호출과는 개별적이고 독립적으로 평가됩니다. 특히 이러한 호출 중 하나의 결과에 적용되는 필터 또는 조인 조건은 다른 호출의 결과에 영향을 미치지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 모든 사용자가 OPENQUERY를 실행할 수 있습니다. 원격 서버 연결에 사용되는 사용 권한은 연결된 서버에 대해 정의된 설정에서 가져옵니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-executing-an-update-pass-through-query"></a>A. UPDATE 통과 쿼리 실행  
 다음 예에서는 예 1에서 만든 연결된 서버에 대해 `UPDATE` 통과 쿼리를 사용합니다.  
  
```sql  
UPDATE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE id = 101')   
SET name = 'ADifferentName';  
```  
  
### <a name="b-executing-an-insert-pass-through-query"></a>B. INSERT 통과 쿼리 실행  
 다음 예에서는 예 1에서 만든 연결된 서버에 대해 `INSERT` 통과 쿼리를 사용합니다.  
  
```sql  
INSERT OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles')  
VALUES ('NewTitle');  
```  
  
### <a name="c-executing-a-delete-pass-through-query"></a>C. DELETE 통과 쿼리 실행  
 다음 예에서는 `DELETE` 통과 쿼리를 사용하여 예 3에서 삽입된 행을 삭제합니다.  
  
```sql  
DELETE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
  
### <a name="d-executing-a-select-pass-through-query"></a>D. SELECT 통과 쿼리 실행  
 다음 예에서는 `SELECT` 통과 쿼리를 사용하여 예 3에서 삽입된 행을 선택합니다.  
  
```sql  
SELECT * FROM OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
    
## <a name="see-also"></a>참고 항목  
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE&#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

---
description: SET NOCOUNT(Transact-SQL)
title: SET NOCOUNT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NOCOUNT
- SET_NOCOUNT_TSQL
- NOCOUNT_TSQL
- SET NOCOUNT
dev_langs:
- TSQL
helpviewer_keywords:
- NOCOUNT option
- number of rows affected by statement
- row affected by statements [SQL Server]
- counting rows
- SET NOCOUNT statement
ms.assetid: eb3e6727-cb26-4bc2-84c7-171cbac02029
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 361afab78b3822c8c4aa5ed7bc3c520acb1e8b43
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471874"
---
# <a name="set-nocount-transact-sql"></a>SET NOCOUNT(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 저장 프로시저의 영향을 받은 행 수를 나타내는 메시지가 결과 집합의 일부로 반환되지 않도록 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
SET NOCOUNT { ON | OFF }   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>설명
 SET NOCOUNT 옵션을 ON으로 설정하면 이 개수가 반환되지 않습니다. SET NOCOUNT 옵션을 OFF로 설정하면 이 수가 반환됩니다.  
  
 SET NOCOUNT가 ON으로 설정되어 있을 때도 @@ROWCOUNT 함수는 업데이트됩니다.  
  
 SET NOCOUNT 옵션을 ON으로 설정하면 저장 프로시저의 각 문에 대해 클라이언트에게 DONE_IN_PROC 메시지를 보내지 않습니다. 실제 데이터를 많이 반환하지 않는 일부 문이 포함된 저장 프로시저 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 루프가 포함된 프로시저의 경우 SET NOCOUNT를 ON으로 설정하면 네트워크 트래픽이 크게 줄기 때문에 성능이 눈에 띄게 향상됩니다.  
  
 SET NOCOUNT로 지정된 설정은 실행 시간 또는 런타임에 적용되며 구문 분석 시에는 적용되지 않습니다.  
  
 이 설정에 대한 현재 설정을 보려면 다음 쿼리를 실행합니다.  
  
```sql
DECLARE @NOCOUNT VARCHAR(3) = 'OFF';  
IF ( (512 & @@OPTIONS) = 512 ) SET @NOCOUNT = 'ON';  
SELECT @NOCOUNT AS NOCOUNT;  
  
```  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 영향을 받은 행 수에 대한 메시지가 표시되지 않도록 지정합니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SET NOCOUNT OFF;  
GO  
-- Display the count message.  
SELECT TOP(5)LastName  
FROM Person.Person  
WHERE LastName LIKE 'A%';  
GO  
-- SET NOCOUNT to ON to no longer display the count message.  
SET NOCOUNT ON;  
GO  
SELECT TOP(5) LastName  
FROM Person.Person  
WHERE LastName LIKE 'A%';  
GO  
-- Reset SET NOCOUNT to OFF  
SET NOCOUNT OFF;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [@@ROWCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

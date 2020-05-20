---
title: sp_prepare (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepare
ms.assetid: f328c9eb-8211-4863-bafa-347e1bf7bb3f
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9e5875d4160ca3bb3e06670d02426e7b3cfe097c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832593"
---
# <a name="sp_prepare-transact-sql"></a>sp_prepare(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

매개 변수가 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 준비 하 고 실행을 위해 문 *핸들* 을 반환 합니다.  `sp_prepare`는 TDS(Tabular Data Stream) 패킷에서 ID = 11을 지정하여 호출합니다.  
  
 ![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_prepare handle OUTPUT, params, stmt, options  
```  
  
## <a name="arguments"></a>인수  
 *처리*  
 는 SQL Server 생성 준비 된 *핸들* 식별자입니다. *handle* 은 **int** 반환 값을 포함 하는 필수 매개 변수입니다.  
  
 *params*  
 매개 변수가 있는 문을 식별합니다. 변수의 매개 변수 정의는 문에서 매개 변수 표식을 *대체 합니다.* *params* 는 **ntext**, **nchar**또는 **nvarchar** 입력 값을 호출 하는 필수 매개 변수입니다. 문에 매개 변수가 없으면 NULL 값을 입력합니다.  
  
 *stmt*  
 커서 결과 집합을 정의합니다. *Stmt* 매개 변수는 필수 이며 **ntext**, **nchar**또는 **nvarchar** 입력 값에 대해를 호출 합니다.  
  
 *options*  
 커서 결과 집합 열의 설명을 반환하는 선택적 매개 변수입니다. *옵션* 에는 다음 int 입력 값이 필요 합니다.  
  
|값|설명|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
## <a name="examples"></a>예  
A. 다음 예제에서는 간단한 문을 준비하고 실행합니다.  
  
```sql  
DECLARE @P1 int;  
EXEC sp_prepare @P1 output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name FROM sys.databases WHERE name=@P1 AND state_desc = @P2';  
EXEC sp_execute @P1, N'tempdb', N'ONLINE';  
EXEC sp_unprepare @P1;  
```

B. 다음 예에서는 AdventureWorks2016 데이터베이스에서 문을 준비 하 고 나중에 핸들을 사용 하 여 실행 합니다.

```sql
-- Prepare query
DECLARE @P1 int;  
EXEC sp_prepare @P1 output,   
    N'@Param int',  
    N'SELECT *
FROM Sales.SalesOrderDetail AS sod
INNER JOIN Production.Product AS p ON sod.ProductID = p.ProductID
WHERE SalesOrderID = @Param
ORDER BY Style DESC;';  

-- Return handle for calling application
SELECT @P1;
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
-----------
1

(1 row affected)
```

그런 다음 응용 프로그램은 준비 된 계획을 삭제 하기 전에 핸들 값 1을 사용 하 여 쿼리를 두 번 실행 합니다.

```sql
EXEC sp_execute 1, 49879;  
GO

EXEC sp_execute 1, 48766;
GO

EXEC sp_unprepare 1; 
GO
```
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  


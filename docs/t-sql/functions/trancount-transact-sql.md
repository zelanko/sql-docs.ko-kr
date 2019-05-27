---
title: '@@TRANCOUNT(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@TRANCOUNT_TSQL'
- '@@TRANCOUNT'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@TRANCOUNT function'
- number of active transactions
- connections [SQL Server], active transactions
- active transactions
ms.assetid: b2638410-e410-4bd0-9b54-90096182b2b6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e313feff62ed3e8ff8f6e34d7e1e59f02e0537c7
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65946689"
---
# <a name="x40x40trancount-transact-sql"></a>&#x40;&#x40;TRANCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 연결에서 발생한 BEGIN TRANSACTION 문의 수를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@TRANCOUNT  
```  
  
## <a name="return-types"></a>반환 형식  
 **integer**  
  
## <a name="remarks"></a>Remarks  
 BEGIN TRANSACTION 문은 @@TRANCOUNT을 1씩 늘립니다. @@TRANCOUNT에 영향을 주지 않는 ROLLBACK TRANSACTION *savepoint_name*을 제외한 ROLLBACK TRANSACTION은 @@TRANCOUNT을 0으로 줄입니다. COMMIT TRANSACTION 또는 COMMIT WORK는 @@TRANCOUNT을 1씩 줄입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-showing-the-effects-of-the-begin-and-commit-statements"></a>1. BEGIN 및 COMMIT 문의 영향  
 다음 예에서는 중첩된 `BEGIN` 및 `COMMIT` 문이 `@@TRANCOUNT` 변수에 주는 영향을 보여 줍니다.  
  
```  
PRINT @@TRANCOUNT  
--  The BEGIN TRAN statement will increment the  
--  transaction count by 1.  
BEGIN TRAN  
    PRINT @@TRANCOUNT  
    BEGIN TRAN  
        PRINT @@TRANCOUNT  
--  The COMMIT statement will decrement the transaction count by 1.  
    COMMIT  
    PRINT @@TRANCOUNT  
COMMIT  
PRINT @@TRANCOUNT  
--Results  
--0  
--1  
--2  
--1  
--0  
```  
  
### <a name="b-showing-the-effects-of-the-begin-and-rollback-statements"></a>2. BEGIN 및 ROLLBACK 문의 영향  
 다음 예에서는 중첩된 `BEGIN TRAN` 및 `ROLLBACK` 문이 `@@TRANCOUNT` 변수에 주는 영향을 보여 줍니다.  
  
```  
PRINT @@TRANCOUNT  
--  The BEGIN TRAN statement will increment the  
--  transaction count by 1.  
BEGIN TRAN  
    PRINT @@TRANCOUNT  
    BEGIN TRAN  
        PRINT @@TRANCOUNT  
--  The ROLLBACK statement will clear the @@TRANCOUNT variable  
--  to 0 because all active transactions will be rolled back.  
ROLLBACK  
PRINT @@TRANCOUNT  
--Results  
--0  
--1  
--2  
--0  
```  
  
## <a name="see-also"></a>참고 항목  
 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TransactION&#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

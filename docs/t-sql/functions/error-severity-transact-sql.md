---
title: ERROR_SEVERITY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ERROR_SEVERITY_TSQL
- ERROR_SEVERITY
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], severity
- messages [SQL Server], severity
- TRY...CATCH [SQL Server]
- CATCH block
- ERROR_SEVERITY function
ms.assetid: 50228f2f-6949-4d2e-8e43-fad11bf973ab
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a8784072fe01c8da2af3af601126957583f9ebf
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52515798"
---
# <a name="errorseverity-transact-sql"></a>ERROR_SEVERITY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

이 함수는 해당 오류가 TRY...CATCH 구문의 CATCH 블록을 실행시키는 경우 오류가 발생하는 오류의 심각도 값을 반환합니다.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ERROR_SEVERITY ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="return-value"></a>반환 값  
오류가 발생하는 CATCH 블록에서 호출되는 경우 `ERROR_SEVERITY`는 `CATCH` 블록이 실행되도록 한 오류의 심각도 값을 반환합니다.  

`ERROR_SEVERITY`는 CATCH 블록 범위 밖에서 호출된 경우 NULL을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
`ERROR_SEVERITY`는 CATCH 블록 범위 내의 어떤 위치에서나 호출을 지원합니다.  
  
`ERROR_SEVERITY`는 `CATCH` 블록의 범위 내에서 실행되는 경우 실행 횟수 또는 실행 위치에 관계 없이 오류의 심각도 값을 반환합니다. 이것은 오류가 발생한 명령문 바로 다음 명령문에 오류 번호만 반환하는 @@ERROR 같은 함수와 대조적입니다.  
  
`ERROR_SEVERITY`는 일반적으로 중첩된 `CATCH` 블록에서 작동합니다. `ERROR_SEVERITY`는 해당 `CATCH` 블록을 참조한 `CATCH` 블록의 범위에 관련된 오류 심각도 값을 반환합니다. 예를 들어 외부 TRY...CATCH 구문의 `CATCH` 블록에는 내부 `TRY...CATCH` 구문이 있을 수 있습니다. 해당 내부 `CATCH` 블록 내에서 `ERROR_SEVERITY`는 내부 `CATCH` 블록을 호출한 오류의 심각도 값을 반환합니다. `ERROR_SEVERITY`가 외부 `CATCH` 블록에서 실행되는 경우 해당 외부 `CATCH` 블록을 호출한 오류의 심각도 값을 반환합니다.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-errorseverity-in-a-catch-block"></a>1. CATCH 블록에서 ERROR_SEVERITY 사용  
이 예에서는 0으로 나누기 오류를 생성하는 저장 프로시저를 보여 줍니다. `ERROR_SEVERITY`는 해당 오류의 심각도 값을 반환합니다.  
```sql  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_SEVERITY() AS ErrorSeverity;  
END CATCH;  
GO  
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
```
-----------

(0 row(s) affected)

ErrorSeverity
-------------
16

(1 row(s) affected)

```  
  
### <a name="b-using-errorseverity-in-a-catch-block-with-other-error-handling-tools"></a>2. CATCH 블록에서 다른 오류 처리 도구와 함께 ERROR_SEVERITY 사용  
이 예에서는 0으로 나누기 오류를 일으키는 `SELECT` 문을 보여 줍니다. 저장된 프로시저는 오류에 대한 정보를 반환합니다.  

```sql  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_LINE() AS ErrorLine,  
        ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
```
-----------

(0 row(s) affected)

ErrorNumber ErrorSeverity ErrorState  ErrorProcedure  ErrorLine   ErrorMessage
----------- ------------- ----------- --------------- ----------- ----------------------------------
8134        16            1           NULL            4           Divide by zero error encountered.

(1 row(s) affected)

```  
  
## <a name="see-also"></a>참고 항목  
 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE&#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR&#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
 [오류 및 이벤트 참조&#40;데이터베이스 엔진&#41;](../../relational-databases/errors-events/errors-and-events-reference-database-engine.md)     
  
    


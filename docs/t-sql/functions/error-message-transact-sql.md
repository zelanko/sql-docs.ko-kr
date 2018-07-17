---
title: ERROR_MESSAGE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ERROR_MESSAGE_TSQL
- ERROR_MESSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- ERROR_MESSAGE function
- errors [SQL Server], text of
- messages [SQL Server], text of
- TRY...CATCH [SQL Server]
- CATCH block
ms.assetid: f32877a6-5f17-418c-a32c-5a1a344b3c45
caps.latest.revision: 53
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ad684b6105de84c82c23297d3d0aa0848dd78e42
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37786004"
---
# <a name="errormessage-transact-sql"></a>ERROR_MESSAGE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

이 함수는 TRY...CATCH 구문의 CATCH 블록을 실행시키는 오류의 메시지 텍스트를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ERROR_MESSAGE ( )   
```  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar(4000)**  
  
## <a name="return-value"></a>반환 값  
CATCH 블록에서 호출된 경우 `ERROR_MESSAGE`는 `CATCH` 블록을 실행시키는 오류 메시지의 전체 텍스트를 반환합니다. 이 텍스트는 대체 가능한 매개 변수(예를 들어 길이, 개체 이름 또는 시간)에 제공된 값을 포함합니다.  
  
`ERROR_MESSAGE`는 CATCH 블록 범위 밖에서 호출된 경우 NULL을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
`ERROR_MESSAGE`는 CATCH 블록 범위 내의 어떤 위치에서나 호출을 지원합니다.  
  
`ERROR_MESSAGE`는 `CATCH` 블록의 범위 내에서 실행되는 경우 실행 횟수 또는 실행 위치에 관계 없이 관련 오류 메시지를 반환합니다. 이것은 오류가 발생한 명령문 바로 다음 명령문에 오류 번호만 반환하는 @@ERROR 같은 함수와 대조적입니다.  
  
중첩된 `CATCH` 블록에서 `ERROR_MESSAGE`는 해당 `CATCH` 블록을 참조한 `CATCH` 블록의 범위에 관련된 오류 메시지를 반환합니다. 예를 들어 외부 TRY...CATCH 구문의 `CATCH` 블록에는 내부 `TRY...CATCH` 구문이 있을 수 있습니다. 해당 내부 `CATCH` 블록 내에서 `ERROR_MESSAGE`는 내부 `CATCH` 블록을 호출한 오류에서 메시지를 반환합니다. `ERROR_MESSAGE`가 외부 `CATCH` 블록에서 실행되는 경우 해당 외부 `CATCH` 블록을 호출한 오류에서 메시지를 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-errormessage-in-a-catch-block"></a>1. CATCH 블록에서 ERROR_MESSAGE 사용  
이 예에서는 0으로 나누기 오류를 일으키는 `SELECT` 문을 보여 줍니다. `CATCH` 블록은 오류 메시지를 반환합니다.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  

-----------

(0 row(s) affected)

ErrorMessage
----------------------------------
Divide by zero error encountered.

(1 row(s) affected)

```  
  
### <a name="b-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>2. 다른 오류 처리 도구로 CATCH 블록에서 ERROR_MESSAGE 사용  
이 예에서는 0으로 나누기 오류를 일으키는 `SELECT` 문을 보여 줍니다. 오류 메시지와 함께 `CATCH` 블록은 해당 오류에 대한 정보를 반환합니다.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  

-----------

(0 row(s) affected)

ErrorNumber ErrorSeverity ErrorState  ErrorProcedure  ErrorLine  ErrorMessage
----------- ------------- ----------- --------------- ---------- ----------------------------------
8134        16            1           NULL            4          Divide by zero error encountered.

(1 row(s) affected)

```
  


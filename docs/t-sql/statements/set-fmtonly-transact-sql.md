---
title: SET FMTONLY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FMTONLY_TSQL
- FMTONLY
- SET FMTONLY
- SET_FMTONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server], only metadata returned
- SET FMTONLY statement
- FMTONLY option
ms.assetid: 02a1d9ac-2e58-433c-9a07-2c5a4a2214e1
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1cf925ce8ec9095acec90a34ed7d08f04826c2c1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="set-fmtonly-transact-sql"></a>SET FMTONLY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  클라이언트에 메타데이터만 반환합니다. 쿼리를 실제로 실행하지 않고 응답 형식을 테스트하는 데 사용할 수 있습니다.  
  
> [!NOTE]  
>  이 기능은 사용할 수 없습니다. 이 기능으로 대체 되었습니다 [sp_describe_first_result_set &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md), [sp_describe_undeclared_parameters &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md), [sys.dm_exec_describe_first_result_set&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md), 및 [sys.dm_exec_describe_first_result_set_for_object&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SET FMTONLY { ON | OFF }   
```  
  
## <a name="remarks"></a>주의  
 SET FMTONLY 옵션을 ON으로 설정하면 요청으로 인해 어떤 행도 처리되거나 클라이언트에게 보내지지 않습니다.  
  
 SET FMTONLY 옵션은 실행 시나 런타임에 설정되며 구문 분석 시에는 설정되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-view-the-column-header-information-for-a-query-without-actually-running-the-query"></a>A: 쿼리를 실제로 실행 하지 않고 쿼리에 대 한 열 헤더 정보 보기  
 다음 예에서는 `SET FMTONLY` 설정을 `ON`으로 변경하고 `SELECT` 문을 실행합니다. 이렇게 설정하면 문 실행 후 열 정보만 반환되고 데이터 행은 반환되지 않습니다.  
  
```  
USE AdventureWorks2012;  
GO  
SET FMTONLY ON;  
GO  
SELECT *   
FROM HumanResources.Employee;  
GO  
SET FMTONLY OFF;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-view-the-column-header-information-for-a-query-without-actually-running-the-query"></a>2. 실제로 쿼리를 실행 하지 않고 쿼리에 대 한 열 머리글 정보를 표시 합니다.  
 다음 예에서는 쿼리에 대 한 열 (메타 데이터) 헤더 정보만 반환 하는 방법을 보여 줍니다. FMTONLY OFF로 설정으로 시작 하 고 SELECT 문의 하기 전에 FMTONLY ON으로 변경 하는 일괄 처리 합니다. 이 인해 반환할 열 머리글만; SELECT 문을 데이터의 아무 행도 반환 합니다.  
  
```  
-- Uses AdventureWorks  
  
BEGIN  
    SET FMTONLY OFF;  
    SET DATEFORMAT mdy;  
    SET FMTONLY ON;  
    SELECT * FROM dbo.DimCustomer;  
    SET FMTONLY OFF;  
END  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  



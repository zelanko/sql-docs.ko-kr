---
description: sys.sp_cdc_stop_job(Transact-SQL)
title: sys. sp_cdc_stop_job (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_stop_job_TSQL
- sys.sp_cdc_stop_job
- sp_cdc_stop_job_TSQL
- sp_cdc_stop_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_stop_job
ms.assetid: 421fc21c-c7a4-407c-8b31-359273b68c63
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1b82d231a4633c2aa3ed7b45833009c8a2bc43a5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89526422"
---
# <a name="syssp_cdc_stop_job-transact-sql"></a>sys.sp_cdc_stop_job(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스의 변경 데이터 캡처 정리 또는 캡처 작업을 중지합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_cdc_stop_job [ [ @job_type = ] 'job_type' ]  
```  
  
## <a name="arguments"></a>인수  
`[ [ @job_type = ] 'job_type_' ]` 추가할 작업 유형입니다. *job_type* 은 **nvarchar (20)** 이며 기본값은 **capture**입니다. 올바른 입력은 **캡처** 및 **정리**입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 sys.sp_cdc_stop_job을 사용하면 관리자가 캡처 작업이나 정리 작업을 명시적으로 중지할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `AdventureWorks2012` 데이터베이스의 정리 작업을 중지합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_stop_job @job_type = N'capture';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [cdc_jobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sp_cdc_start_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md)  
  
  

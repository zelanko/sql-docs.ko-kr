---
title: sysmail_help_status_sp (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_status_sp
- sysmail_help_status_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_status_sp
ms.assetid: b44277c6-81e8-4b4d-85b3-a2f04d602e7a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fb00e1c2838fad01fd26d54490e1c3c29f63d397
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762652"
---
# <a name="sysmail_help_status_sp-transact-sql"></a>sysmail_help_status_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  데이터베이스 메일 큐의 상태를 표시합니다. **Sysmail_start_sp** 를 사용 하 여 데이터베이스 메일 큐를 시작 하 고 **sysmail_stop_sp** 데이터베이스 메일 큐를 중지 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_help_status_sp  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-set"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**상태**|**nvarchar (7)**|데이터베이스 메일의 상태입니다. 가능한 값은 **시작** 및 **중지**됨입니다.|  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버만이 프로시저에 액세스할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 데이터베이스 메일의 상태를 표시합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_help_status_sp ;  
GO  
```  
  
 결과 집합은 다음과 같습니다.  
  
```  
Status  
-------  
STARTED  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일 외부 프로그램](../../relational-databases/database-mail/database-mail-external-program.md)   
 [Transact-sql&#41;sysmail_start_sp &#40;](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [sysmail_stop_sp&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)  
  
  

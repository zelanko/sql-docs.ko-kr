---
title: sp_msx_get_account (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_get_account_TSQL
- sp_msx_get_account
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_get_account
ms.assetid: 7b478049-e2d0-4bac-865a-b97fd1d8dfbc
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3dab15a076200e464e82d0b01ef6a156447a537f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68108041"
---
# <a name="sp_msx_get_account-transact-sql"></a>sp_msx_get_account(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  대상 서버가 마스터 서버에 로그인하는 데 사용하는 자격 증명에 대한 정보를 나열합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_msx_get_account  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 다음 결과 집합을 반환합니다.  
  
|열 이름|Type|Description|  
|-----------------|----------|-----------------|  
|msx_connection|**int**|마스터 서버 연결 번호입니다.|  
|msx_credential_id|**int**|이 마스터 서버 연결에 사용된 자격 증명의 ID입니다.|  
|msx_credential_name|**sysname**|이 마스터 서버 연결에 사용된 자격 증명의 이름입니다.|  
|msx_login_name|**nvarchar(4000)**|자격 증명에 대한 Windows 사용자의 도메인 이름 및 사용자 이름입니다.|  
  
## <a name="remarks"></a>설명  
 이 대상 서버에 대해 지정된 자격 증명이 없으면 빈 결과 집합을 반환합니다. 자격 증명을 설정하려면 sp_msx_set_account를 사용하십시오.  
  
## <a name="permissions"></a>사용 권한  
 sysadmin 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 대상 서버가 마스터 서버에 로그인하는 데 사용하는 자격 증명에 대한 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sp_msx_get_account ;  
GO  
```  
  
 결과 집합 예는 다음과 같습니다.  
  
 `msx_connection msx_credential_id msx_credential_name  msx_login_name`  
  
 `-------------- ----------------- -------------------- ------------------------------`  
  
 `1              65538             MsxAccount           AdventureWorks2012\MsxAccount`  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 SQL Server 에이전트](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [Transact-sql&#41;sp_msx_set_account &#40;](../../relational-databases/system-stored-procedures/sp-msx-set-account-transact-sql.md)  
  
  

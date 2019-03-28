---
title: sp_msx_set_account (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_set_account
- sp_msx_set_account_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_set_account
ms.assetid: 314ec720-3a37-48f7-bb6b-8d5b894bf843
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 16d5c1815e42e419940223b7f25a565e04ab0508
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533255"
---
# <a name="spmsxsetaccount-transact-sql"></a>sp_msx_set_account(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  대상 서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 마스터 서버 계정 이름과 암호를 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_msx_set_account [ @credential_name = ] 'credential_name'  | [ @credential_id = ] credential_id  
```  
  
## <a name="arguments"></a>인수  
`[ @credential_name = ] 'credential_name'` 마스터 서버에 로그인 하는 데 자격 증명의 이름입니다. 제공된 이름은 기존 자격 증명의 이름이어야 합니다. 어느 *credential_name* 하거나 *credential_id* 지정 해야 합니다.  
  
`[ @credential_id = ] credential_id` 마스터 서버에 로그인 하는 데 자격 증명에 대 한 식별자입니다. 식별자는 기존 자격 증명의 식별자여야 합니다. 어느 *credential_name* 하거나 *credential_id* 지정 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 자격 증명을 사용하여 대상 서버가 마스터 서버에 로그인하는 데 사용하는 사용자 이름 및 암호 정보를 저장합니다. 이 프로시저는 이 대상 서버의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 마스터 서버에 로그인하는 데 사용하는 자격 증명을 설정합니다.  
  
 지정된 자격 증명은 기존 자격 증명이어야 합니다. 자격 증명을 만드는 방법에 대 한 자세한 내용은 참조 하세요. [CREATE CREDENTIAL &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 실행 권한은 **sp_msx_set_account** 기본의 멤버에는 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 서버가 `MsxAccount` 자격 증명을 사용하여 마스터 서버에 로그인하도록 설정합니다.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sp_msx_set_account @credential_name = MsxAccount ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_msx_get_account &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-get-account-transact-sql.md)  
  
  

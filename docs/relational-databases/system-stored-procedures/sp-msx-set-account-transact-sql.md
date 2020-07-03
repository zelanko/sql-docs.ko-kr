---
title: sp_msx_set_account (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e9e0e355c033c0ee33dd8c503875d03a163f998b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893454"
---
# <a name="sp_msx_set_account-transact-sql"></a>sp_msx_set_account(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  대상 서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 마스터 서버 계정 이름과 암호를 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_msx_set_account [ @credential_name = ] 'credential_name'  | [ @credential_id = ] credential_id  
```  
  
## <a name="arguments"></a>인수  
`[ @credential_name = ] 'credential_name'`마스터 서버에 로그인 하는 데 사용할 자격 증명의 이름입니다. 제공된 이름은 기존 자격 증명의 이름이어야 합니다. *Credential_name* 또는 *credential_id* 를 지정 해야 합니다.  
  
`[ @credential_id = ] credential_id`마스터 서버에 로그인 하는 데 사용할 자격 증명의 식별자입니다. 식별자는 기존 자격 증명의 식별자여야 합니다. *Credential_name* 또는 *credential_id* 를 지정 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 자격 증명을 사용하여 대상 서버가 마스터 서버에 로그인하는 데 사용하는 사용자 이름 및 암호 정보를 저장합니다. 이 프로시저는 이 대상 서버의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 마스터 서버에 로그인하는 데 사용하는 자격 증명을 설정합니다.  
  
 지정된 자격 증명은 기존 자격 증명이어야 합니다. 자격 증명을 만드는 방법에 대 한 자세한 내용은 [CREATE credential &#40;transact-sql&#41;](../../t-sql/statements/create-credential-transact-sql.md)를 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 Execute 권한은 **sysadmin** 고정 서버 역할의 멤버에 게 기본적으로 **sp_msx_set_account** 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 서버가 `MsxAccount` 자격 증명을 사용하여 마스터 서버에 로그인하도록 설정합니다.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sp_msx_set_account @credential_name = MsxAccount ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 SQL Server 에이전트](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;자격 증명 &#40;만들기](../../t-sql/statements/create-credential-transact-sql.md)   
 [Transact-sql&#41;sp_msx_get_account &#40;](../../relational-databases/system-stored-procedures/sp-msx-get-account-transact-sql.md)  
  
  

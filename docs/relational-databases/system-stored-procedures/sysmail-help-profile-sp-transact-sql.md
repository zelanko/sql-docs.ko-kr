---
title: sysmail_help_profile_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_profile_sp_TSQL
- sysmail_help_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profile_sp
ms.assetid: d7169a8e-92b1-49eb-9124-3b2f69755ddb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3b953f619ab422eba81a925375d9ae8b0cd60e82
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47836461"
---
# <a name="sysmailhelpprofilesp-transact-sql"></a>sysmail_help_profile_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  하나 이상의 메일 프로필에 대한 정보를 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_help_profile_sp  [   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@profile_id** = ] *profile_id*  
 정보를 반환할 프로필 ID입니다. *profile_id* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 정보를 반환할 프로필 이름입니다. *profile_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 다음 열을 포함한 결과 집합을 반환합니다.  
  
||||  
|-|-|-|  
|열 이름|데이터 형식|Description|  
|**profile_id**|**int**|프로필 ID입니다.|  
|**name**|**sysname**|프로필 이름입니다.|  
|**description**|**nvarchar(256)**|프로필에 대한 설명입니다.|  
  
## <a name="remarks"></a>Remarks  
 프로필 이름이 나 프로필 id를 지정 하면 **sysmail_help_profile_sp** 해당 프로필에 대 한 정보를 반환 합니다. 이 고, 그렇지 **sysmail_help_profile_sp** 에서 모든 프로필에 대 한 정보를 반환 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.  
  
 저장된 프로시저 **sysmail_help_profile_sp** 에 **msdb** 데이터베이스 및 소유 하는 **dbo** 스키마입니다. 현재 데이터베이스에는 없는 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다 **msdb**합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저 기본의 멤버에 대 한 권한을 실행 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 **A. 모든 프로필 나열**  
  
 다음 예에서는 인스턴스에 있는 모든 프로필을 나열합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profile_sp;  
```  
  
 다음은 줄 길이에 맞추어 재구성된 결과 집합 예입니다.  
  
```  
profile_id  name                          description  
----------- ----------------------------- ------------------------------  
56          AdventureWorks Administrator  Administrative mail profile.    
57          AdventureWorks Operator       Operator mail profile.          
```  
  
 **B. 특정 프로필 나열**  
  
 다음 예에서는 `AdventureWorks Administrator` 프로필에 대한 정보를 나열합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profile_sp  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
 다음은 줄 길이에 맞추어 재구성된 결과 집합 예입니다.  
  
```  
profile_id  name                          description  
----------- ----------------------------- ------------------------------  
56          AdventureWorks Administrator  Administrative mail profile.    
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

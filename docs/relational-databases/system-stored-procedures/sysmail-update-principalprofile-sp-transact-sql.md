---
title: sysmail_update_principalprofile_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_update_principalprofile_sp
- sysmail_update_principalprofile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_principalprofile_sp
ms.assetid: 9fe96e9a-4758-4e4a-baee-3e1217c4426c
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7539eb785bc0ae03a68b8a734b89012a29590d3d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailupdateprincipalprofilesp-transact-sql"></a>sysmail_update_principalprofile_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  보안 주체와 프로필 간 연결 정보를 업데이트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_update_principalprofile_sp { @principal_id = principal_id | @principal_name = 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    [ @is_default = ] 'is_default'  
```  
  
## <a name="arguments"></a>인수  
 [ **@principal_id** = ] *principal_id*  
 데이터베이스 사용자 또는 역할의 ID는 **msdb** 변경 하려면 연결에 대 한 데이터베이스입니다. *principal_id* 은 **int**, 기본값은 NULL입니다. 어느 *principal_id* 또는 *principal_name* 지정 해야 합니다.  
  
 [ **@principal_name** = ] **'***principal_name***'**  
 데이터베이스 사용자 또는 역할의 이름에서 **msdb** 업데이트할 연결에 대 한 데이터베이스입니다. *principal_name* 은 **sysname**, 기본값은 NULL입니다. 어느 *principal_id* 또는 *principal_name* 지정할 수 있습니다.  
  
 [ **@profile_id** = ] *profile_id*  
 연결을 변경할 프로필의 ID입니다. *profile_id* 은 **int**, 기본값은 NULL입니다. 어느 *profile_id* 또는 *profile_name* 지정 해야 합니다.  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 연결을 변경할 프로필의 이름입니다. *profile_name* 은 **sysname**, 기본값은 NULL입니다. 어느 *profile_id* 또는 *profile_name* 지정 해야 합니다.  
  
 [ **@is_default** = ] **'***is_default***'**  
 이 프로필이 데이터베이스 사용자의 기본 프로필인지 여부입니다. 데이터베이스 사용자는 하나의 기본 프로필만 가질 수 있습니다. *is_default* 은 **비트**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 이 저장 프로시저는 지정된 프로필이 데이터베이스 사용자의 기본 프로필인지 여부를 변경합니다. 데이터베이스 사용자는 기본 개인 프로필을 하나만 가질 수 있습니다.  
  
 연결의 사용자 이름 경우 **공용** 연결에 대 한 보안 주체 id가 또는 **0**,이 저장된 프로시저는 공개 프로필을 변경 합니다. 기본 공개 프로필은 하나만 있을 수 있습니다.  
  
 때  **@is_default**  은 '**1**'에서 주 서버를 둘 이상의 프로필에 연결 하 고, 지정한 프로필이 보안 주체의 기본 프로필이 됩니다. 이전에 기본 프로필이던 프로필은 보안 주체와 계속 연결되어 있긴 하지만 더 이상 기본 프로필이 아닙니다.  
  
 저장된 프로시저 **sysmail_update_principalprofile_sp** 에 **msdb** 데이터베이스에 있으며가 소유 하 고는 **dbo** 스키마입니다. 현재 데이터베이스 없는 경우 세 부분으로 이루어진 이름으로 프로시저를 실행 해야 **msdb**합니다.  
  
## <a name="permissions"></a>Permissions  
 실행의 구성원에 게이 프로시저 기본값에 대 한 권한을 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 **A. 데이터베이스에 대 한 기본 공개 프로필로 프로필 설정**  
  
 다음 예제에서는 설정 프로필 `General Use Profile` 사용자에 대 한 기본 공개 프로필로 **msdb** 데이터베이스입니다.  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'General Use Profile',  
    @is_default = '1';  
```  
  
 **B. 사용자에 대 한 기본 개인 프로필로 프로필 설정**  
  
 다음 예제에서는 설정 프로필 `AdventureWorks Administrator` 보안 주체의 기본 프로필로 `ApplicationUser` 에 **msdb** 데이터베이스입니다. 프로필은 보안 주체에 이미 연결되어 있어야 합니다. 이전에 기본 프로필이던 프로필은 보안 주체와 계속 연결되어 있긴 하지만 더 이상 기본 프로필이 아닙니다.  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator',  
    @is_default = '1' ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [데이터베이스 메일 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

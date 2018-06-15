---
title: sysmail_help_principalprofile_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_help_principalprofile_sp_TSQL
- sysmail_help_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_principalprofile_sp
ms.assetid: 0cfd6464-09c7-4f03-9d25-58001c096a9e
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca2ad195b8360a8e8963f95df4d0f0c517b907ce
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33259503"
---
# <a name="sysmailhelpprincipalprofilesp-transact-sql"></a>sysmail_help_principalprofile_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일 프로필과 데이터베이스 보안 주체 간 연결에 대한 정보를 나열합니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_help_principalprofile_sp [ {   [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ]  
    [ [ , ] {   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@principal_id=** ] *principal_id*  
 데이터베이스 사용자 또는 역할의 id는 **msdb** 나열할 연결에 대 한 데이터베이스입니다. *principal_id* 은 **int**, 기본값은 NULL입니다. 어느 *principal_id* 또는 *principal_name* 지정할 수 있습니다.  
  
 [ **@principal_name=** ] **'***principal_name***'**  
 데이터베이스 사용자 또는 역할의 이름인는 **msdb** 나열할 연결에 대 한 데이터베이스입니다. *principal_name* 은 **sysname**, 기본값은 NULL입니다. 어느 *principal_id* 또는 *principal_name* 지정할 수 있습니다.  
  
 [ **@profile_id=** ] *profile_id*  
 나열할 연결에 대한 프로필의 ID입니다. *profile_id* 은 **int**, 기본값은 NULL입니다. 어느 *profile_id* 또는 *profile_name* 지정할 수 있습니다.  
  
 [ **@profile_name=** ] **'***profile_name***'**  
 나열할 연결에 대한 프로필의 이름입니다. *profile_name* 은 **sysname**, 기본값은 NULL입니다. 어느 *profile_id* 또는 *profile_name* 지정할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 다음 표에 나열된 열이 포함된 결과 집합을 반환합니다.  
  
||||  
|-|-|-|  
|열 이름|데이터 형식|Description|  
|**principal_id**|**int**|데이터베이스 사용자의 ID입니다.|  
|**principal_name**|**sysname**|데이터베이스 사용자의 이름입니다.|  
|**profile_id**|**int**|데이터베이스 메일 프로필의 ID입니다.|  
|**profile_name**|**sysname**|데이터베이스 메일 프로필의 이름입니다.|  
|**is_default**|**bit**|프로필이 해당 사용자의 기본 프로필인지 여부를 나타내는 플래그입니다.|  
  
## <a name="remarks"></a>주의  
 경우 **sysmail_help_principalprofile_sp** 호출 되는 반환 된 결과 집합 나열 모든 인스턴스의 연결 매개 변수 없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 그렇지 않으면 결과 집합은 제공된 매개 변수와 일치하는 연결에 대한 정보를 포함합니다. 예를 들어 프로필 이름이 제공된 경우 프로시저가 해당 프로필에 대한 모든 연결을 나열합니다.  
  
 **sysmail_help_principalprofile_sp** 에 **msdb** 데이터베이스에 있으며가 소유 하 고는 **dbo** 스키마입니다. 현재 데이터베이스 없는 경우 세 부분으로 이루어진 이름으로 프로시저를 실행 해야 **msdb**합니다.  
  
## <a name="permissions"></a>Permissions  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-information-for-a-specific-association"></a>1. 특정 연결에 대한 정보 나열  
 다음 예에서는 `AdventureWorks Administrator` 데이터베이스에 있는 `ApplicationLogin` 프로필과 `msdb` 보안 주체 간의 모든 연결에 대한 정보 목록을 보여 줍니다.  
  
```  
EXECUTE msdb.dbo.sysmail_help_principalprofile_sp  
    @principal_name = 'danw',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
 다음은 줄 길이에 맞추어 재구성된 결과 집합 예입니다.  
  
```  
principal_id principal_name     profile_id  profile_name                   is_default  
------------ ------------------ ----------- ------------------------------ ----------  
5            danw               9           AdventureWorks Administrator   1  
```  
  
### <a name="b-listing-information-for-all-associations"></a>2. 모든 연결에 대한 정보 나열  
 다음 예에서는 인스턴스의 모든 연결에 대한 정보 목록을 보여 줍니다.  
  
```  
EXECUTE msdb.dbo.sysmail_help_principalprofile_sp ;  
```  
  
 다음은 줄 길이에 맞추어 재구성된 결과 집합 예입니다.  
  
```  
principal_id principal_name     profile_id  profile_name                   is_default  
------------ ------------------ ----------- ------------------------------ ----------  
6            terrid             3           Product Update Profile         1  
5            danw               9           AdventureWorks Administrator   1  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

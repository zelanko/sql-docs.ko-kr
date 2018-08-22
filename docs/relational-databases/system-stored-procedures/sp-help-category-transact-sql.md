---
title: sp_help_category (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_category
- sp_help_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_category
ms.assetid: 8cad1dcc-b43e-43bd-bea0-cb0055c84169
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a84cde301cf3c3db39f8df1999b9e4c39416c324
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392877"
---
# <a name="sphelpcategory-transact-sql"></a>sp_help_category(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 클래스의 작업, 경고 또는 운영자에 관한 정보를 제공합니다.  
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_category [ [ @class = ] 'class' ]   
     [ , [ @type = ] 'type' ]   
     [ , [ @name = ] 'name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>인수  
 [ **@class=**] **'***class***'**  
 정보를 요청한 대상 클래스입니다. *클래스* 됩니다 **varchar(8)**, 기본값은 **작업**합니다. *클래스* 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**JOB**|작업 범주에 관한 정보를 제공합니다.|  
|**경으십시오**|경고 범주에 관한 정보를 제공합니다.|  
|**연산자**|운영자 범주에 관한 정보를 제공합니다.|  
  
 [ **@type=** ] **'***type***'**  
 정보를 요청한 대상 범주의 유형입니다. *형식* 됩니다 **varchar(12)**, 기본값은 NULL 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**LOCAL**|로컬 작업 범주입니다.|  
|**다중-서버**|다중 서버 작업 범주입니다.|  
|**NONE**|이외의 다른 클래스에 대 한 범주 **작업**합니다.|  
  
 [ **@name=** ] **'***name***'**  
 정보를 요청한 대상 범주의 이름입니다. *이름* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [ **@suffix=** ] *suffix*  
 지정 여부는 **category_type** 결과 집합의 열은 ID 또는 이름. *접미사* 됩니다 **비트**, 기본값은 **0**합니다. **1** 표시 된 **category_type** 이름으로 및 **0** ID로 표시  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 때 **@suffix** 됩니다 **0**를 **sp_help_category** 다음 결과 집합을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|범주 ID입니다.|  
|**category_type**|**tinyint**|범주의 유형입니다.<br /><br /> **1** = 로컬<br /><br /> **2** = 다중 서버<br /><br /> **3** = 없음|  
|**name**|**sysname**|범주의 이름입니다.|  
  
 때 **@suffix** 됩니다 **1**를 **sp_help_category** 다음 결과 집합을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|범주 ID입니다.|  
|**category_type**|**sysname**|범주의 유형입니다. 중 하나 **로컬**하십시오 **MULTI-SERVER**, 또는 **NONE**|  
|**name**|**sysname**|범주의 이름입니다.|  
  
## <a name="remarks"></a>Remarks  
 **sp_help_category** 에서 실행 해야 합니다 **msdb** 데이터베이스입니다.  
  
 매개 변수가 지정되지 않은 경우에는 결과 집합이 모든 작업 범주에 관한 정보를 제공합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-local-job-information"></a>1. 로컬 작업 정보 반환  
 다음 예에서는 로컬로 관리되는 작업에 대한 정보를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @type = N'LOCAL' ;  
GO  
```  
  
### <a name="b-returning-alert-information"></a>2. 경고 정보 반환  
 다음 예에서는 복제 경고 범주에 대한 정보를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @class = N'ALERT',  
    @name = N'Replication' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_add_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [sp_delete_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_update_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

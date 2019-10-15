---
title: sp_help_category (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_category
- sp_help_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_category
ms.assetid: 8cad1dcc-b43e-43bd-bea0-cb0055c84169
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1b44f5962e8241afa95b9e68cf75d493dff01ad5
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304809"
---
# <a name="sp_help_category-transact-sql"></a>sp_help_category(Transact-SQL)
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
`[ @class = ] 'class'` 정보를 요청 하는 클래스입니다. *클래스* 는 **varchar (8)** 이며 기본값은 **JOB**입니다. *클래스* 는 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**JOB**|작업 범주에 관한 정보를 제공합니다.|  
|**ALERT**|경고 범주에 관한 정보를 제공합니다.|  
|**연산자**|운영자 범주에 관한 정보를 제공합니다.|  
  
`[ @type = ] 'type'` 정보를 요청 하는 범주의 유형입니다. *type* 은 **varchar (12)** 이며 기본값은 NULL이 고 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**LOCAL**|로컬 작업 범주입니다.|  
|**다중 서버**|다중 서버 작업 범주입니다.|  
|**NONE**|**JOB**이 아닌 다른 클래스에 대 한 범주입니다.|  
  
`[ @name = ] 'name'` 정보를 요청 하는 범주의 이름입니다. *name* 은 **sysname**이며 기본값은 NULL입니다.  
  
`[ @suffix = ] suffix`은 결과 집합의 **category_type** 열이 ID 인지 아니면 이름 인지를 지정 합니다. *접미사* 는 **bit**이며 기본값은 **0**입니다. **1** 은 **category_type** 를 이름으로 표시 하 고 **0** 은 ID로 표시 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 **@No__t-1suffix** 가 **0**이면 **sp_help_category** 는 다음 결과 집합을 반환 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|범주 ID입니다.|  
|**category_type**|**tinyint**|범주의 유형입니다.<br /><br /> **1** = 로컬<br /><br /> **2** = 다중 서버<br /><br /> **3** = 없음|  
|**name**|**sysname**|범주의 이름입니다.|  
  
 **@No__t-1suffix** 가 **1**이면 **sp_help_category** 는 다음 결과 집합을 반환 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|범주 ID입니다.|  
|**category_type**|**sysname**|범주의 유형입니다. **로컬**, **다중 서버**또는 **없음** 중 하나|  
|**name**|**sysname**|범주의 이름입니다.|  
  
## <a name="remarks"></a>설명  
 **sp_help_category** 는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
 매개 변수가 지정되지 않은 경우에는 결과 집합이 모든 작업 범주에 관한 정보를 제공합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-local-job-information"></a>A. 로컬 작업 정보 반환  
 다음 예에서는 로컬로 관리되는 작업에 대한 정보를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @type = N'LOCAL' ;  
GO  
```  
  
### <a name="b-returning-alert-information"></a>2\. 경고 정보 반환  
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
 [sp_add_category &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [sp_delete_category &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_update_category &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

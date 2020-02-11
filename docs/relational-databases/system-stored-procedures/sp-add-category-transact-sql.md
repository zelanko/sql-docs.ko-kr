---
title: sp_add_category (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_category
- sp_add_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_category
ms.assetid: 6cca32cd-d941-4378-aed6-a7c90cb7520a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 076d5ade1f4951183578b1b46761d49dafbce8be
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70810547"
---
# <a name="sp_add_category-transact-sql"></a>sp_add_category(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  작업, 경고 또는 운영자의 지정된 범주를 서버에 추가합니다. 대체 방법은 [SQL Server Management Studio를 사용 하 여 작업 범주 만들기](/sql/ssms/agent/create-a-job-category)를 참조 하세요.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
 > [!IMPORTANT]  
 > 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_category   
     [ [ @class = ] 'class', ]   
     [ [ @type = ] 'type', ]   
     { [ @name = ] 'name' }  
```  
  
## <a name="arguments"></a>인수  
`[ @class = ] 'class'`추가할 범주의 클래스입니다. *클래스* 는 기본값은 JOB이 고 다음 값 중 하나일 수 있는 **varchar (8)** 입니다.  
  
|값|Description|  
|-----------|-----------------|  
|JOB|작업 범주를 추가합니다.|  
|ALERT|경고 범주를 추가합니다.|  
|OPERATOR|운영자 범주를 추가합니다.|  
  
`[ @type = ] 'type'`추가할 범주의 유형입니다. *type* 은 **varchar (12)** 이며 기본값은 **LOCAL**이 고 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|LOCAL|로컬 작업 범주|  
|다중 서버|다중 서버 작업 범주|  
|없음|JOB이 아닌 다른 클래스에 대 한 범주입니다 **.**|  
  
`[ @name = ] 'name'`추가할 범주의 이름입니다. 이름은 지정한 클래스 내에서 고유해야 합니다. *name* 은 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **sp_add_category** 는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_add_category**를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdminJobs`라는 로컬 작업 범주를 만듭니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_category  
    @class=N'JOB',  
    @type=N'LOCAL',  
    @name=N'AdminJobs' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_delete_category &#40;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [Transact-sql&#41;sp_help_category &#40;](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [Transact-sql&#41;sp_update_category &#40;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [sysjobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)   
 [&#40;Transact-sql&#41;의 dbo. sysjobservers](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

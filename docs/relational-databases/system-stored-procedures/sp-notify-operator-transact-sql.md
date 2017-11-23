---
title: sp_notify_operator (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_notify_operator_TSQL
- sp_notify_operator
dev_langs: TSQL
helpviewer_keywords: sp_notify_operator
ms.assetid: c440f5c9-9884-4196-b07c-55d87afb17c3
caps.latest.revision: "43"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2ff7b50b5eef5d5ff753039bf4dd7ab501160eda
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="spnotifyoperator-transact-sql"></a>sp_notify_operator(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일을 사용하여 운영자에게 전자 메일 메시지를 보냅니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_notify_operator  
    [ @profile_name = ] 'profilename' ,  
    [ @id = ] id ,  
    [ @name = ] 'name' ,  
    [ @subject = ] 'subject' ,  
    [ @body = ] 'message' ,  
    [ @file_attachments = ] 'attachment'  
    [ @mail_database = ] 'mail_host_database'  
```  
  
## <a name="arguments"></a>인수  
 [  **@profile_name=** ] **'***profilename***'**  
 메시지를 보내는 데 사용할 데이터베이스 메일 프로필의 이름입니다. *profilename* 은 **nvarchar (128)**합니다. 경우 *profilename* 를 지정 하지 않으면 기본 데이터베이스 메일 프로필이 사용 됩니다.  
  
 [  **@id=** ] *id*  
 메시지를 받을 운영자의 식별자입니다. *id* 은 **int**, 기본값은 NULL입니다. 중 하나 *id* 또는 *이름* 지정 해야 합니다.  
  
 [  **@name=** ] **'***이름***'**  
 메시지를 받을 운영자의 이름입니다. *이름* 은 **nvarchar (128)**, 기본값은 NULL입니다. 중 하나 *id* 또는 *이름* 지정 해야 합니다.  
  
> **참고:** 메시지를 보내기 전에 운영자에 대 한 전자 메일 주소를 정의 해야 합니다.  
  
 [  **@subject=** ] **'***주체***'**  
 전자 메일 메시지의 제목입니다. *제목* 은 **nvarchar (256)** 이며 기본값은 없습니다.  
  
 [  **@body=** ] **'***메시지***'**  
 전자 메일 메시지의 본문입니다. *메시지* 은 **nvarchar (max)** 이며 기본값은 없습니다.  
  
 [  **@file_attachments=** ] **'***첨부***'**  
 전자 메일 메시지에 첨부할 파일의 이름입니다. *첨부 파일* 은 **nvarchar (512)**, 기본값은 없습니다.  
  
 [  **@mail_database=** ] **'***mail_host_database***'**  
 메일 호스트 데이터베이스의 이름을 지정합니다. *mail_host_database* 은 **nvarchar (128)**합니다. 없는 경우 *mail_host_database* 지정는 **msdb** 데이터베이스는 기본적으로 사용 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 지정한 메시지를 지정된 운영자의 전자 메일 주소로 보냅니다. 운영자의 전자 메일 주소가 설정되지 않은 경우 오류를 반환합니다.  
  
 데이터베이스 메일과 메일 호스트 데이터베이스는 운영자에게 알림을 보내기 전에 구성해야 합니다.  
  
## <a name="permissions"></a>Permissions  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 `François Ajenstat` 데이터베이스 메일 프로필을 사용하여 운영자 `AdventureWorks Administrator`에게 알림 전자 메일을 보냅니다. 전자 메일의 제목은 `Test Notification`입니다. 전자 메일 메시지에는 "This is a test of notification via e-mail."이라는 문장이 포함되어 있습니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_notify_operator  
   @profile_name = N'AdventureWorks Administrator',  
   @name = N'François Ajenstat',  
   @subject = N'Test Notification',  
   @body = N'This is a test of notification via e-mail.' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 에이전트 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_operator &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_help_operator &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_delete_operator &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)  
  
  

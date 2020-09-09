---
description: sp_audit_write(Transact-SQL)
title: sp_audit_write (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_audit_write
- sp_audit_write_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_audit_write
ms.assetid: 4c523848-1ce6-49ad-92b3-e0e90f24f1c2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 56795d7ed3da83dff9f50d70f639300dae0da3a1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536718"
---
# <a name="sp_audit_write-transact-sql"></a>sp_audit_write(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **USER_DEFINED_AUDIT_GROUP**에 사용자 정의 감사 이벤트를 추가 합니다. **USER_DEFINED_AUDIT_GROUP** 을 사용 하지 않는 경우 **sp_audit_write** 무시 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_audit_write [ @user_defined_event_id = ] user_defined_event_id
    [ , [ @succeeded = ] succeeded ]
    [ , [ @user_defined_information = ] 'user_defined_information' ]
    [ ; ]
```  
  
## <a name="arguments"></a>인수  
 `[ @user_defined_event_id = ] user_defined_event_id`  
 사용자가 정의 하 고 감사 로그의 **user_defined_event_id** 열에 기록 되는 매개 변수입니다. * \@ user_defined_event_id* 은 **smallint**유형입니다.  
  
 `[ @succeeded = ] succeeded`  
 이벤트 성공 여부를 표시하기 위해 사용자가 전달하는 매개 변수입니다. 이 매개 변수는 감사 로그의 succeeded 열에 표시됩니다. `@succeeded` 는 **bit**입니다.  
  
 `[ @user_defined_information = ] 'user_defined_information'`  
 사용자가 정의하며 감사 로그의 새 user_defined_event_id 열에 기록되는 텍스트입니다. `@user_defined_information` 는 **nvarchar (4000)** 입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
 입력 매개 변수가 잘못되었거나 대상 감사 로그에 쓸 수 없는 경우 실패가 반환됩니다.  
  
## <a name="remarks"></a>설명  
 서버 감사 사양 또는 데이터베이스 감사 사양에 **USER_DEFINED_AUDIT_GROUP** 추가 되 면 **sp_audit_write** 에 의해 트리거되는 이벤트가 감사 로그에 포함 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Public** 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-creating-a-user-defined-audit-event-with-informational-text"></a>A. 정보 텍스트를 포함하여 사용자 정의 감사 이벤트 만들기  
 다음 예에서는 ID가 27인 감사 이벤트, succeeded 값 0, 그리고 선택적으로 포함되는 정보 텍스트를 작성합니다.  
  
```  
EXEC sp_audit_write @user_defined_event_id =  27 ,   
              @succeeded =  0   
            , @user_defined_information = N'Access to a monitored object.' ;  
```  
  
### <a name="b--creating-a-user-defined-audit-event-without-informational-text"></a>B.  정보 텍스트 없이 사용자 정의 감사 이벤트 만들기  
 다음 예에서는 ID가 27인 감사 이벤트와 succeeded 값 0을 작성하되 선택적 정보 텍스트 또는 매개 변수 이름은 포함하지 않습니다.  
  
```  
EXEC sp_audit_write 27, 0;  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_addrole&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_grantdbaccess&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_grantlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

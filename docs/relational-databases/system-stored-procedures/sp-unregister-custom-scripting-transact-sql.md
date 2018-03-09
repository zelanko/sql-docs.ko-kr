---
title: sp_unregister_custom_scripting (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_unregister_custom_scripting_TSQL
- sp_unregister_custom_scripting
helpviewer_keywords: sp_unregister_custom_scripting
ms.assetid: b6e9e0d2-9144-434d-88af-4874f2582399
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fce6b2d16e732b76519cb0fbf66a16ca5db6928f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spunregistercustomscripting-transact-sql"></a>sp_unregister_custom_scripting(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 저장된 프로시저는 사용자 정의 사용자 지정 저장된 프로시저를 제거 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일을 실행 하 여 등록 된 [sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_unregister_custom_scripting [ @type  = ] 'type'  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@type**  =] **'***형식***'**  
 제거되는 사용자 지정 저장 프로시저 또는 스크립트의 유형입니다. *형식* 은 **varchar (16)**이며 기본값은 없고 수는 다음 값 중 하나 여야 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**삽입**|INSERT 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저 또는 스크립트입니다.|  
|**업데이트**|UPDATE 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저 또는 스크립트입니다.|  
|**삭제**|DELETE 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저 또는 스크립트입니다.|  
|**custom_script**|DDL(데이터 정의 언어) 트리거 끝에서 실행되는 등록된 사용자 지정 저장 프로시저 또는 스크립트입니다.|  
  
 [  **@publication**  =] **'***게시***'**  
 사용자 지정 저장 프로시저 또는 스크립트가 제거되는 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@article**  =] **'***문서***'**  
 사용자 지정 저장 프로시저 또는 스크립트가 제거되는 아티클의 이름입니다. *문서* 은 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_unregister_custom_scripting** 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정 서버 역할의 **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_ unregister_custom_scripting**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_register_custom_scripting &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  

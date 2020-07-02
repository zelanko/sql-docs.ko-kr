---
title: sp_unregister_custom_scripting (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_unregister_custom_scripting_TSQL
- sp_unregister_custom_scripting
helpviewer_keywords:
- sp_unregister_custom_scripting
ms.assetid: b6e9e0d2-9144-434d-88af-4874f2582399
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5c638c37da5907295cf4f8ef0dbb63d7eef17f05
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762771"
---
# <a name="sp_unregister_custom_scripting-transact-sql"></a>sp_unregister_custom_scripting(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  이 저장 프로시저는 [!INCLUDE[tsql](../../includes/tsql-md.md)] [sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)를 실행 하 여 등록 된 사용자 정의 사용자 지정 저장 프로시저 또는 스크립트 파일을 제거 합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_unregister_custom_scripting [ @type  = ] 'type'  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @type = ] 'type'`제거할 사용자 지정 저장 프로시저 또는 스크립트의 유형입니다. *type* 은 **varchar (16)** 이며 기본값은 없고 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**넣거나**|INSERT 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저 또는 스크립트입니다.|  
|**update**|UPDATE 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저 또는 스크립트입니다.|  
|**delete**|DELETE 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저 또는 스크립트입니다.|  
|**custom_script**|DDL(데이터 정의 언어) 트리거 끝에서 실행되는 등록된 사용자 지정 저장 프로시저 또는 스크립트입니다.|  
  
`[ @publication = ] 'publication'`사용자 지정 저장 프로시저 또는 스크립트가 제거 되는 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @article = ] 'article'`사용자 지정 저장 프로시저 또는 스크립트가 제거 되는 아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_unregister_custom_scripting** 는 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할, **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버만이 **sp_unregister_custom_scripting**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_register_custom_scripting &#40;](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  

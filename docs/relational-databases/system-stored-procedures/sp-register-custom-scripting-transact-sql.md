---
description: sp_register_custom_scripting(Transact-SQL)
title: sp_register_custom_scripting (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_register_custom_scripting
- sp_register_custom_scripting_TSQL
helpviewer_keywords:
- sp_register_custom_scripting
ms.assetid: a8159282-de3b-4b9e-bdc9-3d3fce485c7f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4f73353cc5d2e0e9be02be5a0e6dc59eaf2f909f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547511"
---
# <a name="sp_register_custom_scripting-transact-sql"></a>sp_register_custom_scripting(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  복제를 사용하면 트랜잭션 복제에서 사용되는 하나 이상의 기본 프로시저를 사용자 정의 사용자 지정 저장 프로시저로 바꿀 수 있습니다. 이러한 저장 프로시저는 복제된 테이블에서 스키마 변경이 발생하면 다시 생성됩니다. **sp_register_custom_scripting** [!INCLUDE[tsql](../../includes/tsql-md.md)] 새 사용자 정의 사용자 지정 저장 프로시저에 대 한 정의를 스크립팅 하기 위해 스키마 변경이 발생할 때 실행 되는 저장 프로시저 또는 스크립트 파일을 sp_register_custom_scripting 등록 합니다. 새 사용자 정의 사용자 지정 저장 프로시저는 테이블에 대한 새 스키마를 반영해야 합니다. **sp_register_custom_scripting** 는 게시 데이터베이스의 게시자에서 실행 되 고 스키마 변경이 발생할 때 등록 된 스크립트 파일 또는 저장 프로시저가 구독자에서 실행 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @type = ] 'type'` 등록 중인 사용자 지정 저장 프로시저 또는 스크립트의 유형입니다. *type* 은 **varchar (16)** 이며 기본값은 없고 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**insert**|INSERT 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저입니다.|  
|**update**|UPDATE 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저입니다.|  
|**delete**|DELETE 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저입니다.|  
|**custom_script**|DDL(데이터 정의 언어) 트리거의 끝에 실행되는 스크립트입니다.|  
  
`[ @value = ] 'value'` 등록 되는 스크립트 파일의 저장 프로시저 또는 이름 및 정규화 된 경로 이름입니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] . *value* 는 **nvarchar (1024)** 이며 기본값은 없습니다.  
  
> [!NOTE]  
>  *Value*매개 변수에 NULL을 지정 하면 이전에 등록 된 스크립트의 등록이 취소 됩니다 .이 스크립트는 [sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)실행과 동일 합니다.  
  
 *Type* 값이 **custom_script**되 면 스크립트 파일의 이름 및 전체 경로가 [!INCLUDE[tsql](../../includes/tsql-md.md)] 필요 합니다. 그렇지 않은 경우 *값* 은 등록 된 저장 프로시저의 이름 이어야 합니다.  
  
`[ @publication = ] 'publication'` 사용자 지정 저장 프로시저 또는 스크립트가 등록 되는 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 **NULL**입니다.  
  
`[ @article = ] 'article'` 사용자 지정 저장 프로시저 또는 스크립트가 등록 되는 아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 **NULL**입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_register_custom_scripting** 는 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
 이 저장 프로시저는 복제된 테이블에서 스키마 변경이 발생하기 전에 실행해야 합니다. 이 저장 프로시저를 사용 하는 방법에 대 한 자세한 내용은 [스키마 변경 내용을 반영 하기 위해 사용자 지정 트랜잭션 프로시저 다시 생성](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)을 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할, **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버만이 **sp_register_custom_scripting**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_unregister_custom_scripting &#40;](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  

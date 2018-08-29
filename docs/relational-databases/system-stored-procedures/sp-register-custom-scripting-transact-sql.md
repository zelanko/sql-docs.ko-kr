---
title: sp_register_custom_scripting (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_register_custom_scripting
- sp_register_custom_scripting_TSQL
helpviewer_keywords:
- sp_register_custom_scripting
ms.assetid: a8159282-de3b-4b9e-bdc9-3d3fce485c7f
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 738139cae553dff72dc04b8761b578da692482a4
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036886"
---
# <a name="spregistercustomscripting-transact-sql"></a>sp_register_custom_scripting(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  복제를 사용하면 트랜잭션 복제에서 사용되는 하나 이상의 기본 프로시저를 사용자 정의 사용자 지정 저장 프로시저로 바꿀 수 있습니다. 이러한 저장 프로시저는 복제된 테이블에서 스키마 변경이 발생하면 다시 생성됩니다. **sp_register_custom_scripting** 저장된 프로시저를 등록 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 새 사용자 정의 사용자 지정 저장된 프로시저의 정의 스크립팅 하는 스키마 변경이 발생할 때 실행 되는 스크립트 파일입니다. 새 사용자 정의 사용자 지정 저장 프로시저는 테이블에 대한 새 스키마를 반영해야 합니다. **sp_register_custom_scripting** 게시 데이터베이스의 게시자에서 실행 되 고 스키마 변경이 발생할 때 등록 된 스크립트 파일 또는 저장된 프로시저를 구독자에서 실행 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@type** =] **'***형식***'**  
 등록되는 사용자 지정 저장 프로시저 또는 스크립트의 유형입니다. *형식* 됩니다 **varchar(16)** 이며 기본값은 없고 수 있습니다 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**insert**|INSERT 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저입니다.|  
|**업데이트**|UPDATE 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저입니다.|  
|**delete**|DELETE 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저입니다.|  
|**custom_script**|DDL(데이터 정의 언어) 트리거의 끝에 실행되는 스크립트입니다.|  
  
 [ **@value**=] **'***값***'**  
 등록되는 저장 프로시저의 이름 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일의 이름과 정규화된 경로입니다. *값* 됩니다 **nvarchar(1024)**, 기본값은 없습니다.  
  
> [!NOTE]  
>  NULL을 지정 *값*매개 변수는 이전에 등록 된 스크립트를 실행 하는 것은 등록이 취소 됩니다 [sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)합니다.  
  
 때 값 *형식* 됩니다 **custom_script**를의 전체 경로 이름을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일이 합니다. 그렇지 않으면 *값* 등록 된 저장된 프로시저의 이름 이어야 합니다.  
  
 [ **@publication**=] **'***게시***'**  
 사용자 지정 저장 프로시저 또는 스크립트가 등록되는 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 **NULL**합니다.  
  
 [ **@article**=] **'***문서***'**  
 사용자 지정 저장 프로시저 또는 스크립트가 등록되는 아티클의 이름입니다. *문서* 됩니다 **sysname**, 기본값은 **NULL**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_register_custom_scripting** 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
 이 저장 프로시저는 복제된 테이블에서 스키마 변경이 발생하기 전에 실행해야 합니다. 이 저장된 프로시저를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [다시 생성 사용자 지정 트랜잭션 프로시저 스키마 변경 반영을](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)입니다.  
  
## <a name="permissions"></a>사용 권한  
 구성원만 합니다 **sysadmin** 고정 서버 역할을 **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_ register_custom_scripting**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_unregister_custom_scripting &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  

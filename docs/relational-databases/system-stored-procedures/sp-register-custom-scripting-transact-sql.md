---
title: sp_register_custom_scripting (Transact SQL) | Microsoft Docs
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
- sp_register_custom_scripting
- sp_register_custom_scripting_TSQL
helpviewer_keywords: sp_register_custom_scripting
ms.assetid: a8159282-de3b-4b9e-bdc9-3d3fce485c7f
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16274b71d1ce14b2a143e5d6ce723bcb64cbaebd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spregistercustomscripting-transact-sql"></a>sp_register_custom_scripting(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  복제를 사용하면 트랜잭션 복제에서 사용되는 하나 이상의 기본 프로시저를 사용자 정의 사용자 지정 저장 프로시저로 바꿀 수 있습니다. 이러한 저장 프로시저는 복제된 테이블에서 스키마 변경이 발생하면 다시 생성됩니다. **sp_register_custom_scripting** 저장된 프로시저를 등록 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 는 새 사용자 정의 사용자 지정 저장된 프로시저에 대 한 정의 스크립팅 하는 스키마 변경이 발생할 때 실행 되는 스크립트 파일입니다. 새 사용자 정의 사용자 지정 저장 프로시저는 테이블에 대한 새 스키마를 반영해야 합니다. **sp_register_custom_scripting** 게시 데이터베이스의 게시자에서 실행 되는 스키마 변경이 발생할 때 등록 된 스크립트 파일 또는 저장된 프로시저는 구독자에서 실행 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@type**  =] **'***형식***'**  
 등록되는 사용자 지정 저장 프로시저 또는 스크립트의 유형입니다. *형식* 은 **varchar (16)**이며 기본값은 없고 수는 다음 값 중 하나 여야 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**삽입**|INSERT 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저입니다.|  
|**업데이트**|UPDATE 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저입니다.|  
|**삭제**|DELETE 문이 복제될 때 실행되는 등록된 사용자 지정 저장 프로시저입니다.|  
|**custom_script**|DDL(데이터 정의 언어) 트리거의 끝에 실행되는 스크립트입니다.|  
  
 [  **@value** =] **'***값***'**  
 등록되는 저장 프로시저의 이름 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일의 이름과 정규화된 경로입니다. *값* 은 **nvarchar (1024)**, 기본값은 없습니다.  
  
> [!NOTE]  
>  NULL을 지정 하면 *값*매개 변수는 등록을 취소는 이전에 등록 된 스크립트는 실행 중으로 동일한 [sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)합니다.  
  
 때의 값 *형식* 은 **custom_script**, 이름 및의 전체 경로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일이 있어야 합니다. 그렇지 않으면 *값* 등록 된 저장된 프로시저의 이름 이어야 합니다.  
  
 [  **@publication** =] **'***게시***'**  
 사용자 지정 저장 프로시저 또는 스크립트가 등록되는 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 **NULL**합니다.  
  
 [  **@article** =] **'***문서***'**  
 사용자 지정 저장 프로시저 또는 스크립트가 등록되는 아티클의 이름입니다. *문서* 은 **sysname**, 기본값은 **NULL**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_register_custom_scripting** 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
 이 저장 프로시저는 복제된 테이블에서 스키마 변경이 발생하기 전에 실행해야 합니다. 이 저장된 프로시저를 사용 하는 방법에 대 한 자세한 내용은 참조 [다시 생성 사용자 지정 트랜잭션 프로시저 스키마 변경 내용을 반영 하려면](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정 서버 역할의 **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_ register_custom_scripting**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_unregister_custom_scripting &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  

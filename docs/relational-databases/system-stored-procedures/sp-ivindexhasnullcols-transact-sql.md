---
title: sp_ivindexhasnullcols (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_ivindexhasnullcols
- sp_ivindexhasnullcols_TSQL
helpviewer_keywords:
- sp_ivindexhasnullcols
ms.assetid: ed2cde63-37e1-43cf-b6ba-3b6114a0f797
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 77a0e3f1795545e553347ae699e719af2ad506b4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62959641"
---
# <a name="spivindexhasnullcols-transact-sql"></a>sp_ivindexhasnullcols(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  인덱싱된 뷰의 클러스터형 인덱스가 고유하며 인덱싱된 뷰를 사용하여 트랜잭션 게시를 만들려는 경우 Null이 될 수 있는 열을 포함하고 있지 않은지 확인합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_ivindexhasnullcols [ @viewname = ] 'view_name'  
        , [ @fhasnullcols= ] field_has_null_columns OUTPUT  
```  
  
## <a name="arguments"></a>인수  
`[ @viewname = ] 'view_name'` 확인할 뷰의 이름이입니다. *view_name* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @fhasnullcols = ] field_has_null_columns OUTPUT` 뷰 인덱스에 NULL을 허용 하는 열에 있는지 여부를 나타내는 플래그입니다. *view_name* 됩니다 **sysname**, 기본값은 없습니다. 값을 반환 **1** 뷰 인덱스에는 열이 NULL을 허용 하는 경우. 값을 반환 **0** 보기에 NULL을 허용 하는 열이 없는 경우.  
  
> [!NOTE]  
>  저장된 프로시저 자체가 반환 코드를 반환 하는 경우 **1**오류가 있었습니다 즉 저장된 프로시저 실행,이 값은 **0** 무시 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_ivindexhasnullcols** 트랜잭션 복제에 사용 됩니다.  
  
 기본적으로 게시에 있는 인덱싱된 뷰 아티클은 구독자에서 테이블로 만들어집니다. 단, 인덱싱된 열에서 NULL 값을 허용하는 경우 인덱싱된 뷰는 구독자에서 테이블 대신 인덱싱된 뷰로 만들어집니다. 이 저장 프로시저를 실행하면 현재 인덱싱된 뷰에 이 문제가 있는지 여부를 사용자에게 경고할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_ivindexhasnullcols**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

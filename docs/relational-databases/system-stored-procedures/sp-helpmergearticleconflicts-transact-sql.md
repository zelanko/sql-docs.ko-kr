---
title: sp_helpmergearticleconflicts (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- sp_helpmergearticleconflicts
- sp_helpmergearticleconflicts_TSQL
helpviewer_keywords: sp_helpmergearticleconflicts
ms.assetid: 4678a2b9-9a5f-4193-a20d-2e11fc896c3a
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b7a1d10d6d2ba731ceaaaba51b8f786b262a2e28
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpmergearticleconflicts-transact-sql"></a>sp_helpmergearticleconflicts(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  충돌이 있는 게시 내의 아티클을 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자 또는 병합 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpmergearticleconflicts [ [ @publication = ] 'publication' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publsher_db' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication=**] **'***게시***'**  
 병합 게시의 이름이입니다. *게시* 은 **sysname**, 기본값은  **%** , 충돌이 있는 데이터베이스의 모든 아티클을 반환 하는 합니다.  
  
 [  **@publisher=**] **'***게시자***'**  
 게시자의 이름이입니다. *게시자* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 게시자 데이터베이스의 이름이입니다. *publisher_db* 은 **sysname**, 기본값은 NULL입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**문서**|**sysname**|아티클의 이름입니다.|  
|**source_owner**|**sysname**|원본 개체 소유자의 이름입니다.|  
|**source_object**|**nvarchar (386)**|원본 개체의 이름입니다.|  
|**conflict_table**|**nvarchar (258)**|삽입 또는 업데이트 충돌을 저장하고 있는 테이블의 이름입니다.|  
|**guidcolname**|**sysname**|원본 개체에 대한 RowGuidCol의 이름입니다.|  
|**centralized_conflicts**|**int**|충돌 레코드가 지정된 게시자에 저장되는지를 나타냅니다.|  
  
 문서에만 삭제 충돌 및 아니요 **conflict_table** 행의 이름에서 **conflict_table** 결과 집합은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_helpmergearticleconflicts** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 및 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_helpmergearticleconflicts**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

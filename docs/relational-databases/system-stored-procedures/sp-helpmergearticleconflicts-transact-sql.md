---
title: sp_helpmergearticleconflicts (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticleconflicts
- sp_helpmergearticleconflicts_TSQL
helpviewer_keywords:
- sp_helpmergearticleconflicts
ms.assetid: 4678a2b9-9a5f-4193-a20d-2e11fc896c3a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 47a49e5d2c6faad6be65bc93b0151b6ab8d85fc6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759251"
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
 [ **@publication=**] **'***publication***'**  
 병합 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 **%**, 충돌이 있는 데이터베이스의 모든 문서를 반환 하는 합니다.  
  
 [ **@publisher=**] **'***publisher***'**  
 게시자의 이름이입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 게시자 데이터베이스의 이름이입니다. *publisher_db* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**article**|**sysname**|아티클의 이름입니다.|  
|**source_owner**|**sysname**|원본 개체 소유자의 이름입니다.|  
|**source_object**|**nvarchar(386)**|원본 개체의 이름입니다.|  
|**conflict_table**|**nvarchar(258)**|삽입 또는 업데이트 충돌을 저장하고 있는 테이블의 이름입니다.|  
|**guidcolname**|**sysname**|원본 개체에 대한 RowGuidCol의 이름입니다.|  
|**centralized_conflicts**|**int**|충돌 레코드가 지정된 게시자에 저장되는지를 나타냅니다.|  
  
 아티클에 삭제 충돌만 있고 아니요 있으면 **conflict_table** 개 행의 이름을 합니다 **conflict_table** 결과 집합의 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpmergearticleconflicts** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 및 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_helpmergearticleconflicts**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

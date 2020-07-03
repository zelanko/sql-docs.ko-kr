---
title: sp_helpmergearticleconflicts (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticleconflicts
- sp_helpmergearticleconflicts_TSQL
helpviewer_keywords:
- sp_helpmergearticleconflicts
ms.assetid: 4678a2b9-9a5f-4193-a20d-2e11fc896c3a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 776f46d1f2e61c0f866352ee9c373e4619a2e282
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893558"
---
# <a name="sp_helpmergearticleconflicts-transact-sql"></a>sp_helpmergearticleconflicts(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  충돌이 있는 게시 내의 아티클을 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자 또는 병합 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpmergearticleconflicts [ [ @publication = ] 'publication' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publsher_db' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`병합 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 **%** 충돌 하는 데이터베이스의 모든 아티클을 반환 하는입니다.  
  
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시자 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**문서**|**sysname**|아티클의 이름입니다.|  
|**source_owner**|**sysname**|원본 개체 소유자의 이름입니다.|  
|**source_object**|**nvarchar (386)**|원본 개체의 이름입니다.|  
|**conflict_table**|**nvarchar(258)**|삽입 또는 업데이트 충돌을 저장하고 있는 테이블의 이름입니다.|  
|**guidcolname**|**sysname**|원본 개체에 대한 RowGuidCol의 이름입니다.|  
|**centralized_conflicts**|**int**|충돌 레코드가 지정된 게시자에 저장되는지를 나타냅니다.|  
  
 아티클에 삭제 충돌만 있고 **conflict_table** 행이 없는 경우 결과 집합의 **conflict_table** 이름이 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helpmergearticleconflicts** 는 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 및 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_helpmergearticleconflicts**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

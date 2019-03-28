---
title: sp_replsetoriginator (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replsetoriginator
- sp_replsetoriginator_TSQL
helpviewer_keywords:
- sp_replsetoriginator
ms.assetid: 030e5226-0585-439f-b8cd-36f48367d86d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0f72558a573e0cee0ab7fb2ab9b762246964a884
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526185"
---
# <a name="spreplsetoriginator-transact-sql"></a>sp_replsetoriginator(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  양방향 트랜잭션 복제에서 루프백 검색 및 핸들링을 호출하는 데 사용합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replsetoriginator [ @server_name= ] 'server_name'   
    , [ @database_name= ] 'database_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @server_name = ] 'server_name'` 트랜잭션이 적용 되는 서버의 이름이입니다. *originating_server* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @database_name = ] 'database_name'` 트랜잭션이 적용 되는 데이터베이스의 이름이입니다. *originating_db* 됩니다 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_replsetoriginator** 복제에 의해 적용 되는 트랜잭션의 원본을 기록 하기 배포 에이전트가 실행 됩니다. 이 정보는 루프백 특성이 설정된 양방향 트랜잭션 구독에 대한 루프백 검색을 호출하기 위해 사용합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할의 멤버는 게시자는 **db_owner** 게시 데이터베이스 또는 사용자에 게 게시 액세스 목록 (PAL) 고정된 데이터베이스 역할 를실행할수있습니다**sp_replsetoriginator**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

---
title: sp_replsetoriginator (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1811a523e23de9726517bfabd1ddf8417aa3c5fc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85626741"
---
# <a name="sp_replsetoriginator-transact-sql"></a>sp_replsetoriginator(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  양방향 트랜잭션 복제에서 루프백 검색 및 핸들링을 호출하는 데 사용합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replsetoriginator [ @server_name= ] 'server_name'   
    , [ @database_name= ] 'database_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @server_name = ] 'server_name'`트랜잭션이 적용 되는 서버의 이름입니다. *originating_server* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @database_name = ] 'database_name'`트랜잭션이 적용 되는 데이터베이스의 이름입니다. *originating_db* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 배포 에이전트에서 **sp_replsetoriginator** 를 실행 하 여 복제에 의해 적용 되는 트랜잭션의 원본을 기록 합니다. 이 정보는 루프백 특성이 설정된 양방향 트랜잭션 구독에 대한 루프백 검색을 호출하기 위해 사용합니다.  
  
## <a name="permissions"></a>사용 권한  
 게시자에서 **sysadmin** 고정 서버 역할의 멤버, 게시 데이터베이스에 대 한 **db_owner** 고정 데이터베이스 역할의 멤버 또는 PAL (게시 액세스 목록)의 사용자만 **sp_replsetoriginator**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

---
description: sp_replshowcmds(Transact-SQL)
title: sp_replshowcmds (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replshowcmds
- sp_replshowcmds_TSQL
helpviewer_keywords:
- sp_replshowcmds
ms.assetid: 199f5a74-e08e-4d02-a33c-b8ab0db20f44
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9bbc74050303a854b39ced508caf8a49e1ffdd1d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534877"
---
# <a name="sp_replshowcmds-transact-sql"></a>sp_replshowcmds(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  복제용으로 표시된 트랜잭션에 대한 명령을 읽을 수 있는 형식으로 반환합니다. **sp_replshowcmds** 는 클라이언트 연결 (현재 연결 포함)이 로그에서 복제 된 트랜잭션을 읽지 않는 경우에만 실행할 수 있습니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replshowcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>인수  
`[ @maxtrans = ] maxtrans` 정보를 반환할 트랜잭션의 수입니다. *maxtrans* 은 **int**이며 기본값은 **sp_replshowcmds** 정보를 반환 하는 복제 보류 중인 최대 트랜잭션 수를 지정 하는 **1**입니다.  
  
## <a name="result-sets"></a>결과 집합  
 **sp_replshowcmds** 은 실행 되는 게시 데이터베이스에 대 한 정보를 반환 하는 진단 프로시저입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|명령의 시퀀스 번호입니다.|  
|**originator_id**|**int**|명령 보낸 사람의 ID 이며 항상 **0**입니다.|  
|**publisher_database_id**|**int**|게시자 데이터베이스의 ID 이며 항상 **0**입니다.|  
|**article_id**|**int**|아티클의 ID입니다.|  
|**type**|**int**|명령의 유형입니다.|  
|**command**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 명령입니다.|  
  
## <a name="remarks"></a>설명  
 **sp_replshowcmds** 은 트랜잭션 복제에 사용 됩니다.  
  
 **Sp_replshowcmds**를 사용 하 여 현재 배포 되지 않은 트랜잭션 (배포자에 전송 되지 않은 트랜잭션 로그에 남아 있는 트랜잭션)을 볼 수 있습니다.  
  
 **Sp_replshowcmds** 및 **sp_replcmds** 를 실행 하는 클라이언트는 동일한 데이터베이스 내에서 18752 오류를 수신 합니다.  
  
 이 오류를 방지 하려면 첫 번째 클라이언트의 연결을 끊거나 **sp_replflush**를 실행 하 여 로그 판독기로 클라이언트의 역할을 해제 해야 합니다. 모든 클라이언트가 로그 판독기에서 연결을 끊은 후 **sp_replshowcmds** 성공적으로 실행 될 수 있습니다.  
  
> [!NOTE]  
>  **sp_replshowcmds** 는 복제 관련 문제를 해결 하기 위해서만 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_replshowcmds**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류 메시지](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [Transact-sql&#41;sp_repldone &#40;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [Transact-sql&#41;sp_replflush &#40;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [Transact-sql&#41;sp_repltrans &#40;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

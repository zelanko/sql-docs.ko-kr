---
description: sp_replcmds(Transact-SQL)
title: sp_replcmds (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replcmds_TSQL
- sp_replcmds
helpviewer_keywords:
- sp_replcmds
ms.assetid: 7e932f80-cc6e-4109-8db4-2b7c8828df73
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dde94b7383bd6d043972bc8ad496e0b40165e206
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485779"
---
# <a name="sp_replcmds-transact-sql"></a>sp_replcmds(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  복제용으로 표시된 트랜잭션에 대한 명령을 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  **Sp_replcmds** 프로시저는 복제 관련 문제를 해결 하기 위해서만 실행 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>인수  
`[ @maxtrans = ] maxtrans` 정보를 반환할 트랜잭션의 수입니다. *maxtrans* 은 **int**이며 기본값은 배포 대기 중인 다음 트랜잭션을 지정 하는 **1**입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**문서 id**|**int**|아티클의 ID입니다.|  
|**partial_command**|**bit**|부분 명령인지 여부를 나타냅니다.|  
|**command**|**varbinary (1024)**|명령 값입니다.|  
|**xactid**|**binary(10)**|트랜잭션 ID입니다.|  
|**xact_seqno**|**varbinary(16)**|트랜잭션 시퀀스 번호입니다.|  
|**publication_id**|**int**|게시의 ID입니다.|  
|**command_id**|**int**|[MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)명령의 ID입니다.|  
|**command_type**|**int**|명령의 유형입니다.|  
|**originator_srvname**|**sysname**|트랜잭션이 시작된 서버입니다.|  
|**originator_db**|**sysname**|트랜잭션이 시작된 데이터베이스입니다.|  
|**pkHash**|**int**|내부적으로만 사용됩니다.|  
|**originator_publication_id**|**int**|트랜잭션이 시작된 게시의 ID입니다.|  
|**originator_db_version**|**int**|트랜잭션이 시작된 데이터베이스의 버전입니다.|  
|**originator_lsn**|**varbinary(16)**|원본 게시에서 명령의 LSN(로그 시퀀스 번호)을 식별합니다.|  
  
## <a name="remarks"></a>설명  
 **sp_replcmds** 은 트랜잭션 복제의 로그 판독기 프로세스에서 사용 됩니다.  
  
 복제는 지정 된 데이터베이스 내에서 **sp_replcmds** 를 실행 하는 첫 번째 클라이언트를 로그 판독기로 처리 합니다.  
  
 이 프로시저는 소유자 한정 테이블에 대한 명령을 생성하거나 테이블 이름을 한정하지 않습니다(기본값). 한정된 테이블 이름을 추가할 경우 한 데이터베이스 내의 특정 사용자가 소유한 테이블에서 다른 데이터베이스 내의 같은 사용자가 소유한 테이블로 데이터를 복제할 수 있습니다.  
  
> [!NOTE]  
>  원본 데이터베이스의 테이블 이름은 소유자 이름에 의해 한정되므로 대상 데이터베이스의 테이블 소유자는 반드시 같은 소유자 이름을 사용해야 합니다.  
  
 동일한 데이터베이스 내에서 **sp_replcmds** 를 실행 하려고 시도 하는 클라이언트는 첫 번째 클라이언트가 연결을 끊을 때까지 18752 오류를 수신 합니다. 첫 번째 클라이언트가 연결을 끊은 후에는 다른 클라이언트가 **sp_replcmds**를 실행 하 여 새 로그 판독기가 됩니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] 텍스트 포인터가 동일한 트랜잭션에서 검색 되지 않았기 때문에 **sp_replcmds** 에서 텍스트 명령을 복제할 수 없는 경우 오류 로그와 Windows 응용 프로그램 로그에 모두 경고 메시지 번호 18759이 추가 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_replcmds**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류 메시지](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [Transact-sql&#41;sp_repldone &#40;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [Transact-sql&#41;sp_replflush &#40;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [Transact-sql&#41;sp_repltrans &#40;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

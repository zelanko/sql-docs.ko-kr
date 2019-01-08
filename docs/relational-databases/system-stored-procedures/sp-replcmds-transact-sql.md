---
title: sp_replcmds (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c868fe69df1f3fd34fe0c1f550507e7db7b6c944
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52823427"
---
# <a name="spreplcmds-transact-sql"></a>sp_replcmds(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  복제용으로 표시된 트랜잭션에 대한 명령을 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  합니다 **sp_replcmds** 프로시저 복제를 사용 하 여 문제 해결에 실행 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>인수  
 [  **@maxtrans=**] *maxtrans*  
 정보를 반환할 트랜잭션의 수입니다. *maxtrans* 됩니다 **int**, 기본값은 **1**, 배포 대기 중인 다음 트랜잭션을 지정 하는 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**문서 id**|**int**|아티클의 ID입니다.|  
|**partial_command**|**bit**|부분 명령인지 여부를 나타냅니다.|  
|**명령**|**varbinary(1024)**|명령 값입니다.|  
|**xactid**|**binary(10)**|트랜잭션 ID입니다.|  
|**xact_seqno**|**varbinary(16)**|트랜잭션 시퀀스 번호입니다.|  
|**publication_id**|**int**|게시의 ID입니다.|  
|**command_id**|**int**|명령 ID [MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)합니다.|  
|**command_type**|**int**|명령의 유형입니다.|  
|**originator_srvname**|**sysname**|트랜잭션이 시작된 서버입니다.|  
|**originator_db**|**sysname**|트랜잭션이 시작된 데이터베이스입니다.|  
|**pkHash**|**int**|내부적으로만 사용됩니다.|  
|**originator_publication_id**|**int**|트랜잭션이 시작된 게시의 ID입니다.|  
|**originator_db_version**|**int**|트랜잭션이 시작된 데이터베이스의 버전입니다.|  
|**originator_lsn**|**varbinary(16)**|원본 게시에서 명령의 LSN(로그 시퀀스 번호)을 식별합니다.|  
  
## <a name="remarks"></a>Remarks  
 **sp_replcmds** 트랜잭션 복제 로그 판독기 프로세스에서 사용 됩니다.  
  
 복제 처리를 실행 하는 첫 번째 클라이언트가 **sp_replcmds** 로그 판독기로 지정된 된 데이터베이스 내에서.  
  
 이 프로시저는 소유자 한정 테이블에 대한 명령을 생성하거나 테이블 이름을 한정하지 않습니다(기본값). 한정된 테이블 이름을 추가할 경우 한 데이터베이스 내의 특정 사용자가 소유한 테이블에서 다른 데이터베이스 내의 같은 사용자가 소유한 테이블로 데이터를 복제할 수 있습니다.  
  
> [!NOTE]  
>  원본 데이터베이스의 테이블 이름은 소유자 이름에 의해 한정되므로 대상 데이터베이스의 테이블 소유자는 반드시 같은 소유자 이름을 사용해야 합니다.  
  
 실행 하려고 하는 클라이언트가 **sp_replcmds** 첫 번째 클라이언트가 연결을 끊을 때까지 동일한 데이터베이스 내 18752 오류를 수신 합니다. 첫 번째 클라이언트가 연결을 끊은 후 다른 클라이언트를 실행할 수 **sp_replcmds**, 되며 새 로그 판독기입니다.  
  
 경고 메시지 18759 둘 다에 추가 되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 하는 경우 Windows 응용 프로그램 로그 **sp_replcmds** 텍스트 포인터가 없기 때문에 텍스트 명령을 복제할 수 없는 동일한 트랜잭션에서 검색 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_replcmds**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [오류 메시지](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_repldone &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

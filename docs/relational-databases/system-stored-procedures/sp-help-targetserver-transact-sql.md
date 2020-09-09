---
description: sp_help_targetserver(Transact-SQL)
title: sp_help_targetserver (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_targetserver_TSQL
- sp_help_targetserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_targetserver
ms.assetid: f841d3bd-901a-4980-ad0b-1c6eeba3f717
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 02304ff4c41f45e90c24fb4be1a815be49c1336a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89527606"
---
# <a name="sp_help_targetserver-transact-sql"></a>sp_help_targetserver(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  모든 대상 서버를 나열합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_targetserver   
     [ [ @server_name = ] 'server_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @server_name = ] 'server_name'` 정보를 반환할 서버의 이름입니다. *server_name* 은 **nvarchar (30)** 이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 *Server_name* 지정 하지 않으면 **sp_help_targetserver** 이 결과 집합을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|서버 ID입니다.|  
|**server_name**|**nvarchar(30)**|서버 이름입니다.|  
|**location**|**nvarchar(200)**|지정된 서버의 위치입니다.|  
|**time_zone_adjustment**|**int**|GMT(그리니치 표준시)를 적용한 표준 시간대 조정입니다.|  
|**enlist_date**|**datetime**|지정된 서버의 포함 목록 날짜입니다.|  
|**last_poll_date**|**datetime**|서버가 작업에 대해 마지막으로 폴링된 날짜입니다.|  
|**status**|**int**|지정된 서버의 상태입니다.|  
|**unread_instructions**|**int**|서버가 명령을 읽지 않았는지의 여부를 결정합니다. 모든 행을 다운로드 한 경우이 열은 **0**입니다.|  
|**local_time**|**datetime**|마스터 서버가 마지막으로 폴링한 대상 서버의 로컬 시간을 기준으로 하는 대상 서버의 로컬 날짜 및 시간입니다.|  
|**enlisted_by_nt_user**|**nvarchar (100)**|대상 서버에 참여하는 Microsoft Windows 사용자입니다.|  
|**poll_interval**|**int**|대상 서버가 작업을 다운로드하고 작업 상태를 업로드하기 위해 마스터 SQLServerAgent 서비스를 폴링하는 빈도(초)입니다.|  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 사용자가 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-listing-information-for-all-registered-target-servers"></a>A. 등록된 모든 대상 서버에 대한 정보 나열  
 다음 예에서는 등록된 모든 대상 서버에 대한 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-target-server"></a>B. 특정 대상 서버에 대한 정보 나열  
 다음 예에서는 대상 서버 `SEATTLE2`에 대한 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [Transact-sql&#41;sp_delete_targetserver &#40;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [Transact-sql&#41;sp_delete_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [Transact-sql&#41;sp_update_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)   
 [dbo.sysdownloadlist &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

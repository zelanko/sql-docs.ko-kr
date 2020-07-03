---
title: sp_help_log_shipping_monitor_primary (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_monitor_primary
- sp_help_log_shipping_monitor_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_monitor_primary
ms.assetid: d9dfcb8f-1da6-49ca-a2c8-411574915434
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c133218f7714bd7611e76c2dd202e81041cfa725
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891773"
---
# <a name="sp_help_log_shipping_monitor_primary-transact-sql"></a>sp_help_log_shipping_monitor_primary(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  모니터 테이블에서 주 데이터베이스에 관한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_log_shipping_monitor_primary  
[ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database'  
```  
  
## <a name="arguments"></a>인수  
`[ @primary_server = ] 'primary_server'`[!INCLUDE[msCoName](../../includes/msconame-md.md)]로그 전달 구성에 있는의 주 인스턴스 이름입니다 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . *primary_server* 는 **sysname** 이며 NULL 일 수 없습니다.  
  
`[ @primary_database = ] 'primary_database'`주 서버에 있는 데이터베이스의 이름입니다. *primary_database* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|설명|  
|-----------------|-----------------|  
|**primary_id**|로그 전달 구성의 주 데이터베이스의 ID입니다.|  
|**primary_server**|로그 전달 구성의 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 대한 주 인스턴스 이름입니다.|  
|**primary_database**|로그 전달 구성의 주 데이터베이스의 이름입니다.|  
|**backup_threshold**|백업 작업 간 허용되는 시간(분)입니다. 이 시간이 지나면 경고가 발생합니다.|  
|**threshold_alert**|백업 임계값이 초과될 때 발생하는 경고입니다.|  
|**threshold_alert_enabled**|백업 임계값 경고를 설정할지 여부를 결정합니다. 1 = 설정, 0 = 해제|  
|**last_backup_file**|가장 최근 트랜잭션 로그 백업의 절대 경로입니다.|  
|**last_backup_date**|주 데이터베이스에서 마지막으로 수행된 트랜잭션 로그 백업 작업의 시간과 날짜입니다.|  
|**last_backup_date_utc**|주 데이터베이스에서 마지막으로 수행된 트랜잭션 로그 백업 작업의 시간과 날짜(UTC)입니다.|  
|**history_retention_period**|지정된 기본 데이터베이스의 로그 전달 기록 레코드가 삭제되기까지 보관되는 기간(분)입니다.|  
  
## <a name="remarks"></a>설명  
 **sp_help_log_shipping_monitor_primary** 는 모니터 서버에 있는 **master** 데이터베이스에서 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만이 프로시저를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

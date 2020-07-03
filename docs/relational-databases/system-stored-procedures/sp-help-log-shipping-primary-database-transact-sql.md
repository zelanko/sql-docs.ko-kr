---
title: sp_help_log_shipping_primary_database (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_primary_database_TSQL
- sp_help_log_shipping_primary_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_primary_database
ms.assetid: e711b01c-ef29-4eb6-a016-0e647e337818
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5606c29eb4592f15eff641d969f6fcd28c89fa90
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891745"
---
# <a name="sp_help_log_shipping_primary_database-transact-sql"></a>sp_help_log_shipping_primary_database(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  주 데이터베이스 설정을 검색합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_log_shipping_primary_database  
[ @database = ] 'database' OR  
[ @primary_id = ] 'primary_id'  
```  
  
## <a name="arguments"></a>인수  
`[ @database = ] 'database'`로그 전달 주 데이터베이스의 이름입니다. *데이터베이스* 는 **sysname**이며 기본값은 없고 NULL 일 수 없습니다.  
  
`[ @primary_id = ] 'primary_id'`로그 전달 구성에 대 한 주 데이터베이스의 ID입니다. *primary_id* 은 **uniqueidentifier** 이며 NULL 일 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|설명|  
|-----------------|-----------------|  
|**primary_id**|로그 전달 구성의 주 데이터베이스의 ID입니다.|  
|**primary_database**|로그 전달 구성의 주 데이터베이스의 이름입니다.|  
|**backup_directory**|주 서버의 트랜잭션 로그 백업 파일이 저장되는 디렉터리입니다.|  
|**backup_share**|백업 디렉터리의 네트워크 또는 UNC 경로입니다.|  
|**backup_retention_period**|백업 디렉터리에서 로그 백업 파일이 삭제되기까지 보관되는 기간(분)입니다.|  
|**backup_compression**|로그 전달 구성에서 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md)을 사용 하는지 여부를 나타냅니다.<br /><br /> **0** = 사용 안 함 로그 백업을 압축하지 않습니다.<br /><br /> **1** = 사용 항상 로그 백업을 압축합니다.<br /><br /> **2** = [백업 압축 기본값 서버 구성 옵션](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)의 설정을 사용 합니다. 기본값입니다.<br /><br /> 백업 압축은 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상 버전에서만 지원됩니다. 다른 버전의 경우 값은 항상 2입니다.|  
|**backup_job_id**|주 서버의 백업 작업과 연관된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 작업 ID입니다.|  
|**monitor_server**|로그 전달 구성에서 모니터 서버로 사용되는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스의 이름입니다.|  
|**monitor_server_security_mode**|모니터 서버 연결에 사용되는 보안 모드입니다.<br /><br /> 1 = [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증|  
|**backup_threshold**|백업 작업 간 허용되는 시간(분)입니다. 이 시간이 지나면 경고가 발생합니다.|  
|**threshold_alert**|백업 임계값이 초과될 때 발생하는 경고입니다.|  
|**threshold_alert_enabled**|백업 임계값 경고를 설정할지 여부를 결정합니다.<br /><br /> **1** = 사용<br /><br /> **0** = 사용 안 함|  
|**last_backup_file**|가장 최근 트랜잭션 로그 백업의 절대 경로입니다.|  
|**last_backup_date**|마지막 로그 백업 작업의 시간과 날짜입니다.|  
|**last_backup_date_utc**|주 데이터베이스에서 마지막으로 수행된 트랜잭션 로그 백업 작업의 시간과 날짜(UTC)입니다.|  
|**history_retention_period**|지정된 기본 데이터베이스의 로그 전달 기록 레코드가 삭제되기까지 보관되는 기간(분)입니다.|  
  
## <a name="remarks"></a>설명  
 **sp_help_log_shipping_primary_database** 는 주 서버의 **master** 데이터베이스에서 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **sp_help_log_shipping_primary_database** 를 사용 하 여 데이터베이스에 대 한 주 데이터베이스 설정을 검색 하는 방법을 보여 줍니다 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
EXEC master.dbo.sp_help_log_shipping_primary_database @database=N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

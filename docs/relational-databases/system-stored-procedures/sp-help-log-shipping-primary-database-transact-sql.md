---
title: sp_help_log_shipping_primary_database (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_primary_database_TSQL
- sp_help_log_shipping_primary_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_primary_database
ms.assetid: e711b01c-ef29-4eb6-a016-0e647e337818
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 257d4310d46f757ab2d34760b99a394bba933330
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sphelplogshippingprimarydatabase-transact-sql"></a>sp_help_log_shipping_primary_database(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  주 데이터베이스 설정을 검색합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_log_shipping_primary_database  
[ @database = ] 'database' OR  
[ @primary_id = ] 'primary_id'  
```  
  
## <a name="arguments"></a>인수  
 [  **@database =** ] '*데이터베이스*'  
 로그 전달 주 데이터베이스의 이름입니다. *데이터베이스* 은 **sysname**, 기본값은 없고 NULL 일 수 없습니다.  
  
 [ **@primary_id =** ] '*primary_id*'  
 로그 전달 구성의 주 데이터베이스의 ID입니다. *primary_id* 은 **uniqueidentifier** NULL 일 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|Description|  
|-----------------|-----------------|  
|**primary_id**|로그 전달 구성의 주 데이터베이스의 ID입니다.|  
|**primary_database**|로그 전달 구성의 주 데이터베이스의 이름입니다.|  
|**backup_directory**|주 서버의 트랜잭션 로그 백업 파일이 저장되는 디렉터리입니다.|  
|**backup_share**|백업 디렉터리의 네트워크 또는 UNC 경로입니다.|  
|**backup_retention_period**|백업 디렉터리에서 로그 백업 파일이 삭제되기까지 보관되는 기간(분)입니다.|  
|**backup_compression**|로그 전달 구성을 사용할지 여부를 나타내는 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md)합니다.<br /><br /> **0** = 사용 안 함. 로그 백업을 압축하지 않습니다.<br /><br /> **1** = 사용 하도록 설정 합니다. 항상 로그 백업을 압축합니다.<br /><br /> **2** =의 설정을 사용 하 여는 [백업 압축 기본값 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)합니다. 이 값은 기본값입니다.<br /><br /> 백업 압축은 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상 버전에서만 지원됩니다. 다른 버전의 경우 값은 항상 2입니다.|  
|**backup_job_id**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 주 서버의 백업 작업과 연결 된 에이전트 작업 ID입니다.|  
|**monitor_server**|로그 전달 구성에서 모니터 서버로 사용되는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스의 이름입니다.|  
|**monitor_server_security_mode**|모니터 서버 연결에 사용되는 보안 모드입니다.<br /><br /> 1 = [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.|  
|**backup_threshold**|백업 작업 간 허용되는 시간(분)입니다. 이 시간이 지나면 경고가 발생합니다.|  
|**threshold_alert**|백업 임계값이 초과될 때 발생하는 경고입니다.|  
|**threshold_alert_enabled**|백업 임계값 경고를 설정할지 여부를 결정합니다.<br /><br /> **1** = 사용 하도록 설정 합니다.<br /><br /> **0** = 사용 안 함.|  
|**last_backup_file**|가장 최근 트랜잭션 로그 백업의 절대 경로입니다.|  
|**last_backup_date**|마지막 로그 백업 작업의 시간과 날짜입니다.|  
|**last_backup_date_utc**|주 데이터베이스에서 마지막으로 수행된 트랜잭션 로그 백업 작업의 시간과 날짜(UTC)입니다.|  
|**history_retention_period**|지정된 기본 데이터베이스의 로그 전달 기록 레코드가 삭제되기까지 보관되는 기간(분)입니다.|  
  
## <a name="remarks"></a>주의  
 **sp_help_log_shipping_primary_database** 에서 실행 되어야 합니다는 **마스터** 주 서버의 데이터베이스입니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 이 예제에서는 사용 하 여 **sp_help_log_shipping_primary_database** 데이터베이스에 대 한 주 데이터베이스 설정을 검색 하려면 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]합니다.  
  
```  
EXEC master.dbo.sp_help_log_shipping_primary_database @database=N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 & #40;에 대 한 SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

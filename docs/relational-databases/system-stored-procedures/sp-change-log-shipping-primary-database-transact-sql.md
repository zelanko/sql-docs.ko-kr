---
title: sp_change_log_shipping_primary_database (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_change_log_shipping_primary_database
- sp_change_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_primary_database
ms.assetid: 8c9dce6b-d2a3-4ca7-a832-8f59a5adb214
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5d4a266a220a1be4597a82248618413348e4d62b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spchangelogshippingprimarydatabase-transact-sql"></a>sp_change_log_shipping_primary_database(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  주 데이터베이스 설정을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_change_log_shipping_primary_database [ @database = ] 'database'  
[, [ @backup_directory = ] 'backup_directory']   
[, [ @backup_share = ] 'backup_share']   
[, [ @backup_retention_period = ] 'backup_retention_period']  
[, [ @monitor_server_security_mode = ] 'monitor_server_security_mode']  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @backup_threshold = ] 'backup_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
[, [ @backup_compression = ] backup_compression_option ]   
```  
  
## <a name="arguments"></a>인수  
 [  **@database =** ] '*데이터베이스*'  
 주 서버의 데이터베이스 이름입니다. *primary_database* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@backup_directory =** ] '*backup_directory*'  
 주 서버의 백업 폴더에 대한 경로입니다. *backup_directory* 은 **nvarchar (500)**, 기본값은 없고 NULL 일 수 없습니다.  
  
 [  **@backup_share =** ] '*backup_share*'  
 주 서버의 백업 디렉터리에 대한 네트워크 경로입니다. *backup_share* 은 **nvarchar (500)**, 기본값은 없고 NULL 일 수 없습니다.  
  
 [  **@backup_retention_period =** ] '*backup_retention_period*'  
 주 서버에서 백업 디렉터리에 로그 백업 파일이 보관되는 시간(분)입니다. *backup_retention_period* 은 **int**, 기본값은 없고 NULL 일 수 없습니다.  
  
 [  **@monitor_server_security_mode =** ] '*monitor_server_security_mode*'  
 모니터 서버 연결에 사용되는 보안 모드입니다.  
  
 1 = Windows 인증  
  
 0 = SQL Server 인증  
  
 *monitor_server_security_mode* 은 **비트** NULL 일 수 없습니다.  
  
 [ **@monitor_server_login =** ] '*monitor_server_login*'  
 모니터 서버에 액세스하는 데 사용되는 계정의 사용자 이름입니다.  
  
 [ **@monitor_server_password =** ] '*monitor_server_password*'  
 모니터 서버에 액세스하는 데 사용되는 계정의 암호입니다.  
  
 [  **@backup_threshold =** ] '*backup_threshold*'  
 시간 (분) 하기 전에 마지막 백업 후의 길이 *threshold_alert* 오류가 발생 합니다. *backup_threshold* 은 **int**, 기본값은 60 분입니다.  
  
 [  **@threshold_alert =** ] '*threshold_alert*'  
 백업 임계값이 초과될 때 발생하는 경고입니다. *threshold_alert* 은 **int** NULL 일 수 없습니다.  
  
 [  **@threshold_alert_enabled =** ] '*threshold_alert_enabled*'  
 경고가 발생 하는지 여부를 지정 하면 *backup_threshold* 을 초과 합니다.  
  
 1 = 사용  
  
 0 = 사용 안 함  
  
 *threshold_alert_enabled* 은 **비트** NULL 일 수 없습니다.  
  
 [  **@history_retention_period =** ] '*history_retention_period*'  
 기록이 보존되는 기간(분)입니다. *history_retention_period* 은 **int**합니다. 지정된 값이 없으면 14420을 사용합니다.  
  
 [ **@backup_compression**=] *backup_compression_option*  
 로그 전달 구성을 사용할지 여부 지정 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md)합니다. 이 매개 변수는 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상 버전에서만 지원됩니다.  
  
 0 = 사용 안 함. 로그 백업을 압축하지 않습니다.  
  
 1 = 사용. 항상 로그 백업을 압축합니다.  
  
 2 =의 설정을 사용 하 여는 [백업 압축 기본값 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)합니다. 이 값은 기본값입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 **sp_change_log_shipping_primary_database** 에서 실행 되어야 합니다는 **마스터** 주 서버의 데이터베이스입니다. 이 저장 프로시저는 다음을 수행합니다.  
  
1.  설정을 변경는 **log_shipping_primary_database** 필요한 경우를 기록 합니다.  
  
2.  로컬 레코드 변경 **log_shipping_monitor_primary** 주 서버에서 사용 하 여 제공 된 인수를 필요한 경우.  
  
3.  변경 기록의 모니터 서버가 주 서버에서 다른 경우 **log_shipping_monitor_primary** 모니터 서버를 사용 하 여 제공 된 인수를 필요한 경우.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 이 예제에서는 **sp_change_log_shipping_primary_database** 주 데이터베이스와 관련 된 설정을 업데이트 하지 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]합니다.  
  
```  
EXEC master.dbo.sp_change_log_shipping_primary_database   
 @database = N'AdventureWorks'   
, @backup_directory = N'c:\LogShipping'   
, @backup_share = N'\\tribeca\LogShipping'   
, @backup_retention_period = 1440   
, @backup_threshold = 60   
, @threshold_alert = 0   
, @threshold_alert_enabled = 1   
, @history_retention_period = 1440   
,@monitor_server_security_mode = 1  
,@backup_compression = 1;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 & #40;에 대 한 SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [log_shipping_primary_databases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)  
  
  

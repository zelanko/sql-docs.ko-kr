---
title: sp_change_log_shipping_primary_database (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_primary_database
- sp_change_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_primary_database
ms.assetid: 8c9dce6b-d2a3-4ca7-a832-8f59a5adb214
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 02ba9c11d9c74daa6cc88051ada7037edc16f35b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715933"
---
# <a name="sp_change_log_shipping_primary_database-transact-sql"></a>sp_change_log_shipping_primary_database(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  주 데이터베이스 설정을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @database = ] 'database'`주 서버에 있는 데이터베이스의 이름입니다. *primary_database* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @backup_directory = ] 'backup_directory'`는 주 서버의 백업 폴더에 대 한 경로입니다. *backup_directory* 는 **nvarchar (500)** 이며 기본값은 없고 NULL 일 수 없습니다.  
  
`[ @backup_share = ] 'backup_share'`주 서버의 백업 디렉터리에 대 한 네트워크 경로입니다. *backup_share* 는 **nvarchar (500)** 이며 기본값은 없고 NULL 일 수 없습니다.  
  
`[ @backup_retention_period = ] 'backup_retention_period'`주 서버의 백업 디렉터리에 로그 백업 파일을 유지 하는 데 걸리는 시간 (분)입니다. *backup_retention_period* 은 **int**이며 기본값은 없고 NULL 일 수 없습니다.  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'`모니터 서버에 연결 하는 데 사용 되는 보안 모드입니다.  
  
 1 = Windows 인증  
  
 0 = SQL Server 인증  
  
 *monitor_server_security_mode* 은 **bit** 이며 NULL 일 수 없습니다.  
  
`[ @monitor_server_login = ] 'monitor_server_login'`모니터 서버에 액세스 하는 데 사용 되는 계정의 사용자 이름입니다.  
  
`[ @monitor_server_password = ] 'monitor_server_password'`모니터 서버에 액세스 하는 데 사용 되는 계정의 암호입니다.  
  
`[ @backup_threshold = ] 'backup_threshold'`마지막 백업 후 *threshold_alert* 오류가 발생 하기 까지의 시간 (분)입니다. *backup_threshold* 은 **int**이며 기본값은 60 분입니다.  
  
`[ @threshold_alert = ] 'threshold_alert'`백업 임계값이 초과 될 때 발생 하는 경고입니다. *threshold_alert* 는 **int** 이며 NULL 일 수 없습니다.  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'`*Backup_threshold* 를 초과할 때 경고가 발생 하는지 여부를 지정 합니다.  
  
 1 = 사용  
  
 0 = 사용 안 함  
  
 *threshold_alert_enabled* 은 **bit** 이며 NULL 일 수 없습니다.  
  
`[ @history_retention_period = ] 'history_retention_period'`기록이 보존 되는 시간 (분)입니다. *history_retention_period* 은 **int**입니다. 지정 된 값이 없는 경우에는 14420 값이 사용 됩니다.  
  
`[ @backup_compression = ] backup_compression_option`로그 전달 구성에서 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md)을 사용할지 여부를 지정 합니다. 이 매개 변수는 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상 버전에서만 지원됩니다.  
  
 0 = 사용 안 함. 로그 백업을 압축하지 않습니다.  
  
 1 = 사용. 항상 로그 백업을 압축합니다.  
  
 2 = [백업 압축 기본값 서버 구성 옵션](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)의 설정을 사용 합니다. 기본값입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **sp_change_log_shipping_primary_database** 는 주 서버의 **master** 데이터베이스에서 실행 해야 합니다. 이 저장 프로시저는 다음을 수행합니다.  
  
1.  필요한 경우 **log_shipping_primary_database** 레코드의 설정을 변경 합니다.  
  
2.  필요한 경우 제공 된 인수를 사용 하 여 주 서버에서 **log_shipping_monitor_primary** 의 로컬 레코드를 변경 합니다.  
  
3.  모니터 서버가 주 서버와 다른 경우 필요한 경우 제공 된 인수를 사용 하 여 모니터 서버의 **log_shipping_monitor_primary** 레코드를 변경 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예제  
 이 예에서는 **sp_change_log_shipping_primary_database** 를 사용 하 여 주 데이터베이스와 연관 된 설정을 업데이트 하는 방법을 보여 줍니다 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
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
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [log_shipping_primary_databases&#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)  
  
  

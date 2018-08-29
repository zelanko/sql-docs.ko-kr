---
title: sp_help_log_shipping_secondary_database (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_secondary_database
- sp_help_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_secondary_database
ms.assetid: 11ce42ca-d3f1-44c8-9cac-214ca8896b9a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bfdfd891065f0a0fa4cf30376fdaa0c55c5e10a0
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43033629"
---
# <a name="sphelplogshippingsecondarydatabase-transact-sql"></a>sp_help_log_shipping_secondary_database(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 저장 프로시저는 하나 이상의 보조 데이터베이스에 대한 설정을 검색합니다.  
  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database' OR  
[ @secondary_id = ] 'secondary_id'  
```  
  
## <a name="arguments"></a>인수  
 [  **@secondary_database =** ] '*secondary_database*'  
 보조 데이터베이스의 이름입니다. *secondary_database* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ **@secondary_id =** ] '*secondary_id*'  
 로그 전달 구성의 보조 서버의 ID입니다. *secondary_id* 됩니다 **uniqueidentifier** NULL 일 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|Description|  
|-----------------|-----------------|  
|**secondary_id**|로그 전달 구성의 보조 서버의 ID입니다.|  
|**primary_server**|기본 인스턴스 이름을 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 로그 전달 구성에서 합니다.|  
|**primary_database**|로그 전달 구성의 주 데이터베이스의 이름입니다.|  
|**backup_source_directory**|주 서버의 트랜잭션 로그 백업 파일이 저장되는 디렉터리입니다.|  
|**backup_destination_directory**|백업 파일이 복사되는 보조 서버의 디렉터리입니다.|  
|**file_retention_period**|보조 서버에서 백업 파일이 삭제되기까지 보관되는 기간(분)입니다.|  
|**copy_job_id**|보조 서버의 복사 작업과 연관된 ID입니다.|  
|**restore_job_id**|보조 서버의 복원 작업과 연관된 ID입니다.|  
|**monitor_server**|로그 전달 구성에서 모니터 서버로 사용되는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스의 이름입니다.|  
|**monitor_server_security_mode**|모니터 서버 연결에 사용되는 보안 모드입니다.<br /><br /> 1 = [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.|  
|**secondary_database**|로그 전달 구성의 보조 데이터베이스의 이름입니다.|  
|**restore_delay**|보조 서버가 지정된 백업 파일을 복원하기 전에 대기하는 시간(분)입니다. 기본값은 0분입니다.|  
|**restore_all**|1로 설정될 경우 보조 서버는 복원 작업 실행 시 모든 사용 가능한 트랜잭션 백업을 복원합니다. 그렇지 않으면 파일을 하나 복원한 후 중지합니다.|  
|**restore_mode**|보조 데이터베이스의 복원 모드입니다.<br /><br /> 0 = NORECOVERY로 로그 복원<br /><br /> 1 = STANDBY로 로그 복원|  
|**disconnect_users**|1로 설정될 경우 복원 작업 수행 시 보조 데이터베이스에서 사용자 연결이 끊어집니다. 기본값 = 0|  
|**block_size**|백업 장치의 블록 크기로 사용되는 크기(바이트)입니다.|  
|**buffer_count**|백업 또는 복원 작업에 사용되는 버퍼의 총 개수입니다.|  
|**max_transfer_size**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 백업 장치로 발급하는 최대 입력 또는 출력 요청의 크기(바이트)입니다.|  
|**restore_threshold**|복원 작업 간 허용되는 시간(분)입니다. 이 시간이 지나면 경고가 발생합니다.|  
|**threshold_alert**|복원 임계값을 초과할 경우 발생하는 경고입니다.|  
|**threshold_alert_enabled**|복원 임계값 경고를 설정할지 여부를 결정합니다.<br /><br /> 1 = 사용.<br /><br /> 0 = 사용 안 함.|  
|**last_copied_file**|보조 서버로 복사된 마지막 백업 파일의 파일 이름입니다.|  
|**last_copied_date**|보조 서버에 수행된 마지막 복사 작업의 시간과 날짜입니다.|  
|**last_copied_date_utc**|보조 서버에 수행된 마지막 복사 작업의 시간과 날짜(UTC)입니다.|  
|**last_restored_file**|보조 데이터베이스에 복원된 마지막 백업 파일의 이름입니다.|  
|**last_restored_date**|보조 데이터베이스에 수행된 마지막 복원 작업의 시간과 날짜입니다.|  
|**last_restored_date_utc**|보조 데이터베이스에 수행된 마지막 복원 작업의 시간과 날짜(UTC)입니다.|  
|**history_retention_period**|지정된 보조 데이터베이스에서 로그 전달 기록 레코드가 삭제되기까지 보관되는 기간(분)입니다.|  
|**last_restored_latency**|로그 백업이 주 서버 또는 데이터베이스에서 생성되어 보조 서버 또는 데이터베이스에서 복원될 때까지 경과한 시간(분)입니다.<br /><br /> 초기 값은 NULL입니다.|  
  
## <a name="remarks"></a>Remarks  
 포함 하는 경우는 *secondary_database* 매개 변수를 포함 하는 경우 결과 집합에 해당 보조 데이터베이스에 대 한 정보 포함 수 됩니다 합니다 *secondary_id* 매개 변수를 결과 집합에 포함 됩니다 보조 ID와 연결 된 모든 보조 데이터베이스에 대 한 정보  
  
 **sp_help_log_shipping_secondary_database** 에서 실행 해야 합니다 **마스터** 보조 서버의 데이터베이스.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_help_log_shipping_secondary_primary &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql.md)   
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

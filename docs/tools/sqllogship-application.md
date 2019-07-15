---
title: sqllogship 응용 프로그램 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- sqllogship
ms.assetid: 8ae70041-f3d9-46e4-8fa8-31088572a9f8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ca6a9765c7813fd0fbece4d8c392c23e2f784ec2
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728077"
---
# <a name="sqllogship-application"></a>sqllogship 애플리케이션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **sqllogship** 애플리케이션은 로그 전달 구성에 대해 백업, 복사, 복원 작업 및 관련 정리 태스크를 수행합니다. 이 작업은 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 특정 인스턴스에서 특정 데이터베이스에 대해 수행됩니다.  
  
 ![항목 링크 아이콘](../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") 구문 표기 규칙에 대 한 참조 [명령 프롬프트 유틸리티 참조 &#40;데이터베이스 엔진&#41;](../tools/command-prompt-utility-reference-database-engine.md).  
  
## <a name="syntax"></a>구문  
  
```  
  
sqllogship -server instance_name { -backup primary_id | -copy secondary_id | -restore secondary_id } [ -verboselevel level ] [ -logintimeout timeout_value ] [ -querytimeout timeout_value ]  
```  
  
## <a name="arguments"></a>인수  
 **-server** _instance_name_  
 작업을 실행할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 지정합니다. 지정할 서버 인스턴스는 로그 전달 작업이 지정되는지 여부에 따라 달라집니다. **-backup**의 경우 *instance_name* 은 로그 전달 구성의 주 서버 이름이어야 합니다. **-copy** 또는 **-restore**의 경우 *instance_name* 은 로그 전달 구성의 보조 서버 이름이어야 합니다.  
  
 **-backup** _primary_id_  
 주 ID가 *primary_id*로 지정된 주 데이터베이스에 대한 백업 작업을 수행합니다. [log_shipping_primary_databases](../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md) 시스템 테이블에서 선택하거나 [sp_help_log_shipping_primary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md) 저장 프로시저를 사용하여 이 ID를 가져올 수 있습니다.  
  
 백업 작업은 백업 디렉터리에 로그 백업을 만듭니다. 그런 다음 **sqllogship** 애플리케이션은 파일 보존 기간을 기준으로 모든 이전 백업 파일을 정리합니다. 다음으로 애플리케이션은 주 서버 및 모니터 서버의 백업 작업에 대한 기록을 작성합니다. 마지막으로 애플리케이션은 보존 기간을 기준으로 이전 기록 정보를 정리하는 [sp_cleanup_log_shipping_history](../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)를 실행합니다.  
  
 **-copy** _secondary_id_  
 보조 ID가 *secondary_id*로 지정된 데이터베이스 또는 보조 데이터베이스의 지정된 보조 서버에서 백업을 복사하는 복사 작업을 수행합니다. [log_shipping_secondary](../relational-databases/system-tables/log-shipping-secondary-transact-sql.md) 시스템 테이블에서 선택하거나 [sp_help_log_shipping_secondary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md) 저장 프로시저를 사용하여 이 ID를 가져올 수 있습니다.  
  
 이 작업은 백업 디렉터리에서 대상 디렉터리로 백업 파일을 복사합니다. 그런 다음 **sqllogship** 애플리케이션은 보조 서버 및 모니터 서버의 복사 작업에 대한 기록을 작성합니다.  
  
 **-restore** _secondary_id_  
 보조 ID가 *secondary_id*로 지정된 데이터베이스 또는 보조 데이터베이스의 지정된 보조 서버에서 복원 작업을 수행합니다. **sp_help_log_shipping_secondary_database** 저장 프로시저를 사용하여 이 ID를 가져올 수 있습니다.  
  
 최근 복원 지점 이후에 생성된 대상 디렉터리의 백업 파일이 데이터베이스 또는 보조 데이터베이스에 복원됩니다. 그런 다음 **sqllogship** 애플리케이션은 파일 보존 기간을 기준으로 모든 이전 백업 파일을 정리합니다. 다음으로 애플리케이션은 보조 서버 및 모니터 서버의 복원 작업에 대한 기록을 작성합니다. 마지막으로 애플리케이션은 보존 기간을 기준으로 이전 기록 정보를 정리하는 **sp_cleanup_log_shipping_history**를 실행합니다.  
  
 **-verboselevel** _level_  
 로그 전달 기록에 추가된 메시지 수준을 지정합니다. *level* 은 다음 정수 중 하나입니다.  
  
|level|설명|  
|-----------|-----------------|  
|0|추적 및 디버깅 메시지를 출력하지 않습니다.|  
|1|오류 처리 메시지를 출력합니다.|  
|2|경고 및 오류 처리 메시지를 출력합니다.|  
|**3**|정보 메시지, 경고 및 오류 처리 메시지를 출력합니다. 이것은 기본값입니다.|  
|4|모든 디버깅 및 추적 메시지를 출력합니다.|  
  
 **-logintimeout** _timeout_value_  
 서버 인스턴스 로그인에 할당된 제한 시간 값을 지정합니다. 기본값은 15초입니다. *timeout_value* 는 **int**_입니다._  
  
 **-querytimeout** _timeout_value_  
 지정된 작업을 시작하는 데 할당된 제한 시간 값을 지정합니다. 기본값은 제한 시간 없음입니다. *timeout_value* 는 **int**_입니다._  
  
## <a name="remarks"></a>Remarks  
 가능하면 백업, 복사 및 복원 작업을 사용하여 백업, 복사 및 복원을 수행하는 것이 좋습니다. 일괄 처리 작업 또는 다른 애플리케이션에서 이러한 작업을 시작하려면 [sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md) 저장 프로시저를 호출하세요.  
  
 **sqllogship** 에서 생성된 로그 전달 기록은 로그 전달 백업, 복사 및 복원 작업으로 생성된 기록과 섞여 있습니다. 로그 전달 구성에 대해 백업, 복사 또는 복원 작업을 수행하도록 **sqllogship** 을 반복적으로 사용하려면 해당 로그 전달 작업을 비활성화하는 것을 고려하십시오. 자세한 내용은 [Disable or Enable a Job](../ssms/agent/disable-or-enable-a-job.md)을 참조하세요.  
  
 **sqllogship** 애플리케이션인 SqlLogShip.exe는 x:\Program Files\Microsoft SQL Server\130\Tools\Binn 디렉터리에 설치됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **sqllogship** 은 Windows 인증을 사용합니다. 명령이 실행될 Windows 인증 계정에는 Windows 디렉터리 액세스 권한 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 권한이 필요합니다. 요구 사항은 **sqllogship** 명령이 **-backup**, **-copy**또는 **-restore** 옵션을 지정하는지에 따라 다릅니다.  
  
|옵션|디렉터리 액세스 권한|사용 권한|  
|------------|----------------------|-----------------|  
|**-backup**|백업 디렉터리에 대한 읽기/쓰기 권한이 필요합니다.|BACKUP 문과 같은 권한이 필요합니다. 자세한 내용은 [BACKUP&#40;Transact-SQL&#41;](../t-sql/statements/backup-transact-sql.md)을 참조하세요.|  
|**-copy**|백업 디렉터리에 대한 읽기 권한과 복사 디렉터리에 대한 쓰기 권한이 필요합니다.|[sp_help_log_shipping_secondary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md) 저장 프로시저와 같은 권한이 필요합니다.|  
|**-restore**|복사 디렉터리에 대한 읽기/쓰기 권한이 필요합니다.|RESTORE 문과 같은 권한이 필요합니다. 자세한 내용은 [RESTORE&#40;Transact-SQL&#41;](../t-sql/statements/restore-statements-transact-sql.md)를 참조하세요.|  
  
> [!NOTE]  
>  백업 및 복사 디렉터리의 경로를 찾기 위해 **sp_help_log_shipping_secondary_database** 저장 프로시저를 실행하거나 **msdb**의 **log_shipping_secondary** 테이블을 볼 수 있습니다. 백업 디렉터리 및 대상 디렉터리의 경로는 **backup_source_directory** 및 **backup_destination_directory** 열에 각각 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_primary_databases&#40;Transact-SQL&#41;](../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)   
 [log_shipping_secondary&#40;Transact-SQL&#41;](../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)   
 [sp_cleanup_log_shipping_history&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_help_log_shipping_primary_database&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [sp_start_job&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)  
  
  

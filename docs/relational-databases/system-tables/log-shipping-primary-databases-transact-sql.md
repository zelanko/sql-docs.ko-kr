---
title: log_shipping_primary_databases (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_primary_databases
- log_shipping_primary_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_primary_databases system table
ms.assetid: 56888756-a798-42be-9b5e-0f9aa05a2cc6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0881204a5b1d282ac295f2017981eb7bb46107be
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764198"
---
# <a name="log_shipping_primary_databases-transact-sql"></a>log_shipping_primary_databases(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  로그 전달 구성에서 주 데이터베이스마다 하나의 레코드를 저장합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|로그 전달 구성의 주 데이터베이스의 ID입니다.|  
|**primary_database**|**sysname**|로그 전달 구성의 주 데이터베이스의 이름입니다.|  
|**backup_directory**|**nvarchar (500)**|주 서버의 트랜잭션 로그 백업 파일이 저장되는 디렉터리입니다.|  
|**backup_share**|**nvarchar (500)**|백업 디렉터리의 네트워크 또는 UNC 경로입니다.|  
|**backup_retention_period**|**int**|백업 디렉터리에서 로그 백업 파일이 삭제되기까지 보관되는 기간(분)입니다.|  
|**backup_job_id**|**uniqueidentifier**|주 서버의 백업 작업과 연관된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 작업 ID입니다.|  
|**monitor_server**|**sysname**|로그 전달 구성에서 모니터 서버로 사용되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스의 이름입니다.|  
|**monitor_server_security_mode**|**bit**|모니터 서버 연결에 사용되는 보안 모드입니다.<br /><br /> 1 = Windows 인증<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증|  
|**last_backup_file**|**nvarchar (500)**|가장 최근 트랜잭션 로그 백업의 절대 경로입니다.|  
|**last_backup_date**|**datetime**|마지막 로그 백업 작업의 시간과 날짜입니다.|  
|**user_specified_monitor**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **sp_help_log_shipping_primary_database** 및 **sp_help_log_shipping_secondary_primary** 이 열을 사용 하 여에서 모니터 설정의 표시를 제어 합니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .<br /><br /> 0 = 이러한 두 저장 프로시저 중 하나를 호출할 때 사용자가 ** \@ monitor_server** 매개 변수에 대 한 명시적 값을 지정 하지 않았습니다.<br /><br /> 1 = 사용자가 명시적 값을 지정했습니다.|  
|**backup_compression**|**tinyint**|로그 전달 구성이 서버 수준 백업 압축 동작을 재정의하는지 여부를 나타냅니다.<br /><br /> 0 = 사용 안 함. 서버에 구성된 백업 압축 설정에 관계없이 로그 백업이 압축되지 않습니다.<br /><br /> 1 = 사용. 서버에 구성된 백업 압축 설정에 관계없이 로그 백업이 항상 압축됩니다.<br /><br /> 2 = [백업 압축 기본값 서버 구성 옵션](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) 서버 구성 옵션의 서버 구성을 사용 합니다. 기본값입니다.<br /><br /> 백업 압축은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition에서만 지원됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Transact-sql&#41;sp_add_log_shipping_primary_database &#40;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [Transact-sql&#41;sp_delete_log_shipping_primary_database &#40;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_primary_database&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  

---
title: log_shipping_primary_databases (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- log_shipping_primary_databases
- log_shipping_primary_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_primary_databases system table
ms.assetid: 56888756-a798-42be-9b5e-0f9aa05a2cc6
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 233f883e4c714fb7c8eead62e885dabfb5f0167c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="logshippingprimarydatabases-transact-sql"></a>log_shipping_primary_databases(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로그 전달 구성에서 주 데이터베이스마다 하나의 레코드를 저장합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|로그 전달 구성의 주 데이터베이스의 ID입니다.|  
|**primary_database**|**sysname**|로그 전달 구성의 주 데이터베이스의 이름입니다.|  
|**backup_directory**|**nvarchar(500)**|주 서버의 트랜잭션 로그 백업 파일이 저장되는 디렉터리입니다.|  
|**backup_share**|**nvarchar(500)**|백업 디렉터리의 네트워크 또는 UNC 경로입니다.|  
|**backup_retention_period**|**int**|백업 디렉터리에서 로그 백업 파일이 삭제되기까지 보관되는 기간(분)입니다.|  
|**backup_job_id**|**uniqueidentifier**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 주 서버의 백업 작업과 연결 된 에이전트 작업 ID입니다.|  
|**monitor_server**|**sysname**|인스턴스 이름을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 로그 전달 구성에서 모니터 서버로 사용 합니다.|  
|**monitor_server_security_mode**|**bit**|모니터 서버 연결에 사용되는 보안 모드입니다.<br /><br /> 1 = Windows 인증<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.|  
|**last_backup_file**|**nvarchar(500)**|가장 최근 트랜잭션 로그 백업의 절대 경로입니다.|  
|**last_backup_date**|**datetime**|마지막 로그 백업 작업의 시간과 날짜입니다.|  
|**user_specified_monitor**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **sp_help_log_shipping_primary_database** 및 **sp_help_log_shipping_secondary_primary** 모니터 설정의 표시를 제어 하려면이 열은 사용할 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.<br /><br /> 0 = 이러한 두 저장된 프로시저 중 하나를 호출할 때 사용자에 대 한 명시적 값을 지정 하지 않았습니다 고 **@monitor_server** 매개 변수입니다.<br /><br /> 1 = 사용자가 명시적 값을 지정했습니다.|  
|**backup_compression**|**tinyint**|로그 전달 구성이 서버 수준 백업 압축 동작을 재정의하는지 여부를 나타냅니다.<br /><br /> 0 = 사용 안 함. 서버에 구성된 백업 압축 설정에 관계없이 로그 백업이 압축되지 않습니다.<br /><br /> 1 = 사용. 서버에 구성된 백업 압축 설정에 관계없이 로그 백업이 항상 압축됩니다.<br /><br /> 2 =에 대 한 서버 구성을 사용 하 여 [백업 압축 기본값 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) 서버 구성 옵션입니다. 이 값은 기본값입니다.<br /><br /> 백업 압축은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition에서만 지원됩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 & #40;에 대 한 SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_primary_database&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  

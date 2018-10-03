---
title: log_shipping_primary_databases (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3904f6188ad1087c58a6044c1abd9fc2493c8129
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826541"
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
|**backup_job_id**|**uniqueidentifier**|합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 주 서버의 백업 작업과 연결 된 에이전트 작업 ID입니다.|  
|**monitor_server**|**sysname**|인스턴스의 이름을 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 로그 전달 구성에서 모니터 서버로 사용 합니다.|  
|**monitor_server_security_mode**|**bit**|모니터 서버 연결에 사용되는 보안 모드입니다.<br /><br /> 1 = Windows 인증<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.|  
|**last_backup_file**|**nvarchar(500)**|가장 최근 트랜잭션 로그 백업의 절대 경로입니다.|  
|**last_backup_date**|**datetime**|마지막 로그 백업 작업의 시간과 날짜입니다.|  
|**user_specified_monitor**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **sp_help_log_shipping_primary_database** 하 고 **sp_help_log_shipping_secondary_primary** 이 열을 사용 하 여 모니터 설정 표시를 제어 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]입니다.<br /><br /> 0 = 이러한 두 저장된 프로시저 중 하나를 호출할 때 사용자에 대 한 명시적 값을 지정 하지 않았습니다 합니다 **@monitor_server** 매개 변수입니다.<br /><br /> 1 = 사용자가 명시적 값을 지정했습니다.|  
|**backup_compression**|**tinyint**|로그 전달 구성이 서버 수준 백업 압축 동작을 재정의하는지 여부를 나타냅니다.<br /><br /> 0 = 사용 안 함. 서버에 구성된 백업 압축 설정에 관계없이 로그 백업이 압축되지 않습니다.<br /><br /> 1 = 사용. 서버에 구성된 백업 압축 설정에 관계없이 로그 백업이 항상 압축됩니다.<br /><br /> 2 =에 대 한 서버 구성을 사용 합니다 [보거나 backup compression default 서버 구성 옵션 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) 서버 구성 옵션입니다. 이것은 기본값입니다.<br /><br /> 백업 압축은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition에서만 지원됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_primary_database&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  

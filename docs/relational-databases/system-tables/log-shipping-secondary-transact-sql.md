---
title: log_shipping_secondary (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_secondary
- log_shipping_secondary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_secondary system table
ms.assetid: 69723419-4544-49c6-a517-adb30ffa5741
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5debab1572bc2f788c0dc13773d0dc140c693108
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82805973"
---
# <a name="log_shipping_secondary-transact-sql"></a>log_shipping_secondary(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  보조 ID 당 레코드 하나를 저장합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**secondary_id**|**uniqueidentifier**|로그 전달 구성의 보조 서버의 ID입니다.|  
|**primary_server**|**sysname**|로그 전달 구성의 SQL Server 데이터베이스 엔진에 대한 주 인스턴스의 이름입니다.|  
|**primary_database**|**sysname**|로그 전달 구성의 주 데이터베이스의 이름입니다.|  
|**backup_source_directory**|**nvarchar (500)**|주 서버의 트랜잭션 로그 백업 파일이 저장되는 디렉터리입니다.|  
|**backup_destination_directory**|**nvarchar (500)**|백업 파일이 복사되는 보조 서버의 디렉터리입니다.|  
|**file_retention_period**|**int**|보조 서버에서 백업 파일이 삭제되기까지 보관되는 기간(분)입니다.|  
|**copy_job_id**|**uniqueidentifier**|보조 서버의 복사 작업과 연관된 ID입니다.|  
|**restore_job_id**|**uniqueidentifier**|보조 서버의 복원 작업과 연관된 ID입니다.|  
|**monitor_server**|**sysname**|로그 전달 구성에서 모니터 서버로 사용되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스의 이름입니다.|  
|**monitor_server_security_mode**|**bit**|모니터 서버 연결에 사용되는 보안 모드입니다.<br /><br /> 1 = Windows 인증<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증|  
|**last_copied_file**|**nvarchar (500)**|보조 서버로 복사된 마지막 백업 파일의 파일 이름입니다.|  
|**last_copied_date**|**datetime**|보조 서버에 수행된 마지막 복사 작업의 시간과 날짜입니다.|  
  
## <a name="remarks"></a>설명  
 지정 된 주 데이터베이스에 대 한 동일한 보조 서버의 여러 보조 데이터베이스가 **log_shipping_secondary** 테이블의 일부 설정을 공유 합니다. 이러한 보조 데이터베이스 중 하나에서 공유된 설정이 변경되면 해당 설정은 모든 데이터베이스에서도 변경됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Transact-sql&#41;sp_add_log_shipping_secondary_database &#40;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [Transact-sql&#41;sp_change_log_shipping_secondary_database &#40;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql.md)   
 [Transact-sql&#41;sp_delete_log_shipping_secondary_database &#40;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [Transact-sql&#41;sp_help_log_shipping_secondary_database &#40;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  

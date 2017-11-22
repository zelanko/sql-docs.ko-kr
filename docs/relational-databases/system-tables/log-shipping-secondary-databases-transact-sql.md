---
title: log_shipping_secondary_databases (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- log_shipping_secondary_databases_TSQL
- log_shipping_secondary_databases
dev_langs: TSQL
helpviewer_keywords: log_shipping_secondary_databases system table
ms.assetid: ba2374af-86b8-480c-a10c-51e7c4e3ae23
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 60237602284820c646513b0ff6d8c1fcc8002cce
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="logshippingsecondarydatabases-transact-sql"></a>log_shipping_secondary_databases(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로그 전달 구성에서 보조 데이터베이스마다 하나의 레코드를 저장합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**secondary_database**|**sysname**|로그 전달 구성의 보조 데이터베이스의 이름입니다.|  
|**secondary_id**|**uniqueidentifier**|로그 전달 구성의 보조 서버의 ID입니다.|  
|**restore_delay**|**int**|보조 서버가 지정된 백업 파일을 복원하기 전에 대기하는 시간(분)입니다. 기본값은 0 분입니다.|  
|**restore_all**|**bit**|1로 설정될 경우 보조 서버는 복원 작업 실행 시 모든 사용 가능한 트랜잭션 로그 백업을 복원합니다. 그렇지 않으면 파일을 하나 복원한 후 중지합니다.|  
|**restore_mode**|**bit**|보조 데이터베이스의 복원 모드입니다.<br /><br /> 0 = NORECOVERY로 로그 복원<br /><br /> 1 = STANDBY로 로그 복원|  
|**disconnect_users**|**bit**|1로 설정될 경우 복원 작업 수행 시 보조 데이터베이스에서 사용자 연결이 끊어집니다. 기본값은 0입니다.|  
|**block_size**|**int**|백업 장치의 블록 크기로 사용되는 크기(바이트)입니다.|  
|**buffer_count**|**int**|백업 또는 복원 작업에 사용되는 버퍼의 총 개수입니다.|  
|**max_transfer_size**|**int**|최대 입력 또는 출력 요청의 발행를 바이트 단위로 크기 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 장치에 있습니다.|  
|**last_restored_file**|**nvarchar (500)**|보조 데이터베이스에 복원된 마지막 백업 파일의 이름입니다.|  
|**last_restored_date**|**datetime**|보조 데이터베이스에 수행된 마지막 복원 작업의 시간과 날짜입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_secondary_database &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [log_shipping_secondary&#40; Transact SQL &#41;](../../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)   
 [시스템 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  

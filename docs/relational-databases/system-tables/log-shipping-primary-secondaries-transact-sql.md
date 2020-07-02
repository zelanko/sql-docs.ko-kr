---
title: log_shipping_primary_secondaries (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_primary_secondaries_TSQL
- log_shipping_primary_secondaries
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_primary_secondaries system table
ms.assetid: 4b315c70-7265-4acd-b35b-a4dbb7881d98
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0d4aa527c1c1d7c77d637885e8d450a0a97188fa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750164"
---
# <a name="log_shipping_primary_secondaries-transact-sql"></a>log_shipping_primary_secondaries(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  각 주 데이터베이스를 보조 데이터베이스로 매핑합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|로그 전달 구성의 주 데이터베이스의 ID입니다.|  
|**secondary_server**|**sysname**|[!INCLUDE[msCoName](../../includes/msconame-md.md)]로그 전달 구성에 있는의 보조 인스턴스의 이름입니다 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] .|  
|**secondary_database**|**sysname**|로그 전달 구성의 보조 데이터베이스의 이름입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Transact-sql&#41;sp_add_log_shipping_primary_secondary &#40;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql.md)   
 [Transact-sql&#41;sp_delete_log_shipping_primary_secondary &#40;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql.md)   
 [Transact-sql&#41;sp_help_log_shipping_primary_secondary &#40;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-secondary-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  

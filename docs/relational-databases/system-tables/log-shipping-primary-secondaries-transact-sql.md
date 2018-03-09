---
title: log_shipping_primary_secondaries (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- log_shipping_primary_secondaries_TSQL
- log_shipping_primary_secondaries
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_primary_secondaries system table
ms.assetid: 4b315c70-7265-4acd-b35b-a4dbb7881d98
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 325b38e3b2cdb8f3fab90d4350ecfd449b512b81
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="logshippingprimarysecondaries-transact-sql"></a>log_shipping_primary_secondaries(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 주 데이터베이스를 보조 데이터베이스로 매핑합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|로그 전달 구성의 주 데이터베이스의 ID입니다.|  
|**secondary_server**|**sysname**|보조 인스턴스의 이름에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 로그 전달 구성의 합니다.|  
|**secondary_database**|**sysname**|로그 전달 구성의 보조 데이터베이스의 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 &#40;에 대 한 SQL Server &#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_primary_secondary &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql.md)   
 [sp_delete_log_shipping_primary_secondary &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql.md)   
 [sp_help_log_shipping_primary_secondary &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-secondary-transact-sql.md)   
 [시스템 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  

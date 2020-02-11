---
title: cdc. lsn_time_mapping (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.lsn_time_mapping
- cdc.lsn_time_mapping_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.lsn_time_mapping
ms.assetid: 1cb7aedc-48a4-486e-9b91-d30c4bd4084e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1e89e67b49498320e4500b99332fc5584d5f38d8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68066668"
---
# <a name="cdclsn_time_mapping-transact-sql"></a>cdc.lsn_time_mapping(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  변경 테이블에 행이 있는 각 트랜잭션에 대해 한 개의 행을 반환합니다. 이 테이블은 LSN(로그 시퀀스 번호) 커밋 값과 트랜잭션 커밋 시간을 매핑하는 데 사용됩니다. 변경 테이블 항목이 없는 경우에도 항목이 기록됩니다. 이렇게 하면 해당 테이블이 변경 작업이 적거나 없는 시간에 LSN 처리 완료를 기록할 수 있습니다.  
  
 시스템 테이블은 직접 쿼리하지 않는 것이 좋습니다. 대신 transact-sql&#41;및 [fn_cdc_map_time_to_lsn &#40;transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) 시스템 함수를 [&#40;fn_cdc_map_lsn_to_time](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md) 를 실행 합니다.  
    
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**start_lsn**|**binary (10)**|커밋된 트랜잭션의 LSN입니다.|  
|**tran_begin_time**|**datetime**|LSN과 연관된 트랜잭션이 시작된 시간입니다.|  
|**tran_end_time**|**datetime**|트랜잭션이 종료된 시간입니다.|  
|**tran_id**|**varbinary (10)**|트랜잭션 ID입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [&#60;capture_instance&#62;_CT &#40;Transact-sql&#41;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
  
  

---
title: cdc.ddl_history (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- cdc.ddl_history_TSQL
- cdc.ddl_history
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.ddl_history
ms.assetid: cb97ea71-da2f-441a-bbd2-db1f5f48ab49
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96232efb8041bceeff92f479a56b4b56483ab1fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="cdcddlhistory-transact-sql"></a>cdc.ddl_history(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  변경 데이터 캡처가 활성화된 테이블에 적용된 각 DDL(데이터 정의 언어) 변경에 대해 한 개의 행을 반환합니다. 이 테이블을 사용하면 원본 테이블에서 DDL 변경이 발생한 시점과 변경 내용을 확인할 수 있습니다. DDL 변경이 발생하지 않은 원본 테이블의 경우 이 테이블에 항목이 없습니다.  
  
 시스템 테이블은 직접 쿼리하지 않는 것이 좋습니다. 대신, 실행 된 [sys.sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md) 저장 프로시저입니다.  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**source_object_id**|**int**|DDL 변경이 적용된 원본 테이블의 ID입니다.|  
|**object_id**|**int**|원본 테이블에 대한 캡처 인스턴스와 관련된 변경 테이블의 ID입니다.|  
|**required_column_update**|**bit**|캡처된 열의 데이터 형식이 원본 테이블에서 수정되었음을 나타냅니다. 이로 인해 변경 테이블의 열이 변경됩니다.|  
|**ddl_command**|**nvarchar(max)**|원본 테이블에 적용된 DDL 문입니다.|  
|**ddl_lsn**|**binary(10)**|DDL 수정의 커밋과 관련된 LSN(로그 시퀀스 번호)입니다.|  
|**ddl_time**|**datetime**|원본 테이블에 적용된 DDL 변경의 날짜 및 시간입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [sys.sp_cdc_help_change_data_capture &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  

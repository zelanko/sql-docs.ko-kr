---
title: sys.fn_cdc_map_lsn_to_time (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
f1_keywords:
- sys.fn_cdc_map_lsn_to_time_TSQL
- sys.fn_cdc_map_lsn_to_time
- fn_cdc_map_lsn_to_time_TSQL
- fn_cdc_map_lsn_to_time
dev_langs: TSQL
helpviewer_keywords:
- sys.fn_cdc_map_lsn_to_time
- fn_cdc_map_lsn_to_time
ms.assetid: 405aa29c-8bd8-42d3-9f39-7494b643fc6f
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b003297afa47956f6059721a22554e0a2c831286
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysfncdcmaplsntotime-transact-sql"></a>sys.fn_cdc_map_lsn_to_time(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  날짜 및 시간 값을 반환 된 **tran_end_time** 열에는 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) 시스템 테이블에 지정 된 로그 시퀀스 번호 (LSN). 이 함수를 사용하여 변경 테이블의 날짜 범위에 LSN 범위를 체계적으로 매핑할 수 있습니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_cdc_map_lsn_to_time ( lsn_value )  
```  
  
## <a name="arguments"></a>인수  
 *lsn_value*  
 대조할 LSN 값입니다. *lsn_value* 은 **binary (10)**합니다.  
  
## <a name="return-type"></a>반환 형식  
 **datetime**  
  
## <a name="remarks"></a>주의  
 변경이 커밋된 기준 시간을 결정 하려면이 함수를 사용할 수는 **__ $start_lsn** 값이 변경 데이터의 행에 반환 합니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `sys.fn_cdc_map_lsn_to_time` 함수를 사용하여 `HumanResources_Employee` 캡처 인스턴스에 대해 지정된 LSN 간격에서 처리된 마지막 변경에 관련된 커밋 시간을 확인합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @max_lsn binary(10);  
SELECT @max_lsn = MAX(__$start_lsn)  
FROM cdc.fn_cdc_get_all_changes_HumanResources_Employee(@from_lsn, @to_lsn, 'all');  
SELECT sys.fn_cdc_map_lsn_to_time(@max_lsn);  
GO   
```  
  
## <a name="see-also"></a>관련 항목:  
 [cdc.lsn_time_mapping &#40; Transact SQL &#41;](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)   
 [sys.fn_cdc_map_time_to_lsn &#40; Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60; capture_instance& &#62; &#40; Transact SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60; capture_instance& &#62;  &#40; Transact SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  

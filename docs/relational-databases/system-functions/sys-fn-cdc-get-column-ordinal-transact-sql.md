---
title: sys.fn_cdc_get_column_ordinal (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- sys.fn_cdc_get_column_ordinal
- fn_cdc_get_column_ordinal_TSQL
- fn_cdc_get_column_ordinal
- sys.fn_cdc_get_column_ordinal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_column_ordinal
- sys.fn_cdc_get_column_ordinal
ms.assetid: 4bb21a57-2b94-4208-8bdf-6a3e2681d881
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 70ca20e98ba1330482fd19265b7f54f07d9711e4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysfncdcgetcolumnordinal-transact-sql"></a>sys.fn_cdc_get_column_ordinal(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  에 표시 된 것으로 지정 된 열의 열 서 수는 반환 된 [변경 테이블](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) 지정한 캡처 인스턴스와 연결 된 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_cdc_get_column_ordinal ( 'capture_instance','column_name')  
```  
  
## <a name="arguments"></a>인수  
 **'** *capture_instance* **'**  
 지정된 열이 캡처된 열로 식별된 캡처 인스턴스의 이름입니다. *capture_instance* 은 **sysname**합니다.  
  
 **'** *column_name* **'**  
 보고할 열입니다. *column_name* 은 **sysname**합니다.  
  
## <a name="return-type"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>주의  
 이 함수는 변경 데이터 캡처 업데이트 마스크에서 캡처된 열의 서수 위치를 식별하는 함수로, 함수와 함께에 주로 사용은 [sys.fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) 변경 데이터를 쿼리할 때 업데이트 마스크에서 정보를 추출 하 합니다.  
  
## <a name="permissions"></a>Permissions  
 원본 테이블의 모든 캡처된 열에 대해 SELECT 권한이 필요합니다. 캡처 인스턴스에 대해 변경 데이터 캡처 구성 요소의 데이터베이스 역할이 지정되어 있으면 해당 역할의 멤버 자격도 필요합니다.  
  
## <a name="examples"></a>예  
 다음은 `VacationHours` 캡처 인스턴스에 대한 업데이트 마스크에서 `HumanResources_Employee` 열의 서수 위치를 가져오는 예입니다. 이 값은 반환된 업데이트 마스크에서 정보를 추출하기 위해 `sys.fn_cdc_is_bit_set`에 대한 호출에 사용됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10),  @VacationHoursOrdinal int;  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HumanResources_Employee');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SET @VacationHoursOrdinal = sys.fn_cdc_get_column_ordinal   
    ( 'HumanResources_Employee','VacationHours');  
SELECT *, sys.fn_cdc_is_bit_set(@VacationHoursOrdinal,  
    __$update_mask) as 'VacationHours'  
FROM cdc.fn_cdc_get_net_changes_HumanResources_Employee  
    ( @from_lsn, @to_lsn, 'all with mask');  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [변경 데이터 캡처 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)   
 [변경 데이터 캡처 정보&#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [sys.sp_cdc_help_change_data_capture &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [sys.sp_cdc_get_captured_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)   
 [sys.fn_cdc_is_bit_set &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md)  
  
  

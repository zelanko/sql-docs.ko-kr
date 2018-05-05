---
title: sys.fn_cdc_get_min_lsn (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- sys.fn_cdc_get_min_lsn
- fn_cdc_get_min_lsn
- fn_cdc_get_min_lsn_TSQL
- sys.fn_cdc_get_min_lsn_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_min_lsn
- sys.fn_cdc_get_min_lsn
ms.assetid: bd49e28a-128b-4f6b-8545-6a2ec3f4afb3
caps.latest.revision: 17
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 291d1410a6a75fd8045cb6ddc7daacf576ac14ff
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysfncdcgetminlsn-transact-sql"></a>sys.fn_cdc_get_min_lsn(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 캡처 인스턴스에 대 한 start_ls 열 값을 반환 합니다.는 [cdc.change_tables](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md) 시스템 테이블입니다. 이 값은 캡처 인스턴스에 대한 유효성 간격의 하위 끝점을 나타냅니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_cdc_get_min_lsn ( 'capture_instance_name' )  
```  
  
## <a name="arguments"></a>인수  
 **'** *capture_instance_name* **'**  
 캡처 인스턴스의 이름입니다. *capture_instance_name* 은 **sysname**합니다.  
  
## <a name="return-types"></a>반환 형식  
 **binary(10)**  
  
## <a name="remarks"></a>주의  
 캡처 인스턴스가 없거나 호출자가 캡처 인스턴스와 관련된 변경 데이터에 액세스할 권한이 없는 경우 0x00000000000000000000을 반환합니다.  
  
 이 함수는 일반적으로 캡처 인스턴스와 관련된 변경 데이터 캡처 시간대의 하위 끝점을 식별하는 데 사용됩니다. 또한 이 함수를 사용하면 변경 데이터를 요청하기 전에 쿼리 범위의 끝점이 캡처 인스턴스 시간대 내에 있는지 확인할 수 있습니다. 변경 테이블에서 정리가 수행될 때 캡처 인스턴스의 하위 끝점이 변경되므로 이러한 확인을 거치는 것이 중요합니다. 변경 데이터 요청 사이의 시간이 긴 경우 이전 변경 데이터 요청의 상위 끝점으로 설정된 하위 끝점이라도 현재 시간대를 벗어날 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 sysadmin 고정 서버 역할 또는 db_owner 고정 데이터베이스 역할의 멤버여야 합니다. 다른 모든 사용자의 경우 원본 테이블에서 캡처된 모든 열에 대한 SELECT 권한이 필요하며 캡처 인스턴스에 대한 제어 역할이 정의된 경우 해당 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-minimum-lsn-value-for-a-specified-capture-instance"></a>1. 지정된 캡처 인스턴스에 대한 최소 LSN 값 반환  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `HumanResources_Employee` 캡처 인스턴스에 대한 최소 LSN 값을 반환합니다.  
  
```  
USE AdventureWorks2-12;  
GO  
SELECT sys.fn_cdc_get_min_lsn ('HumanResources_Employee')AS min_lsn;  
  
```  
  
### <a name="b-verifying-the-low-endpoint-of-a-query-range"></a>2. 쿼리 범위의 하위 끝점 확인  
 다음 예에서는 `sys.fn_cdc_get_min_lsn`에서 반환된 최소 LSN 값을 사용하여 변경 데이터 쿼리에 대해 제안된 하위 끝점이 `HumanResources_Employee` 캡처 인스턴스의 현재 시간대에 유효한지 확인합니다. 이 예에서는 캡처 인스턴스에 대한 이전 상위 끝점 LSN이 저장되었고 `@save_to_lsn` 변수를 설정하는 데 사용할 수 있다고 가정합니다. 설명을 위해 오류 처리 섹션이 실행되도록 예의 `@save_to_lsn`은 0x000000000000000000으로 설정되어 있습니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @min_lsn binary(10), @from_lsn binary(10),@save_to_lsn binary(10), @to_lsn binary(10);  
-- Sets @save_to_lsn to the previous high endpoint saved from the last change data request.  
SET @save_to_lsn = 0x000000000000000000;  
-- Sets the upper endpoint for the query range to the current maximum LSN.  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
-- Sets the @min_lsn parameter to the current minimum LSN for the capture instance.  
SET @min_lsn = sys.fn_cdc_get_min_lsn ('HumanResources_Employee');  
-- Sets the low endpoint for the query range to the LSN that follows the previous high endpoint.  
SET @from_lsn = sys.fn_cdc_increment_lsn(@save_to_lsn);  
-- Tests to verify the low endpoint is valid for the current capture instance.  
IF (@from_lsn < @min_lsn)  
    BEGIN  
        RAISERROR('Low endpoint of the request interval is invalid.', 16, -1);  
    END  
ELSE  
-- Return the changes occurring within the query range.  
    SELECT * FROM cdc.fn_cdc_get_all_changes_HumanResources_Employee(@from_lsn, @to_lsn, 'all');  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.fn_cdc_get_max_lsn &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md)   
 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)  
  
  

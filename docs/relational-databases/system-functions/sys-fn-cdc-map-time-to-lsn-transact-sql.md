---
title: sys.fn_cdc_map_time_to_lsn (Transact SQL) | Microsoft Docs
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
- sys.fn_cdc_map_time_to_lsn
- fn_cdc_map_time_to_lsn_TSQL
- sys.fn_cdc_map_time_to_lsn_TSQL
- fn_cdc_map_time_to_lsn
dev_langs: TSQL
helpviewer_keywords:
- fn_cdc_map_time_to_lsn
- sys.fn_cdc_map_time_to_lsn
ms.assetid: 6feb051d-77ae-4c93-818a-849fe518d1d4
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 593d3b93d9cb9300087c4427d7881636a16aee61
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysfncdcmaptimetolsn-transact-sql"></a>sys.fn_cdc_map_time_to_lsn(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로그 시퀀스 번호 (LSN) 값을 반환는 **start_lsn** 열에는 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) 시스템 테이블에 지정된 된 시간입니다. 이 함수를 사용 하 여 변경 데이터 캡처 열거 함수에 필요한 LSN 기반 범위로 날짜/시간 범위를 체계적으로 매핑할 [cdc.fn_cdc_get_all_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) 및 [cdc.fn _cdc_get_net_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) 범위 내에서 데이터 변경 내용을 반환 하도록 합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_cdc_map_time_to_lsn ( '<relational_operator>', tracking_time )  
  
<relational_operator> ::=  
{  largest less than  
 | largest less than or equal  
 | smallest greater than  
 | smallest greater than or equal  
}  
```  
  
## <a name="arguments"></a>인수  
 **'**< relational_operator >**'** {보다 작은 가장 큰 | 보다 작은 가장 큰 크거나 | 보다 큰 가장 작은 | 최소 크기 보다 크거나 같은}  
 내에 있는 고유한 LSN 값을 식별 하는 데 사용 되는 **cdc.lsn_time_mapping** 가 연결 된 테이블 **tran_end_time** 비교 했을 때 관계를 충족 하는 *tracking_time*  값입니다.  
  
 *relational_operator* 은 **nvarchar (30)**합니다.  
  
 *tracking_time*  
 대조할 날짜/시간 값입니다. *tracking_time* 은 **datetime**합니다.  
  
## <a name="return-type"></a>반환 형식  
 **binary(10)**  
  
## <a name="remarks"></a>주의  
 이해 하는 방법을 **sys.fn_cdc_map_time_lsn** 는 날짜/시간 범위를 LSN 범위 매핑할 다음 시나리오를 고려 하는 데 사용할 수 있습니다. 변경 데이터를 매일 추출하려는 고객이 있다고 가정해 보십시오. 즉, 고객은 지정된 날에 자정까지(자정 포함)의 변경 내용만 원합니다. 시간 범위의 하한은 전날 자정까지이며 자정은 포함하지 않습니다. 상한은 지정된 날의 자정까지이며 자정도 포함합니다. 다음 예제에서는 어떻게 함수 **sys.fn_cdc_map_time_to_lsn** 변경 데이터 캡처 열거 함수 모두 반환 하는 데 필요한 LSN 기반 범위로이 시간 기반 범위를 체계적으로 매핑하여 데 사용할 수 있습니다 해당 범위 내의 변경 됩니다.  
  
 `DECLARE @begin_time datetime, @end_time datetime, @begin_lsn binary(10), @end_lsn binary(10);`  
  
 `SET @begin_time = '2007-01-01 12:00:00.000';`  
  
 `SET @end_time = '2007-01-02 12:00:00.000';`  
  
 `SELECT @begin_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than', @begin_time);`  
  
 `SELECT @end_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);`  
  
 `SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@begin_lsn, @end_lsn, 'all` `');`  
  
 전날 자정 이후에 발생한 변경으로만 제한하기 위해 관계형 연산자 '`smallest greater than`'이 사용되었습니다. 여러 항목을 서로 다른 LSN 값을 공유 하는 경우는 **tran_end_time** 값의 하 한으로 식별 되는 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) 테이블 함수 보장 하는 가장 작은 LSN이 반환 됩니다 모든 항목이 포함 됩니다. 상한에 관계형 연산자에 대 한 '`largest less than or equal to`' 자정 포함 한 날에 대 한 범위에 모든 항목에 포함 되는지 확인 하는 데 사용 되는 **tran_end_time** 값입니다. 여러 항목을 서로 다른 LSN 값을 공유 하는 경우는 **tran_end_time** 값 함수 상한으로 식별 되는 모든 항목이 포함 되도록 가장 큰 LSN이 반환 됩니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 `sys.fn_cdc_map_time_lsn` 의 어떤 행이 있는지 여부를 결정 하는 함수는 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) 테이블에 **tran_end_time** 값 보다 크거나 같음 자정입니다. 예를 들어 이 쿼리는 캡처 프로세스가 전날 자정 때까지 커밋된 변경 내용을 이미 처리했는지 확인하여 해당 일의 변경 데이터 추출을 계속 진행하는 데 사용할 수 있습니다.  
  
```  
DECLARE @extraction_time datetime, @lsn binary(10);  
SET @extraction_time = '2007-01-01 12:00:00.000';  
SELECT @lsn = sys.fn_cdc_map_time_to_lsn ('smallest greater than or equal', @extraction_time);  
IF @lsn IS NOT NULL  
BEGIN  
<some action>  
END  
```  
  
## <a name="see-also"></a>관련 항목:  
 [cdc.lsn_time_mapping &#40; Transact SQL &#41;](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)   
 [sys.fn_cdc_map_lsn_to_time &#40; Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60; capture_instance& &#62; &#40; Transact SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60; capture_instance& &#62;  &#40; Transact SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  

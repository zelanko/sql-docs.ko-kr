---
description: sys.fn_cdc_map_time_to_lsn(Transact-SQL)
title: sys. fn_cdc_map_time_to_lsn (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_map_time_to_lsn
- fn_cdc_map_time_to_lsn_TSQL
- sys.fn_cdc_map_time_to_lsn_TSQL
- fn_cdc_map_time_to_lsn
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_map_time_to_lsn
- sys.fn_cdc_map_time_to_lsn
ms.assetid: 6feb051d-77ae-4c93-818a-849fe518d1d4
author: rothja
ms.author: jroth
ms.openlocfilehash: 638bf2b99069c718e4e84ab0ccc888300a56bc68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427885"
---
# <a name="sysfn_cdc_map_time_to_lsn-transact-sql"></a>sys.fn_cdc_map_time_to_lsn(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  지정 된 시간 동안 [cdc. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) 시스템 테이블의 **START_LSN** 열에서 LSN (로그 시퀀스 번호) 값을 반환 합니다. 이 함수를 사용 하 여 날짜/시간 범위를 변경 데이터 캡처 열거 함수 cdc에 필요한 LSN 기반 범위에 체계적으로 매핑할 수 있습니다. [fn_cdc_get_all_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) 및 [cdc. ](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) fn_cdc_get_net_changes_<capture_instance>하 여 해당 범위 내에서 데이터 변경 내용을 반환 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 **'**<relational_operator>**'** {가장 크거나 같은 가장 작은 값 보다 작거나 같음 \| \| \| }  
 는 *tracking_time* 값과 비교 했을 때 관계를 충족 하는 연결 된 **tran_end_time** 를 사용 하 여 **cdc. LSN_TIME_MAPPING** 테이블 내에서 고유 LSN 값을 식별 하는 데 사용 됩니다.  
  
 *relational_operator* 은 **nvarchar (30)** 입니다.  
  
 *tracking_time*  
 대조할 날짜/시간 값입니다. *tracking_time* 은 **datetime**입니다.  
  
## <a name="return-type"></a>반환 형식  
 **binary(10)**  
  
## <a name="remarks"></a>설명  
 **Fn_cdc_map_time_lsn** 를 사용 하 여 datetime 범위를 lsn 범위에 매핑할 수 있는 방법을 이해 하려면 다음 시나리오를 고려 하십시오. 변경 데이터를 매일 추출하려는 고객이 있다고 가정해 보십시오. 즉, 고객은 지정된 날에 자정까지(자정 포함)의 변경 내용만 원합니다. 시간 범위의 하한은 전날 자정까지이며 자정은 포함하지 않습니다. 상한은 지정된 날의 자정까지이며 자정도 포함합니다. 다음 예에서는 **fn_cdc_map_time_to_lsn** 함수를 사용 하 여이 시간 기반 범위를 변경 데이터 캡처 열거 함수에서 필요한 lsn 기반 범위에 체계적으로 매핑하여 해당 범위 내의 모든 변경 내용을 반환 하는 방법을 보여 줍니다.  
  
 `DECLARE @begin_time datetime, @end_time datetime, @begin_lsn binary(10), @end_lsn binary(10);`  
  
 `SET @begin_time = '2007-01-01 12:00:00.000';`  
  
 `SET @end_time = '2007-01-02 12:00:00.000';`  
  
 `SELECT @begin_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than', @begin_time);`  
  
 `SELECT @end_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);`  
  
 `SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@begin_lsn, @end_lsn, 'all` `');`  
  
 전날 자정 이후에 발생한 변경으로만 제한하기 위해 관계형 연산자 '`smallest greater than`'이 사용되었습니다. LSN 값이 서로 다른 여러 항목이 [cdc. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) 테이블의 하 한 **tran_end_time** 값을 공유 하는 경우 함수는 모든 항목이 포함 되도록 가장 작은 LSN을 반환 합니다. 상한에 대해 ' ' 관계 연산자를 사용 하 여 해당 범위에 tran_end_time 값으로 자정을 포함 하는 항목을 포함 하 여 해당 `largest less than or equal to` 날짜의 모든 **tran_end_time** 항목을 포함 하는지 확인 합니다. LSN 값이 서로 다른 여러 항목이 상한으로 식별 된 **tran_end_time** 값을 공유 하는 경우 함수는 모든 항목이 포함 되도록 가장 큰 LSN을 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 함수를 사용 하 여 `sys.fn_cdc_map_time_lsn` [lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) 테이블에 자정 보다 크거나 같은 **tran_end_time** 값이 있는 행이 있는지 여부를 확인 합니다. 예를 들어 이 쿼리는 캡처 프로세스가 전날 자정 때까지 커밋된 변경 내용을 이미 처리했는지 확인하여 해당 일의 변경 데이터 추출을 계속 진행하는 데 사용할 수 있습니다.  
  
```  
DECLARE @extraction_time datetime, @lsn binary(10);  
SET @extraction_time = '2007-01-01 12:00:00.000';  
SELECT @lsn = sys.fn_cdc_map_time_to_lsn ('smallest greater than or equal', @extraction_time);  
IF @lsn IS NOT NULL  
BEGIN  
<some action>  
END  
```  
  
## <a name="see-also"></a>참고 항목  
 [lsn_time_mapping &#40;Transact-sql&#41;](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)   
 [fn_cdc_map_lsn_to_time &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)   
 [fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  

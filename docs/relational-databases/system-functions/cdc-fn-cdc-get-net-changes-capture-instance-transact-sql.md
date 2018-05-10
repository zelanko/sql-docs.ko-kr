---
title: cdc.fn_cdc_get_net_changes_&lt;capture_instance&gt; (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_net_changes_<capture_instance>
- change data capture [SQL Server], querying metadata
- cdc.fn_cdc_get_net_changes_<capture_instance>
ms.assetid: 43ab0d1b-ead4-471c-85f3-f6c4b9372aab
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d4f66b0608afcfa883f4e12d0e3dfe39e8bf7512
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="cdcfncdcgetnetchangesltcaptureinstancegt-transact-sql"></a>cdc.fn_cdc_get_net_changes_&lt;capture_instance&gt; (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  에 대 한 지정된 된 로그 시퀀스 번호 (LSN) 범위 내에서 변경 된 각 원본 행당 하나의 순 변경 행을 반환 합니다.  
  
 **대기 LSN 이란?** 모든 레코드는 [SQL Server 트랜잭션 로그](../logs/the-transaction-log-sql-server.md) 로그 시퀀스 번호 (LSN)으로 고유 하 게 식별 됩니다. LSN2 LSN1 보다 큰 경우 로그 레코드 LSN2에서 참조 하 여 발생 한 되도록 Lsn은 정렬 **후** 변경이 이후에 로그 레코드 LSN입니다.  
  
 중요 한 이벤트가 발생 한 로그 레코드의 LSN은 올바른 복원 시퀀스를 생성 하는 것에 대 한 유용할 수 있습니다. Lsn은 정렬 하기 때문에 같음 또는 같지 않음을 비교할 수 있습니다 (즉, \<, >, =, \<=, > =) 합니다. 이러한 비교 방식은 복원 시퀀스를 만들 때 유용하게 사용할 수 있습니다.  
  
 원본 행에 있는 LSN 범위 동안 여러 번 변경 된 경우 행의 최종 내용을 반영 하는 단일 행 아래에 설명 된 열거 함수에 의해 반환 됩니다. 예를 들어 트랜잭션이 원본 테이블의 행을 삽입 하 고 LSN 범위 내의 후속 트랜잭션이 해당 행의 하나 이상의 열을 업데이트, 함수 반환만 **하나의** 업데이트 된 열 값을 포함 하는 행이 있습니다.  
  
 이 열거 함수는 원본 테이블에 변경 데이터 캡처를 사용하도록 설정되어 있고 순 변경 추적이 지정된 경우에 생성됩니다. 순 변경 추적을 사용하려면 원본 테이블에 기본 키 또는 고유 인덱스가 있어야 합니다. 함수 이름을 파생 되 고 형식 cdc.fn_cdc_get_net_changes_를 사용 하 여*capture_instance*여기서 *capture_instance* 원본 테이블이 때 캡처 인스턴스에 대해 지정 된 값이 변경 데이터 캡처를 사용할 수 있습니다. 자세한 내용은 참조 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
cdc.fn_cdc_get_net_changes_capture_instance ( from_lsn , to_lsn , '<row_filter_option>' )  
  
<row_filter_option> ::=  
{ all  
 | all with mask  
 | all with merge  
}  
```  
  
## <a name="arguments"></a>인수  
 *from_lsn*  
 결과 집합에 포함할 LSN 범위의 하위 끝점을 나타내는 LSN입니다. *from_lsn* 은 **binary (10)** 합니다.  
  
 행만 [cdc.&#91; capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) 보다 크거나 __ $start_lsn의 값이 있는 테이블을 변경 *from_lsn* 결과 집합에 포함 됩니다.  
  
 *to_lsn*  
 결과 집합에 포함할 LSN 범위의 상위 끝점을 나타내는 LSN입니다. *to_lsn* 은 **binary (10)** 합니다.  
  
 행만 [cdc.&#91; capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) __ $start_lsn의 작은 보다 작거나 값이 있는 테이블을 변경 *from_lsn* 같음 *to_lsn* 결과 집합에 포함 됩니다.  
  
 *< row_filter_option >* :: = {모든 | 마스크가 포함 된 모두 | 병합을 통해 모든}  
 결과 집합에 반환되는 행과 메타데이터 열의 내용을 제어하는 옵션입니다. 다음 옵션 중 하나를 사용할 수 있습니다.  
  
 all  
 행 및 메타 데이터 열 __ $start_lsn의 행을 적용 하는 데 필요한 작업에 마지막 변경의 LSN을 반환 하 고 \_ \_$operation 합니다. 열 \_ \_$update_mask는 항상 NULL입니다.  
  
 all with mask  
 행 및 메타 데이터 열 __ $start_lsn의 행을 적용 하는 데 필요한 작업에 마지막 변경의 LSN을 반환 하 고 \_ \_$operation 합니다. 또한 업데이트 작업이 반환 하는 경우 (\_\_$operation = 4)는 업데이트에서 수정 된 캡처된 열에 반환 된 값에 표시 되어 \_ \_$update_mask 합니다.  
  
 all with merge  
 메타데이터 열 __$start_lsn에서 해당 행의 마지막 변경에 대한 LSN을 반환합니다. 열 \_ \_$operation 두 값 중 하나가 됩니다: 1은 삭제 이며 5는 변경을 적용 하는 데 필요한 작업이 삽입 또는 업데이트 중 하나 임을 나타냅니다. 열 \_ \_$update_mask는 항상 NULL입니다.  
  
 지정된 변경에 대한 정확한 작업을 확인하는 논리를 사용하면 쿼리의 복잡성이 가중되므로 경우에 따라 이 옵션을 통해 쿼리 성능을 향상시킬 수 있습니다. 변경 데이터를 적용하는 데 필요한 작업이 삽입 또는 업데이트 중 하나임을 나타내는 것으로 충분하여 두 작업을 명시적으로 구별할 필요가 없을 경우가 이에 속합니다. 이 옵션은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 환경과 같이 병합 작업을 직접 사용할 수 있는 대상 환경에 가장 유용합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|__$start_lsn|**binary(10)**|변경에 대한 커밋 트랜잭션과 연관된 LSN입니다.<br /><br /> 동일한 트랜잭션에서 커밋된 변경의 커밋 LSN은 모두 동일합니다. 예를 들어 업데이트 작업의 원본 테이블에 두 행의 두 열이 수정, 변경 테이블에 동일한 __ $start_lsnvalue는 4 개 행 포함 됩니다.|  
|__$operation|**int**|변경 데이터의 행을 대상 데이터 원본에 적용하는 데 필요한 DML(데이터 조작 언어) 작업을 식별합니다.<br /><br /> row_filter_option 매개 변수의 값이 all 또는 all with mask일 경우 이 열의 값은 다음 값 중 하나일 수 있습니다.<br /><br /> 1 = 삭제<br /><br /> 2 = 삽입<br /><br /> 4 = 업데이트<br /><br /> row_filter_option 매개 변수의 값이 all with merge일 경우 이 열의 값은 다음 값 중 하나일 수 있습니다.<br /><br /> 1 = 삭제|  
|__$update_mask|**varbinary(128)**|캡처 인스턴스에 대해 식별된 각 캡처된 열에 해당하는 비트가 있는 비트 마스크입니다. 이 값에는 __$operation이 1 또는 2인 경우 모두 1로 설정되는 정의된 비트가 있습니다. 때 \_ \_$operation = 3 또는 4, 변경 된 열에 해당 하는 비트만 1로 설정 됩니다.|  
|*\<captured source table columns>*|다양함|함수에서 반환되는 나머지 열은 캡처 인스턴스 생성 시 캡처된 열로 식별된 원본 테이블의 열입니다. 캡처된 열 목록에 아무 열도 지정하지 않으면 원본 테이블의 모든 열이 반환됩니다.|  
  
## <a name="permissions"></a>Permissions  
 sysadmin 고정 서버 역할 또는 db_owner 고정 데이터베이스 역할의 멤버여야 합니다. 다른 모든 사용자의 경우 원본 테이블에서 캡처된 모든 열에 대한 SELECT 권한이 필요하며 캡처 인스턴스에 대한 제어 역할이 정의된 경우 해당 데이터베이스 역할의 멤버 자격이 필요합니다. 호출자에게 원본 데이터를 볼 수 있는 권한이 없으면 함수는 오류 208(개체 이름이 잘못되었습니다)을 반환합니다.  
  
## <a name="remarks"></a>주의  
 지정된 LSN 범위가 캡처 인스턴스에 대한 변경 추적 시간대를 벗어나는 경우 함수는 오류 208(개체 이름이 잘못되었습니다)을 반환합니다.

 행의 고유 식별자에 수정 fn_cdc_get_net_changes를 DELETE 사용 하 여 초기 업데이트 명령을 표시 하 고 다음 명령을 대신 삽입 하면 됩니다.  이 동작은 이전과 이후에 변경 된 키를 추적 해야 합니다.
  
## <a name="examples"></a>예  
 다음 예제에서는 함수를 사용 하 여 `cdc.fn_cdc_get_net_changes_HR_Department` 원본 테이블에 대 한 순 변경을 보고를 `HumanResources.Department` 특정 시간 간격 동안 합니다.  
  
 먼저 `GETDATE` 함수를 사용하여 시간 간격의 시작을 표시합니다. 원본 테이블에 여러 DML 문이 적용된 후 `GETDATE` 함수를 다시 호출하여 시간 간격의 끝을 식별합니다. 함수 [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) LSN 값에 의해 제한 변경 데이터 캡처 쿼리 범위에 시간 간격을 매핑할 사용 됩니다. 마지막으로 `cdc.fn_cdc_get_net_changes_HR_Department` 함수를 쿼리하여 원본 테이블에서 해당 시간 간격에 수행된 순 변경을 가져옵니다. 삽입된 후 삭제된 행은 함수가 반환하는 결과 집합에 나타나지 않습니다. 쿼리 창 내에서 추가된 후 삭제된 행은 원본 테이블에서 시간 간격 동안 순 변경을 생성하지 않기 때문입니다. 이 예제를 실행 하기 전에 먼저의 예제 B를 실행 해야 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @begin_time datetime, @end_time datetime, @from_lsn binary(10), @to_lsn binary(10);  
-- Obtain the beginning of the time interval.  
SET @begin_time = GETDATE() -1;  
-- DML statements to produce changes in the HumanResources.Department table.  
INSERT INTO HumanResources.Department (Name, GroupName)  
VALUES (N'MyDept', N'MyNewGroup');  
  
UPDATE HumanResources.Department  
SET GroupName = N'Resource Control'  
WHERE GroupName = N'Inventory Management';  
  
DELETE FROM HumanResources.Department  
WHERE Name = N'MyDept';  
  
-- Obtain the end of the time interval.  
SET @end_time = GETDATE();  
-- Map the time interval to a change data capture query range.  
SET @from_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than or equal', @begin_time);  
SET @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);  
  
-- Return the net changes occurring within the query window.  
SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@from_lsn, @to_lsn, 'all');  
```  
  
## <a name="see-also"></a>관련 항목:  
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_map_time_to_lsn &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [변경 데이터 캡처 정보&#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  

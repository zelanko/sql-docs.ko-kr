---
title: sys.fn_net_changes_&lt;capture_instance&gt; (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- sys.fn_net_changes_TSQL
- fn_net_changes_TSQL
- fn_net_changes
- sys.fn_net_changes
dev_langs:
- TSQL
helpviewer_keywords:
- fn_net_changes_<capture_instance>
- sys.fn_net_changes_<capture_instance>
ms.assetid: 342fa030-9fd9-4b74-ae4d-49f6038a5073
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a822cb52d98fec1e0d531c09fa3d138d07757cb8
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysfnnetchangesltcaptureinstancegt-transact-sql"></a>sys.fn_net_changes_&lt;capture_instance&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  에 대 한 래퍼는 **순 변경 내용을** 함수를 쿼리 합니다. 이러한 함수를 만드는 데 필요한 스크립트는 sys.sp_cdc_generate_wrapper_function 저장 프로시저에 의해 생성됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
fn_net_changes_<capture_instance> ('start_time', 'end_time', '<row_filter_option>' )  
  
<capture_instance> ::= The name of the capture instance.  
<row_filter_option> ::=  
{ all  
  | all with mask  
  | all with merge  
}  
```  
  
## <a name="arguments"></a>인수  
 *start_time*  
 **datetime** 결과 집합에 포함할 변경 테이블 항목 범위의 하위 끝점을 나타내는 값입니다.  
  
 연결된 된 커밋 시간이 보다 엄격 하 게 크고가 테이블을 변경 하는 cdc. < capture_instance > _CT의 행만 *start_time* 결과 집합에 포함 됩니다.  
  
 이 인수에 값 NULL을 제공하면 쿼리 범위의 하위 끝점이 캡처 인스턴스에 대해 유효한 범위의 하위 끝점에 대응됩니다.  
  
 *end_time*  
 **datetime** 결과 집합에 포함할 변경 테이블 항목 범위의 상위 끝점을 나타내는 값입니다.  
  
 이 매개 변수 수에 대해 선택한 값에 따라 다음 두 가지 의미 중 하나를 사용할 @closed_high_end_point 래퍼 함수를 만드는 스크립트를 생성 하기 위해 sys.sp_cdc_generate_wrapper_function을 호출할 경우:  
  
-   @closed_high_end_point = 1  
  
     값이 있는 테이블을 변경 하는 cdc. < capture_instance > _CT의 행만 \_ \_$start_lsn 및 해당 커밋 시간 보다 작거나 **start_time** 결과 집합에 포함 됩니다.  
  
-   @closed_high_end_point = 0  
  
     값이 있는 테이블을 변경 하는 cdc. < capture_instance > _CT의 행만 \_ \_$start_lsn 및 해당 커밋 시간이 미만 **start_time** 결과 집합에 포함 됩니다.  
  
 이 인수에 값 NULL을 제공하면 쿼리 범위의 상위 끝점이 캡처 인스턴스에 대해 유효한 범위의 상위 끝점에 대응됩니다.  
  
 *< row_filter_option >* :: = {모든 | 마스크가 포함 된 모두 | 병합을 통해 모든}  
 결과 집합에 반환되는 행과 메타데이터 열의 내용을 제어하는 옵션입니다. 다음 옵션 중 하나를 사용할 수 있습니다.  
  
 all  
 내용 열에서 변경된 행의 최종 내용은 물론 메타데이터 열 __CDC_OPERATION에서 해당 행을 적용하는 데 필요한 작업을 반환합니다.  
  
 all with mask  
 내용 열에서 변경된 모든 행의 최종 내용은 물론 메타데이터 열 __CDC_OPERATION에서 각 행을 적용하는 데 필요한 작업을 반환합니다. 래퍼 함수를 만드는 스크립트를 생성할 때 업데이트 플래그 목록이 지정되면 업데이트 마스크를 채우기 위해 이 옵션이 필요합니다.  
  
 all with merge  
 내용 열에서 변경된 모든 행의 최종 내용을 반환합니다.  
  
 __CDC_OPERATION 열은 다음 두 값 중 하나입니다.  
  
-   D - 행을 삭제해야 하는 경우  
  
-   M - 행을 삽입하거나 업데이트해야 하는 경우  
  
 대상에 변경 내용을 적용하는 데 삽입 또는 업데이트 작업이 필요한지 여부를 결정하는 논리를 사용하면 쿼리가 더 복잡해집니다. 삽입 작업과 업데이트 작업을 구분할 필요가 없는 경우 성능을 향상시키려면 이 옵션을 사용합니다. 이 방법은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 환경과 같이 병합 작업을 직접 사용할 수 있는 대상 환경에 가장 유용합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|열 유형|Description|  
|-----------------|-----------------|-----------------|  
|\<열을 @column_list>|**varies**|식별 되는 열은 **column_list** sp_cdc_generate_wrapper_function 래퍼를 만드는 스크립트를 생성 하 라고 하는 경우에 인수입니다. 경우 *column_list* 가 null 인 경우 모든 추적 된 원본 열은 결과 집합에 표시 됩니다.|  
|__CDC_OPERATION|**nvarchar(2)**|행을 대상 환경에 적용하는 데 필요한 작업을 나타내는 작업 코드입니다. 작업 인수의 값에 따라 달라 집니다 *row_filter_option* 다음 호출에 제공 되는:<br /><br /> *row_filter_option* 'all', 'all with mask' =<br /><br /> 'D' - 삭제 작업<br /><br /> 'I' - 삽입 작업<br /><br /> 'UN' - 업데이트 작업<br /><br /> *row_filter_option* 'all with merge' =<br /><br /> 'D' - 삭제 작업<br /><br /> 'M' - 삭제 작업 또는 업데이트 작업|  
|\<열을 @update_flag_list>|**bit**|_uflag를 열 이름에 추가하여 이름을 지정한 비트 플래그입니다. 플래그는 null이 아닌 값에는 경우에만 *row_filter_option* **'all with mask' =** 및 \__CDC_OPERATION **= ' u N '**합니다. 쿼리 창 내에서 해당 열이 수정된 경우 이 플래그는 1로 설정됩니다. 그렇지 않으면 0입니다.|  
  
## <a name="remarks"></a>주의  
 fn_net_changes_<capture_instance> 함수는 cdc.fn_cdc_get_net_changes_<capture_instance> 쿼리 함수의 래퍼 역할을 합니다. 래퍼를 만드는 스크립트를 생성하는 데에는 sys.sp_cdc_generate_wrapper 저장 프로시저가 사용됩니다.  
  
 래퍼 함수는 자동으로 만들어지지 않습니다. 래퍼 함수를 만들려면 다음 두 작업을 수행해야 합니다.  
  
1.  래퍼 생성 스크립트를 만드는 저장 프로시저를 실행합니다.  
  
2.  래퍼 함수를 실제로 만드는 스크립트를 실행합니다.  
  
 래퍼 함수에 의해 제한 간격 내에 발생 한 변경 내용을 체계적으로 쿼리할 수 있도록 **datetime** LSN 값 대신 값입니다. 래퍼 함수는 제공 된 간에 필요한 모든 변환을 수행 합니다. **datetime** 값과 쿼리 함수에 대 한 인수로 서 내부적으로 필요한 LSN 값입니다. 변경 데이터 스트림을 처리하기 위해 래퍼 함수가 직렬로 사용된 경우 특정 호출과 연결된 간격의 @end_time 값이 후속 호출과 연결된 간격의 @start_time 값으로 제공된다는 규칙을 준수하면 데이터가 손실되거나 반복되지 않습니다.  
  
 스크립트를 만들 때 @closed_high_end_point 매개 변수를 사용하면 지정된 쿼리 창에서 닫힌 상한이나 열린 상한을 지원하는 래퍼를 생성할 수 있습니다. 즉, 커밋 시간이 추출 간격의 상한과 같은 항목을 간격에 포함할지 여부를 결정할 수 있습니다. 기본적으로 상한이 포함됩니다.  
  
 반환 된 결과 집합은 **순 변경 내용을** 추적 된 열에 있는 래퍼 함수가 반환은 @column_list 래퍼를 생성 하는 경우. @column_list가 NULL인 경우 추적된 모든 원본 열이 반환됩니다. 원본 열 뒤에는 작업을 식별하는 한 문자 또는 두 문자 열인 작업 열 __CDC_OPERATION이 옵니다.  
  
 결과 매개 변수에서 식별 된 각 열에 대 한 집합에 비트 플래그가 추가 다음 됩니다 @update_flag_list합니다. 에 대 한는 **순 변경 내용을** 래퍼의 경우 플래그는 항상 경우 NULL이 될는 @row_filter_option 즉 'all' 또는 'all with merge'는 래퍼 함수 호출에 사용 합니다. 경우는 @row_filter_option 'all with mask', 및 __CDC_OPERATION으로 설정에 ' 또는 'I' 인 플래그의 값도 NULL이 됩니다. 경우 \__CDC_OPERATION이 ' u N ', 1 또는 0 인지 여부에 따라 플래그를 설정 됩니다는 **net** 업데이트 작업 결과로 열이 변경 합니다.  
  
 변경 데이터 캡처 구성 템플릿 'Instantiate CDC Wrapper TVFs for Schema'에서는 sp_cdc_generate_wrapper_function 저장 프로시저를 사용하여 스키마에 정의된 쿼리 함수의 모든 래퍼 함수에 대한 CREATE 스크립트를 가져오는 방법을 보여 줍니다. 그런 다음 이 템플릿에서는 이러한 스크립트를 만듭니다. 서식 파일에 대 한 자세한 내용은 참조 [템플릿 탐색기](http://msdn.microsoft.com/library/b9ee55c5-bb44-4f76-90ac-792d8d83b4c8)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sys.sp_cdc_generate_wrapper_function &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60; capture_instance& &#62; &#40; Transact SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)  
  
  

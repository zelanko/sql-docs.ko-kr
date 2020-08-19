---
description: sys. fn_net_changes_ &lt; capture_instance &gt; (transact-sql)
title: sys. fn_net_changes_ &lt; capture_instance &gt; (transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 59d8214083046510d9c4d71724d1aab1c96b1e1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427765"
---
# <a name="sysfn_net_changes_ltcapture_instancegt-transact-sql"></a>sys. fn_net_changes_ &lt; capture_instance &gt; (transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Net changes** 쿼리 함수에 대 한 래퍼입니다. 이러한 함수를 만드는 데 필요한 스크립트는 sys.sp_cdc_generate_wrapper_function 저장 프로시저에 의해 생성됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 결과 집합에 포함할 변경 테이블 항목 범위의 하위 끝점을 나타내는 **datetime** 값입니다.  
  
 연결 된 커밋 시간이 *start_time* 보다 엄격 하 게 큰 cdc. <capture_instance>_CT 변경 테이블의 행만 결과 집합에 포함 됩니다.  
  
 이 인수에 값 NULL을 제공하면 쿼리 범위의 하위 엔드포인트가 캡처 인스턴스에 대해 유효한 범위의 하위 엔드포인트에 대응됩니다.  
  
 *end_time*  
 결과 집합에 포함할 변경 테이블 항목 범위의 상위 끝점을 나타내는 **datetime** 값입니다.  
  
 이 매개 변수는 두 가지 의미 중 하나를 사용할 수 있습니다 .이 값은 @closed_high_end_point sp_cdc_generate_wrapper_function가 호출 되어 래퍼 함수를 만드는 스크립트를 생성 합니다.  
  
-   @closed_high_end_point = 1  
  
     $Start _lsn 값을 포함 하는 cdc. <capture_instance>_CT 변경 테이블의 행만 \_ \_ 결과 집합에 포함 됩니다. **start_time**  
  
-   @closed_high_end_point = 0  
  
     $Start _lsn 값을 포함 하는 <capture_instance>_CT 변경 테이블의 행만 \_ \_ 결과 집합에 포함 된 **start_time** 보다 엄격 하 게 해당 커밋 시간을 포함 합니다.  
  
 이 인수에 값 NULL을 제공하면 쿼리 범위의 상위 엔드포인트가 캡처 인스턴스에 대해 유효한 범위의 상위 엔드포인트에 대응됩니다.  
  
 *<row_filter_option>* :: = {all | all | all with mask | all with merge}  
 결과 집합에 반환되는 행과 메타데이터 열의 내용을 제어하는 옵션입니다. 다음 옵션 중 하나를 사용할 수 있습니다.  
  
 모두  
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
  
|열 이름|열 유형|설명|  
|-----------------|-----------------|-----------------|  
|\<columns from @column_list>|**다름**|래퍼를 만드는 스크립트를 생성 하기 위해 호출 될 때 sp_cdc_generate_wrapper_function에 대 한 **column_list** 인수에서 식별 되는 열입니다. *COLUMN_LIST* NULL 인 경우 추적 된 모든 원본 열이 결과 집합에 표시 됩니다.|  
|__CDC_OPERATION|**nvarchar(2)**|행을 대상 환경에 적용하는 데 필요한 작업을 나타내는 작업 코드입니다. 작업은 다음 호출에서 제공 되는 *row_filter_option* 인수 값에 따라 달라 집니다.<br /><br /> *row_filter_option* = ' all ', ' all with mask '<br /><br /> 'D' - 삭제 작업<br /><br /> 'I' - 삽입 작업<br /><br /> 'UN' - 업데이트 작업<br /><br /> *row_filter_option* = ' all with merge '<br /><br /> 'D' - 삭제 작업<br /><br /> 'M' - 삭제 작업 또는 업데이트 작업|  
|\<columns from @update_flag_list>|**bit**|_uflag를 열 이름에 추가하여 이름을 지정한 비트 플래그입니다. 플래그는 *row_filter_option* **= ' all with mask '** 및 _CDC_OPERATION = ' u n ' 인 경우에만 null이 아닌 값을 사용 \_ 합니다. **= 'UN'** 쿼리 창 내에서 해당 열이 수정된 경우 이 플래그는 1로 설정됩니다. 그렇지 않으면 0입니다.|  
  
## <a name="remarks"></a>설명  
 Fn_net_changes_<capture_instance> 함수는 fn_cdc_get_net_changes_<capture_instance 쿼리 함수의 래퍼로 사용 됩니다. 래퍼를 만드는 스크립트를 생성하는 데에는 sys.sp_cdc_generate_wrapper 저장 프로시저가 사용됩니다.  
  
 래퍼 함수는 자동으로 만들어지지 않습니다. 래퍼 함수를 만들려면 다음 두 작업을 수행해야 합니다.  
  
1.  래퍼 생성 스크립트를 만드는 저장 프로시저를 실행합니다.  
  
2.  래퍼 함수를 실제로 만드는 스크립트를 실행합니다.  
  
 래퍼 함수를 사용 하면 사용자가 LSN 값 대신 **datetime** 값으로 제한 된 간격 내에서 발생 한 변경 내용을 체계적으로 쿼리할 수 있습니다. 래퍼 함수는 제공 된 **datetime** 값과 쿼리 함수의 인수로 내부적으로 필요한 LSN 값 사이에 필요한 모든 변환을 수행 합니다. 변경 데이터 스트림을 처리하기 위해 래퍼 함수가 직렬로 사용된 경우 특정 호출과 연결된 간격의 @end_time 값이 후속 호출과 연결된 간격의 @start_time 값으로 제공된다는 규칙을 준수하면 데이터가 손실되거나 반복되지 않습니다.  
  
 스크립트를 만들 때 @closed_high_end_point 매개 변수를 사용하면 지정된 쿼리 창에서 닫힌 상한이나 열린 상한을 지원하는 래퍼를 생성할 수 있습니다. 즉, 커밋 시간이 추출 간격의 상한과 같은 항목을 간격에 포함할지 여부를 결정할 수 있습니다. 기본적으로 상한이 포함됩니다.  
  
 **순 변경** 래퍼 함수에서 반환 되는 결과 집합은 @column_list 래퍼가 생성 될 때에 있던 추적 된 열만 반환 합니다. @column_list가 NULL인 경우 추적된 모든 원본 열이 반환됩니다. 원본 열 뒤에는 작업을 식별하는 한 문자 또는 두 문자 열인 작업 열 __CDC_OPERATION이 옵니다.  
  
 그런 다음 매개 변수에 식별 된 각 열에 대 한 결과 집합에 비트 플래그가 추가 됩니다 @update_flag_list . **Net changes** 래퍼의 경우 @row_filter_option 래퍼 함수 호출에 사용 된이 ' all ' 또는 ' all with merge ' 인 경우 비트 플래그는 항상 NULL이 됩니다. @row_filter_option가 ' all with mask '로 설정 되 고 __CDC_OPERATION이 ' d ' 또는 ' I ' 인 경우에도 플래그 값이 NULL입니다. _CDC_OPERATION ' u n ' 인 경우 \_ 이 플래그는 **net** update 작업으로 인해 열이 변경 되었는지 여부에 따라 1 또는 0으로 설정 됩니다.  
  
 변경 데이터 캡처 구성 템플릿 ' Schema 용 CDC 래퍼 Tvf 인스턴스화 '에서는 sp_cdc_generate_wrapper_function 저장 프로시저를 사용 하 여 스키마에 정의 된 쿼리 함수의 모든 래퍼 함수에 대 한 CREATE 스크립트를 가져오는 방법을 보여 줍니다. 그런 다음 이 템플릿에서는 이러한 스크립트를 만듭니다. 템플릿에 대 한 자세한 내용은 [템플릿 탐색기](../../ssms/template/template-explorer.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [sp_cdc_generate_wrapper_function &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)  
  
  

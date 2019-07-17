---
title: sys.fn_all_changes_&lt;capture_instance&gt; (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_all_changes
- sys.fn_all_changes
- fn_all_changes_TSQL
- sys.fn_all_changes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_all_changes_<capture_instance>
- sys.fn_all_changes_<capture_instance>
ms.assetid: 564fae96-b88c-4f22-9338-26ec168ba6f5
author: rothja
ms.author: jroth
ms.openlocfilehash: de589bbe1fe5f590ef3d75c884aae70b5276804a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140529"
---
# <a name="sysfnallchangesltcaptureinstancegt-transact-sql"></a>sys.fn_all_changes_&lt;capture_instance&gt; (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  에 대 한 래퍼를 **모든 변경 내용을** 함수를 쿼리 합니다. 이러한 함수를 만드는 데 필요한 스크립트는 sys.sp_cdc_generate_wrapper_function 저장 프로시저에 의해 생성됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
fn_all_changes_<capture_instance> ('start_time' ,'end_time', '<row_filter_option>' )  
  
<capture_instance> ::= The name of the capture instance.  
<row_filter_option> ::=  
{ all  
  | all update old  
}  
```  
  
## <a name="arguments"></a>인수  
 *start_time*  
 합니다 **날짜/시간** 결과 집합에 포함할 변경 테이블 항목 범위의 하위 끝점을 나타내는 값입니다.  
  
 연결된 된 커밋 시간이 보다 큰 테이블을 변경 하는 cdc. < capture_instance > _CT의 행만 *start_time* 결과 집합에 포함 됩니다.  
  
 이 인수에 값 NULL을 제공하면 쿼리 범위의 하위 엔드포인트가 캡처 인스턴스에 대해 유효한 범위의 하위 엔드포인트에 대응됩니다.  
  
 *end_time*  
 합니다 **날짜/시간** 결과 집합에 포함할 변경 테이블 항목 범위의 상위 끝점을 나타내는 값입니다.  
  
 이 매개 변수 수에 대해 선택한 값에 따라 두 가지 의미 중 하나에서 사용할 @closed_high_end_point 래퍼 함수에 대 한 create 스크립트를 생성 하기 위해 sys.sp_cdc_generate_wrapper_function을 합니다.  
  
-   @closed_high_end_point = 1  
  
     연결 된 커밋 시간이 같거나 end_time 있는 cdc. < capture_instance > _CT 변경 테이블의 행만 결과 집합에 포함 됩니다...  
  
-   @closed_high_end_point = 0  
  
     연결된 커밋 시간이 end_time 이전인 cdc.capture_instance_CT 변경 테이블의 행만 결과 집합에 포함됩니다.  
  
 이 인수에 값 NULL을 제공하면 쿼리 범위의 상위 엔드포인트가 캡처 인스턴스에 대해 유효한 범위의 상위 엔드포인트에 대응됩니다.  
  
 < row_filter_option >:: = {모든 | 모든 이전 업데이트}  
 결과 집합에 반환되는 메타데이터 열 및 행의 내용을 제어하는 옵션입니다.  
  
 다음 옵션 중 하나를 사용할 수 있습니다.  
  
 all  
 지정된 LSN 범위 내의 모든 변경을 반환합니다. 업데이트 작업으로 인해 발생하는 변경 내용의 경우 이 옵션을 사용하면 업데이트가 적용된 후의 새 값을 포함하는 행만 반환됩니다.  
  
 all update old  
 지정된 LSN 범위 내의 모든 변경을 반환합니다. 업데이트 작업으로 인해 발생하는 변경 내용의 경우 이 옵션을 사용하면 업데이트 전후의 열 값을 포함하는 두 개의 행이 반환됩니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|열 유형|설명|  
|-----------------|-----------------|-----------------|  
|__CDC_STARTLSN|**binary(10)**|변경 내용과 관련된 트랜잭션의 커밋 LSN입니다. 동일한 트랜잭션에서 커밋된 모든 변경 내용은 같은 커밋 LSN을 공유합니다.|  
|__CDC_SEQVAL|**binary(10)**|트랜잭션에서 행 변경 내용을 정렬하는 데 사용되는 시퀀스 값입니다.|  
|\<열에서 @column_list>|**달라 집니다.**|식별 되는 열을 *column_list* 대 sp_cdc_generate_wrapper_function 함수 래퍼 함수를 만드는 스크립트를 생성 하 라고 하는 경우에 대 한 인수입니다.|  
|__CDC_OPERATION|**nvarchar(2)**|대상 환경에 행을 적용하는 데 필요한 작업을 나타내는 작업 코드입니다. 인수의 값에 따라 달라 집니다 *row_filter_option* 호출에 제공 합니다.<br /><br /> *row_filter_option* = 'all'<br /><br /> 'D' - 삭제 작업<br /><br /> 'I' - 삽입 작업<br /><br /> 'UN' - 업데이트 작업 새 값<br /><br /> *row_filter_option* 'all update old' =<br /><br /> 'D' - 삭제 작업<br /><br /> 'I' - 삽입 작업<br /><br /> 'UN' - 업데이트 작업 새 값<br /><br /> 'UO' - 업데이트 작업 이전 값|  
|\<열에서 @update_flag_list>|**bit**|_uflag를 열 이름에 추가하여 이름을 지정한 비트 플래그입니다. 플래그가 항상 NULL로 설정 됩니다 \__CDC_OPERATION 했습니다는 ', 'I', 'u O'입니다. 때 \__CDC_OPERATION은 ' u N '에 업데이트를 해당 열이 변경 되는 경우 1로 설정 됩니다. 그렇지 않으면 0입니다.|  
  
## <a name="remarks"></a>설명  
 < Capture_instance > fn_all_changes_ 함수 cdc.fn_cdc_get_all_changes_ < capture_instance > 쿼리 함수의 래퍼 역할도합니다. 래퍼를 만드는 스크립트를 생성하는 데에는 sys.sp_cdc_generate_wrapper 저장 프로시저가 사용됩니다.  
  
 래퍼 함수는 자동으로 만들어지지 않습니다. 래퍼 함수를 만들려면 다음 두 작업을 수행해야 합니다.  
  
1.  래퍼 생성 스크립트를 만드는 저장 프로시저를 실행합니다.  
  
2.  래퍼 함수를 실제로 만드는 스크립트를 실행합니다.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 래퍼 함수를 사용 하면 제한 간격 내에서 발생 한 변경 내용을 체계적으로 쿼리하려면 **날짜/시간** LSN 값 대신 값입니다. 래퍼 함수는 제공 된 간에 필요한 모든 변환을 수행 **날짜/시간** 값과 쿼리 함수에 대 한 인수로 서 내부적으로 필요한 LSN 값입니다. 변경 데이터 스트림을 처리하기 위해 래퍼 함수가 직렬로 사용된 경우 특정 호출과 연결된 간격의 @end_time 값이 후속 호출과 연결된 간격의 @start_time 값으로 제공된다는 규칙을 준수하면 데이터가 손실되거나 반복되지 않습니다.  
  
 스크립트를 만들 때 @closed_high_end_point 매개 변수를 사용하면 지정된 쿼리 창에서 닫힌 상한이나 열린 상한을 지원하는 래퍼를 생성할 수 있습니다. 즉, 커밋 시간이 추출 간격의 상한과 같은 항목을 간격에 포함할지 여부를 결정할 수 있습니다. 기본적으로 상한이 포함됩니다.  
  
 반환 되는 결과 집합을 **모든 변경 내용을** 래퍼 함수는 __ $start_lsn 반환 및 \_ \_$seqval 열 변경 테이블의 열으로 \__CDC_STARTLSN 및 \__ CDC_SEQVAL, 각각. 뒤에 나타난 추적 된 열만을 사용 하 여 이러한 합니다 *@column_list* 은 래퍼가 생성 될 때 매개 변수입니다. 하는 경우 *@column_list* 가 null 인 경우 모든 추적 된 원본 열이 반환 됩니다. 원본 열 뒤에 작업 열 \_는 작업을 식별 하는 하나 또는 두 문자 열인 _CDC_OPERATION 합니다.  
  
 그런 다음 @update_flag_list 매개 변수에 식별된 각 열에 대한 결과 집합에 비트 플래그가 추가됩니다. 에 대 한 합니다 **모든 변경 내용을** 래퍼에 비트 플래그가 항상 NULL이 됩니다 __CDC_OPERATION이 경우 했습니다 ', 'I' 또는 'u O'입니다. 경우 \__CDC_OPERATION은 ' u N '에 플래그를 1 또는 업데이트 작업 결과로 열이 변경 여부에 따라 0으로 설정 됩니다.  
  
 변경 데이터 캡처 구성 템플릿 ' Instantiate CDC Wrapper TVFs for 스키마 ' 모든 스키마의 정의 된 쿼리 함수의 래퍼 함수에 대 한 CREATE 스크립트를 가져오려면 sp_cdc_generate_wrapper_function 저장 프로시저를 사용 하는 방법을 보여 줍니다. 그런 다음 이 템플릿에서는 이러한 스크립트를 만듭니다. 템플릿에 대 한 자세한 내용은 참조 하세요. [템플릿 탐색기](../../ssms/template/template-explorer.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sys.sp_cdc_generate_wrapper_function &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  

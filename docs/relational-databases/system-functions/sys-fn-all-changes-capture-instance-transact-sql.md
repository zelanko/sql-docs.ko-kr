---
title: sys.fn_all_changes_&lt;capture_instance&gt; (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/02/2016
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
- fn_all_changes
- sys.fn_all_changes
- fn_all_changes_TSQL
- sys.fn_all_changes_TSQL
dev_langs: TSQL
helpviewer_keywords:
- fn_all_changes_<capture_instance>
- sys.fn_all_changes_<capture_instance>
ms.assetid: 564fae96-b88c-4f22-9338-26ec168ba6f5
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9e0ec7fbd660a9664f6d2e54f4756dd85c1bac9a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysfnallchangesltcaptureinstancegt-transact-sql"></a>sys.fn_all_changes_&lt;capture_instance&gt; (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  에 대 한 래퍼는 **모든 변경 내용을** 함수를 쿼리 합니다. 이러한 함수를 만드는 데 필요한 스크립트는 sys.sp_cdc_generate_wrapper_function 저장 프로시저에 의해 생성됩니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
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
 **datetime** 결과 집합에 포함할 변경 테이블 항목 범위의 하위 끝점을 나타내는 값입니다.  
  
 연결된 된 커밋 시간이 보다 큰 테이블을 변경 하는 cdc. < capture_instance > _CT의 행만 *start_time* 결과 집합에 포함 됩니다.  
  
 이 인수에 값 NULL을 제공하면 쿼리 범위의 하위 끝점이 캡처 인스턴스에 대해 유효한 범위의 하위 끝점에 대응됩니다.  
  
 *end_time*  
 **datetime** 결과 집합에 포함할 변경 테이블 항목 범위의 상위 끝점을 나타내는 값입니다.  
  
 이 매개 변수 수에 대해 선택한 값에 따라 두 가지 의미 중 하나를 사용할 @closed_high_end_point 래퍼 함수에 대 한 create 스크립트를 생성 하기 위해 sys.sp_cdc_generate_wrapper_function을 호출할 경우:  
  
-   @closed_high_end_point = 1  
  
     연결된 커밋 시간이 end_time과 같거나 이전인 cdc.<capture_instance>_CT 변경 테이블의 행만 결과 집합에 포함됩니다.  
  
-   @closed_high_end_point = 0  
  
     가진 cdc.capture_instance_CT 변경 테이블의 행만 연결된 된 커밋 시간이 end_time 결과에 포함 된 이전인 설정 했습니다.  
  
 이 인수에 값 NULL을 제공하면 쿼리 범위의 상위 끝점이 캡처 인스턴스에 대해 유효한 범위의 상위 끝점에 대응됩니다.  
  
 <row_filter_option> ::= { all | all update old }  
 결과 집합에 반환되는 메타데이터 열 및 행의 내용을 제어하는 옵션입니다.  
  
 다음 옵션 중 하나를 사용할 수 있습니다.  
  
 all  
 지정된 LSN 범위 내의 모든 변경을 반환합니다. 업데이트 작업으로 인해 발생하는 변경 내용의 경우 이 옵션을 사용하면 업데이트가 적용된 후의 새 값을 포함하는 행만 반환됩니다.  
  
 all update old  
 지정된 LSN 범위 내의 모든 변경을 반환합니다. 업데이트 작업으로 인해 발생하는 변경 내용의 경우 이 옵션을 사용하면 업데이트 전후의 열 값을 포함하는 두 개의 행이 반환됩니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|열 유형|Description|  
|-----------------|-----------------|-----------------|  
|__CDC_STARTLSN|**binary(10)**|변경 내용과 관련된 트랜잭션의 커밋 LSN입니다. 동일한 트랜잭션에서 커밋된 모든 변경 내용은 같은 커밋 LSN을 공유합니다.|  
|__CDC_SEQVAL|**binary(10)**|트랜잭션에서 행 변경 내용을 정렬하는 데 사용되는 시퀀스 값입니다.|  
|\<열을 @column_list>|**달라 집니다.**|식별 되는 열은 *column_list* 인수 sp_cdc_generate_wrapper_function 래퍼 함수를 만드는 스크립트를 생성 하는 호출 될 때입니다.|  
|__CDC_OPERATION|**nvarchar(2)**|대상 환경에 행을 적용하는 데 필요한 작업을 나타내는 작업 코드입니다. 인수 값에 따라 달라 집니다 *row_filter_option* 하면 호출에 제공 합니다.<br /><br /> *row_filter_option* = '모두'<br /><br /> 'D' - 삭제 작업<br /><br /> 'I' - 삽입 작업<br /><br /> 'UN' - 업데이트 작업 새 값<br /><br /> *row_filter_option* 'all update old' =<br /><br /> 'D' - 삭제 작업<br /><br /> 'I' - 삽입 작업<br /><br /> 'UN' - 업데이트 작업 새 값<br /><br /> 'UO' - 업데이트 작업 이전 값|  
|\<열을 @update_flag_list>|**bit**|_uflag를 열 이름에 추가하여 이름을 지정한 비트 플래그입니다. 플래그는 항상 NULL로 설정 \__CDC_OPERATION에는 ', 'I' 또는 'u o'. 때 \__CDC_OPERATION이 ' u N ', 업데이트를 해당 열이 변경 되 면 1로 설정 됩니다. 그렇지 않으면 0입니다.|  
  
## <a name="remarks"></a>주의  
 fn_all_changes_<capture_instance> 함수는 cdc.fn_cdc_get_all_changes_<capture_instance> 쿼리 함수의 래퍼 역할을 합니다. 래퍼를 만드는 스크립트를 생성하는 데에는 sys.sp_cdc_generate_wrapper 저장 프로시저가 사용됩니다.  
  
 래퍼 함수는 자동으로 만들어지지 않습니다. 래퍼 함수를 만들려면 다음 두 작업을 수행해야 합니다.  
  
1.  래퍼 생성 스크립트를 만드는 저장 프로시저를 실행합니다.  
  
2.  래퍼 함수를 실제로 만드는 스크립트를 실행합니다.  
  
 래퍼 함수에 의해 제한 간격 내에 발생 한 변경 내용을 체계적으로 쿼리할 수 있도록 **datetime** LSN 값 대신 값입니다. 래퍼 함수는 제공 된 간에 필요한 모든 변환을 수행 합니다. **datetime** 값과 쿼리 함수에 대 한 인수로 서 내부적으로 필요한 LSN 값입니다. 변경 데이터 스트림을 처리하기 위해 래퍼 함수가 직렬로 사용된 경우 특정 호출과 연결된 간격의 @end_time 값이 후속 호출과 연결된 간격의 @start_time 값으로 제공된다는 규칙을 준수하면 데이터가 손실되거나 반복되지 않습니다.  
  
 스크립트를 만들 때 @closed_high_end_point 매개 변수를 사용하면 지정된 쿼리 창에서 닫힌 상한이나 열린 상한을 지원하는 래퍼를 생성할 수 있습니다. 즉, 커밋 시간이 추출 간격의 상한과 같은 항목을 간격에 포함할지 여부를 결정할 수 있습니다. 기본적으로 상한이 포함됩니다.  
  
 반환 된 결과 집합의 **모든 변경 내용을** 래퍼 함수는 __ $start_lsn 반환 하 고 \_ \_$seqval 열은 변경 테이블의 열으로 \__CDC_STARTLSN 및 \__ CDC_SEQVAL, 각각. 표시 된 추적 된 열만 가진 뒤의  *@column_list*  래퍼가 생성 될 때 매개 변수입니다. 경우  *@column_list*  가 null 인 경우 모든 추적 된 원본 열이 반환 됩니다. 작업 열 원본 열 뒤 \_작업을 식별 하는 하나 또는 두 문자 열인 _CDC_OPERATION 합니다.  
  
 그런 다음 @update_flag_list 매개 변수에 식별된 각 열에 대한 결과 집합에 비트 플래그가 추가됩니다. 에 대 한는 **모든 변경 내용을** 래퍼에 비트 플래그가 항상 NULL이 됩니다 __CDC_OPERATION이 했습니다 ', 'I' 또는 'u O'. 경우 \__CDC_OPERATION이 ' u N ', 1 또는 업데이트 작업 결과로 열이 변경 여부에 따라 0는 플래그를 설정 합니다.  
  
 변경 데이터 캡처 구성 템플릿 'Instantiate CDC Wrapper TVFs for Schema'에서는 sp_cdc_generate_wrapper_function 저장 프로시저를 사용하여 스키마에 정의된 쿼리 함수의 모든 래퍼 함수에 대한 CREATE 스크립트를 가져오는 방법을 보여 줍니다. 그런 다음 이 템플릿에서는 이러한 스크립트를 만듭니다. 서식 파일에 대 한 자세한 내용은 참조 [템플릿 탐색기](http://msdn.microsoft.com/library/b9ee55c5-bb44-4f76-90ac-792d8d83b4c8)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sys.sp_cdc_generate_wrapper_function &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60; capture_instance& &#62;  &#40; Transact SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  

---
title: 변경 데이터 검색을 위한 함수 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],creating function
ms.assetid: 55dd0946-bd67-4490-9971-12dfb5b9de94
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 43809c2be4dca62d150be31f62b833b08a2569b7
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251979"
---
# <a name="create-the-function-to-retrieve-the-change-data"></a>변경 데이터 검색을 위한 함수 만들기

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  변경 데이터를 증분 로드하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 제어 흐름을 완료한 후 다음 태스크는 변경 데이터를 검색하는 테이블 반환 함수를 만드는 것입니다. 첫 번째 증분 로드 전에 이 함수를 한 번만 만들면 됩니다.  
  
> [!NOTE]  
>  변경 데이터를 검색하는 함수 생성 작업은 변경 데이터를 증분 로드하는 패키지 생성 프로세스의 두 번째 단계입니다. 이 패키지를 만들기 위한 전체 프로세스에 대한 설명은 [변경 데이터 캡처&#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)를 참조하세요.  
  
## <a name="design-considerations-for-change-data-capture-functions"></a>변경 데이터 캡처 함수에 대한 디자인 고려 사항  
 변경 데이터를 검색하기 위해 패키지 데이터 흐름의 원본 구성 요소는 다음 변경 데이터 캡처 쿼리 함수 중 하나를 호출합니다.  
  
-   **cdc.fn_cdc_get_net_changes_<capture_instance>** 이 쿼리의 경우 각 업데이트에 대해 반환된 단일 행에는 변경된 각 행의 최종 상태가 포함됩니다. 대부분의 경우 순 변경 내용에 대해 쿼리에서 반환하는 데이터만 필요합니다. 자세한 내용은 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62;&#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)를 참조하세요.  
  
-   **cdc.fn_cdc_get_all_changes_<capture_instance>** 이 쿼리는 캡처 간격 동안 각 행에 발생한 모든 변경 내용을 반환합니다. 자세한 내용은 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;&#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)를 참조하세요.  
  
 그런 다음 원본 구성 요소는 함수에서 반환한 결과를 사용하고 최종 대상에 변경 데이터를 적용하는 다운스트림 변환 및 대상에 해당 결과를 전달합니다.  
  
 그러나 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 원본 구성 요소는 이러한 변경 데이터 캡처 함수를 직접 호출할 수 없습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 원본 구성 요소에는 쿼리에서 반환하는 열에 대한 메타데이터가 필요합니다. 변경 데이터 캡처 함수는 해당 출력 테이블의 열을 정의하지 않습니다. 따라서 이러한 함수는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 원본 구성 요소에 대해 충분한 메타데이터를 반환하지 않습니다.  
  
 테이블 반환 래퍼 함수와 같은 함수는 해당 RETURNS 절에 출력 테이블의 열을 명시적으로 정의하므로 테이블 반환 래퍼 함수를 대신 사용합니다. 이렇게 열을 명시적으로 정의하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 원본 구성 요소에 필요한 메타데이터가 제공됩니다. 변경 데이터를 검색하려는 각 테이블에 대해 이 함수를 만들어야 합니다.  
  
 변경 데이터 캡처 쿼리 함수를 호출하는 테이블 반환 래퍼 함수를 만드는 데는 두 가지 방법이 있습니다.  
  
-   **sys.sp_cdc_generate_wrapper_function** 시스템 저장 프로시저를 호출하여 테이블 반환 함수를 자동으로 만들 수 있습니다.  
  
-   이 항목에 나와 있는 지침과 예를 사용하여 테이블 반환 함수를 직접 작성할 수 있습니다.  
  
## <a name="calling-a-stored-procedure-to-create-the-table-valued-function"></a>저장 프로시저를 호출하여 테이블 반환 함수 만들기  
 필요한 테이블 반환 함수를 만드는 가장 쉽고 빠른 방법은 **sys.sp_cdc_generate_wrapper_function** 시스템 저장 프로시저를 호출하는 것입니다. 이 저장 프로시저는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 원본 구성 요소의 필요에 맞게 특별히 설계된 래퍼 함수를 만드는 스크립트를 생성합니다.  
  
> [!IMPORTANT]  
>  **sys.sp_cdc_generate_wrapper_function** 시스템 저장 프로시저는 래퍼 함수를 직접 만드는 대신 래퍼 함수에 대한 CREATE 스크립트를 생성합니다. 개발자는 저장 프로시저에서 생성한 CREATE 스크립트를 실행해야 증분 로드 패키지에서 래퍼 함수를 호출할 수 있습니다.  
  
 이 시스템 저장 프로시저를 사용하는 방법을 이해하려면 이 프로시저의 작업 내용, 프로시저에서 생성하는 스크립트 및 스크립트에서 만드는 래퍼 함수를 이해해야 합니다.  
  
### <a name="understanding-and-using-the-stored-procedure"></a>저장 프로시저 이해 및 사용  
 **sys.sp_cdc_generate_wrapper_function** 시스템 저장 프로시저는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 사용할 래퍼 함수를 만드는 스크립트를 생성합니다.  
  
 이 저장 프로시저의 정의 중 처음 몇 줄은 다음과 같습니다.  
  
 `CREATE PROCEDURE sys.sp_cdc_generate_wrapper_function`  
  
 `(`  
  
 `@capture_instance sysname = null`  
  
 `@closed_high_end_point bit = 1,`  
  
 `@column_list = null,`  
  
 `@update_flag_list = null`  
  
 `)`  
  
 이 저장 프로시저의 모든 매개 변수는 선택 사항입니다. 어떠한 매개 변수에도 값을 제공하지 않고 저장 프로시저를 호출하면 액세스 권한이 있는 모든 캡처 인스턴스에 대한 래퍼 함수가 만들어집니다.  
  
> [!NOTE]  
>  이 저장 프로시저의 구문과 해당 매개 변수에 대한 자세한 내용은 [sys.sp_cdc_generate_wrapper_function&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)을 참조하세요.  
  
 이 저장 프로시저는 항상 각 캡처 인스턴스의 모든 변경 내용을 반환하는 래퍼 함수를 생성합니다. 캡처 인스턴스를 만들 때 *\@supports_net_changes* 매개 변수가 설정된 경우에는 각 해당 캡처 인스턴스의 순 변경을 반환하는 래퍼 함수도 생성됩니다.  
  
 이 저장 프로시저는 열이 두 개 있는 결과 집합을 반환합니다.  
  
-   저장 프로시저에서 생성한 래퍼 함수의 이름. 이 저장 프로시저는 캡처 인스턴스의 이름에서 함수 이름을 파생합니다. 함수 이름은 'fn_all_changes_' 뒤에 캡처 인스턴스 이름을 추가한 것입니다. 순 변경 함수가 만들어지는 경우에는 'fn_net_changes_'라는 접두사가 사용됩니다.  
  
-   래퍼 함수에 대한 CREATE 문  
  
### <a name="understanding-and-using-the-scripts-created-by-the-stored-procedure"></a>저장 프로시저에서 만든 스크립트 이해 및 사용  
 일반적으로 개발자는 INSERT...EXEC 문을 사용하여 **sys.sp_cdc_generate_wrapper_function** 저장 프로시저를 호출하고 저장 프로시저에서 만든 스크립트를 임시 테이블에 저장합니다. 그런 다음 각 스크립트를 개별적으로 선택 및 실행하여 해당 래퍼 함수를 만듭니다. 그러나 개발자는 다음 예제 코드와 같이 일련의 SQL 명령을 사용하여 모든 CREATE 스크립트를 실행할 수도 있습니다.  
  
```  
create table #wrapper_functions  
      (function_name sysname, create_stmt nvarchar(max))  
insert into #wrapper_functions  
exec sys.sp_cdc_generate_wrapper_function  
  
declare @stmt nvarchar(max)  
declare #hfunctions cursor local fast_forward for   
      select create_stmt from #wrapper_functions  
open #hfunctions  
fetch #hfunctions into @stmt  
while (@@fetch_status <> -1)  
begin  
      exec sp_executesql @stmt  
      fetch #hfunctions into @stmt  
end  
close #hfunctions  
deallocate #hfunctions  
```  
  
### <a name="understanding-and-using-the-functions-created-by-the-stored-procedure"></a>저장 프로시저에서 만든 함수 이해 및 사용  
 생성된 래퍼 함수는 캡처된 변경 데이터의 시간대를 체계적으로 탐색하기 위해 특정 간격의 *\@end_time* 매개 변수가 후속 간격의 *\@start_time* 매개 변수일 것으로 간주합니다. 이러한 규칙이 준수되는 경우 생성된 래퍼 함수에서 다음과 같은 태스크를 수행할 수 있습니다.  
  
-   날짜/시간 값을 내부적으로 사용되는 LSN 값에 매핑  
  
-   손실되거나 반복되는 데이터가 없는지 확인  
  
 생성된 래퍼 함수에서는 변경 테이블의 모든 행을 간단히 쿼리할 수 있도록 다음과 같은 규칙도 지원합니다.  
  
-   @start_time 매개 변수가 null이면 래퍼 함수는 캡처 인스턴스에서 가장 낮은 LSN 값을 쿼리의 하한으로 사용합니다.  
  
-   @end_time 매개 변수가 null이면 래퍼 함수는 캡처 인스턴스에서 가장 높은 LSN 값을 쿼리의 상한으로 사용합니다.  
  
 대부분의 사용자는 **sys.sp_cdc_generate_wrapper_function** 시스템 저장 프로시저에서 만드는 래퍼 함수를 수정하지 않고 그대로 사용할 수 있습니다. 그러나 래퍼 함수를 사용자 지정하려면 CREATE 스크립트를 사용자 지정한 다음 실행해야 합니다.  
  
 패키지에서 래퍼 함수를 호출하는 경우 패키지에서 세 가지 매개 변수에 값을 제공해야 합니다. 이러한 세 가지 매개 변수는 변경 데이터 캡처 함수에서 사용하는 세 가지 매개 변수와 비슷합니다. 이러한 세 가지 매개 변수는 다음과 같습니다.  
  
-   간격의 시작 날짜/시간 값 및 종료 날짜/시간 값. 래퍼 함수는 날짜/시간 값을 쿼리 간격의 끝점으로 사용하지만 변경 데이터 캡처 함수는 두 LSN 값을 끝점으로 사용합니다.  
  
-   행 필터. 래퍼 함수와 변경 데이터 캡처 함수의 *\@row_filter_option* 매개 변수는 서로 동일합니다. 자세한 내용은 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;&#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) 및 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62;&#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)를 참조하세요.  
  
 래퍼 함수에서 반환하는 결과 집합에는 다음과 같은 데이터가 포함됩니다.  
  
-   변경 데이터의 모든 요청된 열  
  
-   1문자 또는 2문자 필드를 사용하여 행에 연결된 작업을 식별하는 __CDC_OPERATION이라는 열. 이 필드의 유효한 값은 다음과 같습니다. ‘I’는 삽입, ‘D’는 삭제, ‘UO’는 이전 값 업데이트 및 ‘UN’은 새 값 업데이트입니다.  
  
-   요청 시 작업 코드 뒤에 *\@update_flag_list* 매개 변수에 지정된 순서대로 비트 열로 표시되는 업데이트 플래그. 이러한 열의 이름은 관련 열 이름에 '_uflag'를 추가한 것입니다.  
  
 패키지에서 모든 변경을 쿼리하는 래퍼 함수를 호출하는 경우 래퍼 함수는 __CDC_STARTLSN 및 \__CDC_SEQVAL 열도 반환합니다. 이러한 두 열은 각각 결과 집합의 첫 번째 열과 두 번째 열이 됩니다. 또한 래퍼 함수는 이러한 두 열에 따라 결과 집합을 정렬합니다.  
  
## <a name="writing-your-own-table-value-function"></a>테이블 반환 함수 직접 작성  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 통해 변경 데이터 캡처 쿼리 함수를 호출하는 테이블 반환 함수를 직접 작성하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장할 수도 있습니다. TRANSACT-SQL 함수를 만드는 방법에 대한 자세한 내용은 [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)을 참조하세요.  
  
 다음 예에서는 지정한 변경 간격 동안 Customer 테이블에서 변경 내용을 검색하는 테이블 반환 함수를 정의합니다. 이 함수는 변경 데이터 캡처 함수를 사용하여 변경 테이블이 내부적으로 사용하는 이진 LSN(로그 시퀀스 번호) 값에 **datetime** 값을 매핑합니다. 또한 이 함수는 다음과 같은 몇 가지 특수 상황을 처리합니다.  
  
-   시작 시간에 대해 Null 값이 전달되는 경우 이 함수는 사용할 수 있는 가장 오래된 값을 사용합니다.  
  
-   종료 시간에 대해 Null 값이 전달되는 경우 이 함수는 사용할 수 있는 최근 값을 사용합니다.  
  
-   시작 LSN이 끝 LSN과 같은 경우(일반적으로 선택 간격에 대한 레코드가 없음을 나타냄) 이 함수는 종료됩니다.  
  
### <a name="example-of-a-table-value-function-that-queries-for-change-data"></a>변경 데이터를 쿼리하는 테이블 반환 함수의 예  
  
```  
CREATE function CDCSample.uf_Customer (  
     @start_time datetime  
    ,@end_time datetime  
)  
returns @Customer table (  
     CustomerID int  
    ,TerritoryID int  
    ,CustomerType nchar(1)  
    ,rowguid uniqueidentifier  
    ,ModifiedDate datetime  
    ,CDC_OPERATION varchar(1)  
) as  
begin  
    declare @from_lsn binary(10), @to_lsn binary(10)  
  
    if (@start_time is null)  
        select @from_lsn = sys.fn_cdc_get_min_lsn('Customer')  
    else  
        select @from_lsn = sys.fn_cdc_increment_lsn(sys.fn_cdc_map_time_to_lsn('largest less than or equal',@start_time))  
  
    if (@end_time is null)  
        select @to_lsn = sys.fn_cdc_get_max_lsn()  
    else  
        select @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal',@end_time)  
  
    if (@from_lsn = sys.fn_cdc_increment_lsn(@to_lsn))  
        return  
  
    -- Query for change data  
    insert into @Customer  
    select   
        CustomerID,      
        TerritoryID,   
        CustomerType,   
        rowguid,   
        ModifiedDate,   
        case __$operation  
                when 1 then 'D'  
                when 2 then 'I'  
                when 4 then 'U'  
                else null  
         end as CDC_OPERATION  
    from   
        cdc.fn_cdc_get_net_changes_Customer(@from_lsn, @to_lsn, 'all')  
  
    return  
end   
go  
  
```  
  
### <a name="retrieving-additional-metadata-with-the-change-data"></a>변경 데이터의 추가 메타데이터 검색  
 위에 나와 있는 사용자가 만든 테이블 반환 함수는 **__$operation** 열을 사용하지만 **cdc.fn_cdc_get_net_changes_<capture_instance>** 함수는 각 변경 행의 메타데이터 열 4개를 반환합니다. 데이터 흐름에 이러한 값을 사용하려면 테이블 반환 래퍼 함수에서 추가 열로 이러한 값을 반환합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|변경에 대한 커밋 트랜잭션과 연관된 LSN입니다.<br /><br /> 동일한 트랜잭션에서 커밋된 변경의 커밋 LSN은 모두 동일합니다. 예를 들어 원본 테이블의 업데이트 작업에서 두 개의 서로 다른 행을 수정하면 변경 테이블에는 모두 동일한 **__$start_lsn** 값이 있는 4개의 행(이전 값과 새 값 두 개씩 포함)이 포함됩니다.|  
|**__$seqval**|**binary(10)**|트랜잭션에서 행 변경 내용을 정렬하는 데 사용되는 시퀀스 값입니다.|  
|**__$operation**|**int**|변경과 연관된 DML(데이터 조작 언어) 작업입니다. 다음 중 하나일 수 있습니다.<br /><br /> 1 = 삭제<br /><br /> 2 = 삽입<br /><br /> 3 = 업데이트(업데이트 작업 전의 값)<br /><br /> 4 = 업데이트(업데이트 작업 후의 값)|  
|**__$update_mask**|**varbinary(128)**|변경된 열을 식별하는 변경 테이블의 열 서수를 기준으로 하는 비트 마스크입니다. 변경된 열을 확인해야 하는 경우 이 값을 검토할 수 있습니다.|  
|**\<captured source table columns>**|다양함|함수에서 반환되는 나머지 열은 캡처 인스턴스 생성 시 캡처된 열로 식별된 원본 테이블의 열입니다. 캡처된 열 목록에 열이 원래 지정되어 있지 않은 경우 원본 테이블의 모든 열이 반환됩니다.|  
  
 자세한 내용은 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62;&#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)를 참조하세요.  
  
## <a name="next-step"></a>다음 단계  
 변경 데이터를 쿼리하는 테이블 반환 함수를 만든 후 다음 단계는 패키지의 데이터 흐름 디자인을 시작하는 것입니다.  
  
 **다음 항목:** [변경 데이터 검색 및 이해](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md)  
  
  

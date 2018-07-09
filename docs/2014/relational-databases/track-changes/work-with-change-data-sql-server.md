---
title: 변경 데이터 작업(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- change data [SQL Server]
- change data capture [SQL Server], query function scenarios
- change data capture [SQL Server], LSN boundaries
- change data capture [SQL Server], query functions
ms.assetid: 5346b852-1af8-4080-b278-12efb9b735eb
caps.latest.revision: 19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: df86d149bcdf6d9e1619499edf2bc41137433392
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153994"
---
# <a name="work-with-change-data-sql-server"></a>변경 데이터 작업(SQL Server)
  변경 데이터는 TVF(테이블 반환 함수)를 통해 변경 데이터 캡처 소비자에게 제공됩니다. 이러한 함수의 모든 쿼리에는 반환된 결과 집합을 개발할 때 고려할 LSN(로그 시퀀스 번호)의 범위를 정의하는 두 매개 변수가 필요합니다. 간격을 한정하는 LSN 하한/상한 값 모두 간격 내에 포함되는 것으로 간주됩니다.  
  
 TVF 쿼리에 적합한 LSN 값을 결정하는 데 유용한 여러 함수가 제공됩니다. [sys.fn_cdc_get_min_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql) 함수는 캡처 인스턴스 유효성 간격과 관련된 가장 작은 LSN을 반환합니다. 유효성 간격은 현재 해당 캡처 인스턴스에 변경 데이터를 사용할 수 있는 시간 간격입니다. [sys.fn_cdc_get_max_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql) 함수는 유효성 간격의 가장 큰 LSN을 반환합니다. [sys.fn_cdc_map_time_to_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql) 및 [sys.fn_cdc_map_lsn_to_time](/sql/relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql) 함수를 사용하여 LSN 값을 기존 시간대에 배치할 수 있습니다. 변경 데이터 캡처는 제한된 쿼리 간격을 사용하므로 연속적인 쿼리 창에서 변경 내용이 중복되지 않도록 시퀀스의 다음 LSN 값을 생성해야 하는 경우도 있습니다. LSN 값에 대한 증분 조정이 필요할 경우 [sys.fn_cdc_increment_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql) 및 [sys.fn_cdc_decrement_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql) 함수가 유용합니다.  
  
##  <a name="LSN"></a> LSN 경계 유효성 검사  
 TVF 쿼리에 사용할 LSN 경계는 사용 전에 항상 유효성을 검사하는 것이 좋습니다. 캡처 인스턴스에 대한 유효성 간격을 벗어나는 Null 끝점이 있을 경우 이로 인해 변경 데이터 캡처 TVF에서 오류를 반환합니다.  
  
 예를 들어 쿼리 간격을 정의하는 데 사용되는 매개 변수가 유효하지 않거나 범위를 벗어난 경우 또는 행 필터 옵션이 잘못된 경우 모든 변경 내용에 대한 쿼리에 대해 다음 오류가 반환됩니다.  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_all_changes_ ...`  
  
 에 대해 반환 되는 해당 오류를 `net changes` 쿼리는 다음과 같습니다.  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_net_changes_ ...`  
  
> [!NOTE]  
>  메시지 313의 메시지는 오해의 소지가 있으며 오류에 대한 실제 원인을 나타내지 않습니다. 이러한 잘못된 사용은 TVF 내에서 명시적 오류를 발생시키지 못했기 때문입니다. 그러나 단순히 빈 결과를 반환하기보다는 정확하지는 않지만 인식할 수 있는 오류를 반환하는 값이 낫다고 간주되었습니다. 빈 결과 집합은 변경 내용을 반환하지 않는 올바른 쿼리와 구분되지 않습니다.  
  
 다음과 같이 모든 변경 내용을 쿼리할 때 권한 부여 실패 시 오류가 반환됩니다.  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object 'fn_cdc_get_all_changes_...', database 'MyDB', schema 'cdc'.`  
  
 순 변경 내용을 쿼리할 때도 마찬가지입니다.  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object fn_cdc_get_net_changes_...', database 'MyDB', schema 'cdc'.`  
  
 알려진 이러한 TVF 오류를 차단하고 오류에 대한 보다 의미 있는 정보를 반환하는 방법을 보려면 Enumerate Net Changes Using TRY CATCH 템플릿을 참조하십시오.  
  
> [!NOTE]  
>  SQL Server Management Studio에서 변경 데이터 캡처 템플릿을 찾으려면 **보기** 메뉴에서 **템플릿 탐색기**를 클릭하고 **SQL Server 템플릿** 을 확장한 다음 **변경 데이터 캡처** 폴더를 확장합니다.  
  
##  <a name="Functions"></a> 쿼리 함수  
 추적하는 원본 테이블의 특징과 해당 캡처 인스턴스가 구성된 방식에 따라 변경 데이터를 쿼리하는 하나 또는 두 개의 TVF가 생성됩니다.  
  
-   [cdc.fn_cdc_get_all_changes_<capture_instance>](/sql/relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql) 함수는 지정된 간격 동안 발생한 모든 변경 내용을 반환합니다. 이 함수는 항상 생성됩니다. 항목은 항상 먼저 변경 내용의 트랜잭션 커밋 LSN순으로 정렬된 다음 해당 트랜잭션 내의 변경을 순서대로 나열하는 값순으로 정렬되어 반환됩니다. 선택한 행 필터 옵션에 따라 업데이트 시 최종 행이 반환(행 필터 옵션 "all")되거나 업데이트 시 새 값과 이전 값이 모두 반환(행 필터 옵션 "all update old")됩니다.  
  
-   원본 테이블을 사용하도록 설정된 경우 @supports_net_changes 매개 변수가 1로 설정되면 [cdc.fn_cdc_get_net_changes_<capture_instance>](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql) 함수가 생성됩니다.  
  
    > [!NOTE]  
    >  이 옵션은 원본 테이블에 정의된 기본 키가 있거나 @index_name 매개 변수를 사용하여 고유 인덱스를 식별한 경우에만 지원됩니다.  
  
     **netchanges** 함수는 수정된 원본 테이블 행당 하나의 변경 내용을 반환합니다. 지정된 간격 동안 해당 행에 대해 둘 이상의 변경 내용이 기록되는 경우 열 값에는 행의 마지막 내용이 반영됩니다. 대상 환경을 업데이트하는 데 필요한 작업을 올바르게 식별하려면 TVF에서 해당 간격 동안 행에 수행한 초기 작업과 행에 수행한 마지막 작업을 모두 고려해야 합니다. 행 필터 옵션 'all'을 지정한 경우 `net changes` 쿼리에서 반환하는 작업은 삽입, 삭제 또는 업데이트(새 값) 중 하나입니다. 집계 마스크를 계산하는 데 비용이 들기 때문에 이 옵션은 항상 업데이트 마스크를 Null로 반환합니다. 행에 대한 모든 변경 내용을 반영하는 집계 마스크가 필요한 경우 'all with mask' 옵션을 사용합니다. 다운스트림 처리에서 삽입과 업데이트를 구분할 필요가 없는 경우 'all with merge' 옵션을 사용합니다. 이 경우 작업 값에는 두 개의 값만 사용됩니다. 즉, 삭제에 대해 1을 사용하고 삽입이나 업데이트가 될 수 있는 작업에 대해서는 5를 사용합니다. 이 옵션을 사용하면 파생된 작업이 삽입인지 업데이트인지를 결정하는 데 필요한 추가 처리를 수행하지 않아도 되므로 이러한 구분이 필요하지 않은 경우 쿼리 성능을 향상시킬 수 있습니다.  
  
 쿼리 함수에서 반환되는 업데이트 마스크는 변경 데이터의 행에서 변경된 모든 열을 식별하는 간단한 표현입니다. 일반적으로 이 정보는 캡처된 열로 구성된 일부 하위 집합에만 필요합니다. 함수를 사용하여 응용 프로그램에서 보다 직접 사용할 수 있는 형식으로 마스크에서 정보를 추출할 수 있습니다. [sys.fn_cdc_get_column_ordinal](/sql/relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql) 함수는 지정한 캡처 인스턴스에 대해 명명된 열의 서수 위치를 반환하는 반면 [sys.fn_cdc_is_bit_set](/sql/relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql) 함수는 제공된 마스크에 있는 비트의 패리티를 함수 호출에서 전달된 서수를 기반으로 반환합니다. 이러한 두 함수를 함께 사용하면 업데이트 마스크의 정보를 효율적으로 추출하고 변경 데이터에 대한 요청과 함께 반환할 수 있습니다. 이러한 함수를 사용하는 방법을 보려면 Enumerate Net Changes Using All With Mask 템플릿을 참조하십시오.  
  
##  <a name="Scenarios"></a> 쿼리 함수 시나리오  
 다음 섹션에서는 cdc.fn_cdc_get_all_changes_<capture_instance> 및 cdc.fn_cdc_get_net_changes_<capture_instance> 함수를 사용하여 변경 데이터 캡처 데이터를 쿼리하는 일반적인 시나리오에 대해 설명합니다.  
  
### <a name="querying-for-all-changes-within-the-capture-instance-validity-interval"></a>캡처 인스턴스 유효성 간격 내의 모든 변경 내용 쿼리  
 변경 데이터에 대한 가장 간단한 요청은 캡처 인스턴스의 유효성 간격 내에 있는 모든 현재 변경 데이터를 반환하는 요청입니다. 이 요청을 만들려면 먼저 유효성 간격의 하한 및 상한 LSN 경계를 확인합니다. 그런 다음 이러한 값을 사용하여 cdc.fn_cdc_get_all_changes_<capture_instance> 또는 cdc.fn_cdc_get_net_changes_<capture_instance> 쿼리 함수에 전달된 @from_lsn 및 @to_lsn 매개 변수를 식별합니다. 하한을 가져오려면 [sys.fn_cdc_get_min_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql) 함수를 사용하고 상한을 가져오려면 [sys.fn_cdc_get_max_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql) 함수를 사용합니다. cdc.fn_cdc_get_all_changes_<capture_instance> 쿼리 함수를 사용하여 유효한 모든 현재 변경 내용을 쿼리하는 예제 코드를 보려면 Enumerate All Changes for the Valid Range 템플릿을 참조하십시오. cdc.fn_cdc_get_net_changes_<capture_instance> 함수를 사용하는 유사한 예를 보려면 Enumerate Net Changes for the Valid Range 템플릿을 참조하십시오.  
  
### <a name="querying-for-all-new-changes-since-the-last-set-of-changes"></a>마지막 변경 내용 집합 이후의 모든 새 변경 내용 쿼리  
 일반적인 응용 프로그램의 경우 변경 데이터 쿼리는 마지막 요청 이후에 발생한 모든 변경 내용을 정기적으로 요청하는 진행 중인 프로세스가 됩니다. 이러한 쿼리의 경우 [sys.fn_cdc_increment_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql) 함수를 사용하여 이전 쿼리의 상한에서 현재 쿼리의 하한을 파생할 수 있습니다. 이 방법을 사용하면 쿼리 간격이 항상 두 끝점이 모두 간격에 포함되는 닫힌 간격으로 처리되기 때문에 행이 반복되지 않습니다. 그런 다음 [sys.fn_cdc_get_max_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql) 함수를 사용하여 새 요청 간격의 상위 끝점을 가져옵니다. 마지막 요청 이후의 모든 변경 내용을 가져오기 위해 쿼리 창을 체계적으로 이동하는 예제 코드를 보려면 Enumerate All Changes Since Previous Request 템플릿을 참조하십시오.  
  
### <a name="querying-for-all-new-changes-up-until-now"></a>현재까지의 모든 새 변경 내용 쿼리  
 쿼리 함수에서 반환하는 변경 내용에 적용되는 일반적인 제약 조건은 이전 요청과 현재 날짜 및 시간 사이에 발생한 변경 내용만 포함하는 것입니다. 이러한 쿼리의 경우 이전 요청에서 하한을 확인하기 위해 사용된 @from_lsn 값에 sys.fn_cdc_increment_lsn 함수를 적용합니다. 시간 간격의 상한은 특정 시점으로 표시되기 때문에 LSN 값으로 변환해야 쿼리 함수에서 사용할 수 있습니다. datetime 값을 해당 LSN 값으로 변환할 수 있기 때문에 캡처 프로세스가 지정된 상한까지 커밋된 모든 변경 내용을 처리했는지 확인해야 합니다. 이 작업은 조건에 맞는 모든 변경 내용이 변경 테이블에 전파되었는지 확인하는 데 필요합니다. 이렇게 하는 한 가지 방법은 데이터베이스 변경 테이블에 대해 기록된 현재 최대 커밋 lsn이 원하는 요청 간격 종료 시간을 초과하는지 정기적으로 검사하는 대기 루프를 만드는 것입니다.  
  
 지연 루프가 캡처 프로세스에서 모든 관련 로그 항목을 이미 처리했는지 확인한 후에는 [sys.fn_cdc_map_time_to_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql) 함수를 사용하여 LSN 값으로 표시된 새 상위 끝점을 확인합니다. 지정된 시간까지 커밋된 모든 항목이 검색되도록 하려면 sys.fn_cdc_map_time_to_lsn 함수를 호출하고 'largest less than or equal' 옵션을 사용합니다.  
  
> [!NOTE]  
>  작업을 하지 않은 기간에는 캡처 프로세스에서 지정된 커밋 시간까지 변경 내용을 처리했다는 사실을 표시하기 위해 cdc.lsn_time_mapping 테이블에 더미 항목이 추가됩니다. 이렇게 하면 처리할 최근 변경 내용이 없는 경우 캡처 프로세스가 지연되었다는 메시지가 표시되지 않습니다.  
  
 Enumerate All Changes Up Until Now 템플릿에서는 위의 전략을 사용하여 변경 데이터를 쿼리하는 방법을 보여 줍니다.  
  
### <a name="adding-a-commit-time-to-an-all-changes-result-set"></a>모든 변경 내용 결과 집합에 커밋 시간 추가  
 데이터베이스 변경 테이블의 항목과 연결된 각 트랜잭션의 커밋 시간은 [cdc.lsn_time_mapping](/sql/relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql)테이블에서 사용할 수 있습니다. 모든 변경 내용에 대한 요청에서 반환한 __$start_lsn 값을 cdc.lsn_time_mapping 테이블 항목의 start_lsn 값과 조인하면 변경 데이터와 함께 tran_end_time을 반환하여 변경 데이터에 원본의 트랜잭션 커밋 시간을 표시할 수 있습니다. Append Commit Time to All Changes Result Set 템플릿에서는 이러한 조인을 수행하는 방법을 보여 줍니다.  
  
### <a name="joining-change-data-with-other-data-from-the-same-transaction"></a>변경 데이터를 동일한 트랜잭션의 다른 데이터와 조인  
 경우에 따라 변경 데이터가 원본에서 커밋될 경우 변경 데이터를 트랜잭션에 대해 수집된 다른 정보와 조인하는 것이 유용할 수 있습니다. cdc.lsn_time_mapping 테이블의 tran_begin_lsn 열은 이러한 조인을 수행하는 데 필요한 정보를 제공합니다. 원본의 업데이트가 발생할 경우 시스템 동적 뷰 [sys.dm_tran_database_transactions](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql) 의 database_transaction_begin_lsn 값을 변경 데이터와 조인할 다른 정보와 함께 저장해야 합니다. fn_convertnumericlsntobinary 함수를 사용하면 database_transaction_begin_lsn 값과 tran_begin_lsn 값을 비교할 수 있습니다. 이 함수를 만드는 코드는 Create Function 템플릿 fn_convertnumericlsntobinary에서 사용할 수 있습니다. Return All Changes with a Given tran_begin_lsn 템플릿에서는 이러한 조인을 수행하는 방법을 보여 줍니다.  
  
### <a name="querying-using-datetime-wrapper-functions"></a>datetime 래퍼 함수를 사용하여 쿼리  
 변경 데이터를 쿼리하는 일반적인 응용 프로그램 시나리오는 datetime 값을 통해 경계가 지정된 슬라이딩 윈도우를 사용하여 변경 데이터를 정기적으로 요청하는 것입니다. 이러한 클래스의 소비자에 대해 변경 데이터 캡처는 변경 데이터 캡처 쿼리 함수에 대한 사용자 지정 래퍼 함수를 만드는 스크립트를 생성하는 [sys.sp_cdc_generate_wrapper_function](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql) 저장 프로시저를 제공합니다. 이러한 사용자 지정 래퍼를 사용하면 쿼리 간격을 datetime 쌍으로 표시할 수 있습니다.  
  
 이 저장 프로시저에 대한 호출 옵션을 사용하면 호출자가 액세스할 수 있는 모든 캡처 인스턴스에 대해 래퍼를 생성하거나 지정된 캡처 인스턴스에 대해서만 래퍼를 생성할 수 있습니다. 지원되는 옵션에는 캡처 간격의 상위 끝점을 열거나 닫을지 여부, 결과 집합에 포함해야 하는 사용 가능한 캡처된 열 및 연결된 업데이트 플래그가 있어야 하는 포함된 열을 지정하는 기능도 있습니다. 이 프로시저는 캡처 인스턴스 이름에서 파생 가능한 생성된 함수 이름 열과 래퍼 저장 프로시저에 대한 CREATE 문 열이 있는 결과 집합을 반환합니다. 모든 변경 내용 쿼리를 래핑하는 함수는 항상 생성됩니다. 캡처 인스턴스를 만들 때 @supports_net_changes 매개 변수를 설정한 경우 순 변경 내용 함수를 래핑하는 함수도 생성됩니다.  
  
 래퍼 저장 프로시저에 대한 CREATE 문을 생성하는 스크립트 생성 저장 프로시저를 호출하고 결과 CREATE 스크립트를 실행하여 함수를 만드는 작업은 응용 프로그램 디자이너가 수행해야 합니다. 이 작업은 캡처 인스턴스가 만들어질 때 자동으로 수행되지 않습니다.  
  
 datetime 래퍼는 사용자가 소유하며 호출자의 기본 스키마에서 만들어지 않습니다. 대부분의 사용자는 생성된 함수를 수정하지 않고 그대로 사용할 수 있습니다. 그러나 함수를 만들기 전에는 생성된 스크립트에 대한 추가 사용자 지정이 항상 가능합니다.  
  
 모든 변경 내용 쿼리를 래핑하는 함수의 이름은 캡처 인스턴스 이름 앞에 fn_all_changes_가 붙는 형태입니다. 순 변경 내용 함수에 사용되는 접두사는 fn_net_changes_입니다. 두 함수는 모두 연결된 변경 데이터 캡처 TVF와 마찬가지로 3개의 인수를 사용합니다. 그러나 래퍼에 대한 쿼리 간격은 두 개의 LSN 값 대신 두 개의 datetime 값에 의해 제한됩니다. 두 함수 집합에 대한 @row_filter_option 매개 변수는 같습니다.  
  
 생성된 래퍼 함수는 변경 데이터 캡처 시간대를 체계적으로 탐색하기 위해 이전 간격의 @end_time 매개 변수가 후속 간격의 @start_time 매개 변수로 사용된다는 규칙을 지원합니다. 래퍼 함수는 이 규칙이 준수되는 경우 datetime 값을 LSN 값에 매핑하고 데이터가 손실되거나 반복되지 않도록 합니다.  
  
 지정된 쿼리 창에서 닫힌 상한이나 열린 상한을 지원하는 래퍼를 생성할 수 있습니다. 즉, 호출자가 커밋 시간이 추출 간격의 상한과 같은 항목을 간격 내에 포함할지 여부를 지정할 수 있습니다. 기본적으로 상한이 포함됩니다.  
  
 @from_lsn 값 또는 @to_lsn 값에 대해 Null 값이 제공되면 생성된 쿼리 TVF가 실패하지만 datetime 래퍼 함수는 Null을 사용하여 datetime 래퍼가 모든 현재 변경 내용을 반환하도록 할 수 있습니다. 즉, NULL이 datetime 래퍼에 쿼리 창의 하위 끝점으로 제공되면 캡처 인스턴스 유효성 간격의 하위 끝점이 쿼리 TVF에 적용되는 기본 SELECT 문에 사용됩니다. 마찬가지로 NULL이 쿼리 창의 상위 끝점으로 제공되면 캡처 인스턴스 유효성 간격의 상위 끝점이 쿼리 TVF에서 선택할 때 사용됩니다.  
  
 래퍼 함수에서 반환하는 결과 집합에는 요청된 모든 열이 포함되며, 그 뒤에는 행과 연결된 작업을 식별하는 한 문자 또는 두 문자로 기록되는 작업 열이 옵니다. 업데이트 플래그는 요청 시 @update_flag_list 매개 변수에 지정된 순서대로 작업 코드 뒤에 비트 열로 표시됩니다. 생성된 datetime 래퍼를 사용자 지정하는 호출 옵션에 대한 자세한 내용은 [sys.sp_cdc_generate_wrapper_function&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql)을 참조하세요.  
  
 Instantiate a Wrapper TVF With Update Flag 템플릿에서는 생성된 래퍼 함수를 사용자 지정하여 지정된 열에 대한 업데이트 플래그를 순 변경 내용 쿼리에서 반환하는 결과 집합에 추가하는 방법을 보여 줍니다. Instantiate CDC Wrapper TVFs for a Schema 템플릿에서는 지정된 데이터베이스 스키마에서 원본 테이블에 대해 생성된 모든 캡처 인스턴스에 대해 쿼리 TVF의 datetime 래퍼를 인스턴스화하는 방법을 보여 줍니다.  
  
 datetime 래퍼를 사용하여 변경 데이터를 쿼리하는 예를 보려면 Get Net Changes Using Wrapper With Update Flags 템플릿을 참조하십시오. 이 템플릿에서는 래퍼가 업데이트 플래그를 반환하도록 구성된 경우 래퍼 함수를 사용하여 순 변경 내용을 쿼리하는 방법을 보여 줍니다. 행 필터 옵션 'all with mask'는 업데이트 시 Null이 아닌 업데이트 마스크를 반환하는 기본 쿼리 함수에 필요합니다. NULL 값은 기본 LSN 기반 쿼리를 수행할 때 캡처 인스턴스에 대한 유효성 간격의 하위 끝점 및 상위 끝점을 사용하도록 함수에 알리기 위해 하한 및 상한 datetime 간격 경계 둘 다에 전달됩니다. 이 함수는 캡처 인스턴스의 유효한 간격 내에서 원본 행이 수정될 때마다 행을 하나씩 반환합니다.  
  
### <a name="using-the-datetime-wrapper-functions-to-transition-between-capture-instances"></a>datetime 래퍼 함수를 사용하여 캡처 인스턴스 간 전환  
 변경 데이터 캡처는 하나의 추적된 원본 테이블당 최대 두 개의 캡처 인스턴스를 지원합니다. 이 기능은 주로 원본 테이블의 DDL(데이터 정의 언어)을 변경할 경우 추적에 사용할 수 있는 열 집합이 확장될 때 여러 인스턴스 간에 전환하는 데 사용됩니다. 새 캡처 인스턴스로 전환할 때 기본 쿼리 함수 이름의 변경으로부터 더 높은 응용 프로그램 수준을 보호하는 한 가지 방법은 래퍼 함수를 사용하여 기본 호출을 래핑하는 것입니다. 그런 다음 래퍼 함수의 이름이 그대로 유지되는지 확인합니다. 전환 작업을 수행할 예정인 경우 이전 래퍼 함수를 삭제하고 이전 래퍼 함수와 동일한 이름을 사용하는 새 래퍼 함수를 만들어 새 쿼리 함수를 참조할 수 있습니다. 먼저 생성된 스크립트를 수정하여 동일한 이름의 래퍼 함수를 만들면 더 높은 응용 프로그램 계층에 영향을 주지 않고 새 캡처 인스턴스로 전환할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 변경 내용 추적&#40;SQL Server&#41;](../track-changes/track-data-changes-sql-server.md)   
 [변경 데이터 캡처 정보&#40;SQL Server&#41;](../track-changes/about-change-data-capture-sql-server.md)   
 [변경 데이터 캡처 설정 및 해제&#40;SQL Server&#41;](../track-changes/enable-and-disable-change-data-capture-sql-server.md)   
 [변경 데이터 캡처 관리 및 모니터링&#40;SQL Server&#41;](../track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  

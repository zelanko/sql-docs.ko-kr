---
title: sys.dm_pdw_exec_requests (거래-SQL) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 4f4ebcbf84da7d899b4d4cbd861cfb2ae3f75863
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82087563"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>sys.dm_pdw_exec_requests (거래 SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서 현재 또는 최근에 활성 상태인 모든 요청에 대한 정보를 보유합니다. 요청/쿼리당 하나의 행을 나열합니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 보기의 키입니다. 요청과 연결된 고유 숫자 ID입니다.|시스템의 모든 요청에 대해 고유합니다.|  
|session_id|**nvarchar(32)**|이 쿼리가 실행된 세션과 연결된 고유 숫자 ID입니다. [sys.dm_pdw_exec_sessions &#40;거래-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)참조하십시오.||  
|상태|**nvarchar(32)**|요청의 현재 상태입니다.|'실행 중', '일시 중단됨', '완료됨', '취소됨', '실패'.|  
|submit_time|**datetime**|실행을 위해 요청이 제출된 시간입니다.|유효한 **날짜 시간은** 현재 시간과 같거나 start_time.|  
|start_time|**datetime**|요청 실행이 시작된 시간입니다.|큐에 대기된 요청에 대해 NULL; 그렇지 않으면 유효한 **날짜 시간이** 현재 시간으로 작거나 동일합니다.|  
|end_compile_time|**datetime**|엔진이 요청 컴파일을 완료한 시간입니다.|아직 컴파일되지 않은 요청에 대해 NULL; 그렇지 않으면 유효한 **날짜 시간이** start_time 미만이고 현재 시간보다 낮거나 같습니다.|
|end_time|**datetime**|요청 실행이 완료, 실패 또는 취소된 시간입니다.|큐에 대기 중인 요청 또는 활성 요청에 대해 Null; 그렇지 않으면 유효한 **날짜 시간이** 현재 시간으로 작거나 동일합니다.|  
|total_elapsed_time|**int**|요청이 시작된 이후 실행 시간이 밀리초 단위로 경과했습니다.|0과 start_time end_time 차이.</br></br> total_elapsed_time 정수의 최대값을 초과하면 total_elapsed_time 계속 최대값이 됩니다. 이 조건은 "최대값이 초과되었습니다"라는 경고를 생성합니다.</br></br> 밀리초의 최대값은 24.8일과 동일합니다.|  
|label|**nvarchar(255)**|일부 SELECT 쿼리 문과 연결된 선택적 레이블 문자열입니다.|'a-z', 'A-Z','0-9',''_'를 포함하는 모든 문자열.|  
|error_id|**은바르차르 (36)**|요청과 연결된 오류의 고유 ID(있는 경우)입니다.|[sys.dm_pdw_errors &#40;거래-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)참조하십시오. 오류가 발생하지 않은 경우 NULL로 설정합니다.|  
|database_id|**int**|명시적 컨텍스트에서 사용하는 데이터베이스의 식별자(예: USE DB_X).|[transact-SQL&#41;&#40;sys.데이터베이스의 ID를 ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)참조하십시오.|  
|command|**nvarchar(4000)**|사용자가 제출한 요청의 전체 텍스트를 보유합니다.|유효한 쿼리 또는 요청 텍스트입니다. 4000바이트보다 긴 쿼리는 잘립니다.|  
|resource_class|**nvarchar (20)**|이 요청에 사용된 워크로드 그룹입니다. |정적 리소스 클래스</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>동적 리소스 클래스</br>스몰RC</br>미디엄 RC</br>라지RC</br>XLargeRC|
|importance|**nvarchar(128)**|실행된 요청을 설정하는 중요도입니다.  이는 이 워크로드 그룹 및 공유 리소스에 대한 워크로드 그룹 간 요청의 상대적 중요성입니다.  분류자에 지정된 중요도는 워크로드 그룹 중요도 설정을 재정의합니다.</br>적용 대상: Azure SQL Data Warehouse|NULL</br>low</br>below_normal</br>일반(기본값)</br>above_normal</br>high|
|group_name|**sysname** |리소스를 사용하는 요청의 경우 group_name 요청이 실행 중인 워크로드 그룹의 이름입니다.  요청이 리소스를 사용하지 않는 경우 group_name null입니다.</br>적용 대상: Azure SQL Data Warehouse|
|classifier_name|**sysname**|리소스를 사용하는 요청의 경우 리소스 및 중요도를 할당하는 데 사용되는 분류자의 이름입니다.||
|resource_allocation_percentage|**십진수 (5,2)**|요청에 할당된 리소스의 백분율 양입니다.</br>적용 대상: Azure SQL Data Warehouse|
|result_cache_hit|**16 진수**|완료된 쿼리가 결과 집합 캐시를 사용했는지 여부를 자세히 설명합니다.  </br>적용 대상: Azure SQL Data Warehouse| 1 = 결과 세트 캐시 적중 </br> 0 = 결과 세트 캐시 누락 </br> 음수 값 = 결과 집합 캐싱이 사용되지 않은 이유입니다.  자세한 내용은 비고 섹션을 참조하십시오.|
||||
  
## <a name="remarks"></a>설명 
 이 뷰에서 유지되는 최대 행에 대한 자세한 내용은 [용량 제한](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 항목의 메타데이터 섹션을 참조하세요.

 result_cache_hit 결과 집합 캐시를 쿼리에서 사용하는 비트마스크입니다.  이 열은 [| (비트 와이즈 OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md) 하나 이상의 값으로 생성됩니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1**|결과 세트 캐시 적중|  
|-**0x00**|결과 세트 캐시 누락|  
|-**0x01**|데이터베이스에서 결과 집합 캐싱을 사용할 수 없습니다.|  
|-**0x02**|세션에서 결과 집합 캐싱이 비활성화됩니다. | 
|-**0x04**|쿼리에 대한 데이터 원본이 없기 때문에 결과 집합 캐싱이 비활성화됩니다.|  
|-**0x08**|행 수준 보안 조건으로 인해 결과 집합 캐싱이 비활성화됩니다.|  
|-**0x10**|쿼리에서 시스템 테이블, 임시 테이블 또는 외부 테이블을 사용하기 때문에 결과 집합 캐싱이 비활성화됩니다.|  
|-**0x20**|쿼리에 런타임 상수, 사용자 정의 함수 또는 비결정 함수가 포함되어 있으므로 결과 집합 캐싱이 비활성화됩니다.|  
|-**0x40**|결과 집합 캐싱은 예상 결과 집합 크기가 10GB>때문에 비활성화됩니다.|  
|-**0x80**|결과 집합에는 크기가 큰 행(>64kb)이 포함되어 있으므로 결과 집합 캐싱이 비활성화됩니다.|  
  
## <a name="permissions"></a>사용 권한

 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="security"></a>보안

 sys.dm_pdw_exec_requests 데이터베이스별 사용 권한에 따라 쿼리 결과를 필터링하지 않습니다. VIEW SERVER 상태 권한이 있는 로그인은 모든 데이터베이스에 대한 결과 쿼리 결과를 얻을 수 있습니다.  
  
>[!WARNING]  
>공격자는 sys.dm_pdw_exec_requests 사용하여 VIEW SERVER STATE 권한을 가지는 것만으로 데이터베이스별 권한이 없는 상태에서 특정 데이터베이스 개체에 대한 정보를 검색할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 보기 &#40;거래-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)

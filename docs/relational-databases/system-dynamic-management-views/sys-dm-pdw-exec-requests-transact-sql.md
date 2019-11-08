---
title: sys. dm_pdw_exec_requests (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 15d27881378a88c8f4ae6d65640be6218ecd3530
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632760"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>sys. dm_pdw_exec_requests (Transact-sql)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서 현재 또는 최근에 활성 상태인 모든 요청에 대 한 정보를 저장 합니다. 요청/쿼리 당 한 개의 행을 나열 합니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 보기의 키입니다. 요청과 연결 된 고유 숫자 ID입니다.|시스템의 모든 요청에 대해 고유 합니다.|  
|session_id|**nvarchar(32)**|이 쿼리가 실행 된 세션과 연결 된 고유 숫자 ID입니다. [Dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)을 참조 하세요.||  
|상태|**nvarchar(32)**|요청의 현재 상태입니다.|' Running ', ' Suspended ', ' Completed ', ' Canceled ', ' Failed '.|  
|submit_time|**datetime**|요청이 실행을 위해 제출 된 시간입니다.|유효한 **날짜/** 시간이 현재 시간 보다 작거나 같고 start_time 합니다.|  
|start_time|**datetime**|요청 실행이 시작 된 시간입니다.|대기 중인 요청에 대해 NULL입니다. 그렇지 않으면 유효한 **날짜/** 시간이 현재 시간 보다 작거나 같습니다.|  
|end_compile_time|**datetime**|엔진이 요청 컴파일을 완료 한 시간입니다.|아직 컴파일되지 않은 요청의 경우 NULL입니다. 그렇지 않으면 start_time 보다 작은 유효한 **날짜/** 시간이 현재 시간 보다 작거나 같습니다.|
|end_time|**datetime**|요청 실행이 완료, 실패 또는 취소 된 시간입니다.|대기 중이거나 활성 요청의 경우 Null입니다. 그렇지 않으면 현재 시간 보다 작거나 같은 유효한 **날짜/** 시간입니다.|  
|total_elapsed_time|**int**|요청이 시작 된 이후 실행에서 경과한 시간 (밀리초)입니다.|0과 end_time 사이의 차이를 start_time 합니다.</br></br> Total_elapsed_time 정수에 대 한 최대값을 초과 하는 경우 total_elapsed_time는 최대 값으로 계속 됩니다. 이 경우 "최 댓 값이 초과 되었습니다." 라는 경고가 생성 됩니다.</br></br> 최대 값 (밀리초)은 24.8 일입니다.|  
|레이블|**nvarchar(255)**|일부 SELECT 쿼리 문과 연결 된 선택적 레이블 문자열입니다.|' A-z ', ' a-z ', ' 0-9 ', ' _ '를 포함 하는 문자열입니다.|  
|error_id|**nvarchar (36)**|요청과 관련 된 오류의 고유 ID입니다 (있는 경우).|[ &#40;Dm_pdw_errors transact-sql을&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)참조 하세요. 오류가 발생 하지 않은 경우 NULL로 설정 합니다.|  
|database_id|**int**|명시적 컨텍스트에서 사용 되는 데이터베이스의 식별자입니다 (예: DB_X 사용).|[SYS .sql &#40;&#41;데이터베이스](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)의 ID를 참조 하십시오.|  
|command|**nvarchar(4000)**|사용자가 제출한 요청의 전체 텍스트를 저장 합니다.|모든 유효한 쿼리 또는 요청 텍스트입니다. 4000 바이트 보다 긴 쿼리는 잘립니다.|  
|resource_class|**nvarchar (20)**|이 요청에 사용 되는 작업 그룹입니다. |정적 리소스 클래스</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>동적 리소스 클래스</br>SmallRC</br>MediumRC</br>LargeRC</br>XLargeRC|
|importance|**nvarchar(128)**|요청을 실행 하는 중요도를 설정 합니다.  이 작업 그룹 및 공유 리소스에 대 한 작업 그룹에 있는 요청의 상대적 중요도입니다.  분류자에 지정 된 중요도는 작업 그룹 중요도 설정을 재정의 합니다.</br>적용 대상: Azure SQL Data Warehouse|NULL</br>low</br>below_normal</br>보통 (기본값)</br>above_normal</br>high|
|group_name|**sysname** |리소스를 활용 하는 요청의 경우 group_name은 요청을 실행 중인 작업 그룹의 이름입니다.  요청에서 리소스를 사용 하지 않는 경우 group_name은 null입니다.</br>적용 대상: Azure SQL Data Warehouse|
|classifier_name|**sysname**|리소스를 활용 하는 요청의 경우 리소스 및 중요도를 할당 하는 데 사용 되는 분류자의 이름입니다.||
|resource_allocation_percentage|**decimal (5, 2)**|요청에 할당 된 리소스의 비율입니다.</br>적용 대상: Azure SQL Data Warehouse|
|result_set_cache|**bit**|완료 된 쿼리가 결과 캐시 적중 (1) 되었는지 아니면 그렇지 않은지 (0)에 대해 자세히 설명 합니다. </br>적용 대상: Azure SQL Data Warehouse|0, 1|
||||
  
 이 보기에 의해 유지 되는 최대 행에 대 한 자세한 내용은 [용량 제한](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 항목에서 메타 데이터 섹션을 참조 하세요.
  
## <a name="permissions"></a>사용 권한

 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="security"></a>보안

 dm_pdw_exec_requests는 데이터베이스 관련 권한에 따라 쿼리 결과를 필터링 하지 않습니다. VIEW SERVER STATE 권한이 있는 로그인은 모든 데이터베이스에 대 한 결과 쿼리 결과를 가져올 수 있습니다.  
  
>[!WARNING]  
>공격자는 보기 서버 상태 권한만 있고 데이터베이스 관련 사용 권한을가지고 있지 않기 때문에 특정 데이터베이스 개체에 대 한 정보를 검색 하는 데 dm_pdw_exec_requests를 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:

 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)

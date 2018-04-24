---
title: 관리 데이터 웨어하우스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: data-collection
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data collector [SQL Server], management data warehouse
- data warehouse
- management data warehouse
ms.assetid: 9874a8b2-7ccd-494a-944c-ad33b30b5499
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a5184f3e59dc3e592b73696b3ebaba994a53211c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="management-data-warehouse"></a>관리 데이터 웨어하우스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  관리 데이터 웨어하우스는 데이터 컬렉션 대상인 서버에서 수집되는 데이터를 포함하는 관계형 데이터베이스입니다. 이 데이터를 사용하여 시스템 데이터 컬렉션 집합의 보고서를 생성하고 사용자 지정 보고서를 만들 수도 있습니다.  
  
 데이터 수집기 인프라는 데이터베이스 관리자가 정의하는 보존 정책을 구현하기 위해 필요한 작업 및 유지 관리 계획을 정의합니다.  
  
> [!IMPORTANT]  
>  이 릴리스의 데이터 수집기에서는 로깅을 최소화하기 위해 단순 복구 모델을 사용하여 관리 데이터 웨어하우스를 만듭니다. 사용자는 해당 조직에 맞는 복구 모델을 구현해야 합니다.  
  
## <a name="deploying-and-using-the-data-warehouse"></a>데이터 웨어하우스 배포 및 사용  
 데이터 수집기가 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 동일한 인스턴스에 관리 데이터 웨어하우스를 설치할 수 있습니다. 그러나 모니터링 중인 서버에서 서버 리소스 또는 성능이 문제가 될 경우 다른 컴퓨터에 관리 데이터 웨어하우스를 설치할 수 있습니다.  
  
 미리 정의된 시스템 컬렉션 집합에 필요한 스키마와 이들의 개체는 관리 데이터 웨어하우스를 만들 때 생성됩니다. 만들어진 스키마는 핵심이며 스냅숏입니다. 세 번째 스키마인 custom_snapshots는 일반 T-SQL 쿼리 수집기 유형을 사용하는 컬렉션 항목을 포함하는 사용자 정의 컬렉션 집합이 만들어질 때 생성됩니다.  
  
###### <a name="core-schema"></a>core 스키마  
 core 스키마는 수집된 데이터를 구성하고 식별하는 데 사용되는 테이블, 저장 프로시저 및 뷰에 대해 설명합니다. 이러한 테이블은 개별 수집기 유형에 대해 생성되는 모든 데이터 테이블에서 공유됩니다. 이 스키마는 잠겨 있으며 관리 데이터 웨어하우스 데이터베이스의 소유자만 수정할 수 있습니다. 이 스키마의 테이블 이름에는 "core"가 접두사로 붙습니다.  
  
 다음 표에서는 core 스키마의 데이터베이스 테이블에 대해 설명합니다. 이러한 데이터베이스 테이블에서는 데이터 수집기를 사용하여 데이터가 있었던 위치, 데이터를 삽입한 사용자 및 데이터가 데이터 웨어하우스에 업로드된 시간을 추적할 수 있습니다.  
  
|테이블 이름|Description|  
|----------------|-----------------|  
|core.performance_counter_report_group_items|관리 데이터 웨어하우스 보고서에서 성능 카운터를 그룹화하고 집계하는 방법에 대한 정보를 저장합니다.|  
|core.snapshots_internal|새로운 각 스냅숏을 식별합니다. 업로드 패키지가 새 일괄 처리 데이터를 업로드하기 시작할 때마다 새 행이 이 테이블에 삽입됩니다.|  
|core.snapshot_timetable_internal|스냅숏 시간에 대한 정보를 저장합니다. 많은 스냅숏이 거의 동시에 발생할 수 있으므로 스냅숏 시간은 별도의 테이블에 저장됩니다.|  
|core.source.info_internal|이 테이블은 데이터 원본에 대한 정보를 저장합니다. 새 컬렉션 집합이 데이터를 데이터 웨어하우스에 업로드하기 시작할 때마다 이 테이블이 업데이트됩니다.|  
|core.supported_collector_types_internal|데이터를 관리 데이터 웨어하우스에 업로드할 수 있는 등록된 수집기 유형의 ID를 포함합니다. 이 테이블은 웨어하우스의 스키마가 새 수집기 유형을 지원하도록 업데이트되는 경우에만 업데이트됩니다. 관리 데이터 웨어하우스가 생성되면 데이터 수집기에서 제공하는 수집기 유형의 ID로 이 테이블이 채워집니다.|  
|core.wait_categories|wait_type 특징에 따라 대기 유형을 그룹핑하는 데 사용되는 범주를 포함합니다.|  
|core.wait_types|데이터 수집기에 의해 인식되는 대기 유형을 포함합니다.|  
|core.purge_info_internal|관리 데이터 웨어하우스로부터 데이터 제거를 중지하기 위해 수행한 요청을 나타냅니다.|  
  
 위의 테이블이 수집기 유형 테이블에 정보를 저장하는 데 사용됩니다. 예를 들어 일반 SQL 추적 수집기 유형은 다음 테이블을 사용하여 추적 데이터를 저장합니다.  
  
-   core.source_info_internal  
  
-   core.snapshots_internal  
  
-   snapshots.trace_info  
  
-   snapshots.trace_data  
  
###### <a name="snapshots-schema"></a>snapshot 스키마  
 snapshots 스키마는 제공된 수집기 유형에 의해 수집된 데이터를 저장하고 유지 관리하는 데 필요한 개체에 대해 설명합니다. 이 스키마의 테이블은 고정되며 수집기 유형의 수명 동안 변경될 필요가 없습니다. 스키마를 변경해야 할 경우에는 mdw_admin 역할의 멤버만 변경할 수 있습니다. 이러한 테이블은 시스템 데이터 컬렉션 집합에서 수집한 데이터를 저장하기 위해 만듭니다.  
  
 다음 테이블은 서버 작업 및 쿼리 통계 컬렉션 집합에 필요한 관리 데이터 웨어하우스 스키마의 일부를 보여 줍니다.  
  
-   시스템 수준 리소스 테이블  
  
    -   **snapshots.os_wait_stats**  
  
    -   **snapshots.os_latch_stats**  
  
    -   **snapshots.os_schedulers**  
  
    -   **snapshots.os_memory_clerks**  
  
    -   **snapshots.os_memory_nodes**  
  
    -   snapshots.sql_process_and_system_memory  
  
-   시스템 작업  
  
    -   snapshots.active_sessions_and_requests  
  
-   쿼리 통계  
  
    -   snapshots.query_stats  
  
-   I/O 통계  
  
    -   **snapshots.io_virtual_file_stats**  
  
-   쿼리 텍스트 및 계획  
  
    -   snapshots.notable_query_text  
  
    -   snapshots.notable_query_plan  
  
-   정규화된 쿼리 통계  
  
    -   snapshots.distinct_queries  
  
    -   snapshots.distinct_query_to_handle  
  
 **Custom_snapshots 스키마**  
  
 custom_snapshots 스키마는 표준 또는 타사 수집기 유형을 사용하여 사용자 정의 컬렉션 집합을 만들 때 생성된 새 테이블과 뷰에 대해 설명합니다. 컬렉션 항목에 새 데이터 테이블이 필요한 모든 수집기 유형은 이 스키마에 테이블을 만들 수 있습니다. 새 테이블은 mdw_writer 역할의 멤버가 추가할 수 있습니다. 스키마에 대한 다른 변경 작업은 mdw_admin 역할의 멤버만 수행할 수 있습니다.  
  
 데이터베이스 테이블 열에 대한 자세한 데이터 형식 및 콘텐츠 정보는 각 테이블에 해당되는 데이터 수집기 저장 프로시저에 대한 설명서를 참조하십시오.  
  
### <a name="best-practices"></a>최선의 구현 방법  
 관리 데이터 웨어하우스를 사용할 때는 다음과 같은 최선의 방법을 따르는 것이 좋습니다.  
  
-   새 수집기 유형을 추가하지 않는 한 관리 데이터 웨어하우스 테이블의 메타데이터를 수정하지 않습니다.  
  
-   관리 데이터 웨어하우스의 데이터를 직접 수정하지 않습니다. 수집한 데이터를 변경하면 수집된 데이터의 타당성이 무효화됩니다.  
  
-   테이블을 직접 사용하는 대신 데이터 수집기와 함께 제공되는 문서화된 저장 프로시저 및 함수를 사용하여 인스턴스 및 응용 프로그램 데이터에 액세스합니다. 테이블 이름과 정의는 변경될 수 있습니다. 이러한 정보는 응용 프로그램을 업데이트할 때 변경되며 후속 릴리스에서 변경될 수 있습니다.  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|"core 스키마" 섹션에 core.performance_counter_report_group_items 테이블이 추가되었습니다.|  
|"snapshots 스키마" 섹션의 테이블 목록이 업데이트되었습니다. snapshots.os_memory_clerks,snapshots.sql_process_and_system_memory 및 snapshots.io_virtual_file_stats가 추가되었습니다. snapshots.os_process_memory 및 snapshots.distinct_query_stats가 제거되었습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [관리 데이터 웨어하우스 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql.md)   
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)   
 [컬렉션 집합 보고서 보기&#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
  

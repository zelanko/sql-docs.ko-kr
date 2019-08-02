---
title: R 및 Python에 대 한 리소스 풀을 만드는 방법
description: SQL Server 데이터베이스 엔진 인스턴스에서 R 또는 Python 프로세스에 대 한 SQL Server 리소스 풀을 정의 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 882b9b15fbba567f30172d625af3867b27ae387e
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715901"
---
# <a name="how-to-create-a-resource-pool-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에 대 한 리소스 풀을 만드는 방법
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server에서 R 및 Python 기계 학습 워크 로드를 관리 하는 데 특별히 리소스 풀을 만들고 사용 하는 방법을 설명 합니다. 이미 기계 학습 기능을 설치 하 고 사용 하도록 설정 하 고, R 또는 Python과 같은 외부 프로세스에서 사용 하는 리소스의 보다 세분화 된 관리를 지원 하도록 인스턴스를 다시 구성 하려고 한다고 가정 합니다.

프로세스에는 여러 단계가 포함 됩니다.

1.  기존 리소스 풀의 상태를 검토 합니다. 기존 리소스를 사용 하는 서비스를 이해 하는 것이 중요 합니다.
2.  서버 리소스 풀을 수정 합니다.
3.  외부 프로세스에 대 한 새 리소스 풀을 만듭니다.
4.  외부 스크립트 요청을 식별 하는 분류 함수를 만듭니다.
5.  새 외부 리소스 풀이 지정 된 클라이언트 또는 계정에서 R 또는 Python 작업을 캡처링 하는지 확인 합니다.

##  <a name="bkmk_ReviewStatus"></a> 기존 리소스 풀의 상태 검토
  
1.  다음 문을 사용 하 여 서버에 대 한 기본 풀에 할당 된 리소스를 확인 합니다.
  
    ```sql
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'
    ```

    **샘플 결과**

    |pool_id|NAME|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|
    |-|-|-|-|-|-|-|-|-|
    |2|기본|0|100|0|100|100|0|0|

2.  기본 **외부** 리소스 풀에 할당된 리소스를 확인합니다.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'
    ```

    **샘플 결과**

    |external_pool_id|NAME|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|기본|100|20|0|2|
 
3.  이러한 서버 기본 설정에서는 외부 런타임에서 대부분의 작업을 완료 하는 데 충분 한 리소스가 없을 수 있습니다. 이를 변경하려면 다음과 같이 서버 리소스 사용을 수정해야 합니다.
  
    -   데이터베이스 엔진에서 사용할 수 있는 최대 컴퓨터 메모리를 줄입니다.
  
    -   외부 프로세스에서 사용할 수 있는 최대 컴퓨터 메모리를 늘립니다.

## <a name="modify-server-resource-usage"></a>서버 리소스 사용 수정

1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 다음 문을 실행하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 사용량을 '최대 서버 메모리' 설정 값의 **60%** 로 제한합니다.

    ```sql
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);
    ```
  
2.  마찬가지로, 다음 문을 실행하여 외부 프로세스의 메모리 사용을 총 컴퓨터 리소스의 **40%** 로 제한합니다.
  
    ```sql
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);
    ```
  
3.  이러한 변경 내용을 적용하려면 다음과 같이 리소스 관리자를 다시 구성하고 다시 시작해야 합니다.
  
    ```sql
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
    > [!NOTE]
    >  이러한 설정으로 시작 하는 것이 좋습니다. 사용자 환경 및 워크 로드에 대 한 올바른 잔액을 확인 하려면 다른 서버 프로세스의 조명에서 기계 학습 작업을 평가 해야 합니다.

## <a name="create-a-user-defined-external-resource-pool"></a>사용자 정의 외부 리소스 풀 만들기
  
1.  리소스 관리자의 구성 변경 내용은 서버 전체에 적용되고 서버에 대한 기본 풀을 사용하는 워크로드 및 외부 풀을 사용하는 워크로드에 영향을 줍니다.
  
     따라서 우선 순위가 있는 워크로드를 보다 세부적으로 제어하려면 사용자 정의 외부 리소스 풀을 새로 만들 수 있습니다. 또한 분류 함수를 정의하고 외부 리소스 풀에 할당해야 합니다. **EXTERNAL** 키워드는 new입니다.
  
     먼저 새 *사용자 정의 외부 리소스 풀*을 만듭니다. 다음 예제에서는 풀 이름이 **ds_ep**로 지정됩니다.
  
    ```sql
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);
    ```

2.  세션 요청 관리에 사용할 `ds_wg`라는 워크로드 그룹을 만듭니다. SQL 쿼리의 경우 기본 풀을 사용하고, 모든 외부 프로세스의 경우 쿼리에서 `ds_ep` 풀을 사용합니다.
  
    ```sql
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";
    ```
  
     요청을 분류할 수 없을 때마다 또는 다른 분류 오류가 있을 경우 요청이 기본 그룹에 할당됩니다.
  
     자세한 내용은 [리소스 관리자 워크로드 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md) 및 [CREATE WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)을 참조하세요.
  
## <a name="create-a-classification-function-for-machine-learning"></a>기계 학습에 대 한 분류 함수 만들기
  
분류 함수는 들어오는 태스크를 검사하고 현재 리소스 풀을 사용하여 실행할 수 있는 태스크인지 확인합니다. 분류 함수의 조건을 충족하지 않는 태스크는 서버의 기본 리소스 풀에 다시 할당됩니다.
  
1. 먼저 Resource Governor에서 분류자 함수를 사용 하 여 리소스 풀을 확인 하도록 지정 합니다. 분류자 함수에 대 한 자리 표시자로 **null** 을 할당할 수 있습니다.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
     자세한 내용은 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)를 참조하세요.
  
2.  각 리소스 풀의 분류자 함수에서 리소스 풀에 할당 해야 하는 문의 형식 또는 들어오는 요청을 정의 합니다.
  
     예를 들어 다음 함수는 요청을 보낸 애플리케이션이 'Microsoft R Host' 또는 'RStudio'인 경우 사용자 정의 외부 리소스 풀에 할당된 스키마의 이름을 반환하고, 그렇지 않으면 기본 리소스 풀을 반환합니다.
  
    ```sql
    USE master
    GO
    CREATE FUNCTION is_ds_apps()
    RETURNS sysname
    WITH schemabinding
    AS
    BEGIN
        IF program_name() in ('Microsoft R Host', 'RStudio') RETURN 'ds_wg';
        RETURN 'default'
        END;
    GO
    ```
  
3.  함수가 생성되면 이전에 정의한 외부 리소스 그룹에 새 분류자 함수를 할당하도록 리소스 그룹을 다시 구성합니다.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);
    ALTER RESOURCE GOVERNOR WITH reconfigure;
    GO
    ```

## <a name="verify-new-resource-pools-and-affinity"></a>새 리소스 풀 및 선호도 확인

변경 된 내용이 있는지 확인 하려면 다음 인스턴스 리소스 풀과 연결 된 각 작업 그룹에 대 한 서버 메모리와 CPU의 구성을 확인 해야 합니다.

+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버에 대 한 기본 풀
+ 외부 프로세스에 대 한 기본 리소스 풀
+ 외부 프로세스에 대 한 사용자 정의 풀

1. 모든 작업 그룹을 보려면 다음 문을 실행 합니다.

    ```sql
    SELECT * FROM sys.resource_governor_workload_groups;
    ```

    **샘플 결과**

    |group_id|NAME|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_id|
    |-|-|-|-|-|-|-|-|-|-|
    |1|내부|보통|25|0|0|0|0|1|2|
    |2|기본|보통|25|0|0|0|0|2|2|
    |256|ds_wg|보통|25|0|0|0|0|2|256|
  
2.  새 카탈로그 뷰 [resource_governor_external_resource_pools &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)을 사용 하 여 모든 외부 리소스 풀을 볼 수 있습니다.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools;
    ```

    **샘플 결과**
    
    |external_pool_id|NAME|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|기본|100|20|0|2|
    |256|ds_ep|100|40|0|1|
  
     자세한 내용은 [리소스 관리자 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)를 참조하세요.
  
3.  다음 문을 실행 하 여 외부 리소스 풀에 선호도가 설정 된 컴퓨터 리소스에 대 한 정보를 반환 합니다 (해당 하는 경우).
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;
    ```
  
     이 경우 풀이 AUTO 선호도로 생성되었으므로 정보가 표시되지 않습니다. 자세한 내용은 [sys.dm_resource_governor_resource_pool_affinity&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

서버 리소스를 관리 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

+  [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md) 
+ [Resource Governor 관련 된 동적 관리 &#40;뷰 transact-sql&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)

기계 학습에 대 한 리소스 관리의 개요는 다음을 참조 하세요.

+  [Machine Learning Services에 대 한 리소스 관리](../../advanced-analytics/r/resource-governance-for-r-services.md)

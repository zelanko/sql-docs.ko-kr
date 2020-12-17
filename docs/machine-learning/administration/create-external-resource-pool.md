---
title: 리소스 풀 만들기
description: SQL Server Machine Learning Services에서 Python 및 R 워크로드를 관리하기 위해 리소스 풀을 만들고 사용하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/06/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: da6f6817856efd9dd0310211998230d49e6f3d1b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471394"
---
# <a name="create-a-resource-pool-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services의 사용자 계정 풀 만들기
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

SQL Server Machine Learning Services에서 Python 및 R 워크로드를 관리하기 위해 리소스 풀을 만들고 사용하는 방법에 대해 알아봅니다. 

이 프로세스에는 여러 단계가 포함됩니다.

1. 기존 리소스 풀의 상태를 검토합니다. 기존 리소스를 사용하는 서비스를 이해하는 것이 중요합니다.
2. 서버 리소스 풀을 수정합니다.
3. 외부 프로세스에 대한 새 리소스 풀을 만듭니다.
4. 외부 스크립트 요청을 식별하는 분류 함수를 만듭니다.
5. 새 외부 리소스 풀이 지정된 클라이언트 또는 계정에서 R 또는 Python 작업을 캡처하고 있는지 확인합니다.

<a name="bkmk_ReviewStatus"></a>

##  <a name="review-the-status-of-existing-resource-pools"></a>기존 리소스 풀의 상태 검토
  
1.  다음과 같은 명령문을 사용하여 서버에 대한 기본 풀에 할당된 리소스를 확인합니다.
  
    ```sql
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'
    ```

    **샘플 결과**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|
    |-|-|-|-|-|-|-|-|-|
    |2|기본값|0|100|0|100|100|0|0|

2.  기본 **외부** 리소스 풀에 할당된 리소스를 확인합니다.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'
    ```

    **샘플 결과**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|버전|
    |-|-|-|-|-|-|
    |2|기본값|100|20|0|2|
 
3.  이러한 서버 기본 설정에서 외부 런타임은 대부분의 작업을 완료하기 위한 리소스가 부족합니다. 리소스를 향상시키려면 다음과 같이 서버 리소스 사용을 수정해야 합니다.
  
    -   데이터베이스 엔진에서 사용할 수 있는 최대 컴퓨터 메모리를 줄입니다.
  
    -   외부 프로세스에서 사용할 수 있는 최대 컴퓨터 메모리를 늘립니다.

## <a name="modify-server-resource-usage"></a>서버 리소스 사용 수정

1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 다음 문을 실행하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 사용량을 '최대 서버 메모리' 설정 값의 **60%** 로 제한합니다.

    ```sql
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);
    ```
  
2. 다음 문을 실행하여 외부 프로세스의 메모리 사용을 총 컴퓨터 리소스의 **40%** 로 제한합니다.
  
    ```sql
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);
    ```
  
3.  이러한 변경 내용을 적용하려면 다음과 같이 리소스 관리자를 다시 구성하고 다시 시작해야 합니다.
  
    ```sql
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
    > [!NOTE]
    >  이러한 설정은 시작하는 제안된 설정일 뿐입니다. 다른 서버 프로세스에 비추어 기계 학습 작업을 평가하여 환경 및 워크로드에 맞는 균형을 확인해야 합니다.

## <a name="create-a-user-defined-external-resource-pool"></a>사용자 정의 외부 리소스 풀 만들기
  
1.  Resource Governor의 구성에 대한 모든 변경 내용은 전체 서버에 적용됩니다. 변경 내용은 서버의 기본 풀을 사용하는 워크로드뿐 아니라 외부 풀을 사용하는 워크로드에도 영향을 줍니다.
  
     우선 순위가 있는 워크로드를 보다 세부적으로 제어하려면 사용자 정의 외부 리소스 풀을 새로 만들 수 있습니다. 분류 함수를 정의하고 외부 리소스 풀에 할당합니다. **EXTERNAL** 키워드가 새로 생성되었습니다.
  
     새 사용자 정의 외부 리소스 풀을 만듭니다. 다음 예제에서는 풀 이름이 **ds_ep** 로 지정됩니다.
  
    ```sql
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);
    ```

2.  세션 요청 관리에 사용할 `ds_wg`라는 워크로드 그룹을 만듭니다. SQL 쿼리의 경우 기본 풀을 사용하고, 모든 외부 프로세스의 경우 쿼리에서 `ds_ep` 풀을 사용합니다.
  
    ```sql
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";
    ```
  
     요청을 분류할 수 없을 때마다 또는 다른 분류 오류가 있을 경우 요청이 기본 그룹에 할당됩니다.

 
자세한 내용은 [리소스 관리자 워크로드 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md) 및 [CREATE WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)을 참조하세요.
  
## <a name="create-a-classification-function-for-machine-learning"></a>기계 학습에 대한 분류 함수 만들기
  
분류 함수는 수신되는 태스크를 검사하여 현재 리소스 풀을 사용하여 실행할 수 있는 태스크인지 여부를 판단합니다. 분류 함수의 조건을 충족하지 않는 태스크는 서버의 기본 리소스 풀에 다시 할당됩니다.
  
1. 리소스 Resource Governor가 리소스 풀을 확인하기 위해 분류자 함수를 사용해야 함을 지정하여 시작합니다. 분류자 함수의 자리 표시자로 **null** 을 할당할 수 있습니다.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
     자세한 내용은 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)를 참조하세요.
  
2.  각 리소스 풀에 대한 분류자 함수에서 리소스 풀에 할당되어야 하는 명령문 또는 들어오는 요청의 유형을 정의합니다.
  
     예를 들어 다음 함수는 요청을 보낸 애플리케이션이 ‘Microsoft R Host’, ‘RStudio’ 또는 ‘Mashup’인 경우 사용자 정의 외부 리소스 풀에 할당된 스키마의 이름을 반환하고, 그렇지 않으면 기본 리소스 풀을 반환합니다.
  
    ```sql
    USE master
    GO
    CREATE FUNCTION is_ds_apps()
    RETURNS sysname
    WITH schemabinding
    AS
    BEGIN
        IF program_name() in ('Microsoft R Host', 'RStudio', 'Mashup') RETURN 'ds_wg';
        RETURN 'default'
        END;
    GO
    ```
  
3.  함수가 생성되면 이전에 정의한 외부 리소스 그룹에 새 분류자 함수를 할당하도록 리소스 그룹을 다시 구성합니다.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    GO
    ```

## <a name="verify-new-resource-pools-and-affinity"></a>새 리소스 풀 및 선호도 확인

각 워크로드 그룹의 서버 메모리 구성과 CPU를 확인합니다. 다음을 검토하여 인스턴스 리소스가 변경되었는지 확인합니다.

+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버에 대한 기본 풀
+ 외부 프로세스에 대한 기본 리소스 풀
+ 외부 프로세스에 대한 사용자 정의 풀

1. 모든 작업 그룹을 보려면 다음 명령문을 실행합니다.

    ```sql
    SELECT * FROM sys.resource_governor_workload_groups;
    ```

    **샘플 결과**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_id|
    |-|-|-|-|-|-|-|-|-|-|
    |1|internal|중간|25|0|0|0|0|1|2|
    |2|default|중간|25|0|0|0|0|2|2|
    |256|ds_wg|중간|25|0|0|0|0|2|256|
  
2.  새 카탈로그 보기인 [sys.resource_governor_external_resource_pools&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)를 사용하여 모든 외부 리소스 풀을 봅니다.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools;
    ```

    **샘플 결과**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|버전|
    |-|-|-|-|-|-|
    |2|default|100|20|0|2|
    |256|ds_ep|100|40|0|1|
  
     자세한 내용은 [리소스 관리자 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)를 참조하세요.
  
3.  해당되는 경우 다음 명령문을 실행하여 외부 리소스 풀에 선호도가 설정된 컴퓨터 리소스에 대한 정보를 반환합니다.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;
    ```
  
     풀이 AUTO 선호도로 생성되었으므로 정보가 표시되지 않을 것입니다. 자세한 내용은 [sys.dm_resource_governor_resource_pool_affinity&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

서버 리소스 관리에 대한 자세한 내용은 다음을 참조하세요.

+ [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md) 
+ [Resource Governor 관련 동적 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)

기계 학습을 위한 리소스 거버넌스에 대한 개요는 다음을 참조하세요.

+ [SQL Server Machine Learning Services에서 Resource Governor를 사용하여 Python 및 R 워크로드 관리](resource-governor.md)

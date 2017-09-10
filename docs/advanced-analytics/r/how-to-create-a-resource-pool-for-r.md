---
title: "방법: R에 대한 리소스 풀 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 10/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c7f7f6e4-774d-4b45-b94a-f06c51718475
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: be3afb3a1ff5175fbb3d0735cde59bd19bb47f6c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="how-to-create-a-resource-pool-for-r"></a>방법: R에 대한 리소스 풀 만들기
  이 항목에서는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 R 워크로드 관리를 위한 리소스 풀을 만들 수 있는 방법을 설명합니다. 이미 R Services(데이터베이스 내)를 설치했으며 R에서 사용되는 리소스의 보다 세분화된 관리를 지원하도록 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스를 다시 구성하려고 합니다.  
  
 서버 리소스를 관리하는 방법에 대한 자세한 내용은 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md) 및 [리소스 관리자 관련 동적 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)를 참조하세요.  
  
 **단계**  
  
1.  기존 리소스 풀의 상태 검토  
  
2.  서버 리소스 풀 수정  
  
3.  외부 프로세스에 대한 새 리소스 풀 만들기  
  
4.  R 요청을 식별하는 분류 함수 만들기  
  
5.  새 외부 리소스 풀이 R 작업을 캡처하는지 확인  
  
##  <a name="bkmk_ReviewStatus"></a> 기존 리소스 풀의 상태 검토  
  
1.  먼저 서버에 대한 기본 풀에 할당된 리소스를 확인합니다.  
  
    ```  
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'  
    ```  
     **결과**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|  
    |-|-|-|-|-|-|-|-|-|  
    |2|기본|0|100|0|100|100|0|0|  

2.  기본 **외부** 리소스 풀에 할당된 리소스를 확인합니다.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'  
    ```  
     
    **결과**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|기본|100|20|0|2|  
 
3.  이러한 서버 기본 설정에서 R 런타임은 대부분의 작업을 완료하기 위한 리소스가 부족합니다. 이를 변경하려면 다음과 같이 서버 리소스 사용을 수정해야 합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 수 있는 최대 컴퓨터 메모리 줄이기  
  
    -   외부 프로세스에서 사용할 수 있는 최대 컴퓨터 메모리 늘리기  
  
## <a name="modify-server-resource-usage"></a>서버 리소스 사용 수정  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 다음 문을 실행하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 사용량을 '최대 서버 메모리' 설정 값의 **60%**로 제한합니다.  
  
    ```  
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);  
    ```  
  
2.  마찬가지로, 다음 문을 실행하여 외부 프로세스의 메모리 사용을 총 컴퓨터 리소스의 **40%**로 제한합니다.  
  
    ```  
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);  
    ```  
  
3.  이러한 변경 내용을 적용하려면 다음과 같이 리소스 관리자를 다시 구성하고 다시 시작해야 합니다.  
  
    ```  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
    > [!NOTE]  
    >  이러한 설정은 시작할 제안 설정일 뿐입니다. 다른 서버 프로세스를 기준으로 R 요구 사항을 평가하여 환경 및 워크로드에 맞는 균형을 확인해야 합니다.  
  
## <a name="create-a-user-defined-external-resource-pool"></a>사용자 정의 외부 리소스 풀 만들기  
  
1.  리소스 관리자의 구성 변경 내용은 서버 전체에 적용되고 서버에 대한 기본 풀을 사용하는 워크로드 및 외부 풀을 사용하는 워크로드에 영향을 줍니다.  
  
     따라서 우선 순위가 있는 워크로드를 보다 세부적으로 제어하려면 사용자 정의 외부 리소스 풀을 새로 만들 수 있습니다. 또한 분류 함수를 정의하고 외부 리소스 풀에 할당해야 합니다.  
  
     먼저 새 *사용자 정의 외부 리소스 풀*을 만듭니다. 다음 예제에서는 풀 이름이 **ds_ep**로 지정됩니다.  
  
    ```  
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);  
    ```  
  
     새 **EXTERNAL** 키워드를 확인합니다.  
  
2.  세션 요청 관리에 사용할 `ds_wg`라는 워크로드 그룹을 만듭니다. SQL 쿼리의 경우 기본 풀을 사용하고, 모든 외부 프로세스의 경우 쿼리에서 `ds_ep` 풀을 사용합니다.  
  
    ```  
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";  
    ```  
  
     요청을 분류할 수 없을 때마다 또는 다른 분류 오류가 있을 경우 요청이 기본 그룹에 할당됩니다.  
  
     자세한 내용은 [리소스 관리자 워크로드 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md) 및 [CREATE WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)을 참조하세요.  
  
## <a name="create-a-classification-function-for-r"></a>R에 대한 분류 함수 만들기  
  
1.  분류 함수는 들어오는 태스크를 검사하고 현재 리소스 풀을 사용하여 실행할 수 있는 태스크인지 확인합니다. 분류 함수의 조건을 충족하지 않는 태스크는 서버의 기본 리소스 풀에 다시 할당됩니다.  
  
     먼저 리소스 관리자가 분류자 함수를 사용하여 리소스 풀을 확인하도록 지정합니다. 분류자 함수의 자리 표시자로 null을 할당할 수 있습니다.  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
     자세한 내용은 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)를 참조하세요.  
  
2.  각 리소스 풀에 대한 분류자 함수에서 리소스 풀에 할당되어야 하는 문 또는 들어오는 요청의 유형을 정의합니다.  
  
     예를 들어 다음 함수는 요청을 보낸 응용 프로그램이 'Microsoft R Host' 또는 'RStudio'인 경우 사용자 정의 외부 리소스 풀에 할당된 스키마의 이름을 반환하고, 그렇지 않으면 기본 리소스 풀을 반환합니다.  
  
    ```  
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
  
    ```  
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);  
    ALTER RESOURCE GOVERNOR WITH reconfigure;  
    go  
    ```  
  
## <a name="verify-new-resource-pools-and-affinity"></a>새 리소스 풀 및 선호도 확인  
  
1.  변경 내용이 있는지 확인하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버의 기본 풀, 외부 프로세스의 기본 리소스 풀, 외부 프로세스의 사용자 정의 풀 등 모든 인스턴스 리소스 풀과 연결된 각 워크로드 그룹의 서버 메모리 및 CPU 구성을 확인합니다.  
  
    ```  
    SELECT * FROM sys.resource_governor_workload_groups;  
    ```  

    **결과**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_idd|  
    |-|-|-|-|-|-|-|-|-|-|  
    |1|내부|보통|25|0|0|0|0|1|2|  
    |2|기본|보통|25|0|0|0|0|2|2|  
    |256|ds_wg|보통|25|0|0|0|0|2|256|  
  
2.  새 카탈로그 뷰인 [sys.resource_governor_external_resource_pools&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)를 사용하여 모든 외부 리소스 풀을 볼 수 있습니다.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools;  
    ```  
    **결과**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|기본|100|20|0|2|  
    |256|ds_ep|100|40|0|1|  
  
     자세한 내용은 [리소스 관리자 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)를 참조하세요.  
  
3.  다음 문은 외부 리소스 풀에 선호도가 설정된 컴퓨터 리소스에 대한 정보를 반환합니다.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;  
    ```  
  
     이 경우 풀이 AUTO 선호도로 생성되었으므로 정보가 표시되지 않습니다. 자세한 내용은 [sys.dm_resource_governor_resource_pool_affinity&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)   
 [R Services에 대한 리소스 관리](../../advanced-analytics/r-services/resource-governance-for-r-services.md)  
  
  


---
title: "방법: R에 대 한 리소스 풀 만들기 | Microsoft Docs"
ms.custom: ""
ms.date: "10/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c7f7f6e4-774d-4b45-b94a-f06c51718475
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# 방법: R에 대 한 리소스 풀 만들기
  이 항목에서 R 작업 관리를 위해 특별히 리소스 풀을 만들 수는 방법에 대해 설명 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]합니다. 이미 R 서비스 (데이터베이스)를 설치 하 고 다시 구성 하려면 가정은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] R. 사용 하는 리소스의 더 세분화 된 관리를 지 원하는 인스턴스  
  
 서버 리소스를 관리 하는 방법에 대 한 자세한 내용은 참조 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md) 및 [리소스 관리자 관련 동적 관리 뷰 및 #40; TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)합니다.  
  
 **단계**  
  
1.  기존 리소스 풀의 상태를 검토 합니다.  
  
2.  서버 리소스 풀을 수정 합니다.  
  
3.  외부 프로세스에 대 한 새 리소스 풀 만들기  
  
4.  R 요청을 식별 하는 분류 함수를 만듭니다  
  
5.  새 외부 리소스 풀은 R 작업 캡처 있는지 확인 하십시오.  
  
##  <a name="bkmk_ReviewStatus"></a> 기존 리소스 풀의 상태를 검토 합니다.  
  
1.  첫째, 서버에 대 한 기본 풀에 할당 된 리소스를 확인 합니다.  
  
    ```  
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'  
    ```  
     **결과**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|  
    |-|-|-|-|-|-|-|-|-|  
    |2|기본|0|100|0|100|100|0|0|  

2.  기본값에 할당 된 리소스를 확인 하십시오 **외부** 리소스 풀입니다.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'  
    ```  
     
    **결과**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|기본|100|20|0|2|  
 
3.  이러한 서버 기본 설정에서는 R 런타임 하는 경우도 대부분의 작업을 완료 하는 리소스가 부족 합니다. 이 변경 하려면 다음과 같이 서버 리소스 사용을 수정 해야 합니다.  
  
    -   사용할 수 있는 최대 컴퓨터 메모리를 줄이기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
    -   외부 프로세스에서 사용할 수 있는 최대 컴퓨터 메모리 늘리기  
  
## 서버 리소스 사용을 수정 합니다.  
  
1.   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], 제한 하려면 다음 문을 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 사용량과 **60%** '최대 서버 메모리' 설정의 값입니다.  
  
    ```  
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);  
    ```  
  
2.  마찬가지로, 다음 문을 실행 하 여에 외부 프로세스의 메모리 사용을 제한 **40%** 총 컴퓨터 리소스입니다.  
  
    ```  
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);  
    ```  
  
3.  이러한 변경 내용을 적용할 다시 구성 하 고 다음과 같이 리소스 관리자를 다시 시작 해야 합니다.  
  
    ```  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
    > [!NOTE]  
    >  부터; 방금 제안 된 설정 환경 및 작업에 대 한 올바른 균형을 확인 하려면 다른 서버 프로세스에 대 한 R 요구 사항을 평가 해야 합니다.  
  
## 외부 사용자 정의 리소스 풀 만들기  
  
1.  리소스 관리자의 구성 변경 내용을 전체적으로 서버에서 적용 됩니다 및 외부 풀을 사용 하는 작업 뿐만 아니라 서버에 대 한 기본 풀을 사용 하는 작업에 영향을 줍니다.  
  
     따라서는 작업은 우선 순위가 보다 세부적으로 제어를 제공 하려면 새 사용자 정의 외부 리소스 풀을 만들 수 있습니다. 또한 분류 함수를 정의 하 고 외부 리소스 풀에 할당 해야 합니다.  
  
     먼저 새 만들어 *외부 사용자 정의 리소스 풀*합니다. 다음 예제에서는 풀 이름은 **ds_ep**합니다.  
  
    ```  
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);  
    ```  
  
     참고 새 **외부** 키워드입니다.  
  
2.  작업 그룹을 만듭니다 `ds_wg` 관리 세션 요청에 사용 하도록 합니다. SQL 쿼리는 기본 풀을 사용 합니다. 모든 외부 프로세스에 대 한 쿼리에서 사용 된 `ds_ep` 풀입니다.  
  
    ```  
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";  
    ```  
  
     요청은 요청을 분류 될 수 없습니다, 때마다 또는 다른 분류 오류가 발생할 경우 기본 그룹에 할당 됩니다.  
  
     자세한 내용은 참조 [리소스 관리자 작업 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md) 및 [CREATE WORKLOAD GROUP 및 #40; TRANSACT-SQL &#41;](../../t-sql/statements/create-workload-group-transact-sql.md)합니다.  
  
## R에 대 한 분류 함수를 만듭니다.  
  
1.  분류 함수 수신 작업을 검사 하 고 작업의 현재 리소스 풀을 사용 하 여 실행할 수 있는 하나 인지 결정 합니다. 분류 함수의 조건을 충족 하지 않는 작업은 서버의 기본 리소스 풀에 다시 할당 됩니다.  
  
     분류자 함수 해야 사용 되도록 지정 하 여 리소스 관리자 리소스 풀을 확인 하 여 시작 합니다. 분류자 함수에 대 한 자리 표시자로 null을 지정할 수 있습니다.  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
     자세한 내용은 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)를 참조하세요.  
  
2.  각 리소스 풀에 대 한 분류자 함수에서 문 또는 리소스 풀에 할당 해야 하는 들어오는 요청 유형을 정의 합니다.  
  
     예를 들어, 다음 함수 반환 응용 프로그램이 있는 경우는 요청을 전달한 ' Microsoft R 호스트 ' 또는 'RStudio'; 외부 사용자 정의 리소스 풀에 할당 된 스키마의 이름 그렇지 않으면 기본 리소스 풀을 반환 합니다.  
  
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
  
3.  함수를 만들면 이전에 정의 된 외부 리소스 그룹에 새 분류자 함수를 할당 하려면 리소스 그룹을 다시 구성 합니다.  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);  
    ALTER RESOURCE GOVERNOR WITH reconfigure;  
    go  
    ```  
  
## 새 리소스 풀 및 선호도 확인 합니다.  
  
1.  변경 내용이 있는지를 확인 하려면 모든 인스턴스 리소스 풀과 연결 된 작업 그룹의 각 서버 메모리와 CPU의 구성을 확인: 기본 풀은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버, 외부 프로세스에 대 한 기본 리소스 풀 및 외부 프로세스에 대 한 사용자 정의 풀입니다.  
  
    ```  
    SELECT * FROM sys.resource_governor_workload_groups;  
    ```  

    **결과**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_idd|  
    |-|-|-|-|-|-|-|-|-|-|  
    |1|내부|보통|25|0|0|0|0|1|2|  
    |2|기본|보통|25|0|0|0|0|2|2|  
    |256|ds_wg|보통|25|0|0|0|0|2|256|  
  
2.  새 카탈로그 뷰를 사용할 수 있습니다 [sys.resource_governor_external_resource_pools &#40; TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), 모든 외부 리소스 풀을 볼 수 있습니다.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools;  
    ```  
    **결과**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|기본|100|20|0|2|  
    |256|ds_ep|100|40|0|1|  
  
     자세한 내용은 참조 [리소스 관리자 카탈로그 뷰 및 #40; TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)합니다.  
  
3.  다음 문은 외부 리소스 풀에 선호도 설정 되는 컴퓨터 리소스에 대 한 정보를 반환 합니다.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;  
    ```  
  
     이 경우에 풀 AUTO의 선호도에 생성 된, 때문에 정보가 표시 됩니다. 자세한 내용은 참조 [sys.dm_resource_governor_resource_pool_affinity &#40; TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)합니다.  
  
## 관련 항목:  
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)   
 [R 서비스에 대 한 리소스 관리](../../advanced-analytics/r-services/resource-governance-for-r-services.md)  
  
  
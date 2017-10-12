---
title: "PolyBase 문제 해결 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 8/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- PolyBase, monitoring
- PolyBase, performance monitoring
helpviewer_keywords:
- PolyBase, troubleshooting
ms.assetid: f119e819-c3ae-4e0b-a955-3948388a9cfe
caps.latest.revision: 22
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: 240e02e3dd0d40f53f8436e241af228b503a43d9
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---
# <a name="polybase-troubleshooting"></a>PolyBase 문제 해결
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  PolyBase 문제를 해결하려면 이 항목에 나와 있는 기술을 사용합니다.  
  
## <a name="catalog-views"></a>카탈로그 뷰  
 PolyBase 작업을 관리하려면 여기에 나와 있는 카탈로그 뷰를 사용합니다.  
  
|||  
|-|-|  
|보기|설명|  
|[sys.external_tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)|외부 테이블을 식별합니다.|  
|[sys.external_data_sources&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)|외부 데이터 원본을 식별합니다.|  
|[sys.external_file_formats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)|외부 파일 형식을 식별합니다.|  
  
## <a name="dynamic-management-views"></a>동적 관리 뷰  
  
|||  
|-|-|  
|[sys.dm_exec_compute_node_errors&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)|[sys.dm_exec_compute_node_status&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md)|  
|[sys.dm_exec_compute_nodes&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|[sys.dm_exec_distributed_request_steps&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)|  
|[sys.dm_exec_distributed_requests&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-requests-transact-sql.md)|[sys.dm_exec_distributed_sql_requests&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-sql-requests-transact-sql.md)|  
|[sys.dm_exec_dms_services&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-services-transact-sql.md)|[sys.dm_exec_dms_workers&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|[sys.dm_exec_external_operations&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-operations-transact-sql.md)|[sys.dm_exec_external_work&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-work-transact-sql.md)|  
  
  PolyBase 쿼리는 sys.dm_exec_distributed_request_steps 내에 있는 일련의 단계로 나뉩니다. 다음 표에는 단계 이름과 연결된 DMV 간의 매핑이 나와 있습니다.
  
 |PolyBase 단계|연결된 DMV|  
 |-|-| 
 |HadoopJobOperation | sys.dm_exec_external_operations|
 |RandomIdOperation | sys.dm_exec_distributed_request_steps|
 |HadoopRoundRobinOperation | sys.dm_exec_dms_workers|
 |StreamingReturnOperation | sys.dm_exec_dms_workers|
 |OnOperation | sys.dm_exec_distributed_sql_requests |
  
  
## <a name="to-monitor-polybase-queries-using-dmvs"></a>DMV를 사용하여 PolyBase 쿼리를 모니터링하려면  
 다음의 DMV를 사용하여 PolyBase를 모니터링하고 문제를 해결합니다.  
  
1.  **가장 오래 실행되는 쿼리 찾기**  
  
     가장 오래 실행되는 쿼리의 실행 ID를 기록합니다.  
  
    ```tsql  
     -- Find the longest running query  
    SELECT execution_id, st.text, dr.total_elapsed_time  
    FROM sys.dm_exec_distributed_requests  dr  
         cross apply sys.dm_exec_sql_text(sql_handle) st  
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
2.  **분산 쿼리의 가장 오래 실행되는 단계 찾기**  
  
     이전 단계에서 기록된 실행 ID를 사용하여 가장 오래 실행되는 단계의 단계 인덱스를 기록합니다.  
  
     가장 오래 실행되는 단계의 location_type을 확인합니다.  
  
    -   Head 또는 Compute: SQL 작업을 의미합니다. 3a단계를 진행합니다.  
  
    -   DMS: PolyBase 데이터 이동 서비스 작업을 의미합니다. 3b단계를 진행합니다.  
  
    ```tsql  
    -- Find the longest running step of the distributed query plan  
    SELECT execution_id, step_index, operation_type, distribution_type,   
    location_type, status, total_elapsed_time, command   
    FROM sys.dm_exec_distributed_request_steps   
    WHERE execution_id = 'QID4547'   
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
3.  **가장 오래 실행되는 단계의 실행 진행률 찾기**  
  
    1.  **SQL 단계의 실행 진행률 찾기**  
  
         이전 단계에서 기록된 실행 ID 및 단계 인덱스를 사용합니다. 이전 단계에서 기록된 실행 ID 및 단계 인덱스를 사용합니다.  
  
        ```tsql  
        -- Find the execution progress of SQL step    
        SELECT execution_id, step_index, distribution_id, status,   
        total_elapsed_time, row_count, command   
        FROM sys.dm_exec_distributed_sql_requests   
        WHERE execution_id = 'QID4547' and step_index = 1;  
  
        ```  
  
    2.  **DMS 단계의 실행 진행률 찾기**  
  
         이전 단계에서 기록된 실행 ID 및 단계 인덱스를 사용합니다.  
  
        ```tsql  
        -- Find the execution progress of DMS step    
        SELECT execution_id, step_index, dms_step_index, status,   
        type, bytes_processed, total_elapsed_time  
        FROM sys.dm_exec_dms_workers   
        WHERE execution_id = 'QID4547'   
        ORDER BY total_elapsed_time DESC;  
  
        ```  
  
4.  **외부 DMS 작업에 대한 정보 찾기**  
  
     이전 단계에서 기록된 실행 ID 및 단계 인덱스를 사용합니다.  
  
    ```tsql  
    SELECT execution_id, step_index, dms_step_index, compute_node_id,   
    type, input_name, length, total_elapsed_time, status   
    FROM sys.dm_exec_external_work   
    WHERE execution_id = 'QID4547' and step_index = 7   
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
## <a name="to-view-the--polybase-query-plan"></a>PolyBase 쿼리 계획을 보려면  
  
1.  SSMS에서 Ctrl+M을 눌러 **실제 실행 계획 포함**을 사용하도록 설정하고 쿼리를 실행합니다.  
  
2.  **실행 계획** 탭을 클릭합니다.  
  
     ![PolyBase 쿼리 계획](../../relational-databases/polybase/media/polybase-query-plan.png "PolyBase 쿼리 계획")  
  
3.  **원격 쿼리 연산자**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
4.  원격 쿼리 값을 복사한 다음 텍스트 편집기에 붙여넣어 XML 원격 쿼리 계획을 확인합니다.  아래에 예가 나와 있습니다.  
  
    ```xml  
  
    <dsql_query number_nodes="1" number_distributions="8" number_distributions_per_node="8">  
      <sql>ExecuteMemo explain query</sql>  
      <dsql_operations total_cost="0" total_number_operations="6">  
        <dsql_operation operation_type="RND_ID">  
          <identifier>TEMP_ID_74</identifier>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_74] ([SensorKey] INT NOT NULL, [CustomerKey] INT NOT NULL, [GeographyKey] INT, [Speed] FLOAT(53) NOT NULL, [YearMeasured] INT NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">EXEC [tempdb].[sys].[sp_addextendedproperty] @name=N'IS_EXTERNAL_STREAMING_TABLE', @value=N'true', @level0type=N'SCHEMA', @level0name=N'dbo', @level1type=N'TABLE', @level1name=N'TEMP_ID_74'</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">UPDATE STATISTICS [tempdb].[dbo].[TEMP_ID_74] WITH ROWCOUNT = 2401, PAGECOUNT = 7</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="MULTI">  
          <dsql_operation operation_type="STREAMING_RETURN">  
            <operation_cost cost="1" accumulative_cost="1" average_rowsize="24" output_rows="5762.1" />  
            <location distribution="AllDistributions" />  
            <select>SELECT [T1_1].[SensorKey] AS [SensorKey],  
           [T1_1].[CustomerKey] AS [CustomerKey],  
           [T1_1].[GeographyKey] AS [GeographyKey],  
           [T1_1].[Speed] AS [Speed],  
           [T1_1].[YearMeasured] AS [YearMeasured]  
    FROM   (SELECT [T2_1].[SensorKey] AS [SensorKey],  
                   [T2_1].[CustomerKey] AS [CustomerKey],  
                   [T2_1].[GeographyKey] AS [GeographyKey],  
                   [T2_1].[Speed] AS [Speed],  
                   [T2_1].[YearMeasured] AS [YearMeasured]  
            FROM   [tempdb].[dbo].[TEMP_ID_74] AS T2_1  
            WHERE  ([T2_1].[Speed] > CAST (6.50000000000000000E+001 AS FLOAT))) AS T1_1</select>  
          </dsql_operation>  
          <dsql_operation operation_type="ExternalRoundRobinMove">  
            <operation_cost cost="16.594848" accumulative_cost="17.594848" average_rowsize="24" output_rows="19207" />  
            <external_uri>hdfs://10.193.26.177:8020/Demo/car_sensordata.tbl/</external_uri>  
            <destination_table>[TEMP_ID_74]</destination_table>  
          </dsql_operation>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_74]</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
      </dsql_operations>  
    </dsql_query>  
    ```  
  
## <a name="to-monitor-nodes-in-a-polybase-group"></a>PolyBase 그룹에서 노드를 모니터링하려면  
 PolyBase 규모 확장 그룹의 일부분으로 컴퓨터 집합을 구성한 후에는 컴퓨터의 상태를 모니터링할 수 있습니다. 스케일 아웃 그룹을 만드는 방법은 [PolyBase 스케일 아웃 그룹](../../relational-databases/polybase/polybase-scale-out-groups.md)을 참조하세요.  
  
1.  그룹의 헤드 노드에서 SQL Server에 연결합니다.  
  
2.  DMV [sys.dm_exec_compute_nodes&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)를 실행하여 PolyBase 그룹의 모든 노드를 확인합니다.  
  
3.  DMV [sys.dm_exec_compute_node_status&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md)를 실행하여 PolyBase 그룹의 모든 노드의 상태를 확인합니다.  
  
 ## <a name="known-limitations"></a>알려진 제한 사항
 
 PolyBase에는 다음과 같은 제한 사항이 있습니다. 
 - 가변 길이 열의 전체 길이를 포함하여 행의 최대 가능 크기가 1MB를 초과할 수 없습니다. 
 - PolyBase는 Hive 0.12+ 데이터 유형(즉, Char(), VarChar())을 지원하지 않습니다.   
 - SQL Server 또는 Azure SQL Data Warehouse에서 ORC 파일 형식으로 데이터를 내보낼 때 텍스트가 많은 열은 java 메모리 부족 오류로 인해 50개 이내로 제한될 수 있습니다. 이 문제를 해결하려면 열의 하위 집합만 내보냅니다.
 - Hadoop에서 암호화된 미사용 데이터를 읽거나 쓸 수 없습니다. 여기에는 HDFS 암호화 영역 또는 투명 암호화가 포함됩니다.
 - KNOX가 활성화되어 있으면 PolyBase가 Hortonworks 인스턴스에 연결할 수 없습니다. 
 - 트랜잭션이 true인 Hive 테이블을 사용하는 경우 PolyBase는 Hive 테이블의 디렉터리에 있는 데이터에 액세스할 수 없습니다. 


[PolyBase는 SQL Server 2016 장애 조치(Failover) 클러스터에 노드를 추가하는 경우 설치되지 않습니다.](https://support.microsoft.com/en-us/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster)

## <a name="hadoop-name-node-high-availability"></a>Hadoop 이름 노드 고가용성
PolyBase는 오늘 Zookeeper 또는 Knox와 같은 이름 노드 HA 서비스와 인터페이스하지 않습니다. 하지만 기능을 제공하는 데 사용할 수 있는 검증된 해결 방법이 있습니다. 

해결 방법: DNS 이름을 사용하여 활성 이름 노드에 대한 연결을 다시 라우팅합니다. 이렇게 하려면 외부 데이터 원본이 DNS 이름을 사용하여 이름 노드와 통신하는지 확인해야 합니다. 이름 노드 장애 조치(failover)가 발생하면 외부 데이터 원본 정의에 사용된 DNS 이름과 연결된 IP 주소를 변경해야 합니다. 그러면 모든 새 연결이 올바른 이름 노드로 다시 라우팅됩니다. 장애 조치(failover)가 발생하면 기존 연결이 실패합니다. 이 프로세스를 자동화하기 위해 "하트 비트"가 활성 이름 노드를 ping할 수 있습니다. 하트 비트가 실패하면 장애 조치(failover)가 발생했다고 가정하고 보조 IP 주소로 자동 전환할 수 있습니다.


## <a name="error-messages-and-possible-solutions"></a>오류 메시지 및 가능한 해결 방법

외부 테이블 오류 문제를 해결하려면 Murshed Zaman 블로그 [https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/](https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/ "PolyBase setup errors and possible solutions")(PolyBase 설치 오류 및 가능한 해결 방법)를 참조하세요.

## <a name="see-also"></a>참고 항목
[PolyBase Kerberos 연결 문제 해결](polybase-troubleshoot-connectivity.md)


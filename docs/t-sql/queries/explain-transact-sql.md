---
title: EXPLAIN(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.reviewer: jrasnick
ms.technology: data-warehouse
ms.topic: conceptual
ms.assetid: 4846a576-57ea-4068-959c-81e69e39ddc1
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 310a607e11bbf99437d67b85b6f2e718161b2401
ms.sourcegitcommit: e4b241fd92689c2aa6e1f5e625874bd0b807dd01
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67564133"
---
# <a name="explain-transact-sql"></a>EXPLAIN(Transact-SQL) 

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  명령문을 실행하지 않고 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 문에 대한 쿼리 계획을 반환합니다. **EXPLAIN**을 사용하여 데이터 이동이 필요한 작업을 미리 보고 쿼리 작업의 예상 비용을 표시합니다. `WITH RECOMMENDATIONS`는 Azure SQL Data Warehouse(미리 보기)에 적용됩니다.
  
 쿼리 계획에 대한 자세한 내용은 [!INCLUDE[pdw-product-documentation_md](../../includes/pdw-product-documentation-md.md)]의 "쿼리 계획 이해"를 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```
EXPLAIN [WITH_RECOMMENDATIONS] SQL_statement  
[;]  
```  
  
## <a name="arguments"></a>인수

 *SQL_statement*  
 **EXPLAIN**이 실행되는 [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 문입니다. *SQL_statement*는 다음 명령 중 하나일 수 있습니다. **SELECT**, **INSERT**, **UPDATE**, **DELETE**, **CREATE TABLE AS SELECT**, **CREATE REMOTE TABLE**.

*WITH_RECOMMENDATIONS* 는 SQL 문의 성능을 최적화하기 위한 권장 사항이 포함된 쿼리 계획을 반환합니다.  
  
## <a name="permissions"></a>사용 권한

 **SHOWPLAN** 권한 및 *SQL_statement*를 실행할 수 있는 권한이 필요합니다. [권한: GRANT, DENY, REVOKE &#40;Azure SQL Data Warehouse, 병렬 Data Warehouse&#41;](../../t-sql/statements/permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse.md)를 참조하세요.  
  
## <a name="return-value"></a>반환 값

 **EXPLAIN** 명령의 반환 값은 다음과 같은 구조의 XML 문서입니다. 이 XML 문서는 지정된 쿼리에 대한 쿼리 계획의 모든 작업을 나열하며, 각 작업은 `<dsql_operation>` 태그로 묶여 있습니다. 반환 값은 **nvarchar(max)** 형식입니다.  
  
 반환된 쿼리 계획은 순차적 SQL 문을 보여 줍니다. 쿼리가 실행되면 병렬 처리된 작업이 포함될 수 있으므로 표시된 순차적 명령문 중 일부가 동시에 실행될 수 있습니다.  
  
```  
\<?xml version="1.0" encoding="utf-8"?>  
<dsql_query>  
  <sql>. . .</sql>  
  <params />  
  <dsql_operations>  
    <dsql_operation>  
     . . .      
    </dsql_operation>  
    [ . . . n ]  
  <dsql_operations>  
</dsql_query>  
```  
  
 XML 태그에 포함되는 정보는 다음과 같습니다.  
  
|XML 태그|요약, 특성 및 콘텐츠|  
|-------------|--------------------------------------|  
|\<dsql_query>|최상위 수준/문서 요소입니다.|
|\<sql>|*SQL_statement*를 에코합니다.|  
|\<params>|이 태그는 현재 사용되지 않습니다.|
|\<materialized_view_candidates>(미리 보기)|SQL 문의 성능 향상을 위해 권장되는 구체화된 뷰의 CREATE 문을 포함합니다.| 
|\<dsql_operations>|쿼리 단계를 요약하고, 포함하며 ,쿼리에 대한 비용 정보를 포함합니다. 또한 모든 `<dsql_operation>` 블록도 포함합니다. 이 태그에는 전체 쿼리에 대한 개수 정보가 포함됩니다.<br /><br /> `<dsql_operations total_cost=total_cost total_number_operations=total_number_operations>`<br /><br /> *total_cost*는 쿼리 실행에 대한 총 예상 시간(밀리초)입니다.<br /><br /> *total_number_operations*는 쿼리에 대한 총 작업 수입니다. 여러 노드에서 병렬 처리되고 실행되는 작업은 단일 작업으로 계산됩니다.|  
|\<dsql_operation>|쿼리 계획 내에 있는 단일 작업을 설명합니다. \< dsql_operation> 태그에는 작업 유형이 특성으로 포함됩니다.<br /><br /> `<dsql_operation operation_type=operation_type>`<br /><br /> *operation_type*은 [sys.dm_pdw_request_steps(Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)에 있는 값 중 하나입니다.<br /><br /> `\<dsql_operation>` 블록의 콘텐츠는 작업 유형에 따라 다릅니다.<br /><br /> 아래 표를 참조하세요.|  
  
|작업 유형|콘텐츠|예제|  
|--------------------|-------------|-------------|  
|BROADCAST_MOVE, DISTRIBUTE_REPLICATED_TABLE_MOVE, MASTER_TABLE_MOVE, PARTITION_MOVE, SHUFFLE_MOVE 및 TRIM_MOVE|이러한 특성이 있는 `<operation_cost>` 요소입니다. 로컬 작업만 반영하는 값은 다음과 같습니다.<br /><br /> -   *cost*는 로컬 연산자 비용이며, 작업 실행에 대한 예상 시간(밀리초)을 표시합니다.<br />-   *accumulative_cost*는 병렬 작업에 대한 합계 값을 포함하여 계획에 표시된 모든 작업의 합계(밀리초)입니다.<br />-   *average_rowsize*는 작업 중에 검색되고 전달된 행의 예상 평균 행 크기(바이트)입니다.<br />-   *output_rows*는 출력(노드) 카디널리티이며, 출력 행 수를 표시합니다.<br /><br /> `<location>`: 작업이 발생할 노드 또는 배포입니다. 사용할 수 있는 옵션은 다음과 같습니다. "Control", "ComputeNode", "AllComputeNodes", "AllDistributions", "SubsetDistributions", "Distribution" 및 "SubsetNodes".<br /><br /> `<source_statement>`: 순서 섞기 이동에 대한 원본 데이터입니다.<br /><br /> `<destination_table>`: 데이터 이동의 대상이 되는 내부 임시 테이블입니다.<br /><br /> `<shuffle_columns>`: (SHUFFLE_MOVE 작업에만 적용 가능). 임시 테이블에 대한 배포 열로 사용할 하나 이상의 열입니다.|`<operation_cost cost="40" accumulative_cost="40" average_rowsize = "50" output_rows="100"/>`<br /><br /> `<location distribution="AllDistributions" />`<br /><br /> `<source_statement type="statement">SELECT [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d].[dist_date] FROM [qatest].[dbo].[flyers] [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d]       </source_statement>`<br /><br /> `<destination_table>Q_[TEMP_ID_259]_[PARTITION_ID]</destination_table>`<br /><br /> `<shuffle_columns>dist_date;</shuffle_columns>`|  
|CopyOperation|`<operation_cost>`: 위의 `<operation_cost>` 내용을 참조하세요.<br /><br /> `<DestinationCatalog>`: 대상 노드 또는 노드.<br /><br /> `<DestinationSchema>`: DestinationCatalog의 대상 스키마입니다.<br /><br /> `<DestinationTableName>`: 대상 테이블의 이름 또는 "TableName".<br /><br /> `<DestinationDatasource>`: 대상 데이터 원본의 이름 또는 연결 정보.<br /><br /> `<Username>` 및 `<Password>`: 대상에 대한 사용자 이름과 암호가 필요할 수 있음을 나타냅니다.<br /><br /> `<BatchSize>`: 복사 작업에 대한 일괄 처리 크기입니다.<br /><br /> `<SelectStatement>`: 복사를 수행하는 데 사용되는 select 문입니다.<br /><br /> `<distribution>`: 복사가 수행되는 배포입니다.|`<operation_cost cost="0" accumulative_cost="0" average_rowsize="4" output_rows="1" />`<br /><br /> `<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>[TableName]</DestinationTableName>`<br /><br /> `<DestinationDatasource>localhost, 8080</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<BatchSize>6000</BatchSize>`<br /><br /> `<SelectStatement>SELECT T1_1.c1 AS c1 FROM [qatest].[dbo].[gigs] AS T1_1</SelectStatement>`<br /><br /> `<distribution>ControlNode</distribution>`|  
|MetaDataCreate_Operation|`<source_table>`: 작업에 대한 원본 테이블입니다.<br /><br /> `<destination_table>`: 작업에 대한 대상 테이블입니다.|`<source_table>databases</source_table>`<br /><br /> `<destination_table>MetaDataCreateLandingTempTable</destination_table>`|  
|ON|`<location>`: 위의 `<location>` 내용을 참조하세요.<br /><br /> `<sql_operation>`: 노드에서 수행할 SQL 명령을 식별합니다.|`<location permanent="false" distribution="AllDistributions">Compute</location>`<br /><br /> `<sql_operation type="statement">CREATE TABLE [tempdb].[dbo]. [Q_[TEMP_ID_259]]_ [PARTITION_ID]]]([dist_date] DATE) WITH (DISTRIBUTION = HASH([dist_date]),) </sql_operation>`|  
|RemoteOnOperation|`<DestinationCatalog>`: 대상 카탈로그.<br /><br /> `<DestinationSchema>`: DestinationCatalog의 대상 스키마입니다.<br /><br /> `<DestinationTableName>`: 대상 테이블의 이름 또는 "TableName".<br /><br /> `<DestinationDatasource>`: 대상 데이터 원본의 이름입니다.<br /><br /> `<Username>` 및 `<Password>`: 대상에 대한 사용자 이름과 암호가 필요할 수 있음을 나타냅니다.<br /><br /> `<CreateStatement>`: 대상 데이터베이스에 대한 테이블 생성 문입니다.|`<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>TableName</DestinationTableName>`<br /><br /> `<DestinationDatasource>DestDataSource</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<CreateStatement>CREATE TABLE [master].[dbo].[TableName] ([col1] BIGINT) ON [PRIMARY] WITH(DATA_COMPRESSION=PAGE);</CreateStatement>`|  
|RETURN|`<resultset>`: 결과 집합에 대한 식별자입니다.|`<resultset>RS_19</resultset>`|  
|RND_ID|`<identifier>`: 만든 개체에 대한 식별자입니다.|`<identifier>TEMP_ID_260</identifier>`|  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 **EXPLAIN**은 **EXPLAIN** 명령의 결과에 따라 향상되거나 수정될 수 있는 *최적화 가능* 쿼리에만 적용할 수 있습니다. 지원되는 **EXPLAIN** 명령은 위에 나와 있습니다. 지원되지 않는 쿼리 유형에서 **EXPLAIN**을 사용하려고 하면 오류를 반환하거나 쿼리를 에코합니다.  
  
 **EXPLAIN**은 사용자 트랜잭션에서 지원되지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 **SELECT** 문에서 실행되는 **EXPLAIN** 명령과 XML 결과를 보여 줍니다.  
  
 **EXPLAIN 문 제출**  
  
 이 예제에 대해 제출되는 명령은 다음과 같습니다.  
  
```  
-- Uses AdventureWorks  
  
EXPLAIN   
    SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
        CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
        G.StateProvinceName, T.SalesTerritoryGroup  
    FROM dbo.DimGeography AS G  
    JOIN dbo.DimSalesTerritory AS T  
        ON G.SalesTerritoryKey = T.SalesTerritoryKey  
    JOIN dbo.DimCustomer AS C  
        ON G.GeographyKey = C.GeographyKey  
    JOIN dbo.FactInternetSales AS FIS  
        ON C.CustomerKey = FIS.CustomerKey  
    WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
        AND Gender = 'F'  
    GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
    ORDER BY AVG(YearlyIncome) DESC;  
GO  
```  
  
 **EXPLAIN** 옵션을 사용하여 명령문이 실행되면, 메시지 탭에 **설명**이라는 제목의 한 줄이 표시되고 `\<?xml version="1.0" encoding="utf-8"?>` XML 텍스트로 시작합니다. XML을 클릭하여 XML 창에서 전체 텍스트를 엽니다. 다음 주석을 더 잘 이해하려면 SSDT에서 줄 번호 표시를 설정해야 합니다.  
  
#### <a name="to-turn-on-line-numbers"></a>줄 번호를 설정하려면  
  
1.  **설명** 탭 SSDT에 출력이 표시되면 **도구** 메뉴에서 **옵션**을 선택합니다.  
  
2.  **텍스트 편집기** 섹션을 펼치고, **XML**을 펼친 다음, **일반**을 클릭합니다.  
  
3.  **표시** 영역에서 **줄 번호**를 확인합니다.  
  
4.  **확인**을 클릭합니다.  
  
 **EXPLAIN 출력 예제**  
  
 행 번호가 켜져 있는 **EXPLAIN** 명령의 XML 결과는 다음과 같습니다.  
  
```  
1  \<?xml version="1.0" encoding="utf-8"?>  
2  <dsql_query>  
3    <sql>SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
4          CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
5          G.StateProvinceName, T.SalesTerritoryGroup  
6      FROM dbo.DimGeography AS G  
7      JOIN dbo.DimSalesTerritory AS T  
8          ON G.SalesTerritoryKey = T.SalesTerritoryKey  
9      JOIN dbo.DimCustomer AS C  
10          ON G.GeographyKey = C.GeographyKey  
11      JOIN dbo.FactInternetSales AS FIS  
12          ON C.CustomerKey = FIS.CustomerKey  
13      WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
14          AND Gender = 'F'  
15      GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
16      ORDER BY AVG(YearlyIncome) DESC</sql>  
17    <dsql_operations total_cost="0.926237696" total_number_operations="9">  
18      <dsql_operation operation_type="RND_ID">  
19        <identifier>TEMP_ID_16893</identifier>  
20      </dsql_operation>  
21      <dsql_operation operation_type="ON">  
22        <location permanent="false" distribution="AllComputeNodes" />  
23        <sql_operations>  
24          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16893] ([CustomerKey] INT NOT NULL, [GeographyKey] INT, [YearlyIncome] MONEY ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
25        </sql_operations>  
26      </dsql_operation>  
27      <dsql_operation operation_type="BROADCAST_MOVE">  
28        <operation_cost cost="0.121431552" accumulative_cost="0.121431552" average_rowsize="16" output_rows="31.6228" />  
29        <source_statement>SELECT [T1_1].[CustomerKey] AS [CustomerKey],  
30         [T1_1].[GeographyKey] AS [GeographyKey],  
31         [T1_1].[YearlyIncome] AS [YearlyIncome]  
32  FROM   (SELECT [T2_1].[CustomerKey] AS [CustomerKey],  
33                 [T2_1].[GeographyKey] AS [GeographyKey],  
34                 [T2_1].[YearlyIncome] AS [YearlyIncome]  
35          FROM   [AdventureWorksPDW2012].[dbo].[DimCustomer] AS T2_1  
36          WHERE  ([T2_1].[Gender] = CAST (N'F' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (1)) COLLATE Latin1_General_100_CI_AS_KS_WS)) AS T1_1</source_statement>  
37        <destination_table>[TEMP_ID_16893]</destination_table>  
38      </dsql_operation>  
39      <dsql_operation operation_type="RND_ID">  
40        <identifier>TEMP_ID_16894</identifier>  
41      </dsql_operation>  
42      <dsql_operation operation_type="ON">  
43        <location permanent="false" distribution="AllDistributions" />  
44        <sql_operations>  
45          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16894] ([StateProvinceName] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS, [SalesTerritoryGroup] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS NOT NULL, [col] BIGINT, [col1] MONEY NOT NULL, [col2] BIGINT, [col3] MONEY NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
46        </sql_operations>  
47      </dsql_operation>  
48      <dsql_operation operation_type="SHUFFLE_MOVE">  
49        <operation_cost cost="0.804806144" accumulative_cost="0.926237696" average_rowsize="232" output_rows="108.406" />  
50        <source_statement>SELECT [T1_1].[StateProvinceName] AS [StateProvinceName],  
51         [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
52         [T1_1].[col2] AS [col],  
53         [T1_1].[col] AS [col1],  
54         [T1_1].[col3] AS [col2],  
55         [T1_1].[col1] AS [col3]  
56  FROM   (SELECT ISNULL([T2_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col],  
57                 ISNULL([T2_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col1],  
58                 [T2_1].[StateProvinceName] AS [StateProvinceName],  
59                 [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
60                 [T2_1].[col] AS [col2],  
61                 [T2_1].[col2] AS [col3]  
62          FROM   (SELECT   COUNT_BIG([T3_2].[YearlyIncome]) AS [col],  
63                           SUM([T3_2].[YearlyIncome]) AS [col1],  
64                           COUNT_BIG(CAST ((0) AS INT)) AS [col2],  
65                           SUM([T3_2].[SalesAmount]) AS [col3],  
66                           [T3_2].[StateProvinceName] AS [StateProvinceName],  
67                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
68                  FROM     (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
69                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
70                            FROM   [AdventureWorksPDW2012].[dbo].[DimSalesTerritory] AS T4_1  
71                            WHERE  (([T4_1].[SalesTerritoryGroup] = CAST (N'North America' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (13)) COLLATE Latin1_General_100_CI_AS_KS_WS)  
72                                    OR ([T4_1].[SalesTerritoryGroup] = CAST (N'Pacific' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (7)) COLLATE Latin1_General_100_CI_AS_KS_WS))) AS T3_1  
73                           INNER JOIN  
74                           (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
75                                   [T4_2].[YearlyIncome] AS [YearlyIncome],  
76                                   [T4_2].[SalesAmount] AS [SalesAmount],  
77                                   [T4_1].[StateProvinceName] AS [StateProvinceName]  
78                            FROM   [AdventureWorksPDW2012].[dbo].[DimGeography] AS T4_1  
79                                   INNER JOIN  
80                                   (SELECT [T5_2].[GeographyKey] AS [GeographyKey],  
81                                           [T5_2].[YearlyIncome] AS [YearlyIncome],  
82                                           [T5_1].[SalesAmount] AS [SalesAmount]  
83                                    FROM   [AdventureWorksPDW2012].[dbo].[FactInternetSales] AS T5_1  
84                                           INNER JOIN  
85                                           [tempdb].[dbo].[TEMP_ID_16893] AS T5_2  
86                                           ON ([T5_1].[CustomerKey] = [T5_2].[CustomerKey])) AS T4_2  
87                                   ON ([T4_2].[GeographyKey] = [T4_1].[GeographyKey])) AS T3_2  
88                           ON ([T3_1].[SalesTerritoryKey] = [T3_2].[SalesTerritoryKey])  
89                  GROUP BY [T3_2].[StateProvinceName], [T3_1].[SalesTerritoryGroup]) AS T2_1) AS T1_1</source_statement>  
90        <destination_table>[TEMP_ID_16894]</destination_table>  
91        <shuffle_columns>StateProvinceName;</shuffle_columns>  
92      </dsql_operation>  
93      <dsql_operation operation_type="ON">  
94        <location permanent="false" distribution="AllComputeNodes" />  
95        <sql_operations>  
96          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16893]</sql_operation>  
97        </sql_operations>  
98      </dsql_operation>  
99      <dsql_operation operation_type="RETURN">  
100        <location distribution="AllDistributions" />  
101        <select>SELECT   [T1_1].[col] AS [col],  
102           [T1_1].[col1] AS [col1],  
103           [T1_1].[StateProvinceName] AS [StateProvinceName],  
104           [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
105           [T1_1].[col2] AS [col2]  
106  FROM     (SELECT CONVERT (INT, [T2_1].[col], 0) AS [col],  
107                   CONVERT (INT, [T2_1].[col1], 0) AS [col1],  
108                   [T2_1].[StateProvinceName] AS [StateProvinceName],  
109                   [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
110                   [T2_1].[col] AS [col2]  
111            FROM   (SELECT CASE  
112                            WHEN ([T3_1].[col] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
113                            ELSE ([T3_1].[col1] / CONVERT (MONEY, [T3_1].[col], 0))  
114                           END AS [col],  
115                           CASE  
116                            WHEN ([T3_1].[col2] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
117                            ELSE ([T3_1].[col3] / CONVERT (MONEY, [T3_1].[col2], 0))  
118                           END AS [col1],  
119                           [T3_1].[StateProvinceName] AS [StateProvinceName],  
120                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
121                    FROM   (SELECT ISNULL([T4_1].[col], CONVERT (BIGINT, 0, 0)) AS [col],  
122                                   ISNULL([T4_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col1],  
123                                   ISNULL([T4_1].[col2], CONVERT (BIGINT, 0, 0)) AS [col2],  
124                                   ISNULL([T4_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col3],  
125                                   [T4_1].[StateProvinceName] AS [StateProvinceName],  
126                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
127                            FROM   (SELECT   SUM([T5_1].[col]) AS [col],  
128                                             SUM([T5_1].[col1]) AS [col1],  
129                                             SUM([T5_1].[col2]) AS [col2],  
130                                             SUM([T5_1].[col3]) AS [col3],  
131                                             [T5_1].[StateProvinceName] AS [StateProvinceName],  
132                                             [T5_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
133                                    FROM     [tempdb].[dbo].[TEMP_ID_16894] AS T5_1  
134                                    GROUP BY [T5_1].[StateProvinceName], [T5_1].[SalesTerritoryGroup]) AS T4_1) AS T3_1) AS T2_1) AS T1_1  
135  ORDER BY [T1_1].[col2] DESC</select>  
136      </dsql_operation>  
137      <dsql_operation operation_type="ON">  
138        <location permanent="false" distribution="AllDistributions" />  
139        <sql_operations>  
140          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16894]</sql_operation>  
141        </sql_operations>  
142      </dsql_operation>  
143    </dsql_operations>  
144  </dsql_query>  
  
```  
  
 **EXPLAIN 출력의 의미**
  
 위의 출력에는 번호가 매겨진 144개의 줄이 포함되어 있습니다. 이 쿼리의 출력은 약간 다를 수 있습니다. 다음 목록은 중요 섹션을 설명합니다.  
  
-   3~16번 줄: 분석되는 쿼리에 대한 설명을 제공합니다.  
  
-   17번 줄: 총 작업 수를 9개로 지정합니다. **dsql_operation** 단어를 찾아서 각 작업의 시작을 찾을 수 있습니다.  
  
-   18번 줄: 작업 1을 시작합니다. 18번 및 19번 줄: **RND_ID** 작업에서 개체 설명에 사용할 임의의 ID 번호를 생성함을 나타냅니다. 위의 출력에서 설명하는 개체는 **TEMP_ID_16893**입니다. 숫자가 다를 수도 있습니다.  
  
-   20번 줄: 작업 2를 시작합니다. 21 ~ 25번 줄: 모든 컴퓨팅 노드에서 **TEMP_ID_16893**이라는 임시 테이블을 만듭니다.  
  
-   26번 줄: 작업 3을 시작합니다. 27 ~ 37번 줄: 브로드캐스트 이동을 사용하여 데이터를 **TEMP_ID_16893**으로 이동합니다. 각 컴퓨팅 노드로 보낸 쿼리가 제공됩니다. 37번 줄: 대상 테이블이 **TEMP_ID_16893**임을 지정합니다.  
  
-   38번 줄: 작업 4를 시작합니다. 39 ~ 40번 줄: 테이블에 대한 임의의 ID를 만듭니다. 위의 예제에서 **TEMP_ID_16894**는 ID 번호입니다. 숫자가 다를 수도 있습니다.  
  
-   41번 줄: 작업 5를 시작합니다. 42 ~ 46번 줄: 모든 노드에서 **TEMP_ID_16894**라는 임시 테이블을 만듭니다.  
  
-   47번 줄: 작업 6을 시작합니다. 48 ~ 91번 줄: 순서 섞기 이동 작업을 사용하여 다양한 테이블(**TEMP_ID_16893** 포함)에서 **TEMP_ID_16894** 테이블로 데이터를 이동합니다. 각 컴퓨팅 노드로 보낸 쿼리가 제공됩니다. 90번 줄: 대상 테이블을 **TEMP_ID_16894**로 지정합니다. 91번 줄: 열을 지정합니다.  
  
-   92번 줄: 작업 7을 시작합니다. 93 ~ 97번 줄: 모든 컴퓨팅 노드에서 **TEMP_ID_16893** 임시 테이블을 삭제합니다.  
  
-   98번 줄: 작업 8을 시작합니다. 99 ~ 135번 줄: 결과를 클라이언트로 반환합니다. 제공된 쿼리를 사용하여 결과를 가져옵니다.  
  
-   136번 줄: 작업 9를 시작합니다. 137 ~ 140번 줄: 모든 노드에서 **TEMP_ID_16894** 임시 테이블을 삭제합니다.  

**WITH_RECOMMENDATIONS EXPLAIN 문 제출**

```sql
-- EXPLAIN WITH_RECOMMENDATIONS
select count(*)
from ((select distinct c_last_name, c_first_name, d_date
       from store_sales, date_dim, customer
       where store_sales.ss_sold_date_sk = date_dim.d_date_sk
         and store_sales.ss_customer_sk = customer.c_customer_sk
         and d_month_seq between 1194 and 1194+11)
       except
      (select distinct c_last_name, c_first_name, d_date
       from catalog_sales, date_dim, customer
       where catalog_sales.cs_sold_date_sk = date_dim.d_date_sk
         and catalog_sales.cs_bill_customer_sk = customer.c_customer_sk
         and d_month_seq between 1194 and 1194+11)
) top_customers
```

**EXPLAIN WITH_RECOMMENDATIONS에 대한 출력 예제**(미리 보기)

아래 출력은 View1이라는 권장되는 구체화된 뷰 만들기를 포함합니다.  

```
<?xml version="1.0" encoding="utf-8"?>
<dsql_query number_nodes="1" number_distributions="8" number_distributions_per_node="8">
  <sql>select count(*) 
from ((select distinct c_last_name, c_first_name, d_date
       from store_sales, date_dim, customer
       where store_sales.ss_sold_date_sk = date_dim.d_date_sk
         and store_sales.ss_customer_sk = customer.c_customer_sk
         and d_month_seq between 1194 and 1194+11)
       except
      (select distinct c_last_name, c_first_name, d_date
       from catalog_sales, date_dim, customer
       where catalog_sales.cs_sold_date_sk = date_dim.d_date_sk
         and catalog_sales.cs_bill_customer_sk = customer.c_customer_sk
         and d_month_seq between 1194 and 1194+11)
) top_customers</sql>
  <materialized_view_candidates>
    <materialized_view_candidates with_constants="False">CREATE MATERIALIZED VIEW View1 WITH (DISTRIBUTION = HASH([Expr0])) AS
SELECT [tpcds10].[dbo].[customer].[c_last_name] AS [Expr0],
       [tpcds10].[dbo].[customer].[c_first_name] AS [Expr1],
       [tpcds10].[dbo].[date_dim].[d_date] AS [Expr2],
       [tpcds10].[dbo].[date_dim].[d_month_seq] AS [Expr3]
FROM [dbo].[store_sales],
     [dbo].[date_dim],
     [dbo].[customer]
WHERE ([tpcds10].[dbo].[store_sales].[ss_customer_sk]=[tpcds10].[dbo].[customer].[c_customer_sk])
  AND ([tpcds10].[dbo].[store_sales].[ss_sold_date_sk]=[tpcds10].[dbo].[date_dim].[d_date_sk])
GROUP BY [tpcds10].[dbo].[customer].[c_last_name],
         [tpcds10].[dbo].[customer].[c_first_name],
         [tpcds10].[dbo].[date_dim].[d_date],
         [tpcds10].[dbo].[date_dim].[d_month_seq]</materialized_view_candidates>
    <materialized_view_candidates with_constants="False">CREATE MATERIALIZED VIEW View2 WITH (DISTRIBUTION = HASH([Expr0])) AS
SELECT [tpcds10].[dbo].[customer].[c_last_name] AS [Expr0],
       [tpcds10].[dbo].[customer].[c_first_name] AS [Expr1],
       [tpcds10].[dbo].[date_dim].[d_date] AS [Expr2],
       [tpcds10].[dbo].[date_dim].[d_month_seq] AS [Expr3]
FROM [dbo].[catalog_sales],
    [dbo].[date_dim],
     [dbo].[customer]
WHERE ([tpcds10].[dbo].[catalog_sales].[cs_bill_customer_sk]=[tpcds10].[dbo].[customer].[c_customer_sk])
  AND ([tpcds10].[dbo].[catalog_sales].[cs_sold_date_sk]=[tpcds10].[dbo].[date_dim].[d_date_sk])
GROUP BY [tpcds10].[dbo].[customer].[c_last_name],
         [tpcds10].[dbo].[customer].[c_first_name],
         [tpcds10].[dbo].[date_dim].[d_date],
         [tpcds10].[dbo].[date_dim].[d_month_seq]</materialized_view_candidates>
    <materialized_view_candidates with_constants="True">CREATE MATERIALIZED VIEW View3 WITH (DISTRIBUTION = HASH([Expr0])) AS
SELECT [tpcds10].[dbo].[customer].[c_last_name] AS [Expr0],
       [tpcds10].[dbo].[customer].[c_first_name] AS [Expr1],
       [tpcds10].[dbo].[date_dim].[d_date] AS [Expr2]
FROM [dbo].[store_sales],
     [dbo].[date_dim],
     [dbo].[customer]
WHERE ([tpcds10].[dbo].[store_sales].[ss_customer_sk]=[tpcds10].[dbo].[customer].[c_customer_sk])
  AND ([tpcds10].[dbo].[store_sales].[ss_sold_date_sk]=[tpcds10].[dbo].[date_dim].[d_date_sk])
  AND ([tpcds10].[dbo].[date_dim].[d_month_seq]&gt;=(1194))
  AND ([tpcds10].[dbo].[date_dim].[d_month_seq]&lt;=(1205))
GROUP BY [tpcds10].[dbo].[customer].[c_last_name],
         [tpcds10].[dbo].[customer].[c_first_name],
         [tpcds10].[dbo].[date_dim].[d_date]</materialized_view_candidates>
    <materialized_view_candidates with_constants="True">CREATE MATERIALIZED VIEW View4 WITH (DISTRIBUTION = HASH([Expr0])) AS
SELECT [tpcds10].[dbo].[customer].[c_last_name] AS [Expr0],
       [tpcds10].[dbo].[customer].[c_first_name] AS [Expr1],
       [tpcds10].[dbo].[date_dim].[d_date] AS [Expr2]
FROM [dbo].[catalog_sales],
     [dbo].[date_dim],
     [dbo].[customer]
WHERE ([tpcds10].[dbo].[catalog_sales].[cs_bill_customer_sk]=[tpcds10].[dbo].[customer].[c_customer_sk])
  AND ([tpcds10].[dbo].[catalog_sales].[cs_sold_date_sk]=[tpcds10].[dbo].[date_dim].[d_date_sk])
  AND ([tpcds10].[dbo].[date_dim].[d_month_seq]&gt;=(1194))
  AND ([tpcds10].[dbo].[date_dim].[d_month_seq]&lt;=(1205))
GROUP BY [tpcds10].[dbo].[customer].[c_last_name],
         [tpcds10].[dbo].[customer].[c_first_name],
         [tpcds10].[dbo].[date_dim].[d_date]</materialized_view_candidates>
  </materialized_view_candidates>
  <dsql_operations total_cost="3472197.35650704" total_number_operations="28">
    <dsql_operation operation_type="RND_ID">
      <identifier>TEMP_ID_1</identifier>
    </dsql_operation>
    <dsql_operation operation_type="ON">
      <location permanent="false" distribution="AllComputeNodes" />
      <sql_operations>
        <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_1] ([c_customer_sk] INT NOT NULL, [c_first_name] CHAR(20) COLLATE SQL_Latin1_General_CP1_CI_AS, [c_last_name] CHAR(30) COLLATE SQL_Latin1_General_CP1_CI_AS ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>
      </sql_operations>
    </dsql_operation>
    <dsql_operation operation_type="BROADCAST_MOVE">
      <operation_cost cost="842400" accumulative_cost="842400" average_rowsize="54" output_rows="65000000" GroupNumber="44" />
      <source_statement>SELECT [T1_1].[c_customer_sk] AS [c_customer_sk],
       [T1_1].[c_first_name] AS [c_first_name],
       [T1_1].[c_last_name] AS [c_last_name]
FROM   [tpcds10].[dbo].[customer] AS T1_1</source_statement>
      <destination_table>[TEMP_ID_1]</destination_table>
    </dsql_operation>
    <dsql_operation operation_type="RND_ID">
      <identifier>TEMP_ID_2</identifier>
    </dsql_operation>
    <dsql_operation operation_type="ON">
      <location permanent="false" distribution="AllComputeNodes" />
      <sql_operations>
        <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_2] ([d_date_sk] INT NOT NULL, [d_date] DATE ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>
      </sql_operations>
    </dsql_operation>
    <dsql_operation operation_type="BROADCAST_MOVE">
      <operation_cost cost="0.62729352" accumulative_cost="842400.62729352" average_rowsize="7" output_rows="373.389" GroupNumber="43" />
      <source_statement>SELECT [T1_1].[d_date_sk] AS [d_date_sk],
       [T1_1].[d_date] AS [d_date]
FROM   (SELECT [T2_1].[d_date_sk] AS [d_date_sk],
               [T2_1].[d_date] AS [d_date]
        FROM   [tpcds10].[dbo].[date_dim] AS T2_1
        WHERE  (([T2_1].[d_month_seq] &gt;= CAST ((1194) AS INT))
                AND ([T2_1].[d_month_seq] &lt;= CAST ((1205) AS INT)))) AS T1_1</source_statement>
      <destination_table>[TEMP_ID_2]</destination_table>
    </dsql_operation>
    <dsql_operation operation_type="RND_ID">
      <identifier>TEMP_ID_3</identifier>
    </dsql_operation>
    <dsql_operation operation_type="ON">
      <location permanent="false" distribution="AllDistributions" />
      <sql_operations>
        <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_3] ([cs_bill_customer_sk] INT, [d_date] DATE ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>
      </sql_operations>
    </dsql_operation>
    <dsql_operation operation_type="SHUFFLE_MOVE">
      <operation_cost cost="610362.9" accumulative_cost="1452763.52729352" average_rowsize="7" output_rows="2906490000" GroupNumber="57" />
      <source_statement>SELECT [T1_1].[cs_bill_customer_sk] AS [cs_bill_customer_sk],
       [T1_1].[d_date] AS [d_date]
FROM   (SELECT [T2_2].[cs_bill_customer_sk] AS [cs_bill_customer_sk],
               [T2_1].[d_date] AS [d_date]
        FROM   [tempdb].[dbo].[TEMP_ID_2] AS T2_1
               INNER JOIN
               [tpcds10].[dbo].[catalog_sales] AS T2_2
               ON ([T2_2].[cs_sold_date_sk] = [T2_1].[d_date_sk])) AS T1_1</source_statement>
      <destination_table>[TEMP_ID_3]</destination_table>
      <shuffle_columns>d_date;</shuffle_columns>
    </dsql_operation>
    <dsql_operation operation_type="ON">
      <location permanent="false" distribution="AllComputeNodes" />
      <sql_operations>
        <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_2]</sql_operation>
      </sql_operations>
    </dsql_operation>
    <dsql_operation operation_type="RND_ID">
      <identifier>TEMP_ID_4</identifier>
    </dsql_operation>
    <dsql_operation operation_type="ON">
      <location permanent="false" distribution="AllComputeNodes" />
      <sql_operations>
        <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_4] ([c_customer_sk] INT NOT NULL, [c_first_name] CHAR(20) COLLATE SQL_Latin1_General_CP1_CI_AS, [c_last_name] CHAR(30) COLLATE SQL_Latin1_General_CP1_CI_AS ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>
      </sql_operations>
    </dsql_operation>
    <dsql_operation operation_type="BROADCAST_MOVE">
      <operation_cost cost="842400" accumulative_cost="2295163.52729352" average_rowsize="54" output_rows="65000000" GroupNumber="36" />
      <source_statement>SELECT [T1_1].[c_customer_sk] AS [c_customer_sk],
       [T1_1].[c_first_name] AS [c_first_name],
       [T1_1].[c_last_name] AS [c_last_name]
FROM   [tpcds10].[dbo].[customer] AS T1_1</source_statement>
      <destination_table>[TEMP_ID_4]</destination_table>
    </dsql_operation>
    <dsql_operation operation_type="RND_ID">
      <identifier>TEMP_ID_5</identifier>
    </dsql_operation>
    <dsql_operation operation_type="ON">
      <location permanent="false" distribution="AllComputeNodes" />
      <sql_operations>
        <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_5] ([d_date_sk] INT NOT NULL, [d_date] DATE ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>
      </sql_operations>
    </dsql_operation>
    <dsql_operation operation_type="BROADCAST_MOVE">
      <operation_cost cost="0.62729352" accumulative_cost="2295164.15458704" average_rowsize="7" output_rows="373.389" GroupNumber="35" />
      <source_statement>SELECT [T1_1].[d_date_sk] AS [d_date_sk],
       [T1_1].[d_date] AS [d_date]
FROM   (SELECT [T2_1].[d_date_sk] AS [d_date_sk],
               [T2_1].[d_date] AS [d_date]
        FROM   [tpcds10].[dbo].[date_dim] AS T2_1
        WHERE  (([T2_1].[d_month_seq] &gt;= CAST ((1194) AS INT))
                AND ([T2_1].[d_month_seq] &lt;= CAST ((1205) AS INT)))) AS T1_1</source_statement>
      <destination_table>[TEMP_ID_5]</destination_table>
    </dsql_operation>
    <dsql_operation operation_type="RND_ID">
      <identifier>TEMP_ID_6</identifier>
    </dsql_operation>
    <dsql_operation operation_type="ON">
      <location permanent="false" distribution="AllDistributions" />
      <sql_operations>
        <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_6] ([ss_customer_sk] INT, [d_date] DATE ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>
      </sql_operations>
    </dsql_operation>
    <dsql_operation operation_type="SHUFFLE_MOVE">
      <operation_cost cost="1177033.2" accumulative_cost="3472197.35458704" average_rowsize="7" output_rows="5604920000" GroupNumber="54" />
      <source_statement>SELECT [T1_1].[ss_customer_sk] AS [ss_customer_sk],
       [T1_1].[d_date] AS [d_date]
FROM   (SELECT [T2_2].[ss_customer_sk] AS [ss_customer_sk],
               [T2_1].[d_date] AS [d_date]
        FROM   [tempdb].[dbo].[TEMP_ID_5] AS T2_1
               INNER JOIN
               [tpcds10].[dbo].[store_sales] AS T2_2
               ON ([T2_2].[ss_sold_date_sk] = [T2_1].[d_date_sk])) AS T1_1</source_statement>
      <destination_table>[TEMP_ID_6]</destination_table>
      <shuffle_columns>d_date;</shuffle_columns>
    </dsql_operation>
    <dsql_operation operation_type="ON">
      <location permanent="false" distribution="AllComputeNodes" />
      <sql_operations>
        <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_5]</sql_operation>
      </sql_operations>
    </dsql_operation>
    <dsql_operation operation_type="ON">
      <location permanent="false" distribution="Control" />
     <sql_operations>
        <sql_operation type="statement">CREATE TABLE [tempdb].[QTables].[QTable_87367172aa554f06b73cf3ed97e5b985] ([col] BIGINT ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>
      </sql_operations>
    </dsql_operation>
    <dsql_operation operation_type="PARTITION_MOVE">
      <operation_cost cost="0.00192" accumulative_cost="3472197.35650704" average_rowsize="8" output_rows="1" GroupNumber="66" />
      <location distribution="AllDistributions" />
      <source_statement>SELECT [T1_1].[col] AS [col]
FROM   (SELECT   COUNT_BIG(CAST ((0) AS INT)) AS [col]
        FROM     (SELECT   0 AS [col]
                  FROM     [tempdb].[dbo].[TEMP_ID_4] AS T3_1
                           INNER JOIN
                           [tempdb].[dbo].[TEMP_ID_6] AS T3_2
                           ON ([T3_2].[ss_customer_sk] = [T3_1].[c_customer_sk])
                  GROUP BY [T3_1].[c_last_name], [T3_1].[c_first_name], [T3_2].[d_date]
                  HAVING   NOT EXISTS (SELECT   1 AS C1
                                       FROM     [tempdb].[dbo].[TEMP_ID_1] AS T4_1
                                                INNER JOIN
                                                [tempdb].[dbo].[TEMP_ID_3] AS T4_2
                                                ON ([T4_2].[cs_bill_customer_sk] = [T4_1].[c_customer_sk])
                                       GROUP BY [T4_1].[c_last_name], [T4_1].[c_first_name], [T4_2].[d_date]
                                       HAVING   (([T3_1].[c_last_name] = [T4_1].[c_last_name]
                                                  OR ([T3_1].[c_last_name] IS NULL
                                                      AND [T4_1].[c_last_name] IS NULL))
                                                 AND ([T3_1].[c_first_name] = [T4_1].[c_first_name]
                                                      OR ([T3_1].[c_first_name] IS NULL
                                                          AND [T4_1].[c_first_name] IS NULL))
                                                     AND ([T3_2].[d_date] = [T4_2].[d_date]
                                                          OR ([T3_2].[d_date] IS NULL
                                                              AND [T4_2].[d_date] IS NULL))))) AS T2_1
        GROUP BY [T2_1].[col]) AS T1_1</source_statement>
      <destination>Control</destination>
      <destination_table>[QTable_87367172aa554f06b73cf3ed97e5b985]</destination_table>
    </dsql_operation>
    <dsql_operation operation_type="ON">
      <location permanent="false" distribution="AllDistributions" />
      <sql_operations>
        <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_6]</sql_operation>
      </sql_operations>
    </dsql_operation>
    <dsql_operation operation_type="ON">
      <location permanent="false" distribution="AllComputeNodes" />
      <sql_operations>
        <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_4]</sql_operation>
      </sql_operations>
    </dsql_operation>
    <dsql_operation operation_type="ON">
      <location permanent="false" distribution="AllDistributions" />
      <sql_operations>
        <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_3]</sql_operation>
      </sql_operations>
    </dsql_operation>
    <dsql_operation operation_type="ON">
      <location permanent="false" distribution="AllComputeNodes" />
      <sql_operations>
        <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_1]</sql_operation>
      </sql_operations>
    </dsql_operation>
    <dsql_operation operation_type="RETURN">
      <location distribution="Control" />
      <select>SELECT [T1_1].[col] AS [col]
FROM   (SELECT CONVERT (INT, [T2_1].[col], 0) AS [col]
        FROM   (SELECT ISNULL([T3_1].[col], CONVERT (BIGINT, 0, 0)) AS [col]
                FROM   (SELECT SUM([T4_1].[col]) AS [col]
                        FROM   [tempdb].[QTables].[QTable_87367172aa554f06b73cf3ed97e5b985] AS T4_1) AS T3_1) AS T2_1) AS T1_1</select>
    </dsql_operation>
    <dsql_operation operation_type="ON">
      <location permanent="false" distribution="Control" />
      <sql_operations>
        <sql_operation type="statement">DROP TABLE [tempdb].[QTables].[QTable_87367172aa554f06b73cf3ed97e5b985]</sql_operation>
      </sql_operations>
    </dsql_operation>
  </dsql_operations>
</dsql_query>
```

## <a name="see-also"></a>관련 항목:
[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure SQL Data Warehouse에서 지원되는 시스템 뷰](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure SQL Data Warehouse에서 지원되는 T-SQL 문](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
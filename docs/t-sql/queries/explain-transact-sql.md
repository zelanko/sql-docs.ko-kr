---
title: "(Transact SQL) 설명 | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4846a576-57ea-4068-959c-81e69e39ddc1
caps.latest.revision: 13
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: af61ec5c670bdc48a3f661080983fac3e7263014
ms.contentlocale: ko-kr
ms.lasthandoff: 10/24/2017

---
# <a name="explain-transact-sql"></a>설명 (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  에 대 한 쿼리 계획을 반환 된 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 문을 실행 하지 않고 문입니다. 사용 하 여 **설명** 미리 보기는 작업에는 데이터 이동 필요 하 고 쿼리 작업의 예상된 비용을 볼 수 있습니다.  
  
 쿼리 계획에 대 한 자세한 내용은 "쿼리 계획 이해"를 참조는 [!INCLUDE[pdw-product-documentation_md](../../includes/pdw-product-documentation-md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  

```  
EXPLAIN SQL_statement  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *SQL_statement*  
 [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 는에서 문 **설명** 실행 됩니다. *SQL_statement* 다음이 명령 중 하나가 될 수 있습니다: **선택**, **삽입**, **업데이트**, **삭제**,  **CREATE TABLE AS SELECT**, **원격 테이블 만들기**합니다.  
  
## <a name="permissions"></a>Permissions  
 필요는 **SHOWPLAN** 사용 권한 및 실행할 수 있는 권한이 *SQL_statement*합니다. 참조 [사용 권한: GRANT, DENY, REVOKE 및 #40; Azure SQL 데이터 웨어하우스, 병렬 데이터 웨어하우스 &#41; ](../../t-sql/statements/permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse.md).  
  
## <a name="return-value"></a>반환 값  
 반환 값은 **설명** 명령 아래에 표시 된 구조와 함께 XML 문서입니다. 이 XML 문서 지정된 쿼리에 대 한 쿼리 계획의 모든 작업에는, 묶어 각는 `<dsql_operation>` 태그입니다. 형식의 반환 값은 **nvarchar (max)**합니다.  
  
 반환 된 쿼리 계획은 SQL 문을 순차적; 보여 줍니다. 쿼리를 실행할 때에 표시 된 순차 문 중 일부 동시에 실행할 수 있도록 병렬된 작업을 포함 될 수 있습니다.  
  
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
  
 이 정보를 포함 하는 XML 태그:  
  
|XML 태그|요약, 특성 및 콘텐츠|  
|-------------|--------------------------------------|  
|\<dsql_query >|최상위 수준/문서 요소입니다.|
|\<sql >|에코 *SQL_statement*합니다.|  
|\<매개 변수 >|이 태그는이 이번에는 사용 되지 않습니다.|  
|\<dsql_operations >|요약 하 고 쿼리 단계를 포함 하 고 쿼리에 대 한 비용 정보가 포함 됩니다. 또한 모든 포함 된 `<dsql_operation>` 블록. 이 태그에는 전체 쿼리에 대 한 개수 정보가 포함 됩니다.<br /><br /> `<dsql_operations total_cost=total_cost total_number_operations=total_number_operations>`<br /><br /> *total_cost* ms에서 실행할 쿼리에 대 한 총 예상된 시간입니다.<br /><br /> *total_number_operations* 쿼리에 대 한 작업의 총 수입니다. 평행 화 되 고 여러 노드에서 실행 되는 작업은 한 번의 작업으로 간주 됩니다.|  
|\<dsql_operation >|쿼리 계획 내 단일 작업에 설명합니다. \<dsql_operation > 태그에 특성으로 작업 유형을 포함 합니다.<br /><br /> `<dsql_operation operation_type=operation_type>`<br /><br /> *operation_type* 에 있는 값 중 하나는 [데이터 쿼리 (SQL Server PDW)](http://msdn.microsoft.com/en-us/3f4f5643-012a-4c36-b5ec-691c4bbe668c)합니다.<br /><br /> 콘텐츠는 `\<dsql_operation>` 블록은 작업 유형에 따라 다릅니다.<br /><br /> 아래 표를 참조 합니다.|  
  
|작업 유형|콘텐츠|예제|  
|--------------------|-------------|-------------|  
|BROADCAST_MOVE, DISTRIBUTE_REPLICATED_TABLE_MOVE, MASTER_TABLE_MOVE, PARTITION_MOVE, SHUFFLE_MOVE, 및 TRIM_MOVE|`<operation_cost>`이러한 특성을 가진 요소입니다. 로컬 작업에만 반영 하는 값:<br /><br /> -   *비용* 로컬 연산자 비용 및 ms에서를 실행 하려면 작업에 대 한 예상된 시간을 보여 줍니다.<br />-   *accumulative_cost* ms에서 병렬 작업에 대 한 합계 값을 포함 하 여 계획에 표시 되는 모든 작업의 합계입니다.<br />-   *average_rowsize* 의 예상된 평균 행 크기 (바이트)의 행 검색 하 고 작업을 하는 동안 전달 됩니다.<br />-   *output_rows* 출력 (노드) 카디널리티가 출력 행의 수를 표시 합니다.<br /><br /> `<location>`: 노드 또는 배포 후 작업을 발생 합니다. 옵션은: "제어", "ComputeNode", "AllComputeNodes", "AllDistributions", "SubsetDistributions", "배포" 및 "SubsetNodes"입니다.<br /><br /> `<source_statement>`:의 원본 데이터의 순서 섞기를 이동합니다.<br /><br /> `<destination_table>`: 내부 임시 테이블 데이터는로 이동 됩니다.<br /><br /> `<shuffle_columns>`: (SHUFFLE_MOVE 작업에만 적용 가능). 임시 테이블에 대 한 배포 열으로 사용할 하나 이상의 열입니다.|`<operation_cost cost="40" accumulative_cost="40" average_rowsize = "50" output_rows="100"/>`<br /><br /> `<location distribution="AllDistributions" />`<br /><br /> `<source_statement type="statement">SELECT [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d].[dist_date] FROM [qatest].[dbo].[flyers] [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d]       </source_statement>`<br /><br /> `<destination_table>Q_[TEMP_ID_259]_[PARTITION_ID]</destination_table>`<br /><br /> `<shuffle_columns>dist_date;</shuffle_columns>`|  
|CopyOperation|`<operation_cost>`: 참조 `<operation_cost>` 위에 있습니다.<br /><br /> `<DestinationCatalog>`: 대상 노드 또는 노드입니다.<br /><br /> `<DestinationSchema>`: DestinationCatalog에 대상 스키마입니다.<br /><br /> `<DestinationTableName>`: "TableName" 또는 대상 테이블의 이름입니다.<br /><br /> `<DestinationDatasource>`: 대상 데이터 원본의 이름 또는 연결 정보입니다.<br /><br /> `<Username>`및 `<Password>`: 이러한 필드는 사용자 이름 및 대상에 대 한 암호 필요할 수 있습니다를 나타냅니다.<br /><br /> `<BatchSize>`: 복사 작업에 대 한 일괄 처리 크기입니다.<br /><br /> `<SelectStatement>`복사를 수행 하는 데 사용: select 문입니다.<br /><br /> `<distribution>`: 배포 복사가 수행 됩니다.|`<operation_cost cost="0" accumulative_cost="0" average_rowsize="4" output_rows="1" />`<br /><br /> `<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>[TableName]</DestinationTableName>`<br /><br /> `<DestinationDatasource>localhost, 8080</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<BatchSize>6000</BatchSize>`<br /><br /> `<SelectStatement>SELECT T1_1.c1 AS c1 FROM [qatest].[dbo].[gigs] AS T1_1</SelectStatement>`<br /><br /> `<distribution>ControlNode</distribution>`|  
|MetaDataCreate_Operation|`<source_table>`: 작업에 대 한 원본 테이블입니다.<br /><br /> `<destionation_table>`: 작업에 대 한 대상 테이블입니다.|`<source_table>databases</source_table>`<br /><br /> `<destination_table>MetaDataCreateLandingTempTable</destination_table>`|  
|ON|`<location>`: 참조 `<location>` 위에 있습니다.<br /><br /> `<sql_operation>`: 노드에서 수행할 수 있는 SQL 명령을 식별 합니다.|`<location permanent="false" distribution="AllDistributions">Compute</location>`<br /><br /> `<sql_operation type="statement">CREATE TABLE [tempdb].[dbo]. [Q_[TEMP_ID_259]]_ [PARTITION_ID]]]([dist_date] DATE) WITH (DISTRIBUTION = HASH([dist_date]),) </sql_operation>`|  
|RemoteOnOperation|`<DestinationCatalog>`: 대상 카탈로그입니다.<br /><br /> `<DestinationSchema>`: DestinationCatalog에 대상 스키마입니다.<br /><br /> `<DestinationTableName>`: "TableName" 또는 대상 테이블의 이름입니다.<br /><br /> `<DestinationDatasource>`: 대상 데이터 원본의 이름입니다.<br /><br /> `<Username>`및 `<Password>`: 이러한 필드는 사용자 이름 및 대상에 대 한 암호 필요할 수 있습니다를 나타냅니다.<br /><br /> `<CreateStatement>`테이블 만들기: 대상 데이터베이스에 대 한 문입니다.|`<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>TableName</DestinationTableName>`<br /><br /> `<DestinationDatasource>DestDataSource</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<CreateStatement>CREATE TABLE [master].[dbo].[TableName] ([col1] BIGINT) ON [PRIMARY] WITH(DATA_COMPRESSION=PAGE);</CreateStatement>`|  
|RETURN|`<resultset>`: 결과 집합에 대 한 식별자입니다.|`<resultset>RS_19</resultset>`|  
|RND_ID|`<identifier>`: 생성 된 개체에 대 한 식별자입니다.|`<identifier>TEMP_ID_260</identifier>`|  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 **설명** 에 적용할 수 *최적화할 수 있는* 쿼리에만 개선 하거나 수정할 수 있는 쿼리는 결과에 따라는 **설명** 명령입니다. 지원 되는 **설명** 위에 명령이 나와 있습니다. 사용 하려고 하면 **설명** 유형 오류를 반환 하거나 쿼리 echo 지원 되지 않는 쿼리를 사용 합니다.  
  
 **설명** 사용자 트랜잭션에서 지원 되지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예제와 **설명** 에서 명령을 실행 한 **선택** 문 및 XML 결과입니다.  
  
 **설명 문을 전송**  
  
 이 예제에 대 한 전송 된 명령을 사용합니다.  
  
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
  
 사용 하 여 문을 실행 한 후의 **설명** 옵션, 메시지 탭 야기할 제목이 한 줄 **설명**, XML 텍스트로 시작 하 고 `\<?xml version="1.0" encoding="utf-8"?>` XML에 전체 텍스트 열을 클릭는 XML 창입니다. 다음 설명은 더 잘 이해 하려면 SSDT에 줄 번호의 표시 설정 해야 합니다.  
  
#### <a name="to-turn-on-line-numbers"></a>줄 번호를 설정 하려면  
  
1.  에 표시 되는 출력으로는 **설명** 탭에서 SSDT는 **도구** 메뉴를 선택 **옵션**합니다.  
  
2.  확장은 **텍스트 편집기** 섹션에서 확장 **XML**, 클릭 하 고 **일반**합니다.  
  
3.  에 **디스플레이** 영역에서 확인 **줄 번호**합니다.  
  
4.  **확인**을 클릭합니다.  
  
 **설명 출력 예**  
  
 XML 결과 **설명** 켜져 행 번호로 명령입니다.  
  
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
  
 **설명 출력의 의미**  
  
 위의 출력 144 번호가 매겨진된 줄을 포함합니다. 이 쿼리의 출력 약간 다를 수 있습니다. 다음 목록에는 중요 한 섹션을 설명합니다.  
  
-   3-16 줄에는 분석 되는 쿼리에 대 한 설명을 제공 합니다.  
  
-   줄 17, 전체 작업 개수 9가 되도록 지정 합니다. 단어를 검색 하 여 각 작업의 시작을 찾을 수 있습니다 **dsql_operation**합니다.  
  
-   18 줄 1 작업을 시작 합니다. 18, 19 줄 있음을 **RND_ID** 작업 개체 설명에 대 한 사용 될 ID 난수 만들어집니다. 위의 출력에 설명 된 개체는 **TEMP_ID_16893**합니다. 프로그램 번호가 달라질 수 있습니다.  
  
-   20 줄 2 작업을 시작합니다. 줄부터 25 21: 모든 계산 노드, 라는 임시 테이블을 만들어 **TEMP_ID_16893**합니다.  
  
-   줄 26 3 작업을 시작 합니다. 줄 27 37-: 데이터를 이동 **TEMP_ID_16893** 브로드캐스트 move를 사용 하 여 합니다. 각 계산 노드에 전송 하는 쿼리 제공 됩니다. 대상 테이블은 줄 37 지정 **TEMP_ID_16893**합니다.  
  
-   38 번째 줄에는 4 작업이 시작 됩니다. 39-40 줄: 테이블에 대 한 임의 ID를 만듭니다. **TEMP_ID_16894** 위의 예에서 ID 번호입니다. 프로그램 번호가 달라질 수 있습니다.  
  
-   줄 41 5 작업을 시작 합니다. 줄 46-42: 라는 임시 테이블을 만들어 모든 노드에서 **TEMP_ID_16894**합니다.  
  
-   줄 47 6 작업을 시작 합니다. 48 91 사이의 줄: 다양 한 테이블에서 데이터를 이동 (포함 하 여 **TEMP_ID_16893**) 테이블에 **TEMP_ID_16894**, 한 순서 섞기를 사용 하 여 이동 작업을 수행 합니다. 각 계산 노드에 전송 하는 쿼리 제공 됩니다. 줄 90으로 대상 테이블을 지정 합니다. **TEMP_ID_16894**합니다. 줄 91 열을 지정합니다.  
  
-   줄 92 7 작업을 시작 합니다. 97 통해 줄 93: 모든 계산 노드, 임시 테이블을 삭제 **TEMP_ID_16893**합니다.  
  
-   줄 98 8 번 작업을 시작합니다. 135 통해 줄 99: 클라이언트에 결과 반환 합니다. 결과를 얻으려면 제공 된 쿼리를 사용 합니다.  
  
-   줄 136 9 작업을 시작 합니다. 줄 137 140-: 임시 테이블을 삭제할 모든 노드에서 **TEMP_ID_16894**합니다.  
  
  



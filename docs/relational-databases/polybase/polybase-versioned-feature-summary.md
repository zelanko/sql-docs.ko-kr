---
title: PolyBase 기능 및 제한 사항 | Microsoft Docs
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bd4c7e7bb150a0eafbd855e1703713f3781bdc49
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71710451"
---
# <a name="polybase-features-and-limitations"></a>PolyBase 기능 및 제한 사항

[!INCLUDE[appliesto-ss2016-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

이 문서는 SQL Server 제품 및 서비스에 사용할 수 있는 PolyBase 기능에 대한 요약입니다.  
  
## <a name="feature-summary-for-product-releases"></a>제품 릴리스에 대한 기능 요약

이 표에서는 PolyBase의 주요 기능과 이를 사용할 수 있는 제품이 나열되어 있습니다.  
  
||||||
|-|-|-|-|-|   
|**기능**|**SQL Server 2016**|**Azure SQL Database**|**Azure SQL 데이터 웨어하우스**|**병렬 데이터 웨어하우스**| 
|다음을 사용하여 Hadoop 데이터 쿼리 [!INCLUDE[tsql](../../includes/tsql-md.md)]|yes|예|예|yes|
|Hadoop에서 데이터 가져오기|yes|예|예|yes|
|Hadoop으로 데이터 내보내기  |yes|예|예| yes|
|Azure HDInsight 쿼리, Azure HDInsight에서 가져오기, Azure HDInsight로 내보내기 |예|예|예|예
|Hadoop으로 쿼리 계산 푸시다운|yes|예|예|yes|  
|Azure Blob 스토리지에서 데이터 가져오기|yes|예|yes|yes| 
|Azure Blob 스토리지로 데이터 내보내기|yes|예|yes|yes|  
|Azure Data Lake Store에서 데이터 가져오기|예|예|yes|예|    
|Azure Data Lake Store에서 데이터 내보내기|예|예|yes|예|
|Microsoft BI 도구에서 PolyBase 쿼리 실행|yes|예|yes|yes|   

## <a name="pushdown-computation-supported-by-t-sql-operators"></a>T-SQL 연산자가 지원하는 푸시 다운 계산

SQL Server 및 APS에서 모든 T-SQL 운영자가 Hadoop 클러스터로 푸시 다운될 수 있는 것은 아닙니다. 이 테이블에는 지원되는 모든 연산자와 지원되지 않는 연산자의 하위 집합이 나열되어 있습니다. 

||||
|-|-|-| 
|**연산자 유형**|**Hadoop으로 푸시 가능**|**Blob 스토리지로 푸시 가능**|
|열 프로젝션|yes|예|
|조건자|yes|예|
|집계|부분|예|
|외부 테이블 간 조인|예|예|
|외부 테이블과 로컬 테이블 간 조인|예|예|
|정렬|예|예|

부분 집계는 데이터가 SQL Server에 도달한 후에 최종 집계가 이루어져야 함을 의미합니다. 하지만 집계의 일부는 Hadoop에서 발생합니다. 이 방법은 대규모 병렬 처리 시스템에서 집계를 계산하는 데 사용됩니다.  

## <a name="known-limitations"></a>알려진 제한 사항

PolyBase에는 다음과 같은 제한 사항이 있습니다.

- PolyBase를 사용하려면 데이터베이스에 대한 sysadmin 또는 CONTROL SERVER 수준 사용 권한이 있어야 합니다.

- 가변 길이 열의 전체 길이를 포함하는 행의 최대 가능 크기는 SQL Server에서 32KB를 초과하거나, Azure SQL Data Warehouse에서 1MB를 초과할 수 없습니다.

- SQL Server 또는 SQL Data Warehouse에서 ORC 파일 형식으로 데이터를 내보낼 때 텍스트가 많은 열이 제한될 수 있습니다. Java 메모리 부족 오류 메시지로 인해 50개 열로 제한될 수 있습니다. 이 문제를 해결하려면 열의 하위 집합만 내보냅니다.

- Knox가 활성화되어 있으면 PolyBase가 Hortonworks 인스턴스에 연결할 수 없습니다.

- 트랜잭션이 true인 Hive 테이블을 사용하는 경우 PolyBase는 Hive 테이블의 디렉터리에 있는 데이터에 액세스할 수 없습니다.

<!--SQL Server 2016-->
::: moniker range="= sql-server-2016 || =sqlallproducts-allversions"

- [PolyBase는 SQL Server 2016 장애 조치(failover) 클러스터에 노드를 추가하는 경우 설치되지 않습니다](https://support.microsoft.com/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster).

::: moniker-end

## <a name="next-steps"></a>다음 단계

PolyBase에 대한 자세한 내용은 [PolyBase란?](polybase-guide.md)을 참조하세요.

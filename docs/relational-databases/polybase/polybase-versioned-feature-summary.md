---
title: PolyBase 기능 및 제한 사항 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b2d02e13ea7ad1d74274f4412b6ab2bf476f452c
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51665428"
---
# <a name="polybase-features-and-limitations"></a>PolyBase 기능 및 제한 사항

[!INCLUDE[appliesto-ss2016-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

이 문서는 SQL Server 제품 및 서비스에 사용할 수 있는 PolyBase 기능에 대한 요약입니다.  
  
## <a name="feature-summary-for-product-releases"></a>제품 릴리스에 대한 기능 요약

이 표에서는 PolyBase의 주요 기능과 이를 사용할 수 있는 제품이 나열되어 있습니다.  
  
||||||
|-|-|-|-|-|   
|**기능**|**SQL Server 2016**|**Azure SQL Database**|**Azure SQL 데이터 웨어하우스**|**병렬 데이터 웨어하우스**| 
|다음을 사용하여 Hadoop 데이터 쿼리 [!INCLUDE[tsql](../../includes/tsql-md.md)]|예|아니오|아니오|예|
|Hadoop에서 데이터 가져오기|예|아니오|아니오|예|
|Hadoop으로 데이터 내보내기  |예|아니오|아니오| 예|
|Azure HDInsight 쿼리, Azure HDInsight에서 가져오기, Azure HDInsight로 내보내기 |아니오|아니오|아니오|아니오
|Hadoop으로 쿼리 계산 푸시다운|예|아니오|아니오|예|  
|Azure Blob 저장소에서 데이터 가져오기|예|아니오|예|예| 
|Azure Blob 저장소로 데이터 내보내기|예|아니오|예|예|  
|Azure Data Lake Store에서 데이터 가져오기|아니오|아니오|예|아니오|    
|Azure Data Lake Store에서 데이터 내보내기|아니오|아니오|예|아니오|
|Microsoft BI 도구에서 PolyBase 쿼리 실행|예|아니오|예|예|   

## <a name="pushdown-computation-supported-by-t-sql-operators"></a>T-SQL 연산자가 지원하는 푸시 다운 계산

SQL Server 및 APS에서 모든 T-SQL 운영자가 Hadoop 클러스터로 푸시 다운될 수 있는 것은 아닙니다. 이 테이블에는 지원되는 모든 연산자와 지원되지 않는 연산자의 하위 집합이 나열되어 있습니다. 

||||
|-|-|-| 
|**연산자 유형**|**Hadoop으로 푸시 가능**|**Blob 저장소로 푸시 가능**|
|열 프로젝션|예|아니오|
|조건자|예|아니오|
|집계|부분|아니오|
|외부 테이블 간 조인|아니오|아니오|
|외부 테이블과 로컬 테이블 간 조인|아니오|아니오|
|정렬|아니오|아니오|

부분 집계는 데이터가 SQL Server에 도달한 후에 최종 집계가 이루어져야 함을 의미합니다. 하지만 집계의 일부는 Hadoop에서 발생합니다. 이 방법은 대규모 병렬 처리 시스템에서 집계를 계산하는 데 사용됩니다.  

## <a name="known-limitations"></a>알려진 제한 사항

PolyBase에는 다음과 같은 제한 사항이 있습니다.

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

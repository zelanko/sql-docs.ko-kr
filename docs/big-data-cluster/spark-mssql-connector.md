---
title: SQL Server에 Spark 연결
titleSuffix: SQL Server big data clusters
description: Spark에서 MSSQL Spark 커넥터를 사용하여 SQL Server를 읽고 쓰는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7720db661d90c3ff2ebec593b22a5aa638038132
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844224"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-mssql-spark-connector"></a>MSSQL Spark 커넥터를 사용하여 Spark에서 SQL Server를 읽고 쓰는 방법

주요 빅 데이터 사용 패턴은 Spark에서 대량 데이터를 처리한 다음, LOB(기간 업무) 애플리케이션이 액세스할 수 있도록 SQL Server에 데이터를 쓰는 것입니다. 이 사용 패턴은 주요 SQL 최적화를 이용하고 효율적인 쓰기 메커니즘을 제공하는 커넥터를 활용합니다.

이 문서에서는 MSSQL Spark 커넥터를 사용하여 빅 데이터 클러스터 내의 다음 위치를 읽고 쓰는 방법의 예제를 제공합니다.

1. SQL Server 마스터 인스턴스
1. SQL Server 데이터 풀

   ![MSSQL Spark 커넥터 다이어그램](./media/spark-mssql-connector/mssql-spark-connector-diagram.png)

샘플은 다음 작업을 수행합니다.

- HDFS에서 파일을 읽고 몇 가지 기본적인 처리를 수행합니다.
- SQL Server 마스터 인스턴스에 데이터 프레임을 SQL 테이블로 쓴 다음, 이 테이블을 데이터 프레임으로 읽어옵니다.
- SQL Server 데이터 풀에 데이터 프레임을 SQL 외부 테이블로 쓴 다음, 이 외부 테이블을 데이터 프레임으로 읽어옵니다.

## <a name="mssql-spark-connector-interface"></a>MSSQL Spark 커넥터 인터페이스

SQL Server 2019는 Spark에서 SQL로 쓰기 위해 SQL Server 대량 쓰기 API를 사용하는 **MSSQL Spark 커넥터**를 빅 데이터 클러스터에 대해 제공합니다. MSSQL Spark 커넥터는 Spark 데이터 원본 API를 기반으로 하며, 익숙한 Spark JDBC 커넥터 인터페이스를 제공합니다. 인터페이스 매개 변수는 [Apache Spark 설명서](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html)를 참조하세요. MSSQL Spark 커넥터는 **com.microsoft.sqlserver.jdbc.spark**라는 이름으로 참조됩니다.

다음 표에서는 변경되었거나 새로 추가된 인터페이스 매개 변수를 설명합니다.

| 속성 이름 | 선택 사항 | 설명 |
|---|---|---|
| **isolationLevel** | 예 | 연결의 격리 수준을 설명합니다. MSSQL Spark 커넥터의 기본값은 **READ_COMMITTED**입니다. |

이 커넥터는 SQL Server 대량 쓰기 API를 사용합니다. 사용자는 모든 대량 쓰기 매개 변수를 선택적 매개 변수로 전달할 수 있으며, 커넥터는 이 매개 변수를 그대로 기본 API에 전달합니다. 대량 쓰기 작업에 대한 자세한 내용은 [SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 빅 데이터 클러스터](deploy-get-started.md)

- [Azure Data Studio](https://aka.ms/getazuredatastudio)

## <a name="create-the-target-database"></a>대상 데이터베이스 만들기

1. Azure Data Studio를 열고 [빅 데이터 클러스터의 SQL Server 마스터 인스턴스에 연결](connect-to-big-data-cluster.md)합니다.

1. 새 쿼리를 만들고 다음 명령을 실행하여 **MyTestDatabase**라는 샘플 데이터베이스를 만듭니다.

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

## <a name="load-sample-data-into-hdfs"></a>HDFS에 샘플 데이터 로드

1. [AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv)를 로컬 머신으로 다운로드합니다.

1. Azure Data Studio를 시작하고 [빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)합니다.

1. 빅 데이터 클러스터의 HDFS 폴더를 마우스 오른쪽 단추로 클릭하고 **새 디렉터리**를 선택합니다. 디렉터리 이름을 **spark_data**로 지정합니다.

1. **spark_data** 디렉터리를 마우스 오른쪽 단추로 클릭하고 **파일 업로드**를 선택합니다. **AdultCensusIncome.csv** 파일을 업로드합니다.

   ![AdultCensusIncome CSV 파일](./media/spark-mssql-connector/spark_data.png)

## <a name="run-the-sample-notebook"></a>샘플 Notebook 실행

이 데이터와 함께 MSSQL Spark 커넥터를 사용하는 방법을 보여 주기 위해 샘플 Notebook을 다운로드하여 Azure Data Studio에서 열고 각 코드 블록을 실행할 수 있습니다. Notebooks 사용 방법에 대한 자세한 내용은 [SQL Server에서 Notebooks를 사용하는 방법](notebooks-guidance.md)을 참조하세요.

1. PowerShell 또는 bash 명령줄에서 다음 명령을 실행하여 **mssql_spark_connector.ipynb** 샘플 Notebook을 다운로드합니다.

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-virtualization/mssql_spark_connector.ipynb"
   ```

1. Azure Data Studio에서 샘플 Notebook 파일을 엽니다. 빅 데이터 클러스터의 HDFS/Spark 게이트웨이에 연결되어 있는지 확인합니다.

1. 샘플의 각 코드 셀을 실행하여 MSSQL Spark 커넥터 사용법을 확인합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [Kubernetes에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md)을 참조하세요.
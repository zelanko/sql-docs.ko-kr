---
title: SQL Server에 Spark 연결
titleSuffix: SQL Server big data clusters
description: Spark에서 SQL Server에 읽기 및 쓰기를 MSSQL Spark 커넥터를 사용 하는 방법에 알아봅니다.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 878e08426fc58d6ad5a921eff4ac33dca18aa03c
ms.sourcegitcommit: f7ad034f748ebc3e5691a5e4c3eb7490e5cf3ccf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469116"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-mssql-spark-connector"></a>읽기 및 MSSQL Spark 커넥터를 사용 하 여 Spark에서 SQL Server에 기록 하는 방법

키 빅 데이터 사용 패턴은 뒤에 기간 업무 응용 프로그램에 대 한 액세스에 대 한 SQL Server로 데이터를 작성 하 여 Spark에서 대용량 데이터 처리 합니다. 이러한 사용 패턴 주요 SQL 최적화를 활용 하 고 효율적인 쓰기 메커니즘을 제공 하는 커넥터에서 활용 합니다.

이 문서에서는 빅 데이터 클러스터 내에서 다음 위치에 읽기 및 쓰기를 MSSQL Spark 커넥터를 사용 하는 방법의 예로 제공:

1. SQL Server 마스터 인스턴스
1. SQL Server 데이터 풀

   ![MSSQL Spark 커넥터 다이어그램](./media/spark-mssql-connector/mssql-spark-connector-diagram.png)

샘플에는 다음 작업을 수행합니다.

- HDFS에서 파일을 읽고 몇 가지 기본 처리를 수행 합니다.
- 데이터 프레임을 SQL 테이블을 SQL Server 마스터 인스턴스에 쓸 하 한 다음 데이터 프레임에 테이블을 읽습니다.
- SQL 외부 테이블로 SQL Server 데이터 풀에 데이터 프레임을 쓰고 데이터 프레임에 외부 테이블을 읽습니다.

## <a name="mssql-spark-connector-interface"></a>MSSQL Spark 커넥터 인터페이스

SQL Server 2019 미리 보기를 제공 합니다 **MSSQL Spark 커넥터** 빅 데이터에 대 한 SQL Server 대량을 사용 하는 클러스터 Api에 대 한 작성 Spark SQL 쓰기입니다. MSSQL Spark 커넥터는 Api Spark 데이터 원본에 기초 하 고 친숙 한 Spark JDBC 커넥터 인터페이스를 제공 합니다. 인터페이스 매개 변수 참조 [Apache Spark 설명서](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html)합니다. MSSQL Spark 커넥터 이름에서 참조 **com.microsoft.sqlserver.jdbc.spark**합니다.

다음 표에서 변경 되었거나 새 되는 인터페이스 매개 변수를 설명 합니다.

| 속성 이름 | 선택 사항 | Description |
|---|---|---|
| **isolationLevel** | 사용자 계정 컨트롤 | 연결의 격리 수준을 설명합니다. MSSQLSpark 커넥터에 대 한 기본값은 **READ_COMMITTED** |

커넥터는 SQL Server 대량 Api를 작성합니다. 매개 변수는 사용자가 선택적 매개 변수로 전달할 수 및으로 전달 되는 모든 대량 쓰기-커넥터는 기본 API 하는 것입니다. 쓰기 작업 대량에 대 한 자세한 내용은을 참조 하세요 [SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions)합니다.

## <a name="prerequisites"></a>사전 요구 사항

- A [SQL Server 빅 데이터 클러스터](deploy-get-started.md)합니다.

- [Azure Data Studio](https://aka.ms/azdata-insiders).

## <a name="create-the-target-database"></a>대상 데이터베이스 만들기

1. Azure 데이터 Studio를 열고 하 고 [빅 데이터 클러스터의 마스터 SQL Server 인스턴스에 연결할](connect-to-big-data-cluster.md)합니다.

1. 새 쿼리를 만들고 이라는 샘플 데이터베이스를 만들려면 다음 명령을 실행 **MyTestDatabase**합니다.

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

## <a name="load-sample-data-into-hdfs"></a>HDFS에 샘플 데이터 로드

1. 다운로드 [AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv) 로컬 컴퓨터에 있습니다.

1. Azure Data Studio를 시작 하 고 [빅 데이터 클러스터에 연결할](connect-to-big-data-cluster.md)합니다.

1. 빅 데이터 클러스터에서 HDFS 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **새 디렉터리**합니다. 디렉터리의 이름을 **spark_data**합니다.

1. 마우스 오른쪽 단추로 클릭 합니다 **spark_data** 디렉터리에 선택한 **파일을 업로드**합니다. 업로드 합니다 **AdultCensusIncome.csv** 파일입니다.

   ![AdultCensusIncome CSV 파일](./media/spark-mssql-connector/spark_data.png)

## <a name="run-the-sample-notebook"></a>샘플 notebook 실행

이 데이터를 사용 하 여 MSSQL Spark 커넥터 사용을 보여 주기 위해 샘플 노트북을 다운로드, Azure Data Studio에서 엽니다 및 각 코드 블록을 실행할 수 있습니다. Notebook 사용 하 여 작업에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 미리 보기에서 notebook을 사용 하는 방법을](notebooks-guidance.md)합니다.

1. PowerShell 또는 bash 명령줄에서 다운로드 하려면 다음 명령을 실행 합니다 **mssql_spark_connector.ipynb** 샘플 notebook:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-virtualization/mssql_spark_connector.ipynb"
   ```

1. Azure Data Studio에서 샘플 전자 필기장 파일을 엽니다. 빅 데이터 클러스터에 대 한 HDFS/Spark 게이트웨이에 연결 되어 있는지 확인 합니다.

1. MSSQL Spark 커넥터의 사용법을 보려면 예제의 각 코드 셀을 실행 합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [Kubernetes 클러스터로 빅 데이터를 SQL Server를 배포 하는 방법](deployment-guidance.md)
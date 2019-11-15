---
title: 샘플 데이터 로드
titleSuffix: SQL Server big data clusters
description: 이 자습서에서는 SQL Server 빅 데이터 클러스터에 샘플 데이터를 로드하는 방법을 보여 줍니다. 샘플 데이터에는 SQL Server 마스터 인스턴스의 관계형 데이터가 포함되어 있습니다. 스토리지 풀의 HDFS 데이터도 포함합니다. 이 데이터는 이 섹션의 다른 자습서를 지원합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 405df2c66917dc5e5b350aaaa0769bede6ccf6c9
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653283"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-big-data-cluster"></a>자습서: SQL Server 빅 데이터 클러스터에 샘플 데이터 로드

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 스크립트를 사용하여 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]에 샘플 데이터를 로드하는 방법을 설명합니다. 설명서의 다른 자습서는 대부분은 이 샘플 데이터를 사용합니다.

> [!TIP]
> [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster) GitHub 리포지토리에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 추가 샘플을 찾을 수 있습니다. 샘플은 **sql-server-samples/samples/features/sql-big-data-cluster/** 경로에 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

- [배포된 빅 데이터 클러스터](deployment-guidance.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
   - **azdata**
   - **kubectl**
   - **sqlcmd**
   - **curl**
 
## <a id="sampledata"></a> 샘플 데이터 로드

다음 단계에서는 부트스트랩 스크립트를 사용하여 SQL Server 데이터베이스 백업을 다운로드하고 빅 데이터 클러스터에 데이터를 로드합니다. 이러한 단계는 간편하게 [Windows](#windows) 및 [Linux](#linux) 섹션으로 구분되어 있습니다.

## <a id="windows"></a> Windows

다음 단계에서는 Windows 클라이언트를 사용하여 빅 데이터 클러스터에 샘플 데이터를 로드하는 방법을 설명합니다.

1. 새 Windows 명령 프롬프트를 엽니다.

   > [!IMPORTANT]
   > Windows PowerShell에서 이 단계를 수행하면 안 됩니다. PowerShell에서는 스크립트가 PowerShell 버전의 **curl**을 사용하기 때문에 오류가 발생합니다.

1. **curl**을 사용하여 샘플 데이터의 부트스트랩 스크립트를 다운로드합니다.

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. **bootstrap-sample-db.sql** Transact-SQL 스크립트를 다운로드합니다. 이 스크립트는 부트스트랩 스크립트에서 호출됩니다.

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 부트스트랩 스크립트에는 빅 데이터 클러스터에 대한 다음과 같은 위치 매개 변수가 필요합니다.

   | 매개 변수 | 설명 |
   |---|---|
   | <CLUSTER_NAMESPACE> | 빅 데이터 클러스터에 지정한 이름입니다. |
   | <SQL_MASTER_IP> | 마스터 인스턴스의 IP 주소입니다. |
   | <SQL_MASTER_SA_PASSWORD> | 마스터 인스턴스의 SA 암호입니다. |
   | <KNOX_IP> | HDFS/Spark 게이트웨이의 IP 주소입니다. |
   | <KNOX_PASSWORD> | HDFS/Spark 게이트웨이의 암호입니다. |

   > [!TIP]
   > [kubectl](cluster-troubleshooting-commands.md)을 사용하여 SQL Server 마스터 인스턴스 및 Knox의 IP 주소를 찾습니다. `kubectl get svc -n <your-big-data-cluster-name>`을 실행하고 마스터 인스턴스(**master-svc-external**) 및 Knox(**gateway-svc-external**)의 EXTERNAL-IP 주소를 확인합니다. 클러스터의 기본 이름은 **mssql-cluster**입니다.

1. 부트스트랩 스크립트를 실행합니다.

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

다음 단계에서는 Linux 클라이언트를 사용하여 빅 데이터 클러스터에 샘플 데이터를 로드하는 방법을 설명합니다.

1. 부트스트랩 스크립트를 다운로드하고 이 스크립트에 실행 파일 권한을 할당합니다.

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. **bootstrap-sample-db.sql** Transact-SQL 스크립트를 다운로드합니다. 이 스크립트는 부트스트랩 스크립트에서 호출됩니다.

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 부트스트랩 스크립트에는 빅 데이터 클러스터에 대한 다음과 같은 위치 매개 변수가 필요합니다.

   | 매개 변수 | 설명 |
   |---|---|
   | <CLUSTER_NAMESPACE> | 빅 데이터 클러스터에 지정한 이름입니다. |
   | <SQL_MASTER_IP> | 마스터 인스턴스의 IP 주소입니다. |
   | <SQL_MASTER_SA_PASSWORD> | 마스터 인스턴스의 SA 암호입니다. |
   | <KNOX_IP> | HDFS/Spark 게이트웨이의 IP 주소입니다. |
   | <KNOX_PASSWORD> | HDFS/Spark 게이트웨이의 암호입니다. |

   > [!TIP]
   > [kubectl](cluster-troubleshooting-commands.md)을 사용하여 SQL Server 마스터 인스턴스 및 Knox의 IP 주소를 찾습니다. `kubectl get svc -n <your-big-data-cluster-name>`을 실행하고 마스터 인스턴스(**master-svc-external**) 및 Knox(**gateway-svc-external**)의 EXTERNAL-IP 주소를 확인합니다. 클러스터의 기본 이름은 **mssql-cluster**입니다.

1. 부트스트랩 스크립트를 실행합니다.

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>다음 단계

부트스트랩 스크립트 실행이 완료되면 빅 데이터 클러스터에 샘플 데이터베이스와 HDFS 데이터가 있습니다. 다음 자습서에서는 샘플 데이터를 사용하여 빅 데이터 클러스터 기능을 보여 줍니다.

데이터 가상화:

- [자습서: SQL Server 빅 데이터 클러스터의 HDFS 쿼리](tutorial-query-hdfs-storage-pool.md)
- [자습서: SQL Server 빅 데이터 클러스터의 Oracle 쿼리](tutorial-query-oracle.md)

데이터 수집:

- [자습서: Transact-SQL을 사용하여 SQL Server 데이터 풀로 데이터 수집](tutorial-data-pool-ingest-sql.md)
- [자습서: Spark 작업을 사용하여 SQL Server 데이터 풀로 데이터 수집](tutorial-data-pool-ingest-spark.md)

Notebook:

- [자습서: SQL Server 2019 빅 데이터 클러스터에서 샘플 Notebook 실행](tutorial-notebook-spark.md)

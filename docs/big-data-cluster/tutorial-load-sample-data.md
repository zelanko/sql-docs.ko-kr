---
title: 샘플 데이터 로드
titleSuffix: SQL Server big data clusters
description: 이 자습서에서는 SQL Server 빅 데이터 클러스터에 샘플 데이터를 로드 하는 방법을 보여 줍니다. 샘플 데이터에는 SQL Server 마스터 인스턴스의 관계형 데이터가 포함 되어 있습니다. 저장소 풀에 HDFS 데이터도 포함 됩니다. 이 데이터는이 섹션의 다른 자습서를 지원 합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5b35eccece4df47cb483932386cf6a38e45d2dc8
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419281"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-big-data-cluster"></a>자습서: SQL Server 빅 데이터 클러스터에 샘플 데이터 로드

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 스크립트를 사용 하 여 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 샘플 데이터를 로드 하는 방법을 설명 합니다. 설명서의 다른 자습서 대부분은이 샘플 데이터를 사용 합니다.

> [!TIP]
> SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 대 한 추가 샘플은 [SQL Server 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster) GitHub 리포지토리에서 찾을 수 있습니다. 이러한 **서버는 sql server-samples/samples/features/sql-빅-데이터-클러스터/** 경로에 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

- [배포 된 빅 데이터 클러스터](deployment-guidance.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
   - **azdata**
   - **kubectl**
   - **sqlcmd**
   - **curl**

## <a id="sampledata"></a>샘플 데이터 로드

다음 단계에서는 부트스트랩 스크립트를 사용 하 여 SQL Server 데이터베이스 백업을 다운로드 하 고 빅 데이터 클러스터에 데이터를 로드 합니다. 사용 편의성을 위해 이러한 단계는 [Windows](#windows) 및 [Linux](#linux) 섹션으로 구분 되었습니다.

## <a id="windows"></a> Windows

다음 단계에서는 Windows 클라이언트를 사용 하 여 빅 데이터 클러스터에 샘플 데이터를 로드 하는 방법을 설명 합니다.

1. 새 Windows 명령 프롬프트를 엽니다.

   > [!IMPORTANT]
   > 이러한 단계에서는 Windows PowerShell을 사용 하지 마십시오. PowerShell에서 스크립트는 PowerShell 버전의 **말아**를 사용 하므로 오류가 발생 합니다.

1. 샘플링 **을 사용 하** 여 샘플 데이터에 대 한 부트스트랩 스크립트를 다운로드 합니다.

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. **Bootstrap-sample-db** 스크립트를 다운로드 합니다. 이 스크립트는 부트스트랩 스크립트에 의해 호출 됩니다.

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 부트스트랩 스크립트에는 빅 데이터 클러스터에 대해 다음과 같은 위치 매개 변수가 필요 합니다.

   | 매개 변수 | 설명 |
   |---|---|
   | <CLUSTER_NAMESPACE> | 빅 데이터 클러스터에 제공한 이름입니다. |
   | <SQL_MASTER_IP> | 마스터 인스턴스의 IP 주소입니다. |
   | <SQL_MASTER_SA_PASSWORD> | 마스터 인스턴스의 SA 암호입니다. |
   | <KNOX_IP> | HDFS/Spark 게이트웨이의 IP 주소입니다. |
   | < KNOX_PASSWORD > | HDFS/Spark 게이트웨이의 암호입니다. |

   > [!TIP]
   > [Kubectl](cluster-troubleshooting-commands.md) 를 사용 하 여 SQL Server 마스터 인스턴스 및 Knox에 대 한 IP 주소를 찾습니다. 를 `kubectl get svc -n <your-big-data-cluster-name>` 실행 하 고 마스터 인스턴스 (**마스터-외부**) 및 Knox (**게이트웨이-외부**)에 대 한 외부 IP 주소를 확인 합니다. 클러스터의 기본 이름은 **mssql-cluster**입니다.

1. 부트스트랩 스크립트를 실행 합니다.

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

다음 단계에서는 Linux 클라이언트를 사용 하 여 빅 데이터 클러스터에 샘플 데이터를 로드 하는 방법을 설명 합니다.

1. 부트스트랩 스크립트를 다운로드 하 고이 스크립트에 실행 파일 사용 권한을 할당 합니다.

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. **Bootstrap-sample-db** 스크립트를 다운로드 합니다. 이 스크립트는 부트스트랩 스크립트에 의해 호출 됩니다.

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 부트스트랩 스크립트에는 빅 데이터 클러스터에 대해 다음과 같은 위치 매개 변수가 필요 합니다.

   | 매개 변수 | 설명 |
   |---|---|
   | <CLUSTER_NAMESPACE> | 빅 데이터 클러스터에 제공한 이름입니다. |
   | <SQL_MASTER_IP> | 마스터 인스턴스의 IP 주소입니다. |
   | <SQL_MASTER_SA_PASSWORD> | 마스터 인스턴스의 SA 암호입니다. |
   | <KNOX_IP> | HDFS/Spark 게이트웨이의 IP 주소입니다. |
   | < KNOX_PASSWORD > | HDFS/Spark 게이트웨이의 암호입니다. |

   > [!TIP]
   > [Kubectl](cluster-troubleshooting-commands.md) 를 사용 하 여 SQL Server 마스터 인스턴스 및 Knox에 대 한 IP 주소를 찾습니다. 를 `kubectl get svc -n <your-big-data-cluster-name>` 실행 하 고 마스터 인스턴스 (**마스터-외부**) 및 Knox (**게이트웨이-외부**)에 대 한 외부 IP 주소를 확인 합니다. 클러스터의 기본 이름은 **mssql-cluster**입니다.

1. 부트스트랩 스크립트를 실행 합니다.

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>다음 단계

부트스트랩 스크립트가 실행 된 후에는 빅 데이터 클러스터에 샘플 데이터베이스 및 HDFS 데이터가 있습니다. 다음 자습서에서는 샘플 데이터를 사용 하 여 빅 데이터 클러스터 기능을 보여 줍니다.

데이터 가상화:

- [자습서: SQL Server 빅 데이터 클러스터의 HDFS 쿼리](tutorial-query-hdfs-storage-pool.md)
- [자습서: SQL Server 빅 데이터 클러스터에서 Oracle 쿼리](tutorial-query-oracle.md)

데이터 수집:

- [자습서: Transact-sql을 사용 하 여 SQL Server 데이터 풀로 데이터 수집](tutorial-data-pool-ingest-sql.md)
- [자습서: Spark 작업을 사용 하 여 SQL Server 데이터 풀로 데이터 수집](tutorial-data-pool-ingest-spark.md)

전자

- [자습서: SQL Server 2019 빅 데이터 클러스터에서 샘플 노트북 실행](tutorial-notebook-spark.md)
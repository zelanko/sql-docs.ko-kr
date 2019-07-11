---
title: 샘플 데이터 로드
titleSuffix: SQL Server big data clusters
description: 이 자습서에는 SQL Server 빅 데이터 클러스터에 샘플 데이터를 로드 하는 방법을 보여 줍니다. 샘플 데이터를 SQL Server 마스터 인스턴스에 관계형 데이터를 포함합니다. 저장소 풀의 HDFS 데이터도 포함 합니다. 이 데이터는이 단원의 다른 자습서를 지원합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 04/23/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f4ea5540c0188ec9a57ad8b6780cf3ab6af5dfc2
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727350"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-big-data-cluster"></a>자습서: SQL Server 빅 데이터 클러스터에 샘플 데이터 로드

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서는 스크립트를 사용 하 여 SQL Server 2019 빅 데이터 클러스터 (미리 보기)로 샘플 데이터를 로드 하는 방법에 설명 합니다. 설명서의 자습서에서는 다른 많은이 샘플 데이터를 사용합니다.

> [!TIP]
> SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 대 한 추가 샘플을 찾을 수 있습니다 합니다 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster) GitHub 리포지토리. 에 위치 합니다 **sql-server-samples/samples/features/sql-big-data-cluster/** 경로입니다.

## <a name="prerequisites"></a>사전 요구 사항

- [배포 된 빅 데이터 클러스터](deployment-guidance.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
   - **mssqlctl**
   - **kubectl**
   - **sqlcmd**
   - **curl**

## <a id="sampledata"></a> 샘플 데이터 로드

다음 단계를 부트스트랩 스크립트를 사용 하 여 SQL Server 데이터베이스 백업 다운로드 및 빅 데이터 클러스터에 데이터를 로드 합니다. 사용 편의성을 위해 이러한 단계는 스페이스로 세분화 했습니다 [Windows](#windows) 하 고 [Linux](#linux) 섹션입니다.

## <a id="windows"></a> Windows

다음 단계를 Windows 클라이언트를 사용 하 여 빅 데이터 클러스터에 샘플 데이터를 로드 하는 방법에 설명 합니다.

1. 새 Windows 명령 프롬프트를 엽니다.

   > [!IMPORTANT]
   > 다음이 단계에 대 한 Windows PowerShell을 사용 하지 마세요. PowerShell에서 스크립트 실패의 PowerShell 버전을 사용할지 **curl**합니다.

1. 사용 하 여 **curl** 샘플 데이터에 대 한 부트스트랩 스크립트를 다운로드 합니다.

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. 다운로드 합니다 **부트스트랩-샘플-db.sql** Transact SQL 스크립트. 이 스크립트는 부트스트랩 스크립트에 의해 호출 됩니다.

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 부트스트랩 스크립트 빅 데이터 클러스터에 대해 다음 위치 매개 변수를 사용 하려면:

   | 매개 변수 | 설명 |
   |---|---|
   | <CLUSTER_NAMESPACE> | 빅 데이터 클러스터에 제공한 이름입니다. |
   | <SQL_MASTER_IP> | 마스터 인스턴스 IP 주소입니다. |
   | <SQL_MASTER_SA_PASSWORD> | 마스터 인스턴스에 대 한 SA 암호입니다. |
   | <KNOX_IP> | HDFS/Spark 게이트웨이의 IP 주소입니다. |
   | <KNOX_PASSWORD> | HDFS/Spark 게이트웨이에 대 한 암호입니다. |

   > [!TIP]
   > 사용 하 여 [kubectl](cluster-troubleshooting-commands.md) SQL Server 마스터 인스턴스와 Knox에 대 한 IP 주소를 찾을 수 있습니다. 실행할 `kubectl get svc -n <your-big-data-cluster-name>` 마스터 인스턴스에 대 한 외부 IP 주소를 확인 하 고 (**마스터 svc 외부**) 및 Knox (**게이트웨이 svc 외부**). 클러스터의 기본 이름은 **mssql 클러스터**합니다.

1. 부트스트랩 스크립트를 실행 합니다.

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

다음 단계는 Linux 클라이언트를 사용 하 여 빅 데이터 클러스터에 샘플 데이터를 로드 하는 방법에 설명 합니다.

1. 부트스트랩 스크립트를 다운로드 하 고 해당 실행 권한을 할당 합니다.

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. 다운로드 합니다 **부트스트랩-샘플-db.sql** Transact SQL 스크립트. 이 스크립트는 부트스트랩 스크립트에 의해 호출 됩니다.

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 부트스트랩 스크립트 빅 데이터 클러스터에 대해 다음 위치 매개 변수를 사용 하려면:

   | 매개 변수 | 설명 |
   |---|---|
   | <CLUSTER_NAMESPACE> | 빅 데이터 클러스터에 제공한 이름입니다. |
   | <SQL_MASTER_IP> | 마스터 인스턴스 IP 주소입니다. |
   | <SQL_MASTER_SA_PASSWORD> | 마스터 인스턴스에 대 한 SA 암호입니다. |
   | <KNOX_IP> | HDFS/Spark 게이트웨이의 IP 주소입니다. |
   | <KNOX_PASSWORD> | HDFS/Spark 게이트웨이에 대 한 암호입니다. |

   > [!TIP]
   > 사용 하 여 [kubectl](cluster-troubleshooting-commands.md) SQL Server 마스터 인스턴스와 Knox에 대 한 IP 주소를 찾을 수 있습니다. 실행할 `kubectl get svc -n <your-big-data-cluster-name>` 마스터 인스턴스에 대 한 외부 IP 주소를 확인 하 고 (**마스터 svc 외부**) 및 Knox (**게이트웨이 svc 외부**). 클러스터의 기본 이름은 **mssql 클러스터**합니다.

1. 부트스트랩 스크립트를 실행 합니다.

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>다음 단계

부트스트랩 스크립트를 실행 한 후 예제 데이터베이스 및 HDFS 데이터를 빅 데이터 클러스터에 있습니다. 다음 자습서는 빅 데이터 클러스터 기능을 보여 주기 위해 샘플 데이터를 사용 합니다.

데이터 가상화:

- [자습서: SQL Server 빅 데이터 클러스터에서 HDFS 쿼리](tutorial-query-hdfs-storage-pool.md)
- [자습서: SQL Server 빅 데이터 클러스터에서 Oracle 쿼리](tutorial-query-oracle.md)

데이터 수집:

- [자습서: TRANSACT-SQL을 사용 하 여 SQL Server 데이터 풀에 데이터를 수집 합니다.](tutorial-data-pool-ingest-sql.md)
- [자습서: Spark 작업을 사용 하 여 SQL Server 데이터 풀에 데이터를 수집 합니다.](tutorial-data-pool-ingest-spark.md)

Notebook:

- [자습서: SQL Server 2019 빅 데이터 클러스터에는 샘플 notebook을 실행 합니다.](tutorial-notebook-spark.md)
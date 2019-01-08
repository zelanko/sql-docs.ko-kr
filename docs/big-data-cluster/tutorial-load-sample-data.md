---
title: 샘플 데이터 로드
titleSuffix: SQL Server 2019 big data clusters
description: 이 자습서에는 SQL Server 빅 데이터 클러스터에 샘플 데이터를 로드 하는 방법을 보여 줍니다. 샘플 데이터를 SQL Server 마스터 인스턴스에 관계형 데이터를 포함합니다. 저장소 풀의 HDFS 데이터도 포함 합니다. 이 데이터는이 단원의 다른 자습서를 지원합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/13/2018
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: 67e97774a00fed123ba6733688e002f1b57ba743
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53439390"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-2019-big-data-cluster"></a>자습서: SQL Server 2019 빅 데이터 클러스터에 샘플 데이터 로드

이 자습서는 스크립트를 사용 하 여 SQL Server 2019 빅 데이터 클러스터 (미리 보기)로 샘플 데이터를 로드 하는 방법에 설명 합니다. 설명서의 자습서에서는 다른 많은이 샘플 데이터를 사용합니다.

> [!TIP]
> SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 대 한 추가 샘플을 찾을 수 있습니다 합니다 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster) GitHub 리포지토리. 에 위치 합니다 **sql-server-samples/samples/features/sql-big-data-cluster/** 경로입니다.

## <a name="prerequisites"></a>사전 요구 사항

- [배포 된 빅 데이터 클러스터](deployment-guidance.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
   - **mssqlctl**
   - **Kubectl**
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

   | 매개 변수 | Description |
   |---|---|
   | &LT; CLUSTER_NAMESPACE &GT; | 빅 데이터 클러스터에 제공한 이름입니다. |
   | &LT; SQL_MASTER_IP &GT; | 마스터 인스턴스 IP 주소입니다. |
   | &LT; SQL_MASTER_SA_PASSWORD &GT; | 마스터 인스턴스에 대 한 SA 암호입니다. |
   | &LT; KNOX_IP &GT; | HDFS/Spark 게이트웨이의 IP 주소입니다. |
   | &LT; KNOX_PASSWORD &GT; | HDFS/Spark 게이트웨이에 대 한 암호입니다. |

   > [!TIP]
   > 사용 하 여 [kubectl](cluster-troubleshooting-commands.md) SQL Server 마스터 인스턴스와 Knox에 대 한 IP 주소를 찾을 수 있습니다. 실행할 `kubectl get svc -n <your-cluster-name>` 마스터 인스턴스에 대 한 외부 IP 주소를 확인 하 고 (**끝점 마스터 풀**) 및 Knox (**서비스-보안-lb** 또는 **서비스-보안-nodeport**).

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

   | 매개 변수 | Description |
   |---|---|
   | &LT; CLUSTER_NAMESPACE &GT; | 빅 데이터 클러스터에 제공한 이름입니다. |
   | &LT; SQL_MASTER_IP &GT; | 마스터 인스턴스 IP 주소입니다. |
   | &LT; SQL_MASTER_SA_PASSWORD &GT; | 마스터 인스턴스에 대 한 SA 암호입니다. |
   | &LT; KNOX_IP &GT; | HDFS/Spark 게이트웨이의 IP 주소입니다. |
   | &LT; KNOX_PASSWORD &GT; | HDFS/Spark 게이트웨이에 대 한 암호입니다. |

   > [!TIP]
   > 사용 하 여 [kubectl](cluster-troubleshooting-commands.md) SQL Server 마스터 인스턴스와 Knox에 대 한 IP 주소를 찾을 수 있습니다. 실행할 `kubectl get svc -n <your-cluster-name>` 마스터 인스턴스에 대 한 외부 IP 주소를 확인 하 고 (**끝점 마스터 풀**) 및 Knox (**서비스-보안-lb** 또는 **서비스-보안-nodeport**).

1. 부트스트랩 스크립트를 실행 합니다.

   ```bash
   ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>다음 단계

부트스트랩 스크립트를 실행 한 후 예제 데이터베이스 및 HDFS 데이터를 빅 데이터 클러스터에 있습니다. 이 데이터 및 빅 데이터 클러스터를 탐색 하려면 참조는 [자습서](tutorial-query-hdfs-storage-pool.md) 이 단원의 합니다.
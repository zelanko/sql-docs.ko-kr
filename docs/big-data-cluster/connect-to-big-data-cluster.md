---
title: 마스터에 연결 하 고 HDFS
titleSuffix: SQL Server 2019 big data clusters
description: SQL Server 마스터 인스턴스와 SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 위한 HDFS/Spark 게이트웨이 연결 하는 방법에 알아봅니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/10/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 4d3ca6a3e43781b35bfd24f04ee1cf0483b1eb05
ms.sourcegitcommit: 1f53b6a536ccffd701fc87e658ddac714f6da7a2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/10/2019
ms.locfileid: "54206269"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Azure Data Studio를 사용 하 여 SQL Server 빅 데이터 클러스터에 연결

이 문서에서는 Azure Data Studio에서 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 연결 하는 방법을 설명 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- 배포 된 [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)합니다.
- [SQL Server 2019 빅 데이터 도구도](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
   - **Kubectl**

## <a name="connect-to-the-cluster"></a>클러스터에 연결

빅 데이터 클러스터에 연결할 때 SQL Server 마스터 인스턴스 또는 HDFS/Spark 게이트웨이에 연결할 수가 있습니다. 다음 섹션에서는 각각에 연결 하는 방법을 보여 줍니다.

## <a id="master"></a> 마스터 인스턴스

SQL Server 마스터 인스턴스는 관계형 SQL Server 데이터베이스가 포함 된 기존 SQL Server 인스턴스입니다. 다음 단계를 사용 하 여 Azure Data Studio 마스터 인스턴스에 연결 하는 방법에 설명 합니다.

1. 명령줄에서 다음 명령 사용 하 여 마스터 인스턴스 IP를 찾습니다.

   ```
   kubectl get svc endpoint-master-pool -n <your-cluster-name>
   ```

1. Azure Data Studio 눌러 **F1** > **새 연결**합니다.

1. **연결 유형**를 선택 **Microsoft SQL Server**합니다.

1. SQL Server 마스터 인스턴스의 IP 주소를 입력 **서버 이름** (예: **\<IP 주소\>31433,**).

1. SQL 로그인을 입력 **사용자 이름** 하 고 **암호**합니다.

   > [!TIP]
   > 기본적으로 사용자 이름이 **SA** 템플릿이며, 변경 하지 않는 한 암호를 **MSSQL_SA_PASSWORD** 배포 중에 사용 되는 환경 변수입니다.

1. 대상 변경 **데이터베이스 이름** 관계형 데이터베이스 중 하나에 있습니다.

   ![마스터 인스턴스에 연결](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. 키를 눌러 **Connect**, 및 **Server 대시보드** 표시 되어야 합니다.

## <a id="hdfs"></a> HDFS/Spark 게이트웨이

합니다 **HDFS/Spark 게이트웨이** Spark 작업을 실행 하는 HDFS 저장소 풀을 사용 하려면 연결할 수 있습니다. 다음 단계에서는 Azure Data Studio를 사용 하 여 연결 하는 방법에 설명 합니다.

1. 명령줄에서 다음 명령 중 하나를 사용 하 여 HDFS/Spark 게이트웨이의 IP 주소를 찾습니다.
   
   **AKS 배포:**

   ```
   kubectl get svc service-security-lb -n <your-cluster-name>
   ```

   **비-AKS 배포**:

   ```
   kubectl get svc service-security-nodeport -n <your-cluster-name>
   ```
 
1. Azure Data Studio 눌러 **F1** > **새 연결**합니다.

1. **연결 유형**를 선택 **SQL Server 빅 데이터 클러스터**합니다.

   > [!TIP]
   > 표시 되지 않으면를 **SQL Server 빅 데이터 클러스터** 연결 입력, 설치 했는지 확인 합니다 [SQL Server 2019 확장](../azure-data-studio/sql-server-2019-extension.md) 확장 완료 한 후 다시 시작 하면 Azure Data Studio 및 설치 합니다.

1. 빅 데이터 클러스터의 IP 주소를 입력 **서버 이름** (포트를 지정 하지 않으면).

1. 입력 `root` 에 대 한는 **사용자** 지정 합니다 **암호** 빅 데이터 클러스터에 있습니다.

   ![HDFS/Spark 게이트웨이에 연결](./media/connect-to-big-data-cluster/connect-to-cluster-hdfs-spark.png)

   > [!TIP]
   > 기본적으로 사용자 이름이 **루트** 암호에 해당 합니다 **KNOX_PASSWORD** 배포 중에 사용 되는 환경 변수입니다.

1. 키를 눌러 **Connect**, 및 **Server 대시보드** 표시 되어야 합니다.

## <a name="next-steps"></a>다음 단계

SQL Server 2019 빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 빅 데이터 클러스터 이란](big-data-cluster-overview.md)합니다.
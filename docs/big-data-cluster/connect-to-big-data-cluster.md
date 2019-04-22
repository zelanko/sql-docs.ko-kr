---
title: 마스터에 연결 하 고 HDFS
titleSuffix: SQL Server big data clusters
description: SQL Server 마스터 인스턴스와 SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 위한 HDFS/Spark 게이트웨이 연결 하는 방법에 알아봅니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ed563fe6d0bfd69ce5dfb7484d4213bc9a47dd54
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860174"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Azure Data Studio를 사용 하 여 SQL Server 빅 데이터 클러스터에 연결

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 Azure Data Studio에서 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 연결 하는 방법을 설명 합니다. 빅 데이터 클러스터와 상호 작용 하는 데 사용 되는 기본 끝점을 두 가지가 있습니다.

| 엔드포인트 | Description |
|---|---|
| SQL Server 마스터 인스턴스 | 관계형 SQL Server 데이터베이스를 포함 하는 클러스터에서 SQL Server 마스터 인스턴스. |
| HDFS/Spark 게이트웨이 | Spark 작업을 실행 하는 기능과 클러스터에 HDFS 저장소에 액세스 합니다. |

> [!TIP]
> Azure Data Studio는 2019 년 2 월 릴리스를 자동으로 SQL Server 마스터 인스턴스에 연결할 HDFS/Spark 게이트웨이에 UI 액세스를 제공 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- 배포 된 [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)합니다.
- [SQL Server 2019 빅 데이터 도구도](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
   - **kubectl**

## <a id="master"></a> 클러스터에 연결

Azure Data Studio를 사용 하 여 빅 데이터 클러스터에 연결 하려면 클러스터의 마스터 SQL Server 인스턴스에 새 연결을 설정 합니다. 다음 단계를 사용 하 여 Azure Data Studio 마스터 인스턴스에 연결 하는 방법에 설명 합니다.

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

Azure Data Studio 2019 년 2 월 릴리스의 SQL Server 마스터 인스턴스에 연결할 있습니다 HDFS/Spark 게이트웨이와 상호 작용할 수 있습니다. 즉, HDFS 및 다음 섹션에서 설명 하는 Spark에 대 한 별도 연결을 사용할 필요가 없습니다.

- 개체 탐색기는 이제 새 포함 **Data Services** 노드를 마우스 오른쪽 단추 클릭 새 노트북을 만들거나 spark 작업을 제출 하는 빅 데이터 클러스터 작업을 지원 합니다. 
- 합니다 **Data Services** 포함는 **HDFS** HDFS 탐색 및 Notebook에서 외부 테이블 만들기 또는 분석 등의 작업 수행에 대 한 폴더입니다.
- **서버 대시보드** 에 연결에 대 한 탭에도 포함 되어 있습니다 **SQL Server 빅 데이터 클러스터** 하 고 **SQL Server 2019 (미리 보기)** 확장이 설치 되는 경우.

   ![Azure Data Studio 데이터 서비스 노드](./media/connect-to-big-data-cluster/connect-data-services-node.png)

> [!IMPORTANT]
> 표시 되 면 **알 수 없는 오류가** ui에서 해야 할 수 있습니다 [HDFS/Spark 게이트웨이에 직접 연결할](#hdfs)합니다. 이 오류에 대 한 한 가지 원인은 SQL Server 마스터 인스턴스 및 HDFS/Spark 게이트웨이에 대 한 서로 다른 암호를 Azure Data Studio 동일한 암호를 둘 다에 사용 되는 것을 가정 합니다.
  
## <a id="hdfs"></a> HDFS/Spark 게이트웨이에 연결

대부분의 경우에서 SQL Server 마스터 인스턴스에 연결할에 액세스할 수는 HDFS 및 Spark 에서도 통해 합니다 **Data Services** 노드. 그러나 전용된 연결을 여전히 만들 수는 **HDFS/Spark 게이트웨이** 필요한 경우. 다음 단계에서는 Azure Data Studio를 사용 하 여 연결 하는 방법에 설명 합니다.

1. 명령줄에서 다음 명령 중 하나를 사용 하 여 HDFS/Spark 게이트웨이의 IP 주소를 찾습니다.

   ```
   kubectl get svc endpoint-security -n <your-cluster-name>
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
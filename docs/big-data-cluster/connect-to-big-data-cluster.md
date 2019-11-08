---
title: 마스터 및 HDFS에 연결 빅 데이터 클러스터
description: '[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 HDFS/Spark 게이트웨이 및 SQL Server 마스터 인스턴스에 연결하는 방법을 알아봅니다.'
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0717226ee785df568d4cea75511e65acb728c592
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532236"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Azure Data Studio를 사용하여 SQL Server 빅 데이터 클러스터에 연결

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 Azure Data Studio에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]에 연결하는 방법을 설명합니다.

## <a name="prerequisites"></a>사전 요구 사항

- 배포된 [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)
- [SQL Server 2019 빅 데이터 도구](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
   - **kubectl**
   - **azdata**

## <a id="master"></a> 클러스터에 연결

Azure Data Studio를 사용하여 빅 데이터 클러스터에 연결하려면 클러스터의 SQL Server 마스터 인스턴스에 대한 새 연결을 설정합니다. 다음 단계에서는 Azure Data Studio를 사용하여 마스터 인스턴스에 연결하는 방법을 설명합니다.

1. SQL Server 마스터 인스턴스 엔드포인트 찾기:

   ```
   azdata bdc endpoint list -e sql-server-master
   ```

   > [!TIP]
   > 엔드포인트를 검색하는 방법에 대한 자세한 내용은 [엔드포인트 검색](deployment-guidance.md#endpoints)을 참조하세요.

1. Azure Data Studio에서 **F1** > **새 연결**을 누릅니다.

1. **연결 형식**에서 **Microsoft SQL Server**를 선택합니다.

1. SQL Server 마스터 인스턴스에서 찾은 엔드포인트 이름을 **서버 이름** 텍스트 상자에 입력합니다(예: **\<IP_Address\>,31433**). 

1. 인증 유형을 선택합니다. 빅 데이터 클러스터에서 실행되는 SQL Server 마스터 인스턴스의 경우 **Windows 인증** 및 **SQL 로그인**만 지원됩니다. 

1. SQL 로그인 **사용자 이름** 및 **암호**를 입력합니다. Windows 인증을 사용하는 경우에는 이 작업이 필요하지 않습니다.

   > [!TIP]
   > 기본적으로, 빅 데이터 클러스터 배포 중에는 사용자 이름 **SA**를 사용할 수 없습니다. 배포 시 사용된 **AZDATA_USERNAME** 환경 변수에 해당하는 이름과 **AZDATA_PASSWORD** 환경 변수에 해당하는 암호를 사용하여 새 sysadmin 사용자가 배포 중에 프로비저닝됩니다.

1. 대상 **데이터베이스 이름**을 관계형 데이터베이스 중 하나로 변경합니다.

   ![마스터 인스턴스에 연결](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. **연결**을 누르면 **서버 대시보드**가 표시됩니다.

Azure Data Studio 2019년 2월 릴리스에서는 SQL Server 마스터 인스턴스에 연결할 경우 HDFS/Spark 게이트웨이도 조작할 수 있습니다. 즉, 다음 섹션에서 설명하는 것처럼 HDFS 및 Spark에 대해 별도의 연결을 사용할 필요가 없습니다.

- 이제 개체 탐색기에 새 Notebook 만들기, spark 작업 제출 등의 빅 데이터 클러스터 작업을 위한 마우스 오른쪽 단추 클릭 메뉴를 지원하는 새 **Data Services** 노드가 포함되었습니다. 
- **Data Services** 노드에는 HDFS 탐색과 외부 테이블 만들기, Notebook에서 분석 등의 작업을 수행하기 위한 **HDFS** 폴더도 있습니다.
- 확장이 설치된 경우 연결의 **서버 대시보드**에 **SQL Server 빅 데이터 클러스터** 및 **SQL Server 2019(미리 보기)** 탭도 포함됩니다.

   ![Azure Data Studio Data Services 노드](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요](big-data-cluster-overview.md)를 참조하세요.

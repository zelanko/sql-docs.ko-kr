---
title: 'Spark 작업 제출: Azure Data Studio'
titleSuffix: SQL Server Big Data Clusters
description: Azure Data Studio에서 SQL Server 빅 데이터 클러스터에 대한 Spark 작업을 제출합니다.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 13510f430c11253a569540e02dc83d3b8b3ca113
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606745"
---
# <a name="submit-spark-jobs-on-big-data-clusters-2019-in-azure-data-studio"></a>Azure Data Studio에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 Spark 작업 제출

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

빅 데이터 클러스터의 주요 시나리오 중 하나는 SQL Server에 대한 Spark 작업을 제출하는 기능입니다. Spark 작업 제출 기능을 사용하면 SQL Server 2019 빅 데이터 클러스터를 참조하는 로컬 Jar 또는 Py 파일을 제출할 수 있습니다. 또한 HDFS 파일 시스템에 이미 있는 Jar 또는 Py 파일을 실행할 수 있습니다. 

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 도구](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
   - **kubectl**

- [빅 데이터 클러스터의 HDFS/Spark 게이트웨이에 Azure Data Studio 연결](connect-to-big-data-cluster.md)

## <a name="open-spark-job-submission-dialog"></a>Spark 작업 제출 대화 상자 열기

Spark 작업 제출 대화 상자를 여는 방법에는 여러 가지가 있습니다. 대시보드, 개체 탐색기의 상황에 맞는 메뉴, 명령 팔레트 등이 포함됩니다.

- Spark 작업 제출 대화 상자를 열려면 대시보드에서 **새 Spark 작업**을 클릭합니다.

    ![대시보드를 클릭하여 표시된 제출 메뉴](./media/submit-spark-job/new-spark-job.png)

- 또는 개체 탐색기에서 클러스터를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **Spark 작업 제출**을 선택합니다.

    ![파일을 마우스 오른쪽 단추로 클릭하여 표시된 제출 메뉴](./media/submit-spark-job/submit-spark-job-1.png)


- Jar/Py 필드가 미리 채워져 있는 Spark 작업 제출 대화 상자를 열려면 개체 탐색기에서 jar/Py 파일을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **Spark 작업 제출**을 선택합니다.  

    ![클러스터를 마우스 오른쪽 단추로 클릭하여 표시된 제출 메뉴](./media/submit-spark-job/submit-spark-job.png)

- **Ctrl+Shift+P**(Windows) 및 **Cmd+Shift+P**(Mac)를 입력하여 명령 팔레트에서 **Spark 작업 제출**을 사용합니다.

    ![Windows의 제출 메뉴 명령 팔레트](./media/submit-spark-job/submit-spark-job-3.png)

    ![Mac의 제출 메뉴 명령 팔레트](./media/submit-spark-job/submit-spark-job-4.png)
  
 
## <a name="submit-spark-job"></a>Spark 작업 제출 

Spark 작업 제출 대화 상자가 다음과 같이 표시됩니다. 작업 이름, JAR/Py 파일 경로, 주 클래스 및 기타 필드를 입력합니다. Jar/Py 파일 원본은 로컬 또는 HDFS에서 가져온 것일 수 있습니다. Spark 작업에 참조 Jar, Py 파일 또는 추가 파일이 있는 경우 **고급** 탭을 클릭하고 해당 파일 경로를 입력합니다. **제출**을 클릭하여 Spark 작업을 제출합니다.

![새 spark 작업 대화 상자](./media/submit-spark-job/submit-spark-job-section.png)

![고급 대화 상자](./media/submit-spark-job/submit-spark-job-section-1.png)

## <a name="monitor-spark-job-submission"></a>Spark 작업 제출 모니터링

Spark 작업이 제출되면 Spark 작업 제출 및 실행 상태 정보가 왼쪽의 작업 기록에 표시됩니다. 진행률 및 로그 세부 정보도 맨 아래의 **출력** 창에 표시됩니다.

- Spark 작업이 진행 중이면 **작업 기록** 패널과 **출력** 창에 진행률이 새로 고쳐집니다.

    ![진행 중인 spark 작업 모니터링](./media/submit-spark-job/monitor-spark-job-submission.png)

- Spark 작업이 성공적으로 완료되면 Spark UI 및 Yarn UI 링크가 **출력** 창에 표시됩니다. 자세한 내용을 보려면 링크를 클릭합니다.

    ![출력의 Spark 작업 링크](./media/submit-spark-job/monitor-spark-job-submission-2.png)

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터 및 관련 시나리오에 대한 자세한 내용은 [SQL Server 빅 데이터 클러스터란?](big-data-cluster-overview.md)을 참조하세요.

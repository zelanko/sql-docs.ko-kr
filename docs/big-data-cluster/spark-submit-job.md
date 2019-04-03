---
title: Azure Data Studio에서 Spark 작업 실행
titleSuffix: SQL Server big data clusters
description: Azure Data Studio의 SQL Server 빅 데이터 클러스터에 Spark 작업을 제출 합니다.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d5354927ff0c7e1c61bf358ad73312611c18f317
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860454"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-clusters-in-azure-data-studio"></a>Azure Data Studio의 SQL Server 빅 데이터 클러스터에 Spark 작업 제출

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

빅 데이터 클러스터에 대 한 주요 시나리오 중 하나에 SQL Server 2019 미리 보기에 대 한 Spark 작업을 제출 하는 기능입니다. Spark 작업 제출 기능을 사용 하면 SQL Server 2019 빅 데이터 클러스터에 대 한 참조를 사용 하 여 로컬 Jar 또는 Py 파일을 제출할 수 있습니다. 또한 HDFS 파일 시스템에 이미 있는 Jar 또는 Py 파일을 실행할 수 있습니다. 

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 도구도](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 extension**
   - **Kubectl**

- [Azure Data Studio 빅 데이터 클러스터의 HDFS/Spark 게이트웨이에 연결할](connect-to-big-data-cluster.md)합니다.

## <a name="open-spark-job-submission-dialog"></a>Spark 작업 제출 대화 상자를 엽니다
여러 가지 방법으로 Spark 작업 제출 대화 상자를 엽니다. 대시보드, 개체 탐색기 및 명령 Palate 상황에 맞는 메뉴를 포함 하는 방법입니다.

+ 클릭 **새 Spark 작업** 대시보드에서 Spark 작업 제출 대화 상자를 엽니다.

    ![대시보드를 클릭 하 여 메뉴를 제출](./media/submit-spark-job/new-spark-job.png)
 
+ 개체 탐색기에서 클러스터를 마우스 오른쪽 단추로 클릭 하 고 선택 **Spark 작업 제출** 상황에 맞는 메뉴입니다. Spark 작업 제출 대화 상자가 열립니다.  
 
    ![클러스터를 마우스 오른쪽 단추로 클릭 하 여 메뉴를 제출](./media/submit-spark-job/submit-spark-job.png)

+ 개체 탐색기에서 Jar/Py 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **Spark 작업 제출** 상황에 맞는 메뉴입니다. 미리 채워지므로 Jar/Py 필드를 사용 하 여 Spark 작업 제출 대화 상자를 엽니다. 
 
    ![마우스 오른쪽 단추로 클릭 파일 메뉴를 제출 합니다.](./media/submit-spark-job/submit-spark-job-2.png)

+ 명령을 사용 하 여 **Spark 작업 제출** Ctrl + Shift + P (Windows)에서 및 Cmd + Shift + P (Mac)에 입력 하 여 명령 팔레트에서.

    ![창의 메뉴 명령 팔레트를 제출 합니다.](./media/submit-spark-job/submit-spark-job-3.png)

    ![Mac의 메뉴 명령 팔레트를 제출 합니다.](./media/submit-spark-job/submit-spark-job-4.png)
  
 
## <a name="submit-spark-job"></a>Spark 작업 제출 
Spark 작업 제출 대화 상자는 다음과 같이 표시 됩니다. 작업 이름, JAR/Py 파일 경로, 기본 클래스 및 다른 필드를 입력 합니다. Jar / 로컬에서 또는 HDFS에서 Py 파일 원본 일 수 있습니다. 작업에 Spark Jar, Py 파일이 나 추가 파일을 참조 하는 경우 클릭 **고급** 탭 하 고 해당 파일 경로 입력 합니다. 클릭 **제출** Spark 작업을 제출 합니다.
 
![새 spark 작업 대화 상자](./media/submit-spark-job/submit-spark-job-section.png)

![고급 대화 상자](./media/submit-spark-job/submit-spark-job-section-1.png)

## <a name="monitor-spark-job-submission"></a>Spark 작업 제출을 모니터링합니다
Spark 작업 제출 되 면 Spark 작업 제출 및 실행 상태 정보는 왼쪽의 작업 기록에 표시 됩니다. 진행률 및 로그에서 세부 정보에도 표시 됩니다는 **출력** 창 맨 아래에 있습니다.
+ Spark 작업이 진행에서 중일 때를 **작업 기록** 패널 및 **출력** 창 진행 상태를 사용 하 여 새로 고침 됩니다.

![진행 중인 spark 작업 모니터](./media/submit-spark-job/monitor-spark-job-submission.png)

+ Spark 작업의 경우 성공적으로 완료 하면 수 Spark UI 및 Yarn UI에서 링크를 참조 합니다 **출력** 창입니다. 자세한 내용은 링크를 클릭할 수 있습니다.

![출력에서 Spark 작업 링크](./media/submit-spark-job/monitor-spark-job-submission-2.png)

## <a name="next-steps"></a>다음 단계
SQL Server 빅 데이터 클러스터 및 관련된 시나리오에 대 한 자세한 내용은 참조 하세요. [SQL Server 빅 데이터 클러스터 란](big-data-cluster-overview.md)?


---
title: Spark를 사용하여 샘플 Notebook 실행
titleSuffix: SQL Server big data clusters
description: 이 자습서에서는 SQL Server 2019 빅 데이터 클러스터에서 샘플 Spark Notebook을 로드하고 실행하는 방법을 보여줍니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 03/30/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ce2b2439f136150348409f591550b8fc07383bd9
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606893"
---
# <a name="run-a-sample-notebook-using-spark"></a>Spark를 사용하여 샘플 Notebook 실행

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 Azure Data Studio에서 Notebook을 로드 및 실행하는 방법을 보여 줍니다. 이를 통해 데이터 과학자 및 데이터 엔지니어가 클러스터에 대해 Python, R 또는 Scala 코드를 실행할 수 있습니다.

> [!TIP]
> 원하는 경우 이 자습서의 명령을 위해 스크립트를 다운로드하여 실행할 수 있습니다. 지침에 대해서는 GitHub의 [Spark 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark)을 참조하세요.

## <a name="prerequisites"></a><a id="prereqs"></a> 필수 조건

- [빅 데이터 도구](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
- [빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)

## <a name="download-the-sample-notebook-file"></a>샘플 Notebook 파일 다운로드

다음 지침에 따라 샘플 Notebook 파일 **spark-sql.ipynb**를 Azure Data Studio에 로드합니다.

1. bash 명령 프롬프트(Linux) 또는 Windows PowerShell을 엽니다.

1. 샘플 Notebook 파일을 다운로드할 디렉터리로 이동합니다.

1. 다음 **curl** 명령을 실행하여 GitHub에서 Notebook 파일을 다운로드합니다.

   ```bash
   curl 'https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-loading/transform-csv-files.ipynb' -o transform-csv-files.ipynb
   ```

## <a name="open-the-notebook"></a>Notebook 열기

다음 단계는 Azure Data Studio에서 Notebook 파일을 여는 방법을 보여 줍니다.

1. Azure Data Studio에서 빅 데이터 클러스터의 마스터 인스턴스에 연결합니다. 자세한 내용은 [빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)을 참조하세요.

1. **서버** 창에서 HDFS/Spark 게이트웨이 연결을 두 번 클릭합니다. 그런 다음, **Notebook 열기**를 선택합니다.

   ![Notebook 열기](media/notebook-tutorial-spark/azure-data-studio-open-notebook.png)

1. **커널** 및 대상 컨텍스트(**연결 대상**)가 채워질 때까지 기다립니다. **커널**을 **PySpark3**으로, **연결 대상**을 빅 데이터 클러스터 엔드포인트의 IP 주소로 설정합니다.

   ![커널 및 연결 대상 설정](media/notebook-tutorial-spark/set-kernel-and-attach-to.png)

## <a name="run-the-notebook-cells"></a>Notebook 셀 실행

셀 왼쪽의 재생 단추를 눌러 각 Notebook 셀을 실행할 수 있습니다. 결과는 셀 실행이 완료된 후 Notebook에 표시됩니다.

![Notebook 셀 실행](media/notebook-tutorial-spark/run-notebook-cell.png)

샘플 Notebook의 각 셀을 연속해서 실행합니다. [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에서 Notebooks를 사용하는 방법에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [Notebook을 사용하는 방법](../azure-data-studio/notebooks-guidance.md)
- [Azure Data Studio에서 Notebooks를 관리하는 방법](notebooks-manage-bdc.md)

## <a name="next-steps"></a>다음 단계

Notebook에 대한 자세한 정보:
> [!div class="nextstepaction"]
> [Notebook을 사용하는 방법](../azure-data-studio/notebooks-guidance.md)

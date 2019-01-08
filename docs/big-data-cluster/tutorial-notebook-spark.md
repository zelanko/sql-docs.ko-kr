---
title: 샘플 노트북을 실행 합니다. | Microsoft Docs
titleSuffix: SQL Server 2019 big data clusters
description: 이 자습서에서는 실행을 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 샘플 Spark 노트북을 로드할 수 있습니다 하는 방법을 보여 줍니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: 55d37969ec3e03a635e948cdafb73eb1922a1795
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432556"
---
# <a name="tutorial-run-a-sample-notebook-on-a-sql-server-2019-big-data-cluster"></a>자습서: SQL Server 2019 빅 데이터 클러스터에는 샘플 notebook을 실행 합니다.

이 자습서에는 로드 하 고 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 Azure Data Studio에서 notebook을 실행 하는 방법을 보여 줍니다. 이렇게 하면 데이터 과학자 및 데이터 엔지니어가 클러스터에 대해 Python, R 또는 Scala 코드를 실행할 수 있습니다.

> [!TIP]
> 원한다 면 다운로드 하 고이 자습서의 명령에 대 한 스크립트를 실행할 수 있습니다. 지침은 합니다 [Spark 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark) github입니다.

## <a id="prereqs"></a> 필수 구성 요소

- [빅 데이터 도구](deploy-big-data-tools.md)
   - **Kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
- [빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)

## <a name="download-the-sample-notebook-file"></a>샘플 노트북 파일 다운로드

샘플 전자 필기장 파일을 로드 하려면 다음 지침을 따르십시오 **spark sql.ipynb** Azure 데이터 스튜디오로입니다.

1. Bash 명령 프롬프트 (Linux) 또는 Windows PowerShell을 엽니다.

1. 샘플 노트북 파일을 다운로드 하려는 디렉터리로 이동 합니다.

1. 다음을 실행 합니다 **curl** GitHub에서 notebook 파일을 다운로드 하는 명령:

   ```bash
   curl 'https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/spark-sql.ipynb' -o spark-sql.ipynb
   ```

## <a name="open-the-notebook"></a>Notebook을 열려면

다음 단계를 Azure Data Studio에서 notebook 파일을 여는 방법을 보여 줍니다.

1. Azure Data Studio, 빅 데이터 클러스터의 HDFS/Spark 게이트웨이에 연결 합니다. 자세한 내용은 [HDFS/Spark 게이트웨이에 연결할](connect-to-big-data-cluster.md#hdfs)합니다.

1. HDFS/Spark 게이트웨이 연결을 두 번 클릭 합니다 **서버** 창입니다. 선택한 **노트북 열기**합니다.

   ![전자 필기장 열기](media/tutorial-notebook-spark/azure-data-studio-open-notebook.png)

1. 대기 합니다 **커널** 대상 컨텍스트와 (**연결할**) 채워져야 합니다. 설정 합니다 **커널** 하 **PySpark3**, 설정 및 **연결할** 빅 데이터 클러스터 끝점의 IP 주소로.

   ![커널을 설정에 연결](media/tutorial-notebook-spark/set-kernel-and-attach-to.png)

## <a name="run-the-notebook-cells"></a>Notebook 셀 실행

셀의 왼쪽에 play 단추를 눌러 각 notebook 셀을 실행할 수 있습니다. 셀 실행이 완료 된 후 결과 노트북에 표시 됩니다.

![Notebook 셀 실행](media/tutorial-notebook-spark/run-notebook-cell.png)

연속에서 샘플 전자 필기장의 각 셀을 실행 합니다. SQL Server 빅 데이터 클러스터를 사용 하 여 notebook을 사용 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [SQL Server 2019 미리 보기에서 notebook을 사용 하는 방법](notebooks-guidance.md)
- [Azure Data Studio에서 notebook을 관리 하는 방법](notebooks-how-to-manage.md)

## <a name="next-steps"></a>다음 단계

Notebook에 대 한 자세한 정보:
> [!div class="nextstepaction"]
> [Notebook에 알아봅니다](notebooks-guidance.md)
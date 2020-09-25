---
title: Azure Data Studio에서 Jupyter Notebook 사용
description: Azure Data Studio에서 Jupyter Notebook을 사용하는 방법을 알아봅니다.
ms.topic: conceptual
ms.prod: azure-data-studio
ms.technology: azure-data-studio
author: yualan
ms.author: alayu
ms.reviewer: achatter, maghan, mikeray
ms.custom: seo-lt-2019
ms.date: 07/01/2020
ms.openlocfilehash: 2a89eecf706c3b1bf1d1c0ba445a896ba4d6f96b
ms.sourcegitcommit: e3460309b301a77d0babec032f53de330da001a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91136813"
---
# <a name="use-jupyter-notebooks-in-azure-data-studio"></a>Azure Data Studio에서 Jupyter Notebook 사용

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

Jupyter Notebook은 라이브 코드, 수식, 시각화 및 내레이션 텍스트를 포함하는 문서를 만들고 공유할 수 있는 오픈 소스 웹 애플리케이션입니다. 사용에는 데이터 정리 및 변환, 숫자 시뮬레이션, 통계 모델링, 데이터 시각화 및 기계 학습이 포함됩니다.

이 문서에서는 최신 버전의 [**Azure Data Studio**](../download-azure-data-studio.md)에서 새 Notebook을 만드는 방법과 여러 커널을 사용하여 고유한 Notebook 작성을 시작하는 방법을 설명합니다.

Notebook에 대한 소개는 5분 분량의 다음 동영상을 시청하세요. Azure Data Studio:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introduction-to-Azure-Data-Studio-Notebooks/player?WT.mc_id=dataexposed-c9-niner]

## <a name="create-a-notebook"></a>Notebook 만들기

새 Notebook을 만드는 방법에는 여러 가지가 있습니다. 어떤 방법을 사용하든 `Notebook-1.ipynb`라는 이름의 새 파일이 열립니다.

- Azure Data Studio에서 **파일 메뉴**로 이동한 다음, **새 Notebook**을 선택합니다.

  ![새 파일 Notebook](media/notebooks-guidance/file-new-notebook.png)

- **SQL Server** 연결을 마우스 오른쪽 단추로 클릭하고 **새 Notebook**을 선택합니다.

  ![새 서버 Notebook](media/notebooks-guidance/server-new-notebook.png)

- 명령 팔레트(**Ctrl+Shift+P**)를 열고 “새 Notebook”을 입력한 다음, **새 Notebook** 명령을 선택합니다.

  ![새 명령 팔레트 Notebook](media/notebooks-guidance/command-palette-new-notebook.png)

## <a name="connect-to-a-kernel"></a>커널에 연결

Azure Data Studio Notebook은 SQL Server, Python, PySpark를 비롯한 다양한 커널을 지원합니다. 각 커널은 Notebook의 코드 셀에서 서로 다른 언어를 지원합니다. 예를 들어, SQL Server 커널에 연결된 경우 Notebook 코드 셀에서 T-SQL 문을 입력하고 실행할 수 있습니다.

**연결 대상**은 커널의 컨텍스트를 제공합니다. 예를 들어 SQL 커널을 사용하는 경우 임의의 SQL Server 인스턴스에 연결할 수 있습니다.
Python3 커널을 사용하는 경우 **localhost**에 연결하고 로컬 Python 개발에 이 커널을 사용할 수 있습니다.

SQL 커널을 사용하여 PostgreSQL 서버 인스턴스에 연결할 수도 있습니다. PostgreSQL 개발자이고 Notebook을 PostgreSQL 서버에 연결하려는 경우, Azure Data Studio 확장 마켓플레이스에서 [**PostgreSQL 확장**](../extensions/postgres-extension.md)을 다운로드한 다음, PostgreSQL 서버에 연결합니다.

SQL Server 2019 빅 데이터 클러스터에 연결되어 있는 경우, 기본 **연결 대상**은 클러스터의 엔드포인트입니다. 클러스터의 Spark 컴퓨팅을 사용하여 Python, Scala 및 R 코드를 제출할 수 있습니다.

| 커널                      | Description                                                  |
|:----------------------------|:-------------------------------------------------------------|
| SQL 커널                  | 관계형 데이터베이스를 대상으로 하는 SQL 코드를 작성합니다.         |
| PySpark3 및 PySpark 커널 | 클러스터의 Spark 컴퓨팅을 사용하여 Python 코드를 작성합니다.      |
| Spark 커널                | 클러스터의 Spark 컴퓨팅을 사용하여 Scala 및 R 코드를 작성합니다. |
| Python 커널               | 로컬 개발을 위한 Python 코드를 작성합니다.                     |

특정 커널에 대한 자세한 내용은 다음을 참조하세요.

- [SQL Server Notebook 만들기 및 실행](./notebooks-sql-kernel.md)
- [Python 노트북 만들기 및 실행](./notebooks-python-kernel.md)
- [Azure Data Studio의 Kqlmagic 확장](./notebooks-kqlmagic.md) - Python 커널의 기능을 확장합니다.

## <a name="add-a-code-cell"></a>코드 셀 추가

코드 셀을 사용하면 Notebook 내에서 대화형으로 코드를 실행할 수 있습니다.

도구 모음에서 **+ 셀** 명령을 클릭하고 **코드 셀**을 선택하여 새 코드 셀을 추가합니다. 현재 선택된 셀 뒤에 새 코드 셀이 추가됩니다.

셀에 선택한 커널에 대한 코드를 입력합니다. 예를 들어 SQL 커널을 사용하는 경우 코드 셀에 T-SQL 명령을 입력할 수 있습니다.

SQL 커널을 사용하여 코드를 입력하는 것은 SQL 쿼리 편집기를 사용하는 방법과 비슷합니다. 코드 셀은 다양한 기능을 갖춘 SQL 편집기, IntelliSense 및 기본 제공 코드 조각과 같은 기본 제공 기능을 통해 최신 SQL 코딩 환경을 지원합니다. 코드 조각을 사용하여 데이터베이스, 테이블, 뷰, 저장 프로시저를 만드는 적절한 SQL 구문을 생성하고 기존 데이터베이스 개체를 업데이트할 수 있습니다. 코드 조각을 통해 개발 또는 테스트 목적으로 데이터베이스 복사본을 빠르게 만들고 스크립트를 생성 및 실행할 수도 있습니다.

![SQL 커널](media/notebooks-guidance/intellisense-code-cell.png)

## <a name="add-a-text-cell"></a>텍스트 셀 추가

텍스트 셀을 사용하면 코드 셀 사이에 Markdown 텍스트 블록을 추가하여 코드를 문서화할 수 있습니다.

도구 모음에서 **+ 셀** 명령을 클릭하고 **텍스트 셀**을 선택하여 새 텍스트 셀을 추가합니다.

셀이 편집 모드에서 시작되므로 Markdown 텍스트를 입력할 수 있습니다. 입력함에 따라 아래에 미리 보기가 표시됩니다.

![markdown 셀](media/notebooks-guidance/notebook-markdown-cell.png)

텍스트 셀 바깥쪽을 선택하면 Markdown 텍스트가 표시됩니다.

![markdown 텍스트](media/notebooks-guidance/notebook-markdown-preview.png)

텍스트 셀 안쪽을 다시 클릭하면 편집 모드로 변경됩니다.

## <a name="run-a-cell"></a>셀 실행

단일 셀을 실행하려면 셀 왼쪽에 있는 **셀 실행**(원형 검은색 화살표)을 클릭하거나 셀을 선택하고 F5 키를 누릅니다. 도구 모음에서 **모두 실행**을 클릭하여 Notebook의 모든 셀을 실행할 수 있습니다. 셀은 한 번에 하나씩 실행되며 셀에서 오류가 발생하면 실행이 중지됩니다.

셀의 결과는 셀 아래에 표시됩니다. Notebook에서 실행된 모든 셀의 결과를 지우려면 도구 모음에서 **결과 지우기** 단추를 선택합니다.

## <a name="save-a-notebook"></a>Notebook 저장

Notebook을 저장하려면 다음 중 하나를 수행합니다.

- Ctrl+S 입력
- **파일** 메뉴에서 **저장** 선택
- **파일** 메뉴에서 **다른 이름으로 저장...** 선택
- **파일** 메뉴에서 **모두 저장** 선택 - 열려 있는 모든 Notebook이 저장됩니다.
- 명령 팔레트에서 **파일: 저장** 입력

Notebook이 `.ipynb` 파일로 저장됩니다.

## <a name="trusted-and-non-trusted"></a>신뢰할 수 있음 및 신뢰할 수 없음

Azure Data Studio에서 열린 Notebook은 기본적으로 **신뢰할 수 있음**으로 설정됩니다.

다른 원본의 Notebook을 여는 경우 **신뢰할 수 없음** 모드로 열린 다음, **신뢰할 수 있음**으로 설정할 수 있습니다.

## <a name="examples"></a>예제

다음 예에서는 여러 커널을 사용하여 간단한 “Hello World” 명령을 실행하는 방법을 보여 줍니다. 커널을 선택하고 셀에 예제 코드를 입력한 다음, **셀 실행**을 클릭합니다.

### <a name="pyspark"></a>Pyspark

![Spark 애플리케이션](media/notebooks-guidance/pyspark.png)

### <a name="spark--scala-language"></a>Spark | Scala 언어

![Spark Scala](media/notebooks-guidance/spark-scala.png)

### <a name="spark--r-language"></a>Spark | R 언어

![Spark R](media/notebooks-guidance/spark-r.png)

### <a name="python-3"></a>Python 3

![로컬 python](media/notebooks-guidance/local-python.png)

## <a name="next-steps"></a>다음 단계

- [SQL Server Notebook 만들기 및 실행](./notebooks-sql-kernel.md).
- [Python 노트북 만들기 및 실행](./notebooks-python-kernel.md)
- [SQL Server Machine Learning Services를 사용하여 Azure Data Studio Notebook에서 Python 및 R 스크립트 실행](../../machine-learning/install/sql-machine-learning-azure-data-studio.md)
- [Azure Data Studio Notebook을 사용하여 SQL Server 빅 데이터 클러스터 배포](../../big-data-cluster/notebooks-deploy.md)
- [Azure Data Studio Notebook을 사용하여 SQL Server 빅 데이터 클러스터 관리](../../big-data-cluster/notebooks-manage-bdc.md)
- [Spark를 사용하여 샘플 Notebook 실행](../../big-data-cluster/notebooks-tutorial-spark.md)
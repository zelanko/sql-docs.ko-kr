---
title: Azure Data Studio에서 노트북을 실행 합니다.
titleSuffix: SQL Server 2019 big data clusters
description: 이 문서에서는 Azure Data Studio conneected에서 SQL Server 2019 빅 데이터 클러스터에 Jupyter Notebook을 실행 하는 방법에 설명 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/12/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 44ba203fcd7445add8fce00dd64913f85bcf4cc1
ms.sourcegitcommit: 11ab8a241a6d884b113b3cf475b2b9ed61ff00e3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161660"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>SQL Server 2019 미리 보기에서 notebook을 사용 하는 방법

이 문서에는 빅 데이터 클러스터에 Jupyter 노트북을 시작 하는 방법 및 고유한 전자 필기장 제작을 시작 하는 방법을 설명 합니다. 또한 클러스터에 대 한 작업을 제출 하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>사전 요구 사항

Notebook을 사용 하려면 다음 필수 구성 요소를 설치 해야 합니다.

- [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)
- [SQL Server 2019 빅 데이터 도구도](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
   - **kubectl**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-sql-server-big-data-cluster-end-point"></a>SQL Server 빅 데이터 클러스터 끝점에 연결

클러스터의 다른 끝점에 연결할 수 있습니다. Microsoft SQL Server 연결 형식 또는 SQL Server 빅 데이터 클러스터 끝점에 연결할 수 있습니다.
Azure 데이터 스튜디오에서 F1을 누르고 클릭 **새 연결** 에 SQL Server 빅 데이터 클러스터 끝점에 연결할 수 있습니다.

![image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>HDFS 찾아보기

연결한 후 HDFS 폴더를 이동할 수 있습니다. SQL Server 시작 WebHDFS 배포가 완료 되 면 시작 됩니다. WebHDFS를 사용 하면 **새로 고침**에 추가 **새 디렉터리**를 **업로드** 파일 및 **삭제**합니다.

![image2](media/notebooks-guidance/image2.png)

이러한 간단한 연산을 HDFS에 고유한 데이터를 가져올 수 있습니다.

## <a name="launch-new-notebooks"></a>새 노트북을 시작 합니다.

>[!NOTE]
>사용자 환경에서 실행 하는 여러 Python 프로세스에 있는 경우 먼저 삭제는 `.scaleoutdata` 설치 디렉터리 아래에 있는 폴더입니다. 이 트리거해야 합니다 `Reinstall Notebook dependencies` Azure Data Studio에서 작업 합니다. 모든 종속성을 설치 하는 데 몇 분 정도 걸립니다.

Ctrl + Shift + P 또는 Macintosh Cmd + Shift + P를 및 유형에 대 한 전자 필기장 종속성을 설치 하는 문제가 있는 경우 클릭 `Reinstall Notebook dependencies` 명령 팔레트에서 합니다.

![image3](media/notebooks-guidance/image3.png)

새 notebook을 시작 하는 방법은 여러 가지입니다.

1. **관리 대시보드**합니다. 새 연결을 구축한 후 대시보드에 표시 됩니다. 클릭 **새 노트북** 대시보드에서 작업 합니다.
  
    ![image4](media/notebooks-guidance/image4.png)

1. HDFS/Spark 연결을 마우스 오른쪽 단추로 클릭 하 고 클릭 **새 노트북** 상황에 맞는 메뉴입니다.

    ![image5](media/notebooks-guidance/image5.png)

    라는 새 파일 `Notebook-0.ipynb` 열립니다.

    ![image6](media/notebooks-guidance/image6.png)

명령 팔레트에서 notebook을 열면 노트북으로 열립니다 `Untitled-0.ipynb`합니다.

## <a name="supported-kernels-and-attach-to-context"></a>커널 지원 및 컨텍스트 연결

Notebook 설치 PySpark 및 Spark에서 Spark를 사용 하 여 Python 및 Scala 코드를 쓸 수 있도록 하는 Spark 매직 커널 지원 합니다. 필요에 따라 로컬 개발을 위해 Python을 선택할 수 있습니다.

![image7](media/notebooks-guidance/image7.png)

이러한 커널의 중 하나를 선택 하면 설치는 가상 환경에서 해당 커널을 구성 하 고 지원 되는 언어로 코드 작성을 시작할 수 있습니다.

|커널|Description
|:-----|:-----
|PySpark3 및 PySpark 커널| 클러스터에서 Spark 계산을 사용 하 여 Python 코드를 작성 합니다.
|Spark 커널|클러스터에서 Spark 계산을 사용 하 여 Scala 및 R 코드를 작성 합니다.
|Python Kernel|로컬 개발에 대 한 Python 코드를 작성 합니다.

`Attach to` 연결할 커널에 대 한 컨텍스트를 제공 합니다. SQL Server 빅 데이터 클러스터 끝점으로, 기본 연결 되어 있는 경우 `Attach to` 클러스터의 해당 끝 지점입니다.

기본값 커널 Python은 빅 데이터 클러스터 SQL Server 끝점으로 연결 되어 있지, 및 `Attach to` 는 `localhost`합니다.

## <a name="hello-world-in-different-contexts"></a>다양 한 상황에서 hello world

### <a name="pyspark3pyspark-kernel"></a>Pyspark3/PySpark 커널

PySpark 커널을 선택 하 고 다음 코드에서 셀 형식에 있습니다.

**실행**을 클릭합니다.

Spark 응용 프로그램 시작 되 고 다음 출력을 반환 합니다.

![image8](media/notebooks-guidance/image8.png)

### <a name="spark-kernel--scala-language"></a>Spark 커널은 | Scala 언어

Spark를 선택 합니다. | Scala 커널에 다음 코드에서 셀 유형입니다.

![image9](media/notebooks-guidance/image9.png)

새 코드 셀을 클릭 하 여 추가 합니다 **+ 코드** 도구 모음에서 명령을 합니다.

이제 Spark를 선택 | 셀 입력/붙여넣기 및 커널에 대 한 드롭다운 목록에서 Scala

![image10](media/notebooks-guidance/image10.png)

아래 – 옵션 아이콘을 클릭할 때에 "셀" 옵션을 볼 수 있습니다.

![image11](media/notebooks-guidance/image11.png)

### <a name="spark-kernel--r-language"></a>Spark 커널은 | R 언어

Spark를 선택 합니다. | 커널에 대 한 드롭다운 목록에서 R입니다. 셀에서 입력 하거나 코드를 붙여 넣습니다. 클릭 **실행** 다음 출력을 볼 수 있습니다.

![image13](media/notebooks-guidance/image13.png)

### <a name="local-python-kernel"></a>로컬 Python 커널

로컬 Python 커널 선택 및-셀 형식

![image14](media/notebooks-guidance/image14.png)

### <a name="markdown-text"></a>Markdown 텍스트

새 텍스트 셀을 클릭 하 여 추가 합니다 **+ 텍스트** 도구 모음에서 명령을 합니다.

![image15](media/notebooks-guidance/image15.png)

편집 보기를 변경 하려면 텍스트 셀 안쪽을 두 번 클릭 

![image16](media/notebooks-guidance/image16.png)

편집 모드로 셀 변경 내용

![image17](media/notebooks-guidance/image17.png)

이제 형식 markdown를 볼 수 있습니다 동시에 미리 보기

![image18](media/notebooks-guidance/image18.png)

**실행**을 클릭합니다. Spark 응용 프로그램 시작으로 Spark 세션을 만듭니다 **spark** 정의 된 **HelloWorld** 개체입니다.

Notebook 다음 이미지와 비슷하게 표시 됩니다.

미리 보기 모드로 변경 됩니다 텍스트 셀 바깥쪽을 클릭 하 고 markdown을 숨깁니다.

![image19](media/notebooks-guidance/image19.png)


## <a name="manage-packages"></a>패키지 관리
로컬 Python 개발에 대 한 액세스에 최적화 된 것 중 하나가 자신의 시나리오에 대 한 고객에 게 해야 하는 패키지를 설치 하는 기능을 포함 하는 것 이었습니다. 기본적으로 같은 공통 패키지가 포함 `pandas`, `numpy` 포함 되지 않은 패키지 notebook 셀에서 다음 코드를 작성 한 다음 예상 되는 경우 있지만 등. 

```python
import <package-name>
```

이 명령을 실행할 때 `Module not found` 반환 됩니다. 다음으로 패키지가 있으면 오류가으로 표시 됩니다.

반환 하는 경우는 `Module not Found` 오류를 클릭 **패키지 관리** 식별 하 여 Virtualenv에 대 한 경로 사용 하 여 터미널을 시작 합니다. 이제 패키지를 로컬로 설치할 수 있습니다. 다음 명령을 사용 하 여 패키지를 설치 합니다.

```bash
./pip install <package-name>
```

패키지를 설치한 후에 Notebook 셀에서 이동 하 고 다음 명령을 입력 하는 일을 할 해야 합니다.

```python
import <package-name>
```

패키지를 제거 하려면 터미널에서 다음 명령을 사용 합니다.

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>다음 단계

기존 노트북을 사용 하는 방법에 알아보려면 참조 [Azure Data Studio에서 notebook을 관리 하는 방법](notebooks-how-to-manage.md)합니다.
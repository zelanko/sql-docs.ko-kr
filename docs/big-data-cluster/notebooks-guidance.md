---
title: Azure Data Studio에서 노트북을 실행 합니다.
titleSuffix: SQL Server 2019 big data clusters
description: 이 문서에서는 Azure Data Studio conneected에서 SQL Server 2019 빅 데이터 클러스터에 Jupyter Notebook을 실행 하는 방법에 설명 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: af1393b38b297e451903d5a39942a3e878c88ee6
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53246612"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>SQL Server 2019 미리 보기에서 notebook을 사용 하는 방법

이 문서에는 빅 데이터 클러스터에 Jupyter 노트북을 시작 하는 방법 및 고유한 전자 필기장 제작을 시작 하는 방법을 설명 합니다. 또한 클러스터에 대 한 작업을 제출 하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>사전 요구 사항

Notebook을 사용 하려면 다음 필수 구성 요소를 설치 해야 합니다.

- [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)
- [SQL Server 2019 빅 데이터 도구도](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
   - **Kubectl**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-hadoop-gateway-knox-end-point"></a>Hadoop 게이트웨이 Knox 끝점에 연결

클러스터의 다른 끝점에 연결할 수 있습니다. Microsoft SQL Server 연결 형식 또는 HDFS/Spark 게이트웨이 끝점으로 연결할 수 있습니다.
Azure 데이터 Studio (미리 보기)에서 F1을 누르고 클릭 **새 연결** HDFS/Spark 게이트웨이 엔드포인트에 연결할 수 있습니다.

![image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>HDFS 찾아보기

연결한 후 HDFS 폴더를 이동할 수 있습니다. WebHDFS 시작 배포가 완료 되 고 할 수 있습니다 **새로 고침**에 추가 **새 디렉터리**를 **업로드** 파일 및 **삭제**.

![이미지 2](media/notebooks-guidance/image2.png)

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

  예를 들어, 전자 필기장의 이름을 제공 `Test.ipynb`합니다. **저장**을 클릭합니다.

![image6](media/notebooks-guidance/image6.png)

## <a name="supported-kernels-and-attach-to-context"></a>커널 지원 및 컨텍스트 연결

Notebook 설치 PySpark 및 Spark에서 Spark를 사용 하 여 Python 및 Scala 코드를 쓸 수 있도록 하는 Spark 매직 커널 지원 합니다. 필요에 따라 로컬 개발을 위해 Python을 선택할 수 있습니다.

![image7](media/notebooks-guidance/image7.png)

이러한 커널의 중 하나를 선택 하면 해당 커널 가상 환경에서 설치 하 고 지원 되는 언어로 코드 작성을 시작할 수 있습니다.

|커널|Description
|:-----|:-----
|PySpark 커널|클러스터에서 Spark 계산을 사용 하 여 Python 코드를 작성 합니다.
|Spark 커널|클러스터에서 Spark 계산을 사용 하 여 Scala 코드를 작성 합니다.
|Python 커널|로컬 개발에 대 한 Python 코드를 작성 합니다.

`Attach to` 연결할 커널에 대 한 컨텍스트를 제공 합니다. HDFS/Spark 게이트웨이 (Knox) 끝에 연결 되어 있는 경우에 기본 지점 `Attach to` 클러스터의 해당 끝 지점입니다.

![image8](media/notebooks-guidance/image8.png)

## <a name="hello-world-in-different-contexts"></a>다양 한 상황에서 hello world

### <a name="pyspark-kernel"></a>Pyspark 커널

PySpark 커널을 선택 하 고 다음 코드에서 셀 형식에:

![image9](media/notebooks-guidance/image9.png)

클릭 하 고 실행 시작 되 고 Spark 응용 프로그램 참조 하는 다음 출력이 표시:

![Image10](media/notebooks-guidance/image10.png)

다음 이미지와 유사한 결과가 출력 됩니다.

![Image11](media/notebooks-guidance/image11.png)

### <a name="spark-kernel"></a>Spark 커널
새 코드 셀을 클릭 하 여 추가 합니다 **+ 코드** 도구 모음에서 명령을 합니다.

![Image12](media/notebooks-guidance/image12.png)

아래 옵션 아이콘을 클릭할 때에 "셀" 옵션을 볼 수 있습니다.

![Image13](media/notebooks-guidance/image13.png)

다음은 모든 셀에 대 한 옵션

![Image14](media/notebooks-guidance/image14.png)-

-셀 입력/붙여넣기 및 커널에 대 한 드롭다운 목록에서 Spark 커널은 이제 선택

![Image15](media/notebooks-guidance/image15.png)

클릭 **실행** 시작 되 고 Spark 응용 프로그램을 표시 및이 Spark 세션을 만듭니다 **spark** 을 정의 합니다 **HelloWorld** 개체입니다.

Notebook 다음 이미지와 비슷하게 표시 됩니다.

![Image16](media/notebooks-guidance/image16.png)

다음 Notebook 셀에서 다음 개체를 정의한 다음 코드를 입력 합니다.

![Image17](media/notebooks-guidance/image17.png)

클릭 **실행** 전자 필기장의 메뉴를 표시 된 "Hello, world!" 출력 합니다.

![Image18](media/notebooks-guidance/image18.png)

### <a name="local-python-kernel"></a>로컬 python 커널
로컬 Python 커널 선택 및-셀 형식

![Image19](media/notebooks-guidance/image19.png)

다음과 같은 출력이 표시 됩니다.

![Image20](media/notebooks-guidance/image20.png)

### <a name="markdown-text"></a>Markdown 텍스트
새 텍스트 셀을 클릭 하 여 추가 합니다 **+ 텍스트** 도구 모음에서 명령을 합니다.

![Image21](media/notebooks-guidance/image21.png)

Markdown 추가 미리 보기 아이콘을 클릭

![Image22](media/notebooks-guidance/image22.png)

방금 markdown 참조를 설정/해제를 다시 미리 보기 아이콘을 클릭

![Image23](media/notebooks-guidance/image23.png)

## <a name="manage-packages"></a>패키지 관리
로컬 Python 개발에 대 한 액세스에 최적화 된 것 중 하나가 자신의 시나리오에 대 한 고객에 게 해야 하는 패키지를 설치 하는 기능을 포함 하는 것 이었습니다. 기본적으로 일반적인 패키지 포함 pandas, numpy 등 하지만 포함 되지 않은 패키지를 예상 하는 경우 다음 코드를 작성 다음 Notebook 셀에서 같은: 

```python
import <package-name>
```

이 명령을 실행할 때를 `Module not found` 오류입니다. 다음으로 패키지가 있으면 오류가으로 표시 됩니다.

있다면를 `Module not Found` 오류를 클릭 **패키지 관리** 식별 하 여 Virtualenv에 대 한 경로 사용 하 여 터미널을 시작 합니다. 이제 패키지를 로컬로 설치할 수 있습니다. 다음 명령을 사용 하 여 패키지를 설치 합니다.

```bash
./pip install <package-name>
```

패키지를 설치한 후에 Notebook 셀에서 이동 하 고 다음 명령을 입력 하는 일을 할 해야 합니다.

```python
import <package-name>
```

더 이상 가져와야 셀을 실행 하면 이제는 `Module not found` 오류입니다.

패키지를 제거 하려면 터미널에서 다음 명령을 사용 합니다.

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>다음 단계

기존 노트북을 사용 하는 방법에 알아보려면 참조 [Azure Data Studio에서 notebook을 관리 하는 방법](notebooks-how-to-manage.md)합니다.
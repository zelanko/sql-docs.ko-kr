---
title: SQL Server 2019 미리 보기에서 notebook을 사용 하는 방법 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/05/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 137da00959f6f8d3498bb3d063ceb21337266aef
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48878016"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>SQL Server 2019 미리 보기에서 notebook을 사용 하는 방법

이 문서에서는 SQL Server 2019 빅 데이터 클러스터에 노트북을 시작 하는 방법을 보여 줍니다. 또한 고유한 전자 필기장 제작을 시작 하는 방법 및 클러스터에 대 한 작업을 제출 하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>필수 구성 요소

Notebook을 사용 하려면 다음 필수 구성 요소를 설치 해야 합니다.

- [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)
- [Azure Data Studio](../azure-data-studio/what-is.md)
- [SQL Server 2019 확장 (미리 보기)](../azure-data-studio/sql-server-2019-extension.md)합니다.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-sql-server-big-data-cluster-end-point"></a>SQL Server 빅 데이터 클러스터 끝점에 연결

클러스터의 다른 끝점에 연결할 수 있습니다. Microsoft SQL Server 연결 형식 또는 SQL Server 빅 데이터 클러스터 끝점에 연결할 수 있습니다.

Azure Data Studio (미리 보기)를 입력 **F1** > **새 연결**, SQL Server 빅 데이터 클러스터 끝점에 연결 합니다.

![image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>HDFS 찾아보기
연결한 후 HDFS 폴더를 이동할 수 있습니다. WebHDFS 시작 배포가 완료 되 고 할 수 있습니다 **새로 고침**에 추가 **새 디렉터리**를 **업로드** 파일 및 **삭제**.

![이미지 2](media/notebooks-guidance/image2.png)

이러한 간단한 연산을 HDFS에 고유한 데이터를 가져올 수 있습니다.

## <a name="launch-new-notebooks"></a>새 노트북을 시작 합니다.

새 notebook을 시작 하는 방법은 여러 가지입니다.

1. 대시보드를 관리 합니다. 새 연결에는 대시보드가 표시 됩니다. 새 Notebook 작업 대시보드에서 클릭 합니다.

  ![image3](media/notebooks-guidance/image3.png)

1. HDFS/Spark 연결을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴를 새 노트북에

![image4](media/notebooks-guidance/image4.png)

노트북의 이름을 입력 (예: *Test.ipynb*)를 클릭 하 고 **저장**합니다.

![image5](media/notebooks-guidance/image5.png)

## <a name="supported-kernels-and-attach-to-context"></a>커널 지원 및 컨텍스트 연결

이 Notebook 설치에서 Spark를 사용 하 여 Python 및 Scala 코드를 작성할 수 있도록 하는 Spark 매직 커널 PySpark 및 Spark를 지원 합니다. 사용자가 해당 로컬 개발을 위해 Python을 선택할 수 있도록 합니다.

![image6](media/notebooks-guidance/image6.png)

이러한 커널의 중 하나를 선택 하면 해당 커널 가상 환경에서 설치 하 고 지원 되는 언어로 코드 작성을 시작할 수 있습니다.

| 커널 | Description
|---- |----
|PySpark 커널| Spark를 사용 하 여 Python 코드를 작성 하는 것에 대 한 클러스터에서 계산 합니다.
|Spark 커널|Spark를 사용 하 여 Scala 코드를 작성 하는 것에 대 한 클러스터에서 계산 합니다.
|Python 커널|로컬 개발에 대 한 Python 코드를 작성 합니다.

연결할 커널에 대 한 컨텍스트를 제공 하는 연결을 선택 합니다. SQL Server 빅 데이터 클러스터 끝점에 연결 하는 해당 끝점은 클러스터의 기본 연결을 선택이 됩니다.

![image7](media/notebooks-guidance/image7.png)

> [!NOTE]
> 기본적으로 Spark 응용 프로그램 1 드라이버 및 연결 되는 약 8.5GB 메모리의 3 개 실행자를 사용 하 여 구성 됩니다. 여러 spark 세션을 실행 하는 것이 좋습니다 최소 32GB의 메모리가 있는 클러스터의 각 서버에 대 한 (예를 들어, AKS 환경에서 사용해 **Standard_D8_v3** 32GB의 메모리가 있는 VM 크기).

## <a name="hello-world-in-the-different-contexts"></a>다양 한 상황에서 hello world

### <a name="pyspark-kernel"></a>Pyspark 커널

PySpark 커널을 선택 하 고 다음 코드에서 셀 형식에:

![image8](media/notebooks-guidance/image8.png)

클릭 하 고 실행 시작 되 고 Spark 응용 프로그램 참조 하는 다음 출력이 표시:

![image9](media/notebooks-guidance/image9.png)

다음 이미지와 유사한 결과가 출력 됩니다.

![Image10](media/notebooks-guidance/image10.png)

### <a name="spark-kernel"></a>Spark 커널
새 코드 셀을 클릭 하 여 추가 된 도구 모음에서 명령 코드 +입니다.

![Image11](media/notebooks-guidance/image11.png)

셀 입력/붙여넣기 및 커널에 대 한 드롭다운 목록에서 Spark 커널을 선택합니다 

![Image12](media/notebooks-guidance/image12.png)

클릭 **실행** 시작 되 고 Spark 응용 프로그램을 표시 하 고 Spark 세션이 만들어집니다 **spark** 정의 하 고는 **HelloWorld** 개체입니다.

Notebook 다음 이미지와 비슷하게 표시 됩니다.

![Image13](media/notebooks-guidance/image13.png)

한 번 정의한 개체 다음에 다음 코드에서 다음 Notebook 셀 유형:

![Image14](media/notebooks-guidance/image14.png)

클릭 **실행** 전자 필기장의 메뉴를 표시 된 "Hello, world!" 출력 합니다.

![Image15](media/notebooks-guidance/image15.png)

### <a name="local-python-kernel"></a>로컬 python 커널
로컬 Python 커널 선택 및 셀 입력에서 * *

![Image16](media/notebooks-guidance/image16.png)

다음과 같은 출력이 표시 됩니다.

![Image17](media/notebooks-guidance/image17.png)

### <a name="markdown-text"></a>Markdown 텍스트
새 텍스트 셀을 클릭 하 여 추가 된 + 도구 모음에서 텍스트 명령입니다.

![Image18](media/notebooks-guidance/image18.png)

Markdown 추가 미리 보기 아이콘을 클릭

![Image19](media/notebooks-guidance/image19.png)

방금 markdown 참조를 설정/해제를 다시 미리 보기 아이콘을 클릭

![Image20](media/notebooks-guidance/image20.png)

## <a name="manage-packages"></a>패키지 관리
로컬 Python 개발에 대 한 액세스에 최적화 된 것 중 하나가 자신의 시나리오에 대 한 고객에 게 해야 하는 패키지를 설치 하는 기능을 포함 하는 것 이었습니다. 기본적으로 일반적인 패키지 포함 pandas, numpy 등 하지만 포함 되지 않은 패키지를 예상 하는 경우 다음 코드를 작성 다음 Notebook 셀에서와 같은

```python
import <package-name>
```

이 명령을 실행할 때를 `Module not found` 오류입니다. 다음으로 패키지가 있으면 오류가으로 표시 됩니다.

있다면를 `Module not Found` 오류를 클릭 합니다 **패키지 관리** 식별 하 여 Virtualenv에 대 한 경로 사용 하 여 터미널을 시작 하려면. 이제 패키지를 로컬로 설치할 수 있습니다. 다음 명령을 사용 하 여 패키지를 설치 합니다.

```
./pip install <package-name>
```

패키지를 설치한 후 Notebook 셀에서 이동 하 고 다음 명령에서 입력을 수 있습니다.

```python
import <package-name>
```

더 이상 가져와야 셀을 실행 하면 이제는 `Module not found` 오류입니다.

패키지를 제거 하려는 경우 터미널에서 다음 명령을 사용 합니다.

```
./pip uninstall <package-name>
```

## <a name="next-steps"></a>다음 단계

기존 노트북을 사용 하는 방법에 알아보려면 참조 [Azure Data Studio에서 notebook을 관리 하는 방법](notebooks-how-to-manage.md)합니다.
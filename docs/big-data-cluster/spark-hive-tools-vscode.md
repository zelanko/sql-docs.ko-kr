---
title: SQL Server 빅 데이터 클러스터에서 VS Code에 대해 Spark & Hive 도구를 사용 하 여 Spark 작업 실행
titleSuffix: SQL Server big data clusters
description: SQL Server 빅 데이터 클러스터에서 Visual Studio Code Spark & Hive 도구를 사용 하 여 spark 작업을 제출 합니다.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4458666792d7f4629b4e1820e98e2dbb9901c2b6
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68425983"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-cluster-in-visual-studio-code"></a>Visual Studio Code에서 SQL Server 빅 데이터 클러스터에 Spark 작업 제출

Visual Studio Code Spark & Hive 도구를 사용 하 여 Apache Spark에 대 한 PySpark 스크립트를 만들고 제출 하는 방법에 대해 먼저 Visual Studio Code에서 Spark & Hive 도구를 설치 하는 방법을 설명한 다음 Spark에 작업을 제출 하는 방법을 안내 합니다.  

Windows, Linux 및 macOS를 포함 하는 Visual Studio Code에서 지원 되는 플랫폼에 Spark & Hive 도구를 설치할 수 있습니다. 아래에서 다양 한 플랫폼에 대 한 필수 조건을 찾을 수 있습니다.


## <a name="prerequisites"></a>사전 요구 사항

이 문서의 단계를 완료 하려면 다음 항목이 필요 합니다.

- SQL Server 빅 데이터 클러스터 [SQL Server 빅 데이터 클러스터](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions)를 참조 하세요.
- 및[Visual Studio Code](https://code.visualstudio.com/)가 있습니다.
- [Mono](https://www.mono-project.com/docs/getting-started/install/). Mono는 Linux 및 macOS에만 필요 합니다.
- [Visual Studio Code에 대 한 PySpark 대화형 환경을 설정](https://docs.microsoft.com/azure/hdinsight/set-up-pyspark-interactive-environment)합니다.
- **Hdexample**한 이름의 로컬 디렉터리입니다.  이 문서에서는 **C:\HD\HDexample**를 사용 합니다.

## <a name="install-spark--hive-tools"></a>Spark & Hive 도구 설치

필수 구성 요소를 완료 한 후에는 Visual Studio Code에 대 한 Spark & Hive 도구를 설치할 수 있습니다.  Spark & Hive 도구를 설치 하려면 다음 단계를 완료 합니다.

1. Visual Studio Code를 엽니다.

2. 메뉴 모음에서**확장** **보기** > 로 이동 합니다.

3. 검색 상자에 **Spark & Hive**를 입력 합니다.

4. 검색 결과에서 **Spark & Hive 도구** 를 선택 하 고 **설치**를 선택 합니다.  

   ![확장 설치](./media/spark-hive-tools-vscode/extension.png)

5. 필요한 경우 다시 로드 합니다.

## <a name="open-work-folder"></a>작업 폴더 열기

작업 폴더를 열고 Visual Studio Code에서 파일을 만들려면 다음 단계를 완료 합니다.

1. 메뉴 모음에서 **파일** > **폴더 열기 ...** 로 이동 합니다. C:\HD\HDexample 폴더 **선택** 단추를 선택 합니다.   >  폴더가 왼쪽의 **탐색기** 보기에 나타납니다.

2. **탐색기** 보기에서 폴더, **hdexample**선택 하 고 작업 폴더 옆의 **새 파일** 아이콘을 선택 합니다.

   ![새 파일](./media/spark-hive-tools-vscode/new-file.png)

3. `.py` (Spark 스크립트) 파일 확장명으로 새 파일의 이름을로 바꿉니다.  이 예제에서는 **HelloWorld.py**를 사용 합니다.
4. 다음 코드를 복사 하 여 스크립트 파일에 붙여 넣습니다.
   ```python
    import sys
    from operator import add
    from pyspark.sql import SparkSession, Row
    
    spark = SparkSession\
        .builder\
        .appName("PythonWordCount")\
        .getOrCreate()
    
    data = [Row(col1='pyspark and spark', col2=1), Row(col1='pyspark', col2=2), Row(col1='spark vs hadoop', col2=2), Row(col1='spark', col2=2), Row(col1='hadoop', col2=2)]
    df = spark.createDataFrame(data)
    lines = df.rdd.map(lambda r: r[0])

    counters = lines.flatMap(lambda x: x.split(' ')) \
        .map(lambda x: (x, 1)) \
        .reduceByKey(add)
    
    output = counters.collect()
    sortedCollection = sorted(output, key = lambda r: r[1], reverse = True)
    
    for (word, count) in sortedCollection:
        print("%s: %i" % (word, count))
   ```

## <a name="link-a-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터 연결

Visual Studio Code에서 클러스터에 스크립트를 제출 하려면 먼저 SQL Server 빅 데이터 클러스터에 연결 해야 합니다.

1. 메뉴 모음에서 **보기** > **명령 팔레트 ...** 로 이동 하 여 Spark/Hive를 **입력 합니다. 클러스터**를 연결 합니다.

   ![클러스터 연결 명령](./media/spark-hive-tools-vscode/link-cluster-command.png)

2. **빅 데이터 SQL Server**연결 된 클러스터 유형을 선택 합니다.

3. SQL Server 빅 데이터 끝점을 입력 합니다.

4. SQL Server 빅 데이터 클러스터 사용자 이름을 입력 합니다.

5. 사용자 관리자의 암호를 입력 합니다.

6. 클러스터의 표시 이름을 설정 합니다 (선택 사항).

7. 클러스터를 나열 하 고 확인을 위해 **출력** 뷰를 검토 합니다.

## <a name="list-clusters"></a>클러스터 나열

1. 메뉴 모음에서 **보기** > **명령 팔레트 ...** 로 이동 하 여 Spark/Hive를 **입력 합니다. 클러스터**를 나열 합니다.

2. **출력** 뷰를 검토 합니다.  이 보기에는 연결 된 클러스터가 표시 됩니다.

    ![기본 클러스터 구성 설정](./media/spark-hive-tools-vscode/list-cluster-result.png)

## <a name="set-default-cluster"></a>기본 클러스터 설정

1. 종결 된 경우 [앞](#open-work-folder) 에서 만든 **hdexample** 폴더를 다시 엽니다.  

2. [이전](#open-work-folder) 에 만든 **HelloWorld.py** 파일을 선택 하면 스크립트 편집기에서 열립니다.

3. 아직 수행 하지 않은 경우 클러스터를 연결 합니다.

4. 스크립트 편집기를 마우스 오른쪽 단추로 클릭 하 고 **Spark/Hive를 선택 합니다. 기본 클러스터**를 설정 합니다.   

5. 현재 스크립트 파일에 대 한 기본 클러스터로 클러스터를 선택 합니다. 도구는 구성 파일을 자동으로 업데이트 **합니다. VSCode\settings.json**. 

   ![기본 클러스터 구성 설정](./media/spark-hive-tools-vscode/set-default-cluster-configuration.png)

## <a name="submit-interactive-pyspark-queries"></a>대화형 PySpark 쿼리 제출

다음 단계를 수행 하 여 대화형 PySpark 쿼리를 제출할 수 있습니다.

1. 종결 된 경우 [앞](#open-work-folder) 에서 만든 **hdexample** 폴더를 다시 엽니다.  

2. [이전](#open-work-folder) 에 만든 **HelloWorld.py** 파일을 선택 하면 스크립트 편집기에서 열립니다.

3. 아직 수행 하지 않은 경우 클러스터를 연결 합니다.

4. 모든 코드를 선택 하 고 스크립트 편집기를 마우스 오른쪽 단추로 클릭 **한 다음 Spark를 선택 합니다. PySpark 대화형** 으로 쿼리를 제출 하거나 **Ctrl + Alt + I**바로 가기를 사용 합니다.

   ![pyspark 대화형 상황에 맞는 메뉴](./media/spark-hive-tools-vscode/pyspark-interactive-right-click.png)

5. 기본 클러스터를 지정 하지 않은 경우 클러스터를 선택 합니다. 몇 분 후에 **Python 대화형** 결과가 새 탭에 나타납니다. 또한이 도구를 사용 하면 상황에 맞는 메뉴를 사용 하 여 전체 스크립트 파일 대신 코드 블록을 제출할 수 있습니다. 

   ![pyspark 대화형 python 대화형 창](./media/spark-hive-tools-vscode/pyspark-interactive-python-interactive-window.png) 

6. **"%% Info"** 를 입력 한 다음 **Shift + enter** 를 눌러 작업 정보를 확인 합니다. (옵션)

   ![작업 정보 보기](./media/spark-hive-tools-vscode/pyspark-interactive-view-job-information.png)

   > [!NOTE] 
   >
   > 설정에서 **Python 확장을 사용 하도록** 설정 하지 않은 경우 (기본 설정이 선택 됨) 제출 된 pyspark 상호 작용 결과는 이전 창을 사용 합니다.
   >
   > ![pyspark 대화형 python 확장 사용 안 함](./media/spark-hive-tools-vscode/pyspark-interactive-python-extension-disabled.png)


## <a name="submit-pyspark-batch-job"></a>PySpark batch 작업 제출

1. 종결 된 경우 [앞](#open-work-folder) 에서 만든 **hdexample** 폴더를 다시 엽니다.  

2. [이전](#open-work-folder) 에 만든 **HelloWorld.py** 파일을 선택 하면 스크립트 편집기에서 열립니다.

3. 아직 수행 하지 않은 경우 클러스터를 연결 합니다.

4. 스크립트 편집기를 마우스 오른쪽 단추로 클릭 한 다음 Spark **를 선택 합니다. 일괄 처리**를 PySpark **Ctrl + Alt + H**를 사용 합니다. 

5. 기본 클러스터를 지정 하지 않은 경우 클러스터를 선택 합니다. Python 작업을 제출한 후에는 제출 로그가 Visual Studio Code의 **출력** 창에 표시 됩니다. **SPARK UI url** 및 **Yarn ui url** 도 표시 됩니다. 웹 브라우저에서 URL을 열어 작업 상태를 추적할 수 있습니다.

   ![Python 작업 결과 제출](./media/spark-hive-tools-vscode/submit-pythonjob-result.png) 

## <a name="apache-livy-configuration"></a>Apache Livy 구성

[Apache Livy](https://livy.incubator.apache.org/) 구성은 지원 되며에서 설정할 수 있습니다 **.** 작업 공간 폴더에 있는 VSCode\settings.json. 현재 Livy 구성은 Python 스크립트만 지원 합니다. 자세한 내용은 [LIVY 추가](https://github.com/cloudera/livy/blob/master/README.rst )정보를 참조 하세요.

### <a id="triggerlivyconf"></a>**Livy 구성을 트리거하는 방법**

#### <a name="method-1"></a>메서드 1

1. 메뉴 모음에서 **파일** > **기본** > **설정 설정**으로 이동 합니다.  
2. **검색 설정** 텍스트 상자에 HDInsight 작업 **sumissums를 입력 합니다. Livy 회의**.  
3. 관련 검색 결과에 대해 **설정 json에서 편집** 을 선택 합니다.

#### <a name="method-2"></a>방법 2

파일 `.vscode` 제출 폴더는 작업 폴더에 자동으로 추가 됩니다. Livy 구성은를 클릭 `.vscode\settings.json`하 여 찾을 수 있습니다.

+ 프로젝트 설정:

    ![Livy 구성](./media/spark-hive-tools-vscode/hdi-livyconfig.png)

>[!NOTE]
>설정 **driverMomory** 및 **executorMomry**에 대해 값을 unit으로 설정 합니다 (예: 1g 또는 1024m). 

### <a name="supported-livy-configurations"></a>지원 되는 Livy 구성

#### <a name="post-batches"></a>사후 배치/일괄 처리

**요청 본문**

| name | description | type |
| :- | :- | :- |
| 파일 | 실행할 응용 프로그램이 포함 된 파일입니다. | path (필수) |
| proxyUser | 작업을 실행할 때 가장할 사용자 | string |
| className | Application Java/Spark main 클래스 | string |
| args | 응용 프로그램에 대 한 명령줄 인수 | 문자열 목록 |
| jars | 이 세션에서 사용할 jar | 문자열 목록 |
| pyFiles | 이 세션에서 사용할 Python 파일 | 문자열 목록 |
| files | 이 세션에 사용할 파일입니다. | 문자열 목록 |
| driverMemory | 드라이버 프로세스에 사용할 메모리 양 | string |
| driverCores | 드라이버 프로세스에 사용할 코어 수 | ssNoversion |
| executorMemory | Executor 프로세스 당 사용할 메모리 양 | string |
| executorCores | 각 실행자에 사용할 코어 수 | ssNoversion |
| numExecutors | 이 세션에 대해 시작할 실행자 수 | ssNoversion |
| archives | 이 세션에서 사용 되는 보관 파일입니다. | 문자열 목록 |
| queue | 전송 된 YARN 큐의 이름입니다. | string |
| name | 이 세션의 이름 | string |
| conf | Spark 구성 속성 | 키 = val의 맵 |

#### <a name="response-body"></a>응답 본문

만든 일괄 처리 개체입니다.

| name | description | type |
| :- | :- | :- |
| id | 세션 id | ssNoversion |
| appId | 이 세션의 응용 프로그램 id입니다. | String |
| appInfo | 자세한 응용 프로그램 정보 | 키 = val의 맵 |
| log | 로그 줄 | 문자열 목록 |
| state | 일괄 처리 상태 | string |

>[!NOTE]
>할당 된 Livy 구성은 스크립트를 제출할 때 출력 창에 표시 됩니다.

## <a name="additional-features"></a>추가 기능

Visual Studio Code에 대 한 Spark & Hive는 다음과 같은 기능을 지원 합니다.

- **IntelliSense 자동 완성**. 키워드, 메서드, 변수 등에 대 한 제안이 팝업 됩니다. 아이콘 마다 다른 유형의 개체를 나타냅니다.

    ![Visual Studio Code IntelliSense 개체 형식에 대 한 Spark & Hive 도구](./media/spark-hive-tools-vscode/hdinsight-for-vscode-auto-complete-objects.png)
- **IntelliSense 오류 표식**입니다. 언어 서비스는 Hive 스크립트에 대 한 편집 오류에 밑줄을 긋습니다.     
- **구문 강조 표시**. 언어 서비스는 변수, 키워드, 데이터 형식, 함수 등을 구분 하기 위해 서로 다른 색을 사용 합니다. 

    ![Visual Studio Code 구문 강조 표시를 위한 Spark & Hive 도구](./media/spark-hive-tools-vscode/hdinsight-for-vscode-syntax-highlights.png)

## <a name="unlink-cluster"></a>클러스터 연결 해제

1. 메뉴 모음에서 **보기** > **명령 팔레트 ...** 로 이동한 다음 Spark/Hive를 입력 **합니다. 클러스터**의 연결을 해제 합니다.  

2. 연결을 끊을 클러스터를 선택 합니다.  

3. 확인을 위해 **출력** 보기를 검토 합니다.  

## <a name="next-steps"></a>다음 단계
빅 데이터 클러스터 SQL Server 및 관련 시나리오에 대 한 자세한 내용은 [SQL Server 빅 데이터 클러스터](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions)를 참조 하세요.

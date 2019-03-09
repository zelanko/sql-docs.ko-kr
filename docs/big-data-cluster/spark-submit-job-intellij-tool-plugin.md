---
title: SQL Server 빅 데이터 클러스터에서 IntelliJ 용 Azure 도구 키트의 Spark 작업 실행
titleSuffix: SQL Server Big Data Clusters
description: IntelliJ 용 Azure 도구 키트의 SQL Server 빅 데이터 클러스터에 Spark 작업을 제출 합니다.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.openlocfilehash: 672898e93331fdcf65b1fe978a5ebb47956fdb5b
ms.sourcegitcommit: 3c4bb35163286da70c2d669a3f84fb6a8145022c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2019
ms.locfileid: "57683623"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-clusters-in-intellij"></a>IntelliJ에서 SQL Server 빅 데이터 클러스터에 Spark 작업 제출

SQL Server 빅 데이터 클러스터에 대 한 주요 시나리오 중 하나에 Spark 작업을 제출 하는 기능입니다. Spark 작업 제출 기능을 사용 하면 SQL Server 빅 데이터 클러스터에 대 한 참조를 사용 하 여 로컬 Jar 또는 Py 파일을 제출할 수 있습니다. 또한 HDFS 파일 시스템에 이미 있는 Jar 또는 Py 파일을 실행할 수 있습니다. 

## <a name="prerequisites"></a>사전 요구 사항

- SQL Server 빅 데이터 클러스터입니다.
- Oracle Java Development 키트입니다. 설치할 수는 [Oracle 웹 사이트](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)합니다.
- IntelliJ IDEA. 설치할 수는 [JetBrains 웹 사이트](https://www.jetbrains.com/idea/download/)합니다.
- 확장 IntelliJ 용 azure 도구 키트입니다. 설치 지침은 [IntelliJ 용 Azure 도구 키트 설치](https://docs.microsoft.com/azure/azure-toolkit-for-intellij-installation)합니다.

## <a name="link-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터 링크
1. IntelliJ IDEA 도구를 엽니다.

2. 자체 서명 된 인증서를 사용 하는 경우 SSL 인증서 유효성 검사를 사용 하지 않도록 설정 **도구** 메뉴에서 **Azure**에 **Spark 클러스터 SSL 인증서의 유효성을 검사**, 다음  **사용 하지 않도록 설정**합니다.

    ![SQL Server 빅 데이터 클러스터에 연결-SSL을 사용 하지 않도록 설정](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-disableSSL.png)

3. Azure Explorer를 엽니다 **뷰** 메뉴에서 **도구 Windows**를 선택한 후 **Azure 탐색기**합니다.
4. 마우스 오른쪽 단추로 클릭 **SQL Server 빅 데이터 클러스터**를 선택 **링크 SQL Server 빅 데이터 클러스터**합니다. 입력 된 **서버**, **사용자 이름**, 및 **암호**, 클릭 **확인**합니다.

    ![빅 데이터 클러스터-연결 대화 상자](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-dialog.png)

5. 신뢰할 수 없는 서버 인증서 대화 상자에 표시 되 면 클릭 **Accept**합니다. 나중에 인증서를 관리, 참조 수 [서버 인증서](https://www.jetbrains.com/help/idea/settings-tools-server-certificates.html)합니다.

6. 연결 된 클러스터 목록에서 **SQL Server 빅 데이터 클러스터**합니다. Spark 기록 UI 및 Yarn UI를 열어 spark 작업을 모니터링할 수 있습니다, 클러스터를 마우스 오른쪽 단추로 클릭 하 여도 끊을 수 없습니다.

    ![빅 데이터 클러스터-상황에 맞는 메뉴](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-contextmenu.png)

## <a name="create-a-spark-scala-application-from-hdinsight-template"></a>HDInsight 템플릿에서 Spark Scala 응용 프로그램 만들기

1. IntelliJ IDEA를 시작 하 고 프로젝트를 만듭니다. 에 **새 프로젝트** 대화 상자에서 아래 단계에 따라: 

   a. 선택 **Azure Spark/HDInsight** > **샘플 (Scala)를 사용 하 여 프로젝트를 Spark**합니다.

   b. 에 **빌드 도구** 목록에서 필요에 따라 다음 중 하나를 선택 합니다.

      * **Maven**, Scala 프로젝트 생성 마법사 지원
      * **SBT**, 종속성 관리 및 Scala 프로젝트에 대 한 빌드에 대 한

    ![새 프로젝트 대화 상자](./media/spark-submit-job-intellij-tool-plugin/create-hdi-scala-app.png)

2. **다음**을 선택합니다.

3. Scala 프로젝트 생성 마법사는 Scala 플러그 인을 설치 했으므로 했는지 여부를 자동으로 검색 합니다. **설치**를 선택합니다.

   ![Scala 플러그 인 확인](./media/spark-submit-job-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. Scala 플러그 인을 다운로드 하려면 **확인**합니다. IntelliJ를 다시 시작 하는 지침을 따릅니다. 

   ![Scala 플러그 인 설치 대화 상자](./media/spark-submit-job-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. 에 **새 프로젝트** 창에서 다음 단계를 수행 합니다.  

    ![Spark SDK 선택](./media/spark-submit-job-intellij-tool-plugin/hdi-new-project.png)

   a. 프로젝트 이름과 위치를 입력 합니다.

   b. 에 **프로젝트 SDK** 드롭 다운 목록에서 **Java 1.8** Spark 2.x 클러스터에 선택 **Java 1.7** Spark 1.x 클러스터에 대 한 합니다.

   다. 에 **Spark 버전** 드롭 다운 목록에서 Scala 프로젝트 생성 마법사는 Spark SDK 및 Scala SDK에 대 한 적절 한 버전을 통합 합니다. Spark 클러스터 버전을 2.0 보다 이전 이면 선택 **Spark 1.x**합니다. 선택이 고, 그렇지 **spark 2.x**합니다. 이 예제에서는 **Spark (Scala 2.11.8) 2.0.2**합니다.

6. **마침**을 선택합니다.

7. Spark 프로젝트가 자동으로를 아티팩트를 만듭니다. 아티팩트를 보려면 다음 단계를 수행 합니다.

   a. 에 **파일** 메뉴에서 **프로젝트 구조**합니다.

   b. 에 **프로젝트 구조** 대화 상자에서 **아티팩트** 만들어지는 기본 아티팩트를 볼 수 있습니다. 더하기 기호를 선택 하 여 사용자 고유의 아티팩트를 만들 수도 있습니다 (**+**).

      ![대화 상자의 아티팩트 정보](./media/spark-submit-job-intellij-tool-plugin/default-artifact.png)
      

## <a name="submit-application-to-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터에 응용 프로그램 제출
SQL Server 빅 데이터 클러스터 링크 후 응용 프로그램을 제출할 수 있습니다.

1. 구성을 설정 **실행/디버그 구성** + 창 클릭->**SQL Server에서 Apache Spark**를 선택 탭 **클러스터에서 원격으로 실행**, 매개 변수를 설정 합니다. 에서는 다음 확인을 클릭 합니다.

    ![구성 항목을 추가 하는 대화형 콘솔](./media/spark-submit-job-intellij-tool-plugin/interactive-console-add-config-entry.png)

    ![빅 데이터 클러스터 구성 링크](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-config.png)

    * 에 대 한 **Spark 클러스터 (Linux 전용)**, 응용 프로그램을 실행 하려는 클러스터를 선택 합니다.

    * IntelliJ 프로젝트에서 아티팩트를 선택 하거나 하드 드라이브에서 선택 합니다.

    * **기본 클래스 이름을** 필드: 기본값은 선택한 파일에서 주 클래스입니다. 줄임표를 선택 하 여 클래스를 변경할 수 있습니다 (**...** ) 하 고 다른 클래스를 선택 합니다.   

    * **작업 구성** 필드:  기본 값은 위에 표시 된 그림으로 설정 됩니다. 값을 변경 하거나 작업 제출을 위해 새로운 키/값을 추가할 수 있습니다. 추가 정보 [Apache Livy REST API](http://livy.incubator.apache.org./docs/latest/rest-api.html)

      ![Spark 제출 대화 상자 작업 구성 의미](./media/spark-submit-job-intellij-tool-plugin/submit-job-configurations.png)

    * **명령줄 인수** 필드: 필요한 경우 기본 클래스에 대 한 공백으로 분할 인수 값을 입력할 수 있습니다.

    * **Jar를 참조** 하 고 **파일 참조** 필드: 있는 경우 참조 된 Jar 및 파일에 대 한 경로 입력할 수 있습니다. 추가 정보 [Apache Spark 구성](https://spark.apache.org/docs/latest/configuration.html#runtime-environment) 

      ![즉 Spark 제출 대화 상자 jar 파일](./media/spark-submit-job-intellij-tool-plugin/jar-files-meaning.png)

       > [!NOTE]  
       > 파일 참조 하 고 참조 된 Jar을 업로드 하려면를 참조 하세요. [클러스터 리소스를 업로드 하는 방법](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-storage-explorer)
                         
    * **업로드 경로**: Jar 또는 Scala 프로젝트 리소스 제출에 대 한 저장소 위치를 지정할 수 있습니다. 지원 되는 여러 가지 저장소 유형이 있습니다. **Spark 대화형 세션을 사용 하 여 업로드할** 고 **업로드를 사용 하 여 WebHDFS**
    
2. 클릭 **SparkJobRun** 프로젝트는 선택한 클러스터에 제출 합니다. 합니다 **클러스터에서 Spark 작업을 원격** 탭 맨 아래에서 작업 실행 진행률을 표시 합니다. 빨간색 단추를 클릭 하 여 응용 프로그램을 중지할 수 있습니다.  

    ![링크 빅 데이터 클러스터 실행](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-run.png)

## <a name="spark-console"></a>Spark 콘솔
로컬 Console(Scala) Spark를 실행 하거나 Spark Livy 대화형 세션 Console(Scala)를 실행할 수 있습니다.

### <a name="spark-local-consolescala"></a>로컬 Console(Scala) spark
WINUTILS 충족 확인 합니다. EXE 필수 구성 요소입니다.

1. 메뉴 모음에서로 이동 **실행할** > **구성 편집...** .

2. **실행/디버그 구성** 창의 왼쪽된 창에서 이동할 **SQL Server 빅 데이터 클러스터에서 Apache Spark** > **[Spark SQL에서] myApp**합니다.

3. 주 창에서 선택 합니다 **로컬로 실행** 탭 합니다.

4. 다음 값을 제공 하 고 선택한 **확인**:

    |속성 |값 |
    |----|----|
    |작업 기본 클래스|기본값은 선택한 파일에서 주 클래스입니다. 줄임표를 선택 하 여 클래스를 변경할 수 있습니다 (**...** ) 하 고 다른 클래스를 선택 합니다.|
    |환경 변수|HADOOP_HOME에 대 한 값이 올바른지 확인 합니다.|
    |WINUTILS.exe 위치|경로가 올바른지 확인 합니다.|

    ![로컬 콘솔 설정 구성](./media/spark-submit-job-intellij-tool-plugin/console-set-configuration.png)

5. 프로젝트에서로 이동 **myApp** > **src** > **주** > **scala**  >  **myApp**합니다.  

6. 메뉴 모음에서로 이동 **도구가** > **Spark 콘솔** > **Spark 로컬 실행 Console(Scala)** 합니다.

7. 다음 두 개의 대화 상자가 자동으로 하려는 경우 종속성을 해결 하기 표시 될 수 있습니다. 만약 그렇다면 선택 **자동 수정**합니다.

    ![Spark 자동 Fix1](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix1.png)

    ![Spark 자동 Fix2](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix2.png)

8. 콘솔을 아래 그림과 유사 합니다. 콘솔 창 입력에서 `sc.appName`, ctrl + Enter를 누릅니다.  결과 나타납니다. 빨간색 단추를 클릭 하 여 로컬 콘솔을 종료할 수 있습니다.

    ![로컬 콘솔 결과](./media/spark-submit-job-intellij-tool-plugin/local-console-result.png)


### <a name="spark-livy-interactive-session-consolescala"></a>Livy 대화형 세션 Console(Scala) spark
Spark Livy 대화형 세션 Console(Scala) IntelliJ 2018.2 2018.3에만 지원 됩니다.

1. 메뉴 모음에서로 이동 **실행할** > **구성 편집...** .

2. **실행/디버그 구성** 창의 왼쪽된 창에서 이동할 **SQL Server 빅 데이터 클러스터에서 Apache Spark** > **[Spark SQL에서] myApp**합니다.

3. 주 창에서 선택 합니다 **클러스터에서 원격으로 실행** 탭 합니다.

4. 다음 값을 제공 하 고 선택한 **확인**:

    |속성 |값 |
    |----|----|
    |Spark 클러스터 (Linux 전용)|응용 프로그램을 실행 하려는 SQL Server에 대 한 빅 데이터 클러스터를 선택 합니다.|
    |주 클래스 이름|기본값은 선택한 파일에서 주 클래스입니다. 줄임표를 선택 하 여 클래스를 변경할 수 있습니다 (**...** ) 하 고 다른 클래스를 선택 합니다.|

    ![대화형 콘솔 설정 구성](./media/spark-submit-job-intellij-tool-plugin/interactive-console-configuration.png)

5. 프로젝트에서로 이동 **myApp** > **src** > **주** > **scala**  >  **myApp**합니다.  

6. 메뉴 모음에서로 이동 **도구가** > **Spark 콘솔** > **실행 Spark Livy 대화형 세션 Console(Scala)** 합니다.

7. 콘솔을 아래 그림과 유사 합니다. 콘솔 창 입력에서 `sc.appName`, ctrl + Enter를 누릅니다.  결과 나타납니다. 빨간색 단추를 클릭 하 여 로컬 콘솔을 종료할 수 있습니다.

    ![대화형 콘솔 결과](./media/spark-submit-job-intellij-tool-plugin/interactive-console-result.png)

### <a name="send-selection-to-spark-console"></a>선택 영역을 Spark 콘솔 보내기

편의 위해 Livy 대화형 세션 Console(Scala) 로컬 콘솔에 일부 코드를 전송 하 여 스크립트 결과 볼 수 있습니다. Scala 파일에 일부 코드를 강조 표시 한 다음 마우스 오른쪽 단추로 클릭 수 **Spark 콘솔 선택 보낼**합니다. 선택한 코드를 콘솔에 전송 되 고 수행할 수 있습니다. 콘솔의 코드 결과 표시 됩니다. 기존 콘솔은 오류를 확인 합니다.  

   ![선택 영역을 Spark 콘솔 보내기](./media/spark-submit-job-intellij-tool-plugin/send-selection-to-console.png)

## <a name="next-steps"></a>다음 단계
SQL Server 빅 데이터 클러스터 및 관련된 시나리오에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 빅 데이터 클러스터 이란](big-data-cluster-overview.md)?

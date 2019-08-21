---
title: SQL Server 빅 데이터 클러스터의 Azure Toolkit for IntelliJ에서 Spark 작업 실행
titleSuffix: SQL Server big data clusters
description: Azure Toolkit for IntelliJ의 SQL Server 빅 데이터 클러스터에 Spark 작업 제출
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 59946731dc1e76716b6202dd6f8aa93d777986b3
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653713"
---
# <a name="submit-spark-jobs-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-in-intellij"></a>IntelliJ의에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] Spark 작업 제출

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

의 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 주요 시나리오 중 하나는 Spark 작업을 제출 하는 기능입니다. Spark 작업 제출 기능을 사용 하면에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]대 한 참조가 있는 로컬 Jar 또는 Py 파일을 제출할 수 있습니다. 또한 HDFS 파일 시스템에 이미 있는 Jar 또는 Py 파일을 실행할 수 있습니다. 

## <a name="prerequisites"></a>사전 요구 사항

- SQL Server 빅 데이터 클러스터
- Oracle Java Development Kit. [Oracle 웹 사이트](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에서 설치할 수 있습니다.
- IntelliJ IDEA. [JetBrains 웹 사이트](https://www.jetbrains.com/idea/download/)에서 설치할 수 있습니다.
- Azure Toolkit for IntelliJ 확장. 설치 지침은 [Azure Toolkit for IntelliJ 설치](https://docs.microsoft.com/azure/azure-toolkit-for-intellij-installation)를 참조하세요.

## <a name="link-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터 연결
1. IntelliJ IDEA 도구를 엽니다.

2. 자체 서명된 인증서를 사용하는 경우 **도구** 메뉴에서 SSL 인증서 유효성 검사를 사용하지 않도록 설정하고 **Azure**, **Spark 클러스터 SSL 인증서 유효성 검사**를 선택한 후 **사용 안 함**을 선택합니다.

    ![SQL Server 빅 데이터 클러스터 연결 - SSL 사용 안 함](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-disableSSL.png)

3. **보기** 메뉴에서 Azure Explorer를 열고 **도구 창**을 선택한 후 **Azure Explorer**를 선택합니다.
4. **SQL Server 빅 데이터 클러스터**를 마우스 오른쪽 단추로 클릭하고 **SQL Server 빅 데이터 클러스터 연결**을 선택합니다. **서버**, **사용자 이름** 및 **암호**를 입력한 다음, **확인**을 클릭합니다.

    ![빅 데이터 클러스터 연결 - 대화 상자](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-dialog.png)

5. 신뢰할 수 없는 서버의 인증서 대화 상자가 나타나면 **허용**을 클릭합니다. 나중에 인증서를 관리할 수 있습니다 [서버 인증서](https://www.jetbrains.com/help/idea/settings-tools-server-certificates.html)를 참조하세요.

6. **SQL Server 빅 데이터 클러스터** 아래에 연결된 클러스터가 표시됩니다. Spark 기록 UI 및 Yarn UI를 열어 spark 작업을 모니터링하고, 클러스터를 마우스 오른쪽 단추로 클릭하여 연결을 끊을 수도 있습니다.

    ![빅 데이터 클러스터 연결 - 상황에 맞는 메뉴](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-contextmenu.png)

## <a name="create-a-spark-scala-application-from-spark-template"></a>Spark 템플릿에서 Spark Scala 애플리케이션 만들기

1. IntelliJ IDEA를 시작하고 프로젝트를 만듭니다. **새 프로젝트** 대화 상자에서 아래 단계를 수행합니다. 

   a. **Azure Spark/HDInsight** > **Spark 프로젝트(샘플 포함)(Scala)** 를 선택합니다.

   b. **빌드 도구** 목록에서 필요에 따라 다음 중 하나를 선택합니다.

      * **Maven**: Scala 프로젝트 만들기 마법사 지원
      * **SBT**: Scala 프로젝트에 대해 종속성 관리 및 빌드 수행

    ![새 프로젝트 대화 상자](./media/spark-submit-job-intellij-tool-plugin/create-hdi-scala-app.png)

2. **다음**을 선택합니다.

3. Scala 프로젝트 만들기 마법사는 Scala 플러그 인을 설치했는지 여부를 자동으로 감지합니다. **설치**를 선택합니다.

   ![Scala 플러그 인 검사](./media/spark-submit-job-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. Scala 플러그 인을 다운로드하려면 **확인**을 선택합니다. 지침에 따라 IntelliJ를 다시 시작합니다. 

   ![Scala 플러그 인 설치 대화 상자](./media/spark-submit-job-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. **새 프로젝트** 창에서 다음 단계를 수행합니다.  

    ![Spark SDK 선택](./media/spark-submit-job-intellij-tool-plugin/hdi-new-project.png)

   a. 프로젝트 이름 및 위치를 입력합니다.

   b. **프로젝트 SDK** 드롭다운 목록에서 Spark 2.x 클러스터에 대해 **Java 1.8**을 선택하거나 Spark 1.x 클러스터에 대해 **Java 1.7**을 선택합니다.

   c. **Spark 버전** 드롭다운 목록에서 Scala 프로젝트 만들기 마법사는 적절한 버전의 Spark SDK 및 Scala SDK를 연결합니다. Spark 클러스터 버전이 2.0 이전인 경우 **Spark 1.x**를 선택합니다. 그렇지 않으면 **Spark2.x**를 선택합니다. 이 예제에서는 **Spark 2.0.2(Scala 2.11.8)** 를 사용합니다.

6. **마침**을 선택합니다.

7. Spark 프로젝트가 자동으로 아티팩트를 만듭니다. 아티팩트를 보려면 다음 단계를 수행합니다.

   a. **파일** 메뉴에서 **프로젝트 구조**를 선택합니다.

   b. **프로젝트 구조** 대화 상자에서 **아티팩트**를 선택하여 만든 기본 아티팩트를 봅니다. 더하기 기호( **+** )를 선택하여 사용자 고유의 아티팩트를 만들 수도 있습니다.

      ![대화 상자의 아티팩트 정보](./media/spark-submit-job-intellij-tool-plugin/default-artifact.png)
      

## <a name="submit-application-to-sql-server-big-data-cluster"></a>애플리케이션을 SQL Server 빅 데이터 클러스터에 제출
SQL Server 빅 데이터 클러스터에 연결한 후 애플리케이션을 제출할 수 있습니다.

1. **실행/디버그 구성** 창에서 구성을 설정하고, +->**SQL Server의 Apache Spark**를 클릭한 후 **클러스터에서 원격으로 실행** 탭을 선택하고, 매개 변수를 다음과 같이 설정한 후 확인을 클릭합니다.

    ![대화형 콘솔 구성 항목 추가](./media/spark-submit-job-intellij-tool-plugin/interactive-console-add-config-entry.png)

    ![빅 데이터 클러스터 연결 - 구성](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-config.png)

    * **Spark 클러스터(Linux만 해당)** 의 경우 애플리케이션을 실행하려는 클러스터를 선택합니다.

    * IntelliJ 프로젝트에서 아티팩트를 선택하거나 하드 드라이브에서 아티팩트를 선택합니다.

    * **기본 클래스 이름** 필드: 기본값은 선택한 파일의 기본 클래스입니다. 줄임표( **...** )를 선택하고 다른 클래스를 선택하여 클래스를 변경할 수 있습니다.   

    * **작업 구성** 필드:  기본값은 위에 표시된 그림처럼 설정됩니다. 작업 제출을 위해 값을 변경하거나 새 키/값을 추가할 수 있습니다. 추가 정보 [Apache Livy REST API](http://livy.incubator.apache.org./docs/latest/rest-api.html)

      ![Spark 제출 대화 상자의 작업 구성 의미](./media/spark-submit-job-intellij-tool-plugin/submit-job-configurations.png)

    * **명령줄 인수** 필드: 필요한 경우 기본 클래스에 대해 공백으로 분할된 인수 값을 입력할 수 있습니다.

    * **참조되는 Jar** 및 **참조 파일** 필드: 참조되는 Jar 및 파일의 경로를 입력할 수 있습니다(있는 경우). 추가 정보 [Apache Spark 구성](https://spark.apache.org/docs/latest/configuration.html#runtime-environment) 

      ![Spark 제출 대화 상자 jar 파일 의미](./media/spark-submit-job-intellij-tool-plugin/jar-files-meaning.png)

       > [!NOTE]  
       > 참조되는 Jar 및 참조 파일을 업로드하려면 다음을 참조하세요. [클러스터에 리소스를 업로드하는 방법](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-storage-explorer)
                         
    * **업로드 경로**: Jar 또는 Scala 프로젝트 리소스 제출을 위한 스토리지 위치를 나타낼 수 있습니다. 지원되는 몇 가지 스토리지 유형은 다음과 같습니다. **Spark 대화형 세션을 사용하여 업로드** 및 **WebHDFS를 사용하여 업로드**
    
2. **SparkJobRun**을 클릭하여 선택한 클러스터에 프로젝트를 제출합니다. **클러스터의 원격 Spark 작업** 탭 아래쪽에는 작업 실행 진행률이 표시됩니다. 빨간색 단추를 클릭하여 애플리케이션을 중지할 수 있습니다.  

    ![빅 데이터 클러스터 연결 - 실행](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-run.png)

## <a name="spark-console"></a>Spark 콘솔
Spark 로컬 콘솔(Scala)을 실행하거나 Spark Livy 대화형 세션 콘솔(Scala)을 실행할 수 있습니다.

### <a name="spark-local-consolescala"></a>Spark 로컬 콘솔(Scala)
WINUTILS.EXE 필수 구성 요소를 충족하는지 확인합니다.

1. 메뉴 모음에서 **실행** > **구성 편집...** 으로 이동합니다.

2. **실행/디버그 구성** 창의 왼쪽 창에서 **SQL Server 빅 데이터 클러스터의 Apache Spark** >  **[SQL의 Spark] myApp**으로 이동합니다.

3. 주 창에서 **로컬 실행** 탭을 선택합니다.

4. 다음 값을 입력하고 **확인**을 선택합니다.

    |속성 |값 |
    |----|----|
    |작업 기본 클래스|기본값은 선택한 파일의 기본 클래스입니다. 줄임표( **...** )를 선택하고 다른 클래스를 선택하여 클래스를 변경할 수 있습니다.|
    |환경 변수|HADOOP_HOME의 값이 올바른지 확인합니다.|
    |WINUTILS.exe 위치|경로가 올바른지 확인합니다.|

    ![로컬 콘솔 구성 설정](./media/spark-submit-job-intellij-tool-plugin/console-set-configuration.png)

5. 프로젝트에서 **myApp** > **src** > **main** > **scala** > **myApp**으로 이동합니다.  

6. 메뉴 모음에서 **도구** > **Spark 콘솔** > **Spark 로컬 콘솔(Scala) 실행**으로 이동합니다.

7. 그러면 종속성을 자동으로 수정할 것인지 묻는 두 개의 대화 상자가 표시될 수 있습니다. 자동으로 수정하려면 **자동 수정**을 선택합니다.

    ![Spark 자동 수정1](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix1.png)

    ![Spark 자동 수정2](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix2.png)

8. 콘솔은 아래 그림과 같이 표시됩니다. 콘솔 창에서 `sc.appName`을 입력한 다음, Ctrl+Enter를 누릅니다.  결과가 표시됩니다. 빨간색 단추를 클릭하여 로컬 콘솔을 종료할 수 있습니다.

    ![로컬 콘솔 결과](./media/spark-submit-job-intellij-tool-plugin/local-console-result.png)


### <a name="spark-livy-interactive-session-consolescala"></a>Spark Livy 대화형 세션 콘솔(Scala)
Spark Livy 대화형 세션 콘솔(Scala)은 IntelliJ 2018.2 및 2018.3에서만 지원됩니다.

1. 메뉴 모음에서 **실행** > **구성 편집...** 으로 이동합니다.

2. **실행/디버그 구성** 창의 왼쪽 창에서 **SQL Server 빅 데이터 클러스터의 Apache Spark** >  **[SQL의 Spark] myApp**으로 이동합니다.

3. 주 창에서 **클러스터에서 원격으로 실행** 탭을 선택합니다.

4. 다음 값을 입력하고 **확인**을 선택합니다.

    |속성 |값 |
    |----|----|
    |Spark 클러스터(Linux만 해당)|애플리케이션을 실행하려는 SQL Server 빅 데이터 클러스터를 선택합니다.|
    |주 클래스 이름|기본값은 선택한 파일의 기본 클래스입니다. 줄임표( **...** )를 선택하고 다른 클래스를 선택하여 클래스를 변경할 수 있습니다.|

    ![대화형 콘솔 구성 설정](./media/spark-submit-job-intellij-tool-plugin/interactive-console-configuration.png)

5. 프로젝트에서 **myApp** > **src** > **main** > **scala** > **myApp**으로 이동합니다.  

6. 메뉴 모음에서 **도구** > **Spark 콘솔** > **Spark Livy 대화형 세션 콘솔(Scala)** 로 이동합니다.

7. 콘솔은 아래 그림과 같이 표시됩니다. 콘솔 창에서 `sc.appName`을 입력한 다음, Ctrl+Enter를 누릅니다.  결과가 표시됩니다. 빨간색 단추를 클릭하여 로컬 콘솔을 종료할 수 있습니다.

    ![대화형 콘솔 결과](./media/spark-submit-job-intellij-tool-plugin/interactive-console-result.png)

### <a name="send-selection-to-spark-console"></a>Spark 콘솔로 선택 내용 보내기

편의상 로컬 콘솔 또는 Livy Interactive Session Console(Scala)에 코드를 전송하여 스크립트 결과를 볼 수 있습니다. Scala 파일에서 일부 코드를 강조 표시한 다음, 마우스 오른쪽 단추로 **Spark 콘솔로 선택 내용 보내기**를 클릭합니다. 선택한 코드가 콘솔로 전송된 후 수행됩니다. 결과는 콘솔의 코드 뒤에 표시됩니다. 콘솔에서 오류가 발생했는지 확인합니다.  

   ![Spark 콘솔로 선택 내용 보내기](./media/spark-submit-job-intellij-tool-plugin/send-selection-to-console.png)

## <a name="next-steps"></a>다음 단계
SQL Server 빅 데이터 클러스터 및 관련 시나리오에 대 한 자세한 내용은 [무엇 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] ](big-data-cluster-overview.md)인가요?를 참조 하세요.

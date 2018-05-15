---
title: 변경 데이터의 준비 여부 확인 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],determining readiness
ms.assetid: 04935f35-96cc-4d70-a250-0fd326f8daff
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 325bd3ad9e274db6263d75e05e8f3117ea259e35
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="determine-whether-the-change-data-is-ready"></a>변경 데이터의 준비 여부 확인
  변경 데이터를 증분 로드하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 제어 흐름에서 두 번째 태스크는 선택한 간격에 대한 변경 데이터가 준비되었는지 확인하는 것입니다. 비동기 캡처 프로세스에서 선택한 끝점까지 변경 내용을 아직 다 처리하지 않았을 수 있기 때문에 이 단계가 필요합니다.  
  
> [!NOTE]  
>  제어 흐름에 대한 첫 번째 태스크는 변경 간격의 끝점을 계산하는 것입니다. 이 태스크에 대한 자세한 내용은 [변경 데이터의 간격 지정](../../integration-services/change-data-capture/specify-an-interval-of-change-data.md)을 참조하세요. 제어 흐름 디자인의 전체 프로세스에 대한 설명은 [데이터 캡처 변경&#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)을 참조하세요.  
  
## <a name="understanding-the-components-of-the-solution"></a>솔루션의 구성 요소 이해  
 이 항목에 설명된 솔루션에서는 다음과 같은 4개의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소를 사용합니다.  
  
-   SQL 실행 태스크의 출력을 반복적으로 평가하는 For 루프 컨테이너  
  
-   변경 데이터 캡처 프로세스에서 유지하는 특수 테이블을 쿼리한 다음 이 정보를 사용하여 데이터가 준비되었는지 여부를 확인하는 SQL 실행 태스크  
  
-   데이터가 준비되지 않았을 때 처리에서 지연을 구현하는 구성 요소. 이 구성 요소는 스크립트 태스크 또는 SQL 실행 태스크일 수 있습니다.  
  
-   SQL 실행 태스크에서 오류 또는 시간 초과 상태를 나타내는 값을 반환할 때 오류 또는 시간 초과를 보고하는 구성 요소(옵션)  
  
 이러한 구성 요소에서는 여러 패키지 변수의 값을 설정하거나 읽어 루프 내에서 그리고 나중에는 패키지에서 실행의 흐름을 제어합니다.  
  
#### <a name="to-set-up-package-variables"></a>패키지 변수를 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 **변수** 창에서 다음 변수를 만듭니다.  
  
    1.  SQL 실행 태스크에서 반환하는 상태 값을 보관할 integer 데이터 형식의 변수를 만듭니다.  
  
         이 예에서는 초기 값이 0인 변수 이름으로 DataReady를 사용합니다.  
  
    2.  데이터가 준비되지 않았을 때 지연할 시간을 보관할 변수를 만듭니다. 스크립트 태스크를 사용하여 지연을 구현하려는 경우 변수의 데이터 형식은 integer여야 합니다. WAITFOR 문이 있는 SQL 실행 태스크를 사용하려는 경우에는 "00:00:10"과 같은 값을 허용하기 위해 변수의 데이터 형식이 string이어야 합니다.  
  
         이 예에서는 초기 값이 10인 변수 이름으로 DelaySeconds를 사용합니다.  
  
    3.  루프의 현재 반복을 보관할 integer 데이터 형식의 변수를 만듭니다.  
  
         이 예에서는 초기 값이 0인 변수 이름으로 TimeoutCount를 사용합니다.  
  
    4.  시간 초과 상태를 보고하기 전에 루프에서 데이터를 테스트해야 하는 횟수를 지정하는 integer 데이터 형식의 변수를 만듭니다.  
  
         이 예에서는 초기 값이 20인 변수 이름으로 TimeoutCeiling을 사용합니다.  
  
    5.  (옵션) 변경 데이터의 첫 번째 로드를 나타내는 데 사용할 수 있는 integer 데이터 형식의 변수를 만듭니다.  
  
         이 예에서는 변수 이름으로 IntervalID를 사용하고 값 0만 검사하여 초기 로드를 나타냅니다.  
  
## <a name="configuring-a-for-loop-container"></a>For 루프 컨테이너 구성  
 변수가 설정되면 For 루프 컨테이너를 첫 번째 구성 요소로 추가합니다.  
  
#### <a name="to-configure-a-for-loop-container-to-wait-until-change-data-is-ready"></a>변경 데이터가 준비될 때까지 대기하도록 For 루프 컨테이너를 구성하려면  
  
1.  **디자이너의** 제어 흐름 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 탭에서 제어 흐름에 For 루프 컨테이너를 추가합니다.  
  
2.  간격의 끝점을 계산하는 SQL 실행 태스크를 For 루프 컨테이너에 연결합니다.  
  
3.  **For 루프 편집기**에서 다음 옵션을 선택합니다.  
  
    1.  **InitExpression**에 `@DataReady = 0`을 입력합니다.  
  
         이 식은 루프 변수의 초기 값을 설정합니다.  
  
    2.  **EvalExpression**에 `@DataReady == 0`을 입력합니다.  
  
         이 식이 **False**로 평가되면 실행이 루프 밖으로 전달되고 증분 로드가 시작됩니다.  
  
## <a name="configuring-the-execute-sql-task-that-queries-for-change-data"></a>변경 데이터를 쿼리하는 SQL 실행 태스크 구성  
 For 루프 컨테이너 내에서 SQL 실행 태스크를 추가합니다. 이 태스크는 변경 데이터 캡처 프로세스에서 데이터베이스에 유지하는 테이블을 쿼리합니다. 이 쿼리의 결과는 변경 데이터가 준비되었는지 여부를 나타내는 상태 값입니다.  
  
 다음 표에서 첫 번째 열은 샘플 Transact-SQL 쿼리에 의해 SQL 실행 태스크에서 반환되는 값을 보여 줍니다. 두 번째 열은 다른 구성 요소에서 이러한 값에 응답하는 방식을 보여 줍니다.  
  
|반환 값|의미|응답|  
|------------------|-------------|--------------|  
|0|변경 데이터가 준비되지 않았음을 나타냅니다.<br /><br /> 선택한 간격의 끝 지점 뒤에 오는 변경 데이터 캡처 레코드가 없습니다.|지연을 구현하는 구성 요소에서 실행이 계속됩니다. 그런 다음 제어가 For 루프 컨테이너로 반환되어 반환되는 값이 0인 한 SQL 실행 태스크가 계속 검사됩니다.|  
|1|변경 데이터가 전체 간격에 대해 캡처되지 않았거나 삭제되었음을 나타낼 수 있습니다. 이는 오류 상태로 처리됩니다.<br /><br /> 선택한 간격의 시작 지점 앞에 오는 변경 데이터 캡처 레코드가 없습니다.|오류를 기록하는 선택적 구성 요소에서 실행이 계속됩니다.|  
|2|데이터가 준비되었음을 나타냅니다.<br /><br /> 선택한 간격의 시작 지점 앞에 오고 끝 지점 뒤에 오는 변경 데이터 캡처 레코드가 모두 있습니다.|실행이 For 루프 밖으로 전달되고 증분 로드가 시작됩니다.|  
|3|사용 가능한 모든 변경 데이터의 초기 로드를 나타냅니다.<br /><br /> 조건부 논리는 이 용도로만 사용되는 특수 패키지 변수에서 이 값을 가져옵니다.|실행이 For 루프 밖으로 전달되고 증분 로드가 시작됩니다.|  
|5|TimeoutCeiling에 도달했음을 나타냅니다.<br /><br /> 루프에서 지정한 횟수만큼 데이터를 테스트했으며 데이터를 여전히 사용할 수 없습니다. 이 테스트나 유사한 테스트를 사용하지 않으면 패키지가 무기한 실행될 수 있습니다.|시간 초과를 기록하는 선택적 구성 요소에서 실행이 계속됩니다.|  
  
#### <a name="to-configure-an-execute-sql-task-to-query-whether-change-data-is-ready"></a>변경 데이터가 준비되었는지 여부를 쿼리하는 SQL 실행 태스크를 구성하려면  
  
1.  For 루프 컨테이너 내에서 SQL 실행 태스크를 추가합니다.  
  
2.  **SQL 실행 태스크 편집기**의 **일반** 페이지에서 다음 옵션을 선택합니다.  
  
    1.  **ResultSet**에 **단일 행**을 선택합니다.  
  
    2.  원본 데이터베이스에 대한 올바른 연결을 구성합니다.  
  
    3.  **SQLSourceType**에 **직접 입력**을 선택합니다.  
  
    4.  **SQLStatement**에 다음 SQL 문을 입력합니다.  
  
        ```  
        declare @DataReady int, @TimeoutCount int  
  
        if not exists (select tran_end_time from cdc.lsn_time_mapping  
                where tran_end_time > ?  )  
            select @DataReady = 0  
        else  
            if ? = 0  
                select @DataReady = 3   
        else  
            if not exists (select tran_end_time from cdc.lsn_time_mapping  
                    where tran_end_time <= ? )  
                select @DataReady = 1   
        else  
            select @DataReady = 2  
  
        select @TimeoutCount = ?  
        if (@DataReady = 0)  
            select @TimeoutCount = @TimeoutCount + 1  
        else  
            select @TimeoutCount = 0  
  
        if (@TimeoutCount > ?)  
            select @DataReady = 5  
  
        select @DataReady as DataReady, @TimeoutCount as TimeoutCount  
  
        ```  
  
3.  **SQL 실행 태스크 편집기** 의 **매개 변수 매핑**페이지에서 다음 매핑을 만듭니다.  
  
    1.  ExtractEndTime 변수를 매개 변수 0에 매핑합니다.  
  
    2.  IntervalID 변수를 매개 변수 1에 매핑합니다.  
  
    3.  ExtractStartTime 변수를 매개 변수 2에 매핑합니다.  
  
    4.  TimeoutCount 변수를 매개 변수 3에 매핑합니다.  
  
    5.  TimeoutCeiling 변수를 매개 변수 4에 매핑합니다.  
  
4.  **SQL 실행 태스크 편집기** 의 **결과 집합**페이지에서 DataReady 결과를 DataReady 변수에 매핑하고 TimeoutCount 결과를 TimeoutCount 변수에 매핑합니다.  
  
## <a name="waiting-until-the-change-data-is-ready"></a>변경 데이터가 준비될 때까지 대기  
 변경 데이터가 준비되지 않은 경우 지연을 구현하는 여러 가지 방법 중 하나를 사용할 수 있습니다. 다음 두 절차에서는 스크립트 태스크나 SQL 실행 태스크를 사용하여 지연을 구현하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  미리 컴파일된 스크립트는 SQL 실행 태스크보다 적은 오버헤드를 발생시킵니다.  
  
#### <a name="to-implement-a-delay-by-using-a-script-task"></a>스크립트 태스크를 사용하여 지연을 구현하려면  
  
1.  For 루프 컨테이너 내에서 스크립트 태스크를 추가합니다.  
  
2.  변경 데이터가 준비되었는지 여부를 확인하기 위해 쿼리하는 SQL 실행 태스크를 새 스크립트 태스크에 연결합니다.  
  
3.  SQL 실행 태스크를 스크립트 태스크에 연결하는 선행 제약 조건을 위해 **선행 제약 조건 편집기** 를 열고 다음 옵션을 선택합니다.  
  
    1.  **평가 작업**에 **식 및 제약 조건**을 선택합니다.  
  
    2.  **값**에 **성공**을 선택합니다.  
  
         **성공** 의 제약 조건 값은 이전 태스크의 성공을 참조합니다. 이 경우에는 SQL 실행 태스크의 성공입니다.  
  
    3.  **식**에 `@DataReady == 0 && @TimeoutCount <= @TimeoutCeiling`를 입력합니다.  
  
    4.  **논리적 AND. 모든 제약 조건이 True가 되어야 합니다**가 선택되지 않은 경우 이 옵션을 선택합니다.  
  
4.  **스크립트 태스크 편집기**의 **스크립트** 페이지에 있는 **ReadOnlyVariables**에 대해 목록에서 **User::DelaySeconds** 정수 변수를 선택합니다.  
  
5.  **스크립트 태스크 편집기**의 **스크립트** 페이지에서 **스크립트 편집** 을 클릭하여 스크립트 개발 환경을 엽니다.  
  
6.  Main 프로시저에 다음 코드 행 중 하나를 입력합니다.  
  
    -   C#에서 프로그래밍하는 경우 다음 코드 행을 입력합니다.  
  
        ```  
        System.Threading.Thread.Sleep((int)Dts.Variables["DelaySeconds"].Value * 1000);  
        ```  
  
         \- 또는-  
  
    -   [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]에서 프로그래밍하는 경우 다음 코드 행을 입력합니다.  
  
        ```  
        System.Threading.Thread.Sleep(Ctype(Dts.Variables("DelaySeconds").Value, Integer) * 1000)  
  
        ```  
  
        > [!NOTE]  
        >  **Thread.Sleep** 메서드는 밀리초 단위로 지정된 인수를 필요로 합니다.  
  
7.  스크립트 실행에서 **DtsExecResult.Success** 를 반환하는 기본 코드 행을 그대로 둡니다.  
  
8.  스크립트 개발 환경 및 **스크립트 태스크 편집기**를 닫습니다.  
  
#### <a name="to-implement-a-delay-by-using-an-execute-sql-task"></a>SQL 실행 태스크를 사용하여 지연을 구현하려면  
  
1.  For 루프 컨테이너 내에서 SQL 실행 태스크를 추가합니다.  
  
2.  변경 데이터가 준비되었는지 여부를 확인하기 위해 쿼리하는 SQL 실행 태스크를 새 SQL 실행 태스크에 연결합니다.  
  
3.  두 SQL 실행 태스크를 연결하는 선행 제약 조건을 위해 **선행 제약 조건 편집기** 를 열고 다음 옵션을 선택합니다.  
  
    1.  **평가 작업**에 **식 및 제약 조건**을 선택합니다.  
  
    2.  **값**에 **성공**을 선택합니다.  
  
         **성공** 의 제약 조건 값은 이전 SQL 실행 태스크의 성공을 참조합니다.  
  
    3.  **식**에 `@DataReady == 0`를 입력합니다.  
  
    4.  **논리적 AND. 모든 제약 조건이 True가 되어야 합니다**가 선택되지 않은 경우 이 옵션을 선택합니다.  
  
         이 옵션을 선택하려면 두 가지 조건인 제약 조건과 식이 모두 true여야 합니다.  
  
4.  **SQL 실행 태스크 편집기**의 **일반** 페이지에서 다음 옵션을 선택합니다.  
  
    1.  **ResultSet**에 **단일 행**을 선택합니다.  
  
    2.  원본 데이터베이스에 대한 올바른 연결을 구성합니다.  
  
    3.  **SQLSourceType**에 **직접 입력**을 선택합니다.  
  
    4.  **SQLStatement**에 다음 SQL 문을 입력합니다.  
  
        ```  
        WAITFOR DELAY ?  
  
        ```  
  
5.  편집기의 **매개 변수 매핑** 페이지에서 DelaySeconds 문자열 변수를 매개 변수 0에 매핑합니다.  
  
## <a name="handling-an-error-condition"></a>오류 상태 처리  
 루프 내에 추가 구성 요소를 구성하여 오류 또는 시간 초과 상태를 기록할 수도 있습니다.  
  
-   DataReady 변수 값이 1인 경우 이 구성 요소가 오류 상태를 기록할 수 있습니다. 이 값은 선택한 간격 시작 전에 사용 가능한 변경 데이터가 없음을 나타냅니다.  
  
-   TimeoutCeiling 변수 값에 도달할 경우 이 구성 요소는 시간 초과 상태를 기록할 수도 있습니다. 이 값은 루프에서 지정한 횟수만큼 데이터를 테스트했으며 데이터를 여전히 사용할 수 없음을 나타냅니다. 이 테스트나 유사한 테스트를 사용하지 않으면 패키지가 무기한 실행될 수 있습니다.  
  
#### <a name="to-configure-an-optional-script-task-to-log-an-error-condition"></a>오류 상태를 기록하는 선택적 스크립트 태스크를 구성하려면  
  
1.  로그에 메시지를 기록하여 오류 또는 시간 초과를 보고하려는 경우 패키지에 대한 로깅을 구성합니다. 자세한 내용은 [SQL Server Data Tools에서 패키지 로깅 사용](../../integration-services/performance/integration-services-ssis-logging.md#ssdt)을 참조하세요.  
  
2.  For 루프 컨테이너 내에서 스크립트 태스크를 추가합니다.  
  
3.  변경 데이터가 준비되었는지 여부를 확인하기 위해 쿼리하는 SQL 실행 태스크를 새 스크립트 태스크에 연결합니다.  
  
4.  SQL 실행 태스크를 스크립트 태스크에 연결하는 선행 제약 조건을 위해 **선행 제약 조건 편집기** 를 열고 다음 옵션을 선택합니다.  
  
    1.  **평가 작업**에 **식 및 제약 조건**을 선택합니다.  
  
    2.  **값**에 **성공**을 선택합니다.  
  
         **성공** 의 제약 조건 값은 이전 태스크의 성공을 참조합니다. 이 경우에는 SQL 실행 태스크의 성공입니다.  
  
    3.  **식**에 `@DataReady == 1 || @DataReady == 5`를 입력합니다.  
  
    4.  **논리적 AND. 모든 제약 조건이 True가 되어야 합니다**가 선택되지 않은 경우 이 옵션을 선택합니다.  
  
         이 옵션을 선택하려면 두 가지 조건인 제약 조건과 식이 모두 true여야 합니다.  
  
5.  **스크립트 태스크 편집기**에서 편집기의 **스크립트** 페이지에 있는 **ReadOnlyVariables**에 대해 목록에서 **User::DataReady** 및 **User::ExtractStartTime** 을 선택하여 해당 값을 스크립트에 사용할 수 있도록 합니다.  
  
     로그에 기록하는 정보에 특정 시스템 변수(예: System::PackageName)의 정보를 포함하려는 경우 해당 변수도 선택합니다.  
  
6.  **스크립트 태스크 편집기**의 **스크립트** 페이지에서 **스크립트 편집** 을 클릭하여 스크립트 개발 환경을 엽니다.  
  
7.  Main 프로시저에 **Dts.Log** 메서드를 호출하여 오류를 기록하거나 **Dts.Events** 인터페이스의 메서드 중 하나를 호출하여 이벤트를 발생시키는 코드를 입력합니다. `Dts.TaskResult = Dts.Results.Failure`를 반환하여 패키지에 오류를 알립니다.  
  
     다음 샘플에서는 로그에 메시지를 기록하는 방법을 보여 줍니다. 자세한 내용은 [Logging in the Script Task](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md), [Raising Events in the Script Task](../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)및 [Returning Results from the Script Task](../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md)을 참조하세요.  
  
    ```  
    ' User variables.  
    Dim dataReady As Integer = _  
      CType(Dts.Variables("DataReady").Value, Integer)  
    Dim extractStartTime As Date = _  
      CType(Dts.Variables("ExtractStartTime").Value, DateTime)  
  
    ' System variables.  
    Dim packageName As String = _  
      Dts.Variables("PackageName").Value.ToString()  
    Dim executionStartTime As Date = _  
      CType(Dts.Variables("StartTime").Value, DateTime)  
  
    Dim eventMessage As New System.Text.StringBuilder()  
  
    If dataReady = 1 OrElse dataReady = 5 Then  
  
      If dataReady = 1 Then  
        eventMessage.AppendLine("Start Time Error")  
      Else  
        eventMessage.AppendLine("Timeout Error")  
      End If  
  
      With eventMessage  
        .Append("The package ")  
        .Append(packageName)  
        .Append(" started at ")  
        .Append(executionStartTime.ToString())  
        .Append(" and ended at ")  
        .AppendLine(DateTime.Now().ToString())  
        If dataReady = 1 Then  
          .Append("The specified ExtractStartTime was ")  
          .AppendLine(extractStartTime.ToString())  
        End If  
      End With  
  
      System.Windows.Forms.MessageBox.Show(eventMessage.ToString())  
  
      Dts.Log(eventMessage.ToString(), 0, Nothing)  
  
      Dts.TaskResult = Dts.Results.Failure  
  
    Else  
  
      Dts.TaskResult = Dts.Results.Success  
  
    End If  
  
    ```  
  
8.  스크립트 개발 환경 및 **스크립트 태스크 편집기**를 닫습니다.  
  
## <a name="next-step"></a>다음 단계  
 변경 데이터가 준비되었는지 확인한 후 다음 단계는 변경 데이터에 대한 쿼리를 준비하는 것입니다.  
  
 **다음 항목:** [변경 데이터에 대한 쿼리 준비](../../integration-services/change-data-capture/prepare-to-query-for-the-change-data.md)  
  
  

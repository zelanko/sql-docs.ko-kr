---
title: 'Python 자습서: 데이터 탐색 및 시각화'
titleSuffix: SQL machine learning
description: SQL Machine Learning을 통해 Python에서 이진 분류를 사용할 준비 작업으로 샘플 데이터를 검토하고 몇 가지 플롯을 생성합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/29/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||>=azuresqldb-mi-current'
ms.openlocfilehash: 0f52df34bb04a94baf14076a9ea345712166ae5a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470324"
---
# <a name="python-tutorial-explore-and-visualize-data"></a>Python 자습서: 데이터 탐색 및 시각화
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

이 5부 자습서 시리즈의 2부에서는 샘플 데이터를 검토하고 몇 가지 플롯을 생성합니다. 그 다음에는 Python에서 그래픽 개체를 직렬화한 후, 개체를 역직렬화하고 플롯을 만드는 방법을 알아봅니다.

이 문서에서는 다음을 수행합니다.

> [!div class="checklist"]
> + 샘플 데이터 검토
> + T-SQL에서 Python을 사용하여 플롯 만들기

[1부](python-taxi-classification-introduction.md)에서는 사전 요구 사항을 설치하고 샘플 데이터베이스를 복원했습니다.

[3부](python-taxi-classification-create-features.md)에서는 Transact-SQL 함수를 사용하여 원시 데이터에서 기능을 만드는 방법을 알아봅니다. 그런 다음 저장 프로시저에서 해당 함수를 호출하여 기능 값이 포함된 테이블을 만듭니다.

[4부](python-taxi-classification-train-model.md)에서는 SQL Server 저장 프로시저를 통해 모듈을 로드하고 필요한 함수를 호출하여 모델을 만들고 학습시킵니다.

[5부](python-taxi-classification-deploy-model.md)에서는 4부에서 학습시키고 저장한 모델을 운영하는 방법을 알아봅니다.

## <a name="review-the-data"></a>데이터 검토

NYC 택시 데이터를 더 쉽게 사용할 수 있도록 몇 가지 항목이 변경되었으므로, 데이터 스키마를 먼저 찾아봅니다.

+ 원래 데이터 세트에는 택시 식별자 및 여정 레코드를 위해 개별 파일이 사용되었습니다. _medallion_, _hack_license_ 및 _pickup_datetime_ 열에 2개의 원본 데이터 세트가 조인되었습니다.  
+ 원본 데이터 세트는 여러 파일에 걸쳐 있고 크기가 상당히 컸습니다. 원래 레코드 수의 1%만 가져오도록 샘플링 크기를 줄였습니다. 현재 데이터 테이블에는 1,703,957개 행과 23개 열이 포함되어 있습니다.

**택시 식별자**

_medallion_ 열은 택시의 고유 ID 번호를 나타냅니다.

_hack_license_ 열은 택시 기사의 운전 면허 번호(익명)를 포함합니다.

**여정 및 요금 레코드**

각 여정 레코드에는 승하차 위치 및 시간과 여정 거리가 포함됩니다.

각 요금 레코드에는 지불 유형, 총 지불 금액, 팁 금액 등의 지불 정보가 포함됩니다.

마지막 세 열은 다양한 Machine Learning 작업에 사용할 수 있습니다.  _tip_amount_ 열에는 연속 숫자 값이 포함되며 회귀 분석의 **레이블** 열로 사용할 수 있습니다. _tipped_ 열에는 예/아니요 값만 포함되며 이진 분류에 사용됩니다. _tip_class_ 열에는 여러 개의 **클래스 레이블** 이 포함되므로 다중 클래스 분류 작업의 레이블로 사용할 수 있습니다.

레이블 열에 사용되는 값은 모두 다음과 같은 비즈니스 규칙을 사용하여 `tip_amount` 열을 기반으로 합니다.

+ 레이블 열 `tipped`에 포함될 수 있는 값은 0 및 1

    `tip_amount` > 0이면 `tipped` = 1이고, 그렇지 않으면 `tipped` = 0입니다.

+ 레이블 열 `tip_class`에 포함될 수 있는 값은 0-4

    클래스 0: `tip_amount` = $0

    클래스 1: `tip_amount` > $0 및 `tip_amount` <= $5
    
    클래스 2: `tip_amount` > $5 및 `tip_amount` <= $10
    
    클래스 3: `tip_amount` > $10 및 `tip_amount` <= $20
    
    클래스 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>T-SQL에서 Python을 사용하여 플롯 만들기

일반적으로 데이터 과학 솔루션 개발에는 데이터 탐색 및 데이터 시각화가 많이 포함됩니다. 시각화는 데이터와 이상값의 분포를 파악하는 데 강력한 도구이므로 Python에서는 데이터 시각화를 위한 여러 패키지를 제공합니다. **matplotlib** 모듈은 시각화를 위한 인기 있는 라이브러리 중 하나이며, 히스토그램, 산점도, 상자 그림 및 기타 데이터 탐색 그래프를 만들기 위한 여러 함수가 포함되어 있습니다.

이 섹션에서는 저장 프로시저를 사용하여 플롯 작업을 수행하는 방법을 알아봅니다. 서버에서 이미지를 여는 대신 Python 개체 `plot`을 **varbinary** 데이터로 저장한 후 다른 곳에서 공유하거나 확인할 수 있는 파일에 이를 기록합니다.

### <a name="create-a-plot-as-varbinary-data"></a>플롯을 varbinary 데이터로 만들기

저장 프로시저는 직렬화된 Python `figure` 개체를 **varbinary** 데이터의 스트림으로 반환합니다. 이진 데이터를 직접 볼 수 없지만, 클라이언트에서 Python 코드를 사용하여 역직렬화하고 숫자를 확인한 후 클라이언트 컴퓨터에 이미지 파일을 저장할 수 있습니다.

1. PowerShell 스크립트로 아직 저장 프로시저 **PyPlotMatplotlib** 가 만들어지지 않았으면, 만듭니다.

    - `@query` 변수는 스크립트 입력 변수 `@input_data_1`에 대한 인수로 Python 코드 블록에 전달되는 쿼리 텍스트 `SELECT tipped FROM nyctaxi_sample`을 정의합니다.
    - Python 스크립트는 상당히 단순합니다. 히스토그램 및 산점도를 만들기 위해 **matplotlib** `figure` 개체가 사용되고, 해당 개체는 `pickle` 라이브러리를 사용하여 직렬화됩니다.
    - Python 그래픽 개체는 출력의 **pandas** DataFrame으로 직렬화됩니다.
  
    ```sql
    DROP PROCEDURE IF EXISTS PyPlotMatplotlib;
    GO

    CREATE PROCEDURE [dbo].[PyPlotMatplotlib]
    AS
    BEGIN
        SET NOCOUNT ON;
        DECLARE @query nvarchar(max) =
        N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'
        EXECUTE sp_execute_external_script
        @language = N'Python',
        @script = N'
    import matplotlib
    matplotlib.use("Agg")
    import matplotlib.pyplot as plt
    import pandas as pd
    import pickle

    fig_handle = plt.figure()
    plt.hist(InputDataSet.tipped)
    plt.xlabel("Tipped")
    plt.ylabel("Counts")
    plt.title("Histogram, Tipped")
    plot0 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.tip_amount)
    plt.xlabel("Tip amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Tip amount")
    plot1 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.fare_amount)
    plt.xlabel("Fare amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Fare amount")
    plot2 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.scatter( InputDataSet.fare_amount, InputDataSet.tip_amount)
    plt.xlabel("Fare Amount ($)")
    plt.ylabel("Tip Amount ($)")
    plt.title("Tip amount by Fare amount")
    plot3 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    OutputDataSet = plot0.append(plot1, ignore_index=True).append(plot2, ignore_index=True).append(plot3, ignore_index=True)
    ',
    @input_data_1 = @query
    WITH RESULT SETS ((plot varbinary(max)))
    END
    GO
    ```

2. 이제 인수 없이 저장 프로시저를 실행하여 입력 쿼리로 하드 코딩된 데이터로부터 플롯을 생성합니다.

    ```sql
    EXEC [dbo].[PyPlotMatplotlib]
    ```

3. 결과가 다음과 같이 표시됩니다.
  
    ```sql
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

4. 이제 [Python 클라이언트](../python/setup-python-client-tools-sql.md)에서 이진 플롯 개체를 생성한 SQL Server 인스턴스에 연결하고 플롯을 볼 수 있습니다. 

    이렇게 하려면 다음 Python 코드를 실행하여 서버 이름, 데이터베이스 이름 및 자격 증명을 적절하게 바꿉니다. Windows 인증의 경우 `UID` 및 `PWD` 매개 변수를 `Trusted_Connection=True`로 바꿉니다. Python 버전이 클라이언트와 서버 모두 동일한지 확인합니다. 또한 클라이언트에서 Python 라이브러리(예: matplotlib)가 서버에 설치된 라이브러리 버전보다 높거나 같은지 확인합니다.
  
    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER=SQL Server;SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSWORD}')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

5. 연결이 성공하면 다음과 비슷한 메시지가 표시됩니다.
  
   *플롯이 다음 디렉터리에 저장됨: xxxx*
  
6. 출력 파일이 Python 작업 디렉터리에 생성됩니다. 플롯을 보려면 Python 작업 디렉터리를 찾아서 파일을 엽니다. 다음 이미지는 클라이언트 컴퓨터에 저장된 플롯을 보여줍니다.
  
   ![팁 금액 및 요금 금액](media/sqldev-python-sample-plot.png "팁 금액 및 요금 금액") 

## <a name="next-steps"></a>다음 단계

이 문서에서는 다음 작업을 수행합니다.

> [!div class="checklist"]
> + 샘플 데이터 검토
> + T-SQL에서 Python을 사용하여 플롯 만들기

> [!div class="nextstepaction"]
> [Python 자습서: T-SQL을 사용하여 데이터 기능 만들기](python-taxi-classification-create-features.md)
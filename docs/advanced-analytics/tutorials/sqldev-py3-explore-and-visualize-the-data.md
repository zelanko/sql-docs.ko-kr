---
title: 데이터를 시각화 및 탐색 3 단계 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2575b1c0d5de8d546d1b1ef1775f3c9e7145adc1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="step-3-explore-and-visualize-the-data"></a>3 단계: 탐색 하 고 데이터를 시각화 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 자습서의 일부는 [SQL 개발자를 위해 데이터베이스에서 Python 분석](sqldev-in-database-python-for-sql-developers.md)합니다. 

이 단계에서는 샘플 데이터 살펴보기 및 일부 플롯을 생성 합니다. 이상에서는 Python의 그래픽 개체를 serialize 한 다음 해당 개체를 deserialize 및 플롯을 확인 하는 방법을 배웁니다.

## <a name="review-the-data"></a>데이터를 검토 합니다.

첫째, NYC 택시 데이터를 사용 하기 쉽도록 변경 수에 따라 데이터 스키마를 검색 하는 데 1 분을 수행합니다

+ 원래 데이터 집합의 택시 식별자 및 여행 레코드에 대 한 별도 파일을 사용 합니다. 열에 두 개의 원래 데이터 집합에 가입 했습니다 우리 _메달_, _hack_license_, 및 _pickup_datetime_합니다.  
+ 원래 데이터 집합이 많은 파일이 포함 되 고 매우 큽니다. 레코드의 원래 수의 1%에로 저해상도 처리를 했습니다. 현재 데이터 테이블 1,703,957 행과 23 열에 있습니다.

**택시 식별자**

_메달_ 열 택시의 고유한 ID 번호를 나타냅니다.

_hack_license_ 열 (익명으로 처리) 하는 택시 운전 면허 번호를 포함 합니다.

**여정 및 요금 레코드**

각 여정 레코드에는 승하차 위치 및 시간과 여정 거리가 포함됩니다.

각 요금 레코드에는 지불 유형, 총 지불 금액, 팁 금액 등의 지불 정보가 포함됩니다.

마지막 세 열은 다양한 Machine Learning 작업에 사용할 수 있습니다.  _tip_amount_ 열에는 연속 숫자 값이 포함되며 회귀 분석의 **레이블** 열로 사용할 수 있습니다. _tipped_ 열에는 예/아니요 값만 포함되며 이진 분류에 사용됩니다. _tip_class_ 열에는 여러 개의 **클래스 레이블** 이 포함되므로 다중 클래스 분류 작업의 레이블로 사용할 수 있습니다.

레이블 열에 사용 되는 값은 모두 기반는 `tip_amount` 이러한 비즈니스 규칙을 사용 하 여 열:

+ 레이블 열 `tipped` 가능한 값이 0과 1 개

    경우 `tip_amount` > 0, `tipped` = 1, 그렇지 않으면 `tipped` = 0

+ 레이블 열 `tip_class` 에 가능한 클래스 값 0-4

    클래스 0: `tip_amount` = $0

    1 클래스: `tip_amount` > \ 0 및 `tip_amount` < = $5
    
    2 클래스: `tip_amount` > $5 및 `tip_amount` < = $10
    
    클래스 3: `tip_amount` > $10 및 `tip_amount` < = $20
    
    클래스 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>T-SQL에서 Python을 사용 하는 점도 만들기

일반적으로 데이터 과학 솔루션 개발에는 데이터 탐색 및 데이터 시각화가 많이 포함됩니다. 시각화 데이터 및 이상 값의 분포를 이해 하는 데 사용 하는 강력한 도구 이므로 Python 데이터 시각화를 다 수의 패키지를 제공 합니다. **matplotlib** 모듈 중 하나를 시각화에 대 한 더 많이 사용 되는 라이브러리 이며 히스토그램, 산 점도, 상자 점도 및 다른 데이터 탐색 그래프를 만들기 위한 많은 함수가 포함 됩니다.

이 섹션에서는 저장된 프로시저를 사용 하 여 플롯을 사용 하는 방법을 배웁니다. 대신 서버에서 이미지를 열려면 보다 저장 Python 개체 `plot` 으로 **varbinary** 데이터 및 다음 쓰기를 파일에 있는 공유 되거나 다른 곳에서 볼 합니다.

### <a name="create-a-plot-as-varbinary-data"></a>Varbinary 데이터는 점도 만들기

**revoscalepy** 에서 비슷한 기능을 지원 하는 SQL Server 2017 컴퓨터 학습 서비스에 포함 된 모듈의 **RevoScaleR** r 패키지  해당 하는 Python을 사용 하 여이 예제 `rxHistogram` 데이터를 기반으로 하는 히스토그램을 그리는 데는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 합니다. 

저장된 프로시저가 반환 serialize 된 Python `figure` 스트림으로 개체 **varbinary** 데이터입니다. 이진 데이터를 직접 볼 수 없지만 클라이언트에서 Python 코드를 사용 하 여 역직렬화 하 고는 수치를 확인 하 고 클라이언트 컴퓨터에서 이미지 파일을 저장할 수 있습니다.

1. 저장된 프로시저 만들기 _SerializePlots_PowerShell 스크립트 하지 이미 않은 경우.

    - 변수 `@query` 쿼리 텍스트를 정의 `SELECT tipped FROM nyctaxi_sample`, Python 코드 블록에 스크립트 입력된 변수를 인수로 전달 되 `@input_data_1`합니다.
    - Python 스크립트는 아주 단순: **matplotlib** `figure` 개체는 히스토그램과 산 점도에 사용 하 고 이러한 개체는 사용 하 여 serialize 한 다음는 `pickle` 라이브러리입니다.
    - Python graphics 개체도 serialize 되는 **팬더** 출력 데이터 프레임입니다.
  
    ```SQL
    CREATE PROCEDURE [dbo].[SerializePlots]
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

2. 이제 입력 쿼리로 하드 코드 된 데이터에서 플롯을 생성 하는 인수 없이 저장된 프로시저를 실행 합니다.

    ```
    EXEC [dbo].[SerializePlots]
    ```

3. 결과 코드는 다음과 같아야 합니다.
  
    ```
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. Python 클라이언트에서 이제 생성 된 이진 점도 개체는 SQL Server 인스턴스에 연결 하 고 볼 수 있습니다는 점도 합니다. 

    이렇게 하려면 서버 이름, 데이터베이스 이름 및 자격 증명 적절 하 게 대체 다음 Python 코드를 실행 합니다. Python 버전은 클라이언트와 서버에서 동일 해야 합니다. 또한 Python 라이브러리 (matplotlib) 등의 클라이언트에서 서버에 설치 된 라이브러리를 기준으로 동일 하거나 더 높은 버전 인지 확인 합니다.
  
    **SQL Server 인증을 사용 합니다.**
    
    ```python
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSWORD}')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[SerializePlots]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

    **Windows 인증을 사용 하 여:**

    ```python
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=yes;')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[SerializePlots]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

5.  연결이 성공 하는 경우에 다음과 같은 메시지가 나타납니다.
  
    *점도 디렉터리에 저장 됩니다: xxxx*
  
6.  출력 파일은 Python 작업 디렉터리에 만들어집니다. 플롯을 보려면 Python 작업 디렉터리를 찾아서 파일을 엽니다. 다음 그림에서는 클라이언트 컴퓨터에 저장 된 플롯을 보여 줍니다.
  
    ![양 vs 요금 양 팁](media/sqldev-python-sample-plot.png "팁 양 vs 요금 양") 

## <a name="next-step"></a>다음 단계

[4단계: T-SQL을 사용하여 데이터 기능 만들기](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>이전 단계

[2단계: PowerShell을 사용하여 SQL Server로 데이터 가져오기](sqldev-py2-import-data-to-sql-server-using-powershell.md)


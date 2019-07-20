---
title: 1 단원 Python 및 T-sql을 사용 하 여 데이터 탐색 및 시각화
description: SQL Server 저장 프로시저 및 T-sql 함수에 Python을 포함 하는 방법을 보여 주는 자습서
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 7faf5ae632ffd94828ce331cd634fda9d4e34058
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345885"
---
# <a name="explore-and-visualize-the-data"></a>데이터 탐색 및 시각화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 [SQL 개발자를 위한 데이터베이스 내 Python 분석](sqldev-in-database-python-for-sql-developers.md)자습서의 일부입니다. 

이 단계에서는 샘플 데이터를 탐색 하 고 몇 가지 플롯을 생성 합니다. 나중에 Python에서 그래픽 개체를 serialize 한 다음 해당 개체를 deserialize 하 고 플롯 하는 방법에 대해 알아봅니다.

## <a name="review-the-data"></a>데이터 검토

먼저 NYC Taxi 데이터를 더 쉽게 사용할 수 있도록 몇 가지 변경 작업을 수행 했으므로 데이터 스키마를 검색 하는 데 1 분 정도 걸립니다.

+ 원래 데이터 집합은 taxi 식별자 및 여행 레코드에 대해 별도의 파일을 사용 했습니다. _Medallion_, _hack_license_및 _pickup_datetime_열에 두 개의 원래 데이터 집합을 조인 했습니다.  
+ 원본 데이터 집합은 많은 파일에 포함 되어 매우 크기 때문에 원래 레코드 수의 1%만 downsampled 했습니다. 현재 데이터 테이블에는 1703957 개의 행과 23 개의 열이 있습니다.

**택시 식별자**

_Medallion_ 열은 taxi의 고유 ID 번호를 나타냅니다.

_Hack_license_ 열에는 taxi 드라이버의 라이선스 번호 (익명화)가 포함 됩니다.

**여정 및 요금 레코드**

각 여정 레코드에는 승하차 위치 및 시간과 여정 거리가 포함됩니다.

각 요금 레코드에는 지불 유형, 총 지불 금액, 팁 금액 등의 지불 정보가 포함됩니다.

마지막 세 열은 다양한 Machine Learning 작업에 사용할 수 있습니다.  _tip_amount_ 열에는 연속 숫자 값이 포함되며 회귀 분석의 **레이블** 열로 사용할 수 있습니다. _tipped_ 열에는 예/아니요 값만 포함되며 이진 분류에 사용됩니다. _tip_class_ 열에는 여러 개의 **클래스 레이블** 이 포함되므로 다중 클래스 분류 작업의 레이블로 사용할 수 있습니다.

레이블 열에 사용 되는 값은 모두 `tip_amount` 열을 기반으로 하며 다음 비즈니스 규칙을 사용 합니다.

+ 레이블 열 `tipped` 에 가능한 값 0과 1이 있습니다.

    > `tip_amount` 0, = `tipped` 1 이면이 고 `tipped` , 그렇지 않으면 0입니다.

+ 레이블 열 `tip_class` 에 가능한 클래스 값 0-4이 있습니다.

    클래스 0: `tip_amount` = $0

    클래스 1: `tip_amount` > $0 및 `tip_amount` < = $5
    
    클래스 2: `tip_amount` > $5 및 `tip_amount` < = $10
    
    클래스 3: `tip_amount` > $10 및 `tip_amount` < = $20
    
    클래스 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>T-sql에서 Python을 사용 하 여 플롯 만들기

일반적으로 데이터 과학 솔루션 개발에는 데이터 탐색 및 데이터 시각화가 많이 포함됩니다. 시각화는 데이터와 이상 값의 분포를 이해 하기 위한 강력한 도구 이므로 Python은 데이터를 시각화 하기 위한 많은 패키지를 제공 합니다. **Matplotlib** 모듈은 시각화를 위해 인기 있는 라이브러리 중 하나 이며 히스토그램, 산 점도, 상자 그림 및 기타 데이터 탐색 그래프를 만들기 위한 많은 함수를 포함 합니다.

이 섹션에서는 저장 프로시저를 사용 하 여 그리기 작업을 수행 하는 방법에 대해 알아봅니다. 서버에서 이미지를 열지 않고 Python 개체 `plot` 를 **varbinary** 데이터로 저장 한 다음 다른 곳에서 공유 하거나 볼 수 있는 파일에 기록 합니다.

### <a name="create-a-plot-as-varbinary-data"></a>Varbinary 데이터로 플롯 만들기

저장 프로시저는 serialize 된 Python `figure` 개체를 **varbinary** 데이터 스트림으로 반환 합니다. 이진 데이터를 직접 볼 수는 없지만 클라이언트에서 Python 코드를 사용 하 여 그림을 deserialize 하 고 본 다음 이미지 파일을 클라이언트 컴퓨터에 저장할 수 있습니다.

1. **PyPlotMatplotlib**저장 프로시저를 만듭니다 (PowerShell 스크립트에서 아직 수행 하지 않은 경우).

    - 변수 `@query` 는 스크립트 입력 변수에 `@input_data_1`대 `SELECT tipped FROM nyctaxi_sample`한 인수로 Python 코드 블록에 전달 되는 쿼리 텍스트를 정의 합니다.
    - Python 스크립트는 매우 간단 합니다. **matplotlib** `figure` 개체는 히스토그램과 산 점도를 만드는 데 사용 되며 이러한 개체는 라이브러리를 `pickle` 사용 하 여 serialize 됩니다.
    - Python graphics 개체는 출력을 위해 **pandas** 데이터 프레임로 serialize 됩니다.
  
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

2. 이제 인수 없이 저장 프로시저를 실행 하 여 입력 쿼리로 하드 코딩 된 데이터에서 그림을 생성 합니다.

    ```sql
    EXEC [dbo].[PyPlotMatplotlib]
    ```

3. 결과는 다음과 같습니다.
  
    ```sql
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. 이제 [Python 클라이언트](../python/setup-python-client-tools-sql.md)에서 이진 플롯 개체를 생성 한 SQL Server 인스턴스에 연결 하 고 플롯을 볼 수 있습니다. 

    이렇게 하려면 다음 Python 코드를 실행 하 여 서버 이름, 데이터베이스 이름 및 자격 증명을 적절 하 게 바꿉니다. 클라이언트와 서버에서 Python 버전이 동일한 지 확인 합니다. 또한 클라이언트의 Python 라이브러리 (예: matplotlib)가 서버에 설치 된 라이브러리를 기준으로 하는 동일한 버전 이상 인지 확인 합니다.
  
    **SQL Server 인증 사용:**
    
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

    **Windows 인증 사용:**

    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER=SQL Server;SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=True;')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

5.  연결에 성공 하면 다음과 같은 메시지가 표시 됩니다.
  
    *플롯은 xxxx 디렉터리에 저장 됩니다.*
  
6.  출력 파일은 Python 작업 디렉터리에 생성 됩니다. 플롯을 보려면 Python 작업 디렉터리를 찾아 파일을 엽니다. 다음 그림은 클라이언트 컴퓨터에 저장 된 그림을 보여 줍니다.
  
    ![팁 금액 vs 요금](media/sqldev-python-sample-plot.png "팁 금액 vs 요금") 

## <a name="next-step"></a>다음 단계

[T-SQL을 사용하여 데이터 기능 만들기](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>이전 단계

[NYC Taxi 데이터 집합 다운로드](demo-data-nyctaxi-in-sql.md)


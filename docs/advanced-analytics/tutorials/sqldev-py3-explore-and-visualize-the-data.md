---
title: 단원 1 탐색 하 고 Python 및 T-SQL-SQL Server Machine Learning을 사용 하 여 데이터 시각화
description: 포함 하는 방법을 보여 주는 자습서 SQL Server에서 Python 저장 프로시저 및 T-SQL 함수
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e9dd0a0884c96a8f5b17948c21b7f891a2e997ab
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860494"
---
# <a name="explore-and-visualize-the-data"></a>데이터 탐색 및 시각화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 자습서에 일부 [SQL 개발자를 위한 데이터베이스 내 Python 분석](sqldev-in-database-python-for-sql-developers.md)합니다. 

이 단계에서는 샘플 데이터를 탐색 하 고 몇 개의 그림을 생성 합니다. 나중에 Python, 그래픽 개체를 serialize 다음 해당 개체를 deserialize 하 고 도표를 확인 하는 방법에 알아봅니다.

## <a name="review-the-data"></a>데이터 검토

첫째, 잠시 데이터 스키마를 검색할 NYC Taxi 데이터를 사용 하도록 쉽게 수행할 수 있도록 몇 가지 변경 사항이 것 처럼

+ 택시 식별자 및 여정 레코드가 별도 파일을 사용 하는 원래 데이터 집합입니다. 두 개의 원래 데이터 집합 열에 가입 했습니다 _medallion_를 _hack_license_, 및 _pickup_datetime_합니다.  
+ 원래 데이터 집합 많은 파일이 포함 되 고 매우 큽니다. 원래 레코드 수의 1%만 가져오도록를 다운 샘플링이 되었습니다. 현재 데이터 테이블에는 1,703,957 개의 행과 23 개 열에 있습니다.

**택시 식별자**

합니다 _medallion_ 열은 택시의 고유 ID 번호를 나타냅니다.

합니다 _hack_license_ 열은 택시 운전 면허 번호 (익명)를 포함 합니다.

**여정 및 요금 레코드**

각 여정 레코드에는 승하차 위치 및 시간과 여정 거리가 포함됩니다.

각 요금 레코드에는 지불 유형, 총 지불 금액, 팁 금액 등의 지불 정보가 포함됩니다.

마지막 세 열은 다양한 Machine Learning 작업에 사용할 수 있습니다.  _tip_amount_ 열에는 연속 숫자 값이 포함되며 회귀 분석의 **레이블** 열로 사용할 수 있습니다. _tipped_ 열에는 예/아니요 값만 포함되며 이진 분류에 사용됩니다. _tip_class_ 열에는 여러 개의 **클래스 레이블** 이 포함되므로 다중 클래스 분류 작업의 레이블로 사용할 수 있습니다.

레이블 열에 사용 되는 값 모두에 기반한는 `tip_amount` 이러한 비즈니스 규칙을 사용 하 여 열:

+ 레이블 열 `tipped` 가능한 값이 0과 1 개

    하는 경우 `tip_amount` > 0 `tipped` = 1이 고 그렇지 않으면 `tipped` = 0

+ 레이블 열 `tip_class` 클래스 값 0-4

    Class 0: `tip_amount` = $0

    클래스 1: `tip_amount` > \ 0 및 `tip_amount` < = $5
    
    2 클래스: `tip_amount` > 5 달러 및 `tip_amount` < = $10
    
    3 클래스: `tip_amount` > 10 달러 및 `tip_amount` < = $20
    
    클래스 4: `tip_amount` > 20 달러

## <a name="create-plots-using-python-in-t-sql"></a>T-sql로 Python을 사용 하 여 그림 만들기

일반적으로 데이터 과학 솔루션 개발에는 데이터 탐색 및 데이터 시각화가 많이 포함됩니다. 시각화는 데이터와 이상 값의 분포를 이해 하는 데 사용 하는 강력한 도구 이므로 Python 데이터 시각화에 대 한 여러 패키지를 제공 합니다. 합니다 **matplotlib** 모듈은 시각화에 대 한 더 인기 있는 라이브러리 중 하나 이며 히스토그램, 산 점도, 상자 그림 및 기타 데이터 탐색 그래프를 만들기 위한 많은 함수도 포함 되어 있습니다.

이 섹션에서는 저장된 프로시저를 사용 하 여 그림을 사용 하는 방법을 알아봅니다. 대신 서버에서 이미지를 열려면 보다 저장 Python 개체 `plot` 으로 **varbinary** 데이터 및는 파일에는 공유 되거나 다른 곳에서 표시 한 다음 쓰기입니다.

### <a name="create-a-plot-as-varbinary-data"></a>Varbinary 데이터 플롯 만들기

Serialize 된 Python을 반환 하는 저장된 프로시저 `figure` 스트림 개체로 **varbinary** 데이터입니다. 이진 데이터를 직접 볼 수 없습니다 하지만 클라이언트에서 Python 코드를 사용 하 여 deserialize 하 고 수치를 확인 하 고 클라이언트 컴퓨터에 이미지 파일을 저장 합니다.

1. 저장된 프로시저를 만듭니다 **PyPlotMatplotlib**PowerShell 스크립트를 이미 하지 않은 경우.

    - 변수의 `@query` 쿼리 텍스트를 정의 `SELECT tipped FROM nyctaxi_sample`에 스크립트 입력된 변수를 인수로 Python 코드 블록에 전달 되는 `@input_data_1`합니다.
    - Python 스크립트는 간단 합니다. **matplotlib** `figure` 개체 히스토그램 및 산 점도 할 때 사용 되 고 이러한 개체는 사용 하 여 serialize 한 다음는 `pickle` 라이브러리.
    - Python 그래픽 개체가 serialize 되는 **pandas** 데이터 프레임 출력.
  
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

2. 이제 입력 쿼리로 하드 코드 된 데이터에서 플롯을 생성 하려면 인수 없이 저장된 프로시저를 실행 합니다.

    ```sql
    EXEC [dbo].[PyPlotMatplotlib]
    ```

3. 결과 다음과 같이 해야 합니다.
  
    ```sql
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. [Python 클라이언트](../python/setup-python-client-tools-sql.md), 이제 생성 된 이진 그림 개체는 SQL Server 인스턴스에 연결 하 고 그림을 볼 수 있습니다. 

    이렇게 하려면 서버 이름, 데이터베이스 이름 및 자격 증명을 적절 하 게 대체 다음 Python 코드를 실행 합니다. Python 버전 클라이언트와 서버에서 동일 해야 합니다. 또한 Python 라이브러리 (예: matplotlib) 클라이언트에서 라이브러리 서버에 설치를 기준으로 동일 하거나 더 높은 버전 인지 확인 합니다.
  
    **SQL Server 인증을 사용 합니다.**
    
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

    **Windows 인증을 사용 하 여:**

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

5.  연결이 성공 하면 다음과 같은 메시지가 표시 됩니다.
  
    *그림 디렉터리에 저장 됩니다: xxxx*
  
6.  Python 작업 디렉터리에 출력 파일이 생성 됩니다. 그림을 보려면 Python 작업 디렉터리를 찾아서 파일을 엽니다. 다음 이미지에는 클라이언트 컴퓨터에 저장 된 플롯을 보여 줍니다.
  
    ![팁 금액 및 금액](media/sqldev-python-sample-plot.png "팁 금액 및 금액") 

## <a name="next-step"></a>다음 단계

[T-SQL을 사용 하 여 데이터 기능 만들기](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>이전 단계

[NYC Taxi 데이터 집합 다운로드](demo-data-nyctaxi-in-sql.md)


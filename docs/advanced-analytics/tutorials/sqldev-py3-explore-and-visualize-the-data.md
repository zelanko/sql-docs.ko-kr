---
title: "3단계: 데이터 탐색 및 시각화 | Microsoft 문서"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-python
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dfb80fcd3241b22f0ac72c2cf4cd8a18d1add857
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="step-3-explore-and-visualize-the-data"></a>3단계: 데이터 탐색 및 시각화

일반적으로 데이터 과학 솔루션 개발에는 데이터 탐색 및 데이터 시각화가 많이 포함됩니다. 이 단계에서는 샘플 데이터를 탐색 하 고 일부 플롯을 생성 합니다. 나중에 Python, 그래픽 개체를 직렬화 한 다음 해당 개체를 역직렬화 할 및 플롯을 확인 하는 방법에 알아봅니다.

> [!NOTE]
> 이 연습에서는 이진 분류 작업만; 다른 두 개의 기계 학습 작업, 회귀 및 다중 클래스 분류에 대 한 별도 모델을 구축해 보고 시작 됩니다.

## <a name="review-the-data"></a>데이터 검토

원래 데이터 집합에서는 택시 식별자 및 여정 레코드가 별도 파일로 제공되었습니다. 그러나 샘플 데이터를 쉽게 사용할 수 있도록 두 개의 원래 데이터 집합이 _medallion_, _hack_license_및 _pickup_datetime_열에 조인되었습니다.  레코드도 원래 레코드 수의 1%만 가져오도록 샘플링되었습니다. 다운 샘플링된 결과 데이터 집합에는 1,703,957개의 행과 23개 열이 있습니다.

**택시 식별자**

- _medallion_ 열은 택시의 고유 ID 번호를 나타냅니다.
- _hack_license_ 열은 택시 기사의 운전 면허 번호(익명)를 포함합니다.

**여정 및 요금 레코드**

- 각 여정 레코드에는 승하차 위치 및 시간과 여정 거리가 포함됩니다.
- 각 요금 레코드에는 지불 유형, 총 지불 금액, 팁 금액 등의 지불 정보가 포함됩니다.
- 마지막 세 열은 다양한 Machine Learning 작업에 사용할 수 있습니다.  _tip_amount_ 열에는 연속 숫자 값이 포함되며 회귀 분석의 **레이블** 열로 사용할 수 있습니다. _tipped_ 열에는 예/아니요 값만 포함되며 이진 분류에 사용됩니다. _tip_class_ 열에는 여러 개의 **클래스 레이블** 이 포함되므로 다중 클래스 분류 작업의 레이블로 사용할 수 있습니다.
- 레이블 열에 사용되는 값은 모두 다음과 같은 비즈니스 규칙을 사용하여 _tip_amount_ 열을 기반으로 합니다.
  
    |파생 열 이름|규칙|
    |-|-|
     |tipped|If tip_amount > 0, tipped = 1, otherwise tipped = 0|
    |tip_class|Class 0: tip_amount = $0<br /><br />Class 1: tip_amount > $0 and tip_amount <= $5<br /><br />Class 2: tip_amount > $5 and tip_amount <= $10<br /><br />Class 3: tip_amount > $10 and tip_amount <= $20<br /><br />Class 4: tip_amount > $20|

## <a name="create-plots-using-python-in-t-sql"></a>T-SQL에서 Python을 사용 하는 점도 만들기

시각화 데이터 및 이상 값의 분포를 이해 하는 데 사용 하는 강력한 도구 이므로 Python 데이터 시각화를 다 수의 패키지를 제공 합니다. **matplotlib** 모듈은 히스토그램, 산 점도, 상자 점도 및 다른 데이터 탐색 그래프를 만들기 위한 다양 한 함수를 포함 하는 인기 있는 라이브러리입니다.

이 섹션에서는 저장된 프로시저를 사용 하 여 플롯을 사용 하는 방법을 배웁니다. 저장할는 `plot` Python 개체는 **varbinary** 데이터를 입력 하 고 서버에서 생성 된 플롯을 저장 합니다.

### <a name="storing-plots-as-varbinary-data-type"></a>varbinary 데이터 형식으로 그림 저장

**revoscalepy** SQL Server 2017 컴퓨터 학습 서비스에 포함 된 모듈에 있는 모든 라이브러리 RevoScaleR 패키지에서 R 라이브러리와 비슷합니다. 이 예제에서는 사용 하 여 해당 하는 Python `rxHistogram` 데이터를 기반으로 하는 히스토그램을 그리는 데는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 합니다. 쉽게를 래핑할 해당 저장된 프로시저에서 _PlotHistogram_합니다.

저장된 프로시저가 반환 serialize 된 Python `figure` 스트림으로 개체 **varbinary** 데이터입니다. 이진 데이터를 직접 볼 수 없지만 클라이언트에서 Python 코드를 사용 하 여 역직렬화 하 고는 수치를 확인 하 고 클라이언트 컴퓨터에서 이미지 파일을 저장할 수 있습니다.

### <a name="create-the-stored-procedure-plotspython"></a>Plots_Python 저장된 프로시저 만들기

1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 새 **쿼리** 창.

2.  연습에 사용할 데이터베이스를 선택하고 다음 문을 사용하여 프로시저를 만듭니다. 필요한 경우 올바른 테이블 이름을 사용하도록 코드를 수정해야 합니다.
  
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
**참고:**

- 변수 `@query` 쿼리 텍스트를 정의 (`'SELECT tipped FROM nyctaxi_sample'`), Python 코드 블록에 스크립트 입력된 변수를 인수로 전달 되 `@input_data_1`합니다.
- Python 스크립트는 아주 단순: **matplotlib** `figure` 개체는 히스토그램과 산 점도에 사용 하 고 이러한 개체는 사용 하 여 serialize 한 다음는 `pickle` 라이브러리입니다.
- Python graphics 개체는 Python으로 serialize 되는 **팬더** 출력 데이터 프레임입니다.

### <a name="output-varbinary-data-to-viewable-graphics-file"></a>출력 varbinary 데이터를 볼 수 있는 그래픽 파일

1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 다음 문을 실행합니다.
  
    ```
    EXEC [dbo].[SerializePlots]
    ```
  
    **결과**
  
    *그림*
    *0xFFD8FFE000104A4649... * 
     *0xFFD8FFE000104A4649... * 
     *0xFFD8FFE000104A4649... * 
     *0xFFD8FFE000104A4649...*

  
2.  클라이언트 컴퓨터에서 서버 이름, 데이터베이스 이름 및 자격 증명 적절 하 게 대체 다음 Python 코드를 실행 합니다.
  
    **SQL server 인증:**
    
        ```python
        import pyodbc
        import pickle
        import os
        cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSOWRD}')
        cursor = cnxn.cursor()
        cursor.execute("EXECUTE [dbo].[SerializePlots]")
        tables = cursor.fetchall()
        for i in range(0, len(tables)):
            fig = pickle.loads(tables[i][0])
            fig.savefig(str(i)+'.png')
        print("The plots are saved in directory: ",os.getcwd())
        ```  
    **Windows 인증:**

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

    > [!NOTE]
    > Python 버전은 클라이언트와 서버에서 동일 해야 합니다. Python 라이브러리 (matplotlib) 등의 클라이언트에서 사용 중인 서버에 설치 된 라이브러리를 기준으로 동일 하거나 더 높은 버전의 있는지 확인 합니다.


3.  아래 결과 표시는 연결에 성공한 경우
  
    *점도 디렉터리에 저장 됩니다: xxxx*
  
4.  Python 작업 디렉터리에 출력 파일이 만들어질 수 있습니다. 플롯을 보려면 바로 Python 작업 디렉터리를 엽니다. 다음 그림에서는 클라이언트 컴퓨터에 저장 하는 예제에서는 그림을 보여 줍니다.
  
    ![양 vs 요금 양 팁](media/sqldev-python-sample-plot.png "팁 양 vs 요금 양") 

## <a name="next-step"></a>다음 단계

[4단계: T-SQL을 사용하여 데이터 기능 만들기](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>이전 단계

[2단계: PowerShell을 사용하여 SQL Server로 데이터 가져오기](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="see-also"></a>관련 항목:

[기계 학습 Python 사용 하 여 서비스](../python/sql-server-python-services.md)


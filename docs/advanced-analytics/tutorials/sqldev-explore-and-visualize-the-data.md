---
title: Lesson 3 탐색 하 고 데이터를 시각화 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 4be76ebbb8f082e84a00bfe93b36c9bd8c2c0a81
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-3-explore-and-visualize-the-data"></a>3 단원: 데이터를 탐색하고 시각화하기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 SQL Server에서 R을 사용하는 방법에 대한 SQL 개발자를 위한 자습서의 일부입니다.

이 단원에서는 예제 데이터를 검토하고 R 함수를 사용하여 일부 플롯을 생성합니다. 이러한 R 함수 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에 이미 포함됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 R 함수를 호출할 수 있습니다.

## <a name="review-the-data"></a>데이터 검토

일반적으로 데이터 과학 솔루션 개발에는 데이터 탐색 및 데이터 시각화가 많이 포함됩니다. 먼저 잠시 시간을 내서 샘플 데이터를 검토해 보겠습니다.

원본 데이터 집합에서는 택시 식별자 및 여정 기록이 별도의 파일로 제공되었습니다. 그러나 샘플 데이터를 쉽게 사용하기 위해 두 개의 원래 데이터 집합이 medallion, hack_license 및 pickup_datetime 열에 조인되었습니다. 레코드도 원래 레코드 수의 1%만 가져오도록 샘플링되었습니다. 다운 샘플링된 결과 데이터 집합에는 1,703,957개의 행과 23개 열이 있습니다

**택시 식별자**
  
-   _medallion_ 열은 택시의 고유 ID 번호를 나타냅니다.
  
-   heck_license 열은 택시 운전면허 번호를 포함합니다(익명으로 처리).
  
**여정 및 요금 레코드**
  
-   각 여정 레코드에는 승하차 위치 및 시간과 여정 거리가 포함됩니다.
  
-   각 요금 레코드에는 지불 유형, 총 지불 금액, 팁 금액 등의 지불 정보가 포함됩니다.
  
-   마지막 세 열은 다양한 Machine Learning 작업에 사용할 수 있습니다. _tip_amount_ 열은 연속적인 숫자 값을 포함하며 회귀 분석의 레이블 열로 사용할 수 있습니다. _tipped_ 열은 예 / 아니오 값만 있고 이진 분류에 사용됩니다. _tip_class_ 열은 여러 개의 **클래스** 레이블을 가지므로 다중 클래스 분류 작업의 레이블로 사용할 수 있습니다.
  
    이 연습에서는 이진 분류 작업만 보여 주지만, 다른 두 가지 Machine Learning 작업인 회귀 및 다중 클래스 분류 모델도 구축해 보세요.
  
-   레이블 열에 사용되는 값은 모두 아래 비즈니스 규칙을 사용한 _tip_amount_ 열에 기반합니다:
  
    |파생 열 이름|규칙|
    |-|-|
     |tipped|If tip_amount > 0, tipped = 1, otherwise tipped = 0|
    |tip_class|Class 0: tip_amount = $0<br /><br />Class 1: tip_amount > $0 and tip_amount <= $5<br /><br />Class 2: tip_amount > $5 and tip_amount <= $10<br /><br />Class 3: tip_amount > $10 and tip_amount <= $20<br /><br />Class 4: tip_amount > $20|

## <a name="create-plots-using-r-in-t-sql"></a>T-SQL에서 R을 사용하여 플롯 만들기

시각화는 데이터와 이상값의 분포를 파악하는 데 강력한 도구이므로 R에서는 데이터 시각화를 위한 여러 패키지를 제공합니다. R의 표준 오픈 소스 배포에는 히스토그램, 산점도, 상자 그림 및 기타 데이터 탐색 그래프를 만들기 위한 많은 함수도 포함되어 있습니다.

일반적으로 R은 그래픽 출력에 R 장치를 사용하여 이미지를 만듭니다. 이 장치의 출력을 캡처한 다음 응용 프로그램에서 렌더링하기 위해 이미지를 **varbinary** 데이터 형식으로 저장하거나, 이미지를 지원 파일 형식(.JPG, .PDF 등) 중 하나로 저장할 수 있습니다.

이 섹션에서는 저장 프로시저를 사용하여 각 형식의 출력으로 작업하는 방법을 알아봅니다. 전체 프로세스는 다음과 같습니다.

- varbinary 데이터로 R 플롯을 생성하는 저장 프로시저 만들기

- 플롯을 생성하고 이미지 파일에 저장

- 저장 프로시저를 사용하여 이진 플롯 데이터를 JPG 또는 PDF 파일로 변환

### <a name="create-the-stored-procedure-plothistogram"></a>PlotHistogram 저장 프로시저 만들기

1. 플롯을 만들려면 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 제공하는 향상된 R 함수 중의 하나인 rxHistogram을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리의 데이터를 기반으로 히스토그램을 그립니다. R 함수를 쉽게 호출할 수 있도록 저장 프로시저 PlotHistogram 내에 래핑합니다 
    [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서, 새 **쿼리** 창을 엽니다.

2. 자습서 데이터가 포함된 데이터베이스에이 아래 문을 사용하여 프로시저를 만듭니다.

    ```SQL
    CREATE PROCEDURE [dbo].[PlotHistogram]
    AS
    BEGIN
      SET NOCOUNT ON;
      DECLARE @query nvarchar(max) =  
      N'SELECT tipped FROM nyctaxi_sample'  
      EXECUTE sp_execute_external_script @language = N'R',  
                                         @script = N'  
       image_file = tempfile();  
       jpeg(filename = image_file);  
       #Plot histogram  
       rxHistogram(~tipped, data=InputDataSet, col=''lightgreen'',   
       title = ''Tip Histogram'', xlab =''Tipped or not'', ylab =''Counts'');  
       dev.off();  
       OutputDataSet <- data.frame(data=readBin(file(image_file, "rb"), what=raw(), n=1e6));  
       ',  
       @input_data_1 = @query  
       WITH RESULT SETS ((plot varbinary(max)));  
    END
    GO
    ```

    필요한 경우 올바른 테이블 이름을 사용하도록 코드를 수정해야 합니다.
  
    -   `@query` 변수는 스크립트 입력 변수 `@input_data_1`에 대한 인수로 R 스크립트에 전달되는 쿼리 텍스트(`'SELECT tipped FROM nyctaxi_sample'`)를 정의합니다.
  
    -   R 스크립트는 간단합니다. 이미지를 저장할 R 변수(`image_file`)를 정의한 다음 `rxHistogram` 함수를 호출하여 그림을 생성합니다.
  
    -   R 장치는 **off**로 설정되어 있습니다.
  
        R에서 높은 수준의 그리기 명령을 실행하면 R에서 *장치*라는 그래픽 창이 열립니다. 창의 크기 및 색과 기타 측면을 변경하거나, 파일에 쓰거나 다른 방법으로 출력을 처리하는 경우 장치를 끌 수 있습니다.
  
    -   R 그래픽 개체는 출력을 위해 R data.frame으로 직렬화됩니다.

### <a name="generate-the-graphics-data-and-save-to-file"></a>그래픽 데이터를 생성하고 파일에 저장

저장 프로시저는 명확하게 직접 볼 수 없는 varbinary 데이터 스트림으로 이미지를 반환합니다. 그러나 **bcp** 유틸리티를 사용하여 varbinary 데이터를 가져오고 클라이언트 컴퓨터에 이미지 파일로 저장할 수 있습니다.
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 다음 문을 실행합니다.
  
    ```SQL
    EXEC [dbo].[PlotHistogram]
    ```
  
    **결과**
    
    *plot*
    *0xFFD8FFE000104A4649...*
  
2.  PowerShell 명령 프롬프트를 열고 적절한 인스턴스 이름, 데이터베이스 이름, 사용자 이름 및 자격 증명을 인수로 제공하여 다음 명령을 실행합니다.
  
     ```
     bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  <database name>  -U <user name> -P <password>
     ```

    > [!NOTE]
    > Bcp의 명령 스위치는 대/소문자를 구분하지 않습니다.
  
3.  연결에 성공하면 그래픽 파일 형식에 대한 자세한 정보를 입력하라는 메시지가 표시됩니다. 다음과 같은 변경을 제외하고 각 프롬프트에서 Enter 키를 눌러 기본값을 적용합니다.
  
    -   **prefix-length of field plot**에 대해 0을 입력합니다.
  
    -   나중에 다시 사용하기 위해 출력 매개 변수를 저장하려는 경우 **Y** 를 입력합니다.
  
    ```
    Enter the file storage type of field plot [varbinary(max)]:
    Enter prefix-length of field plot [8]: 0
    Enter length of field plot [0]:
    Enter field terminator [none]:
  
    Do you want to save this format information in a file? [Y/n]
    Host filename [bcp.fmt]:
    ```
  
    **결과**
    
    ```
    Starting copy...
    1 rows copied.
    Network packet size (bytes): 4096
    Clock Time (ms.) Total     : 3922   Average : (0.25 rows per sec.)
    ```

    > [!TIP]
    > 서식 정보를 파일(bcp.fmt)에 저장하는 경우 **bcp** 유틸리티는 그래픽 파일 형식 옵션을 묻는 메시지 없이 나중에 유사한 명령에 적용할 수 있는 서식 정의를 생성합니다. 서식 파일을 사용하려면 명령줄의 끝, password 인수 뒤에 `-f bcp.fmt` 를 추가합니다.
  
4.  PowerShell 명령을 실행한 곳과 동일한 디렉터리에 출력 파일이 만들어집니다. 그림을 보려면 plot.jpg 파일을 열기만 하면 됩니다.
  
    ![팁이 있는 택시 여정 및 팁이 없는 택시 여정](media/rsql-devtut-tippedornot.jpg "팁이 있는 택시 여정 및 팁이 없는 택시 여정")  
  
### <a name="export-the-plot-data-to-a-viewable-file"></a>그리기 데이터를 볼 수 있는 파일로 내보내기

R 플롯을 이진 데이터 유형으로 출력하는 것은 응용 프로그램에서 사용하기에 편리할 수 있지만, 데이터 탐색 단계에서 렌더링 된 플롯을 필요로 하는 데이터 과학자에게는 그다지 유용하지 않습니다. 일반적으로 데이터 과학자는 여러 관점에서 데이터에 대한 통찰력을 얻기 위해 여러 데이터 시각화를 생성합니다.

사용자에 대한 그래프를 생성하려면 .JPG, .PDF 및 .PNG와 같은 일반적인 형식으로 R 출력을 만드는 저장 프로시저를 사용할 수 있습니다. 저장 프로시저가 그래픽을 만든 후에는 파일을 열어 플롯을 시각화하면 됩니다.

1. 히스토그램, 산점도 및 기타 R 그래픽을 JPG 및 PDF 형식으로 작성하는 방법을 보여주는 새로운 저장 프로시저 _PlotInOutputFiles_ 를 만듭니다.

    [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 새 **쿼리** 창을 열고 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 붙여 놓습니다.
  
    ```SQL
    CREATE PROCEDURE [dbo].[PlotInOutputFiles]  
    AS  
    BEGIN  
      SET NOCOUNT ON;  
      DECLARE @query nvarchar(max) =  
      N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'  
      EXECUTE sp_execute_external_script @language = N'R',  
      @script = N'  
       # Set output directory for files and check for existing files with same names   
        mainDir <- ''C:\\temp\\plots''  
        dir.create(mainDir, recursive = TRUE, showWarnings = FALSE)  
        setwd(mainDir);  
        print("Creating output plot files:", quote=FALSE)
        
        # Open a jpeg file and output histogram of tipped variable in that file.  
        dest_filename = tempfile(pattern = ''rHistogram_Tipped_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.jpg'',sep="")  
        print(dest_filename, quote=FALSE);  
        jpeg(filename=dest_filename);  
        hist(InputDataSet$tipped, col = ''lightgreen'', xlab=''Tipped'',   
            ylab = ''Counts'', main = ''Histogram, Tipped'');  
         dev.off();  

        # Open a pdf file and output histograms of tip amount and fare amount.   
        # Outputs two plots in one row  
        dest_filename = tempfile(pattern = ''rHistograms_Tip_and_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=7);  
        par(mfrow=c(1,2));  
        hist(InputDataSet$tip_amount, col = ''lightgreen'',   
            xlab=''Tip amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram, Tip amount'', xlim = c(0,40), 100);  
        hist(InputDataSet$fare_amount, col = ''lightgreen'',   
            xlab=''Fare amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram,   
            Fare amount'',   
            xlim = c(0,100), 100);  
       dev.off();  
  
        # Open a pdf file and output an xyplot of tip amount vs. fare amount using lattice;  
        # Only 10,000 sampled observations are plotted here, otherwise file is large.  
        dest_filename = tempfile(pattern = ''rXYPlots_Tip_vs_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=4);  
        plot(tip_amount ~ fare_amount,   
            data = InputDataSet[sample(nrow(InputDataSet), 10000), ],   
            ylim = c(0,50),   
            xlim = c(0,150),   
            cex=.5,   
            pch=19,   
            col=''darkgreen'',    
            main = ''Tip amount by Fare amount'',   
            xlab=''Fare Amount ($)'',   
            ylab = ''Tip Amount ($)'');   
        dev.off();',  
     @input_data_1 = @query  
     END
    ```
  
    -   저장 프로시저 내의 SELECT 쿼리 출력은 기본 R 데이터 프레임인 `InputDataSet`에 저장됩니다. 그런 다음 다양한 R 그리기 함수를 호출하여 실제 그래픽 파일을 생성할 수 있습니다.
  
        포함된 R 스크립트의 대부분은 `plot` 또는 `hist`와 같은 그래픽 함수의 옵션을 나타냅니다.
  
    -   모든 파일은 로컬 폴더 _C:\temp\Plots\\_에 저장됩니다. 대상 폴더는 R 스크립트에 저장 프로시저의 일부로 제공되는 인수에 의해 정의됩니다.  `mainDir`변수 값을 변경하여 대상 폴더를 변경할 수 있습니다.
  
2.  저장 프로시저를 만드는 문을 실행합니다.

    ```SQL
    EXEC PlotInOutputFiles
    ```

    **결과**
    
    ```
    STDOUT message(s) from external script:
    [1] Creating output plot files:[1] C:\temp\plots\rHistogram_Tipped_18887f6265d4.jpg[1] 
    
    C:\temp\plots\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]
    
    C:\temp\plots\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf
    ```

    파일 이름에 숫자를 기존 파일에 쓸 때 오류가 가져오지 않음 되도록 임의로 생성 됩니다.

3. 플롯을 보려면 대상 폴더를 열고 저장 프로시저 내 R 코드에 의해서 생성된 파일을 검토합니다.

    + `rHistogram_Tipped.jpg` 파일은 팁이 있는 승차 수(Counts)와 팁이 없는 승차 수를 보여줍니다(이 히스토그램은 이전 단계에서 생성된 것과 매우 유사합니다.).

    + `rHistograms_Tip_and_Fare_Amount.pdf` 파일은 운임에 대해 그리려는 팁 금액의 분포를 보여줍니다.
    
    ![tip_amount 및 fare_amount 보여 주는 히스토그램](media/rsql-devtut-tipamtfareamt.PNG "tip_amount 및 fare_amount 보여 주는 히스토그램")

    + `rXYPlots_Tip_vs_Fare_Amount.pdf` 파일은 x 축에 운임과 y 축에 팁 금액을 가지는 산점도를 포함합니다.

    ![팁 양 요금 비용을 초과 표시](media/rsql-devtut-tipamtbyfareamt.PNG "팁 양 요금 비용을 초과 표시 됩니다.")

4.  파일을 다른 폴더에 출력하려면 저장 프로시저에 포함된 R 스크립트의 `mainDir` 변수 값을 변경합니다. 다른 형식, 더 많은 파일 등을 출력하도록 스크립트를 수정할 수도 있습니다.

## <a name="next-lesson"></a>다음 단원

[4 단원: T-SQL을 사용하여 데이터 특성 만들기](../tutorials/sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>이전 단원

[2 단원: SQL server PowerShell을 사용하여 데이터 가져오기](../r/sqldev-import-data-to-sql-server-using-powershell.md)

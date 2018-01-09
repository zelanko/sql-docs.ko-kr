---
title: "3 단원: 탐색 하 고 데이터를 시각화 하 | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 7fe670f3-5e62-43ef-97eb-b9af54df9128
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8048bc1eff7437e2a96bd8995f0362b341cbf092
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="lesson-3-explore-and-visualize-the-data"></a>3 단원: 탐색 하 고 데이터를 시각화 합니다.

이 문서는 SQL Server에서 R을 사용 하는 방법에 대 한 SQL 개발자를 위한 자습서의 일부입니다.

이 단원에서는 샘플 데이터를 검토 하 고 R 함수를 사용 하 여 일부 플롯을 생성 합니다. 이러한 R 함수에 이미 포함 되어 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]합니다. R 함수를 호출할 수 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다.

## <a name="review-the-data"></a>데이터를 검토 합니다.

일반적으로 데이터 과학 솔루션 개발에는 데이터 탐색 및 데이터 시각화가 많이 포함됩니다. 아직 없는 경우 샘플 데이터를 검토 하려면 잠시를 먼저 살펴보겠습니다.

원래 데이터 집합에서는 택시 식별자 및 여정 레코드가 별도 파일로 제공되었습니다. 그러나 샘플 데이터를 쉽게 사용할 수 있도록 하려면 두 개의 원래 데이터 집합 결합 열에 _메달_, _해킹\_라이선스_, 및 _픽업\_ 날짜/시간_합니다.  레코드도 원래 레코드 수의 1%만 가져오도록 샘플링되었습니다. 다운 샘플링된 결과 데이터 집합에는 1,703,957개의 행과 23개 열이 있습니다.

**택시 식별자**
  
-   _medallion_ 열은 택시의 고유 ID 번호를 나타냅니다.
  
-   _해킹\_라이선스_ 열 (익명으로 처리) 하는 택시 운전 면허 번호를 포함 합니다.
  
**여정 및 요금 레코드**
  
-   각 여정 레코드에는 승하차 위치 및 시간과 여정 거리가 포함됩니다.
  
-   각 요금 레코드에는 지불 유형, 총 지불 금액, 팁 금액 등의 지불 정보가 포함됩니다.
  
-   마지막 세 열은 다양한 Machine Learning 작업에 사용할 수 있습니다.  _팁\_양_ 열 연속 숫자 값을 포함 하며으로 사용할 수는 **레이블** 회귀 분석에 대 한 열입니다. _tipped_ 열에는 예/아니요 값만 포함되며 이진 분류에 사용됩니다. _팁\_클래스_ 열에 여러 개의 **클래스 레이블을** 따라서 사용할 수는 레이블로 다중 클래스 분류 작업에 대 한 합니다.
  
    이 연습에서는 이진 분류 작업만 보여 주지만, 다른 두 가지 Machine Learning 작업인 회귀 및 다중 클래스 분류 모델도 구축해 보세요.
  
-   레이블 열에 사용 되는 값은 모두 기반는 _팁\_양_ 이러한 비즈니스 규칙을 사용 하 여 열:
  
    |파생 열 이름|규칙|
    |-|-|
     |tipped|If tip_amount > 0, tipped = 1, otherwise tipped = 0|
    |tip_class|Class 0: tip_amount = $0<br /><br />Class 1: tip_amount > $0 and tip_amount <= $5<br /><br />Class 2: tip_amount > $5 and tip_amount <= $10<br /><br />Class 3: tip_amount > $10 and tip_amount <= $20<br /><br />Class 4: tip_amount > $20|

## <a name="create-plots-using-r-in-t-sql"></a>T-SQL에서 R을 사용 하 여 점도 만들기

시각화는 데이터와 이상값의 분포를 파악하는 데 강력한 도구이므로 R에서는 데이터 시각화를 위한 여러 패키지를 제공합니다. R의 표준 오픈 소스 배포에는 히스토그램, 산점도, 상자 그림 및 기타 데이터 탐색 그래프를 만들기 위한 많은 함수도 포함되어 있습니다.

일반적으로 R은 그래픽 출력에 R 장치를 사용하여 이미지를 만듭니다. 이 장치의 출력을 캡처한 다음 응용 프로그램에서 렌더링하기 위해 이미지를 **varbinary** 데이터 형식으로 저장하거나, 이미지를 지원 파일 형식(.JPG, .PDF 등) 중 하나로 저장할 수 있습니다.

이 섹션에서는 저장 프로시저를 사용하여 각 형식의 출력으로 작업하는 방법을 알아봅니다. 전체 프로세스는 다음과 같습니다.

- Varbinary 데이터는 R 플롯을 생성 하는 저장된 프로시저 만들기

- 플롯을 생성 하 고 이미지 파일에 저장

- 저장된 프로시저를 사용 하 여 이진 데이터 JPG 또는 PDF 파일로 변환 하려면

### <a name="create-the-stored-procedure-plothistogram"></a>PlotHistogram 저장된 프로시저 만들기

1. 플롯을 만들려면 사용 `rxHistogram`에 제공 된 고급 R 기능 중 하나 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 데이터를 기반으로 하는 히스토그램을 그리는 데는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 합니다. R 함수를 쉽게 호출할 수 있게 하려면 저장 프로시저 _PlotHistogram_에 래핑합니다.

    [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 새 **쿼리** 창.

2. 자습서 데이터가 포함 된 데이터베이스에이 문을 사용 하 여 프로시저를 만듭니다.

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
  
    -   `@query` 변수는 스크립트 입력 변수`'SELECT tipped FROM nyctaxi_sample'`에 대한 인수로 R 스크립트에 전달되는 쿼리 텍스트( `@input_data_1`)를 정의합니다.
  
    -   R 스크립트는 간단합니다. 이미지를 저장할 R 변수(`image_file`)를 정의한 다음 `rxHistogram` 함수를 호출하여 그림을 생성합니다.
  
    -   R 장치는 **off**로 설정되어 있습니다.
  
        R에서 높은 수준의 그리기 명령을 실행하면 R에서 *장치*라는 그래픽 창이 열립니다. 창의 크기 및 색과 기타 측면을 변경하거나, 파일에 쓰거나 다른 방법으로 출력을 처리하는 경우 장치를 끌 수 있습니다.
  
    -   R 그래픽 개체는 출력을 위해 R data.frame으로 직렬화됩니다.

### <a name="generate-the-graphics-data-and-save-to-file"></a>그래픽 데이터를 생성 하 고 파일에 저장

저장 프로시저는 명확하게 직접 볼 수 없는 varbinary 데이터 스트림으로 이미지를 반환합니다. 그러나 **bcp** 유틸리티를 사용하여 varbinary 데이터를 가져오고 클라이언트 컴퓨터에 이미지 파일로 저장할 수 있습니다.
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 다음 문을 실행합니다.
  
    ```SQL
    EXEC [dbo].[PlotHistogram]
    ```
  
    **결과**
    
    *그림*
    *0xFFD8FFE000104A4649...*
  
2.  PowerShell 명령 프롬프트를 열고 적절한 인스턴스 이름, 데이터베이스 이름, 사용자 이름 및 자격 증명을 인수로 제공하여 다음 명령을 실행합니다.
  
     ```
     bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  <database name>  -U <user name> -P <password>
     ```

    > [!NOTE]
    > Bcp에 대 한 명령 스위치 대/소문자를 구분 하지 않습니다.
  
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
    > 형식 정보를 파일(bcp.fmt)에 저장하는 경우 **bcp** 유틸리티는 그래픽 파일 형식 옵션을 묻는 메시지 없이 나중에 유사한 명령에 적용할 수 있는 형식 정의를 생성합니다. 서식 파일을 사용하려면 명령줄의 끝, password 인수 뒤에 `-f bcp.fmt` 를 추가합니다.
  
4.  PowerShell 명령을 실행한 곳과 동일한 디렉터리에 출력 파일이 만들어집니다. 그림을 보려면 plot.jpg 파일을 열기만 하면 됩니다.
  
    ![팁이 있는 택시 여정 및 팁이 없는 택시 여정](media/rsql-devtut-tippedornot.jpg "팁이 있는 택시 여정 및 팁이 없는 택시 여정")  
  
### <a name="export-the-plot-data-to-a-viewable-file"></a>그리기 데이터를 볼 수 있는 파일로 내보내기

이진 데이터에는 R 플롯을 출력 형식에 대 한 응용 프로그램에 의해 소비 편리할 수 있습니다 하지만 데이터 탐색 단계에서 렌더링 된 그림을 필요로 하는 데이터 과학자에 매우 유용 하지 않습니다. 일반적으로 데이터 과학자는 여러 관점에서 데이터에 대한 이해를 넓히기 위해 여러 데이터 시각화를 생성합니다.

사용자에 대 한 그래프를 생성 하려면와 같은 인기 있는 형식에서 R의 출력을 작성 하는 저장된 프로시저를 사용할 수 있습니다. JPG, 합니다. PDF, 및입니다. PNG 합니다. 저장 프로시저가 그래픽을 만든 후 파일을 열어 그림을 시각화하면 됩니다.

1. 새 저장된 프로시저를 만드는 _PlotInOutputFiles_, 히스토그램, scatterplots, 및 기타 R 그래픽을 작성 하는 방법을 보여 주는 합니다. JPG 및 합니다. PDF 형식입니다.

    [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 새 **쿼리** 창 및 다음에 붙여넣은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문.
  
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
  
        대부분의 포함된 R 스크립트는 `plot` 또는 `hist`와 같은 이러한 그래픽 함수의 옵션을 나타냅니다.
  
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

3. 플롯을 보려면 대상 폴더를 열고 저장된 프로시저에서 R 코드에서 생성 된 파일을 검토 합니다.

    + 파일 `rHistogram_Tipped.jpg` 입니다. 팁이 나타나지 trips 및 팁을 (를) 가져왔습니다와의 수를 보여 줍니다. (이 히스토그램은 이전 단계에서 생성 된 매우 유사한.)

    + 파일 `rHistograms_Tip_and_Fare_Amount.pdf` 요금 총액에 대해 그릴 팁 수량의 분포를 보여 줍니다.
    
    ![tip_amount 및 fare_amount 보여 주는 히스토그램](media/rsql-devtut-tipamtfareamt.PNG "tip_amount 및 fare_amount 보여 주는 히스토그램")

    + 파일 `rXYPlots_Tip_vs_Fare_Amount.pdf` y 축에 x 축에 요금 양 및 팁 scatterplot를 포함 합니다.

    ![팁 양 요금 비용을 초과 표시](media/rsql-devtut-tipamtbyfareamt.PNG "팁 양 요금 비용을 초과 표시 됩니다.")

2.  파일을 다른 폴더에 출력하려면 저장 프로시저에 포함된 R 스크립트의 `mainDir` 변수 값을 변경합니다. 다른 형식, 더 많은 파일 등을 출력하도록 스크립트를 수정할 수도 있습니다.

## <a name="next-lesson"></a>다음 단원

[4 단원: T-SQL을 사용 하 여 데이터 기능 만들기](../tutorials/sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>이전 단원

[2 단원: SQL server PowerShell을 사용 하 여 데이터 가져오기](../r/sqldev-import-data-to-sql-server-using-powershell.md)

---
title: 'R + T-SQL 자습서: 데이터 살펴보기'
description: R 함수를 사용하여 SQL Server 데이터를 살펴보고 시각화하는 방법을 보여주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 213db5ee9b88f7af34e3d000fc0f3b241d8e5791
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73725229"
---
# <a name="lesson-1-explore-and-visualize-the-data"></a>1단원: 데이터 탐색 및 시각화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서는 SQL Server에서 R을 사용하는 방법에 대한 SQL 개발자를 위한 자습서의 일부입니다.

이 단계에서는 샘플 데이터를 살펴본 다음, [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)의 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) 및 기본 R의 제네릭 [Hist](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist) 함수를 사용하여 몇 가지 플롯을 생성합니다. 이러한 R 함수는 이미 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에 포함되어 있습니다.

이 단원의 핵심 목표는 저장 프로시저의 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 R 함수를 호출하고 결과를 애플리케이션 파일 형식으로 저장하는 방법을 보여주는 것입니다.

+ **RxHistogram**을 사용하여 저장 프로시저를 만들어 varbinary 데이터로 R 플롯을 생성합니다. **bcp**를 사용하여 이진 스트림을 이미지 파일로 내보냅니다.
+ **Hist**를 사용하여 저장 프로시저를 만들어 플롯을 생성하고 결과를 JPG 및 PDF 출력으로 저장합니다.

> [!NOTE]
> 시각화는 데이터 모양 및 분포를 이해하는 데 매우 효과적인 도구이므로 R은 히스토그램, 산점도, 상자 그림 및 기타 데이터 탐색 그래프를 생성하는 데 필요한 다양한 함수 및 패키지를 제공합니다. R은 일반적으로 그래픽 출력용 R 디바이스를 사용하여 이미지를 만들므로 애플리케이션에서 렌더링할 **varbinary** 데이터 형식으로 캡처 및 저장할 수 있습니다. 또한 모든 지원 파일 형식(.JPG, .PDF 등)에 이미지를 저장할 수도 있습니다.

## <a name="review-the-data"></a>데이터 검토

일반적으로 데이터 과학 솔루션 개발에는 데이터 탐색 및 데이터 시각화가 많이 포함됩니다. 따라서 샘플 데이터를 검토하지 않은 경우 먼저 검토합니다.

원래 공용 데이터 세트에서는 택시 식별자 및 여정 레코드가 별도 파일로 제공되었습니다. 그러나 샘플 데이터를 쉽게 사용할 수 있도록 두 개의 원래 데이터 세트가 _medallion_, _hack\_license_ 및 _pickup\_datetime_ 열에 조인되었습니다.  레코드도 원래 레코드 수의 1%만 가져오도록 샘플링되었습니다. 다운 샘플링된 결과 데이터 세트에는 1,703,957개의 행과 23개 열이 있습니다.

**택시 식별자**
  
-   _medallion_ 열은 택시의 고유 ID 번호를 나타냅니다.
  
-   _hack\_license_ 열은 택시 기사의 운전 면허 번호(익명)를 포함합니다.
  
**여정 및 요금 레코드**
  
-   각 여정 레코드에는 승하차 위치 및 시간과 여정 거리가 포함됩니다.
  
-   각 요금 레코드에는 지불 유형, 총 지불 금액, 팁 금액 등의 지불 정보가 포함됩니다.
  
-   마지막 세 열은 다양한 Machine Learning 작업에 사용할 수 있습니다. _tip\_amount_ 열에는 연속 숫자 값이 포함되며 회귀 분석의 **레이블** 열로 사용할 수 있습니다. _tipped_ 열에는 예/아니요 값만 포함되며 이진 분류에 사용됩니다. _tip\_class_ 열에는 여러 개의 **클래스 레이블**이 포함되므로 다중 클래스 분류 작업의 레이블로 사용할 수 있습니다.
  
    이 연습에서는 이진 분류 작업만 보여 주지만, 다른 두 가지 Machine Learning 작업인 회귀 및 다중 클래스 분류 모델도 구축해 보세요.
  
-   레이블 열에 사용되는 값은 모두 다음과 같은 비즈니스 규칙을 사용하여 _tip\_amount_ 열을 기반으로 합니다.
  
    |파생 열 이름|규칙|
    |-|-|
     |tipped|If tip_amount > 0, tipped = 1, otherwise tipped = 0|
    |tip_class|Class 0: tip_amount = $0<br /><br />Class 1: tip_amount > $0 and tip_amount <= $5<br /><br />Class 2: tip_amount > $5 and tip_amount <= $10<br /><br />Class 3: tip_amount > $10 and tip_amount <= $20<br /><br />Class 4: tip_amount > $20|

## <a name="create-a-stored-procedure-using-rxhistogram-to-plot-the-data"></a>rxHistogram을 사용하여 데이터를 그리는 저장 프로시저 만들기

플롯을 만들려면 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)에 제공되는 향상된 R 함수 중 하나인 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)을 사용합니다. 이 단계에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리의 데이터를 기반으로 하는 히스토그램을 그립니다. 이 함수를 저장 프로시저 **PlotRxHistogram**에 래핑할 수 있습니다.

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **NYCTaxi_Sample** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.

2. 다음 스크립트를 붙여넣어 히스토그램을 그리는 저장 프로시저를 만듭니다. 이 예의 이름은 **RPlotRxHistogram*입니다.

    ```sql
    CREATE PROCEDURE [dbo].[RxPlotHistogram]
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

이 스크립트에서 이해해야 할 핵심 사항은 다음과 같습니다. 
  
+ `@query` 변수는 스크립트 입력 변수`'SELECT tipped FROM nyctaxi_sample'`에 대한 인수로 R 스크립트에 전달되는 쿼리 텍스트( `@input_data_1`)를 정의합니다. 외부 프로세스로 실행되는 R 스크립트의 경우 스크립트에 대한 입력과 SQL Server에서 R 세션을 시작하는 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 시스템 저장 프로시저에 대한 입력 간의 일대일 매핑이 있어야 합니다.
  
+ R 스크립트 내에 이미지를 저장하는 변수(`image_file`)가 정의됩니다. 

+ RevoScaleR 라이브러리의 **rxHistogram** 함수가 호출되어 플롯이 생성됩니다.
  
+ 이 명령을 SQL Server에서 외부 스크립트로 실행하고 있기 때문에 R 디바이스는 **꺼짐**으로 설정되어 있습니다. 일반적으로 R에서 높은 수준의 그리기 명령을 실행하면 R에서 *디바이스*라는 그래픽 창이 열립니다. 파일에 쓰거나 다른 방법으로 출력을 처리하는 경우 디바이스를 끌 수 있습니다.
  
+ R 그래픽 개체는 출력을 위해 R data.frame으로 직렬화됩니다.

### <a name="execute-the-stored-procedure-and-use-bcp-to-export-binary-data-to-an-image-file"></a>저장 프로시저를 실행하고 bcp를 사용하여 이진 데이터를 이미지 파일로 내보내기

저장 프로시저는 명확하게 직접 볼 수 없는 varbinary 데이터 스트림으로 이미지를 반환합니다. 그러나 **bcp** 유틸리티를 사용하여 varbinary 데이터를 가져오고 클라이언트 컴퓨터에 이미지 파일로 저장할 수 있습니다.
  
1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 다음 문을 실행합니다.
  
    ```sql
    EXEC [dbo].[RxPlotHistogram]
    ```
  
    **결과**
    
    *plot* *0xFFD8FFE000104A4649...*
  
2. PowerShell 명령 프롬프트를 열고 적절한 인스턴스 이름, 데이터베이스 이름, 사용자 이름 및 자격 증명을 인수로 제공하여 다음 명령을 실행합니다. Windows ID를 사용하는 경우 **-U** 및 **-P**를 **-T**로 바꿀 수 있습니다.
  
    ```powershell
    bcp "exec RxPlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  NYCTaxi_Sample  -U <user name> -P <password> -T
    ```

    > [!NOTE]
    > bcp에 대한 명령 스위치는 대/소문자를 구분합니다.
  
3. 연결에 성공하면 그래픽 파일 형식에 대한 자세한 정보를 입력하라는 메시지가 표시됩니다. 

   다음과 같은 변경을 제외하고 각 프롬프트에서 Enter 키를 눌러 기본값을 적용합니다.
    
   + **prefix-length of field plot**에 대해 0을 입력합니다.
  
   + 나중에 다시 사용하기 위해 출력 매개 변수를 저장하려는 경우 **Y** 를 입력합니다.
  
    ```powershell
    Enter the file storage type of field plot [varbinary(max)]: 
    Enter prefix-length of field plot [8]: 0
    Enter length of field plot [0]:
    Enter field terminator [none]:
  
    Do you want to save this format information in a file? [Y/n]
    Host filename [bcp.fmt]:
    ```
  
    **결과**
    
    ```powershell
    Starting copy...
    1 rows copied.
    Network packet size (bytes): 4096
    Clock Time (ms.) Total     : 3922   Average : (0.25 rows per sec.)
    ```

    > [!TIP]
    > 형식 정보를 파일(bcp.fmt)에 저장하는 경우 **bcp** 유틸리티는 그래픽 파일 형식 옵션을 묻는 메시지 없이 나중에 유사한 명령에 적용할 수 있는 형식 정의를 생성합니다. 서식 파일을 사용하려면 명령줄의 끝, password 인수 뒤에 `-f bcp.fmt` 를 추가합니다.
  
4.  PowerShell 명령을 실행한 곳과 동일한 디렉터리에 출력 파일이 만들어집니다. 그림을 보려면 plot.jpg 파일을 열기만 하면 됩니다.
  
    ![팁을 받거나 받지 못한 택시 운행](media/rsql-devtut-tippedornot.jpg "팁을 받거나 받지 못한 택시 운행")  
  
## <a name="create-a-stored-procedure-using-hist-and-multiple-output-formats"></a>Hist 및 여러 출력 형식을 사용하여 저장 프로시저 만들기

일반적으로 데이터 과학자는 여러 관점에서 데이터에 대한 이해를 넓히기 위해 여러 데이터 시각화를 생성합니다. 이 예에서는 JPG 및 PDF 형식으로 히스토그램, 산점도 및 기타 R 그래픽을 작성하는 **RPlotHist**라는 저장 프로시저를 만듭니다.

이 저장 프로시저는 **Hist** 함수를 사용하여 히스토그램을 만들고 이진 데이터를 .JPG, .PDF 및 .PNG와 같은 대중적인 형식으로 내보냅니다. 

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **NYCTaxi_Sample** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.

2. 다음 스크립트를 붙여넣어 히스토그램을 그리는 저장 프로시저를 만듭니다. 이 예의 이름은 **RPlotHist**입니다.
  
    ```sql
    CREATE PROCEDURE [dbo].[RPlotHist]  
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
  
+ 저장 프로시저 내의 SELECT 쿼리 출력은 기본 R 데이터 프레임인 `InputDataSet`에 저장됩니다. 그런 다음 다양한 R 그리기 함수를 호출하여 실제 그래픽 파일을 생성할 수 있습니다. 대부분의 포함된 R 스크립트는 `plot` 또는 `hist`와 같은 이러한 그래픽 함수의 옵션을 나타냅니다.
  
+ 모든 파일은 로컬 폴더 C:\temp\Plots에 저장됩니다. 대상 폴더는 R 스크립트에 저장 프로시저의 일부로 제공되는 인수에 의해 정의됩니다.  `mainDir`변수 값을 변경하여 대상 폴더를 변경할 수 있습니다.

+ 파일을 다른 폴더에 출력하려면 저장 프로시저에 포함된 R 스크립트의 `mainDir` 변수 값을 변경합니다. 다른 형식, 더 많은 파일 등을 출력하도록 스크립트를 수정할 수도 있습니다.

### <a name="execute-the-stored-procedure"></a>저장 프로시저 실행

다음 명령문을 실행하여 이진 플롯 데이터를 JPEG 및 PDF 파일 형식으로 내보냅니다.

```sql
EXEC RPlotHist
```

**결과**
    
```sql
STDOUT message(s) from external script:
[1] Creating output plot files:[1] C:\temp\plots\rHistogram_Tipped_18887f6265d4.jpg[1] 

C:\temp\plots\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]

C:\temp\plots\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf
```

기존 파일에 쓰려고 할 때 오류가 발생하지 않도록 파일 이름의 숫자가 임의로 생성됩니다.

### <a name="view-output"></a>출력 보기 

플롯을 보려면 대상 폴더를 열고 저장 프로시저의 R 코드를 통해 생성된 파일을 검토합니다.

1. STDOUT 메시지에 지정된 폴더로 이동합니다(이 예에서는 C:\temp\plots\)).

2. 팁을 받은 운행 수와 팁을 받지 못한 운행 수를 표시하려면 `rHistogram_Tipped.jpg`를 엽니다. 이 히스토그램은 이전 단계에서 생성한 히스토그램과 매우 비슷합니다.

3. 요금을 기준으로 그려진 팁 금액 분포를 보려면 `rHistograms_Tip_and_Fare_Amount.pdf`를 엽니다.
    
  ![tip_amount 및 fare_amount를 보여주는 히스토그램](media/rsql-devtut-tipamtfareamt.PNG "tip_amount 및 fare_amount를 보여주는 히스토그램")

4. x축에 요금, y축에 팁 금액이 표시된 산점도를 보려면 `rXYPlots_Tip_vs_Fare_Amount.pdf`를 엽니다.

   ![요금을 기준으로 그려진 팁 금액](media/rsql-devtut-tipamtbyfareamt.PNG "요금을 기준으로 그려진 팁 금액")

## <a name="next-lesson"></a>다음 단원

[2단원: T-SQL을 사용하여 데이터 요소 만들기](sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>이전 단원

[NYC Taxi 데모 데이터 설정](demo-data-nyctaxi-in-sql.md)

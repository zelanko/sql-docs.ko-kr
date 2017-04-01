---
title: "1단원: 데이터 준비(데이터 과학 종단 간 연습) | Microsoft Docs"
ms.custom: ""
ms.date: "03/18/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 65fd41d4-c94e-4929-a24a-20e792a86579
caps.latest.revision: 29
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 25
---
# 1단원: 데이터 준비(데이터 과학 종단 간 연습)
이 연습을 준비하려면 다음을 수행해야 합니다.

1. 연습에 사용되는 데이터 및 모든 R 스크립트를 다운로드합니다. GitHub에서의 다운로드로를 간소화하기 위해 PowerShell 스크립트가 제공됩니다.   

2. 서버와 R 워크스테이션 둘 다에서 몇 가지 추가 R 패키지를 설치합니다.  

3. 모델링 및 점수 매기기에 사용되는 데이터베이스 및 데이터를 포함하여 환경을 준비합니다.
 
    이를 위해 두 번째 PowerShell 스크립트 RunSQL_R_Walkthrough.ps1을 사용합니다.
    스크립트는 데이터베이스를 구성하고 지정한 테이블에 데이터를 업로드합니다.  또한 데이터 과학 태스크를 간소화하는 몇 가지 SQL 함수 및 저장 프로시저를 만듭니다. 
 

## <a name="1-download-the-data-and-scripts"></a>1. 데이터 및 스크립트 다운로드  
이 연습을 완료하는 데 필요한 모든 코드는 GitHub 리포지토리에 제공되어 있습니다. PowerShell 스크립트를 사용하여 파일의 로컬 복사본을 만들 수 있습니다.  
  
#### <a name="to-download-all-scripts-using-powershell"></a>PowerShell을 사용하여 모든 스크립트를 다운로드하려면  
  
1.  데이터 과학 클라이언트 컴퓨터에서 관리자 권한으로 Windows PowerShell 명령 프롬프트를 엽니다.  
  
2.  이 인스턴스에서 이전에 PowerShell을 실행한 적이 없거나 스크립트를 실행할 수 있는 권한이 없는 경우 오류가 발생할 수도 있습니다. 이 경우 스크립트를 실행하기 전에 이 명령을 실행하여 시스템 기본값을 변경하지 않고 일시적으로 스크립트를 허용합니다.  
  
    ```  
    Set-ExecutionPolicy Unrestricted -Scope Process -Force  
    ```  
  
3.  다음 명령을 실행하여 스크립트 파일을 로컬 디렉터리로 다운로드합니다. 다른 디렉터리를 지정하지 않으면 기본적으로 c:\tempR이 만들어지고 모든 파일이 해당 위치에 저장됩니다.  
  
    ```  
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_R_Walkthrough.ps1'  
    $ps1_dest = "$pwd\Download_Scripts_R_Walkthrough.ps1"  
    $wc = New-Object System.Net.WebClient  
    $wc.DownloadFile($source, $ps1_dest)  
    .\Download_Scripts_R_Walkthrough.ps1 –DestDir 'C:\tempR'  
  
    ```  
  
    다른 디렉터리에 파일을 저장하려는 경우 *DestDir* 매개 변수의 값을 편집하고 컴퓨터의 다른 폴더를 지정합니다. 존재하지 않는 폴더 이름을 입력하면 PowerShell 스크립트에서 폴더를 만듭니다.  
  
4.  다운로드가 완료된 후 Windows PowerShell 명령 콘솔은 다음과 같이 표시됩니다.  
  
    ![After completion of PowerShell script](../../advanced-analytics/r-services/media/rsql-e2e-psscriptresults.PNG "After completion of PowerShell script")  
  
5.  PowerShell 콘솔에서 `ls` 명령을 실행하여 *DestDir*에 다운로드된 파일 목록을 확인할 수 있습니다.  파일 목록 및 설명은 [포함된 항목](#What-the-Download-Includes)을 참조하세요.
  
## <a name="2-install-required-packages"></a>2. 필요한 패키지 설치  
이 연습을 수행하려면 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]의 일부로 기본적으로 설치되지 않는 일부 R 라이브러리가 필요합니다. 솔루션을 개발할 클라이언트 및 솔루션을 배포할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 둘 다에 패키지를 설치해야 합니다.  
  
### <a name="install-required-packages-on-the-client"></a>클라이언트에 필요한 패키지 설치  
다운로드한 R 스크립트에는 이러한 패키지를 다운로드 및 설치하는 명령이 포함되어 있습니다.  
  
1.  R 환경에서 스크립트 파일 RSQL_R_Walkthrough.R을 엽니다.  
  
2.  해당 줄을 강조 표시하고 실행합니다.  
  
    ```  
    # Install required R libraries for this walkthrough if they are not installed.   
  
    if (!('ggmap' %in% rownames(installed.packages()))){  
      install.packages('ggmap')  
    }  
    if (!('mapproj' %in% rownames(installed.packages()))){  
      install.packages('mapproj')  
    }  
    if (!('ROCR' %in% rownames(installed.packages()))){  
      install.packages('ROCR')  
    }  
    if (!('RODBC' %in% rownames(installed.packages()))){  
      install.packages('RODBC')  
    }  
    ```  
  
### <a name="install-required-packages-on-the-server"></a>서버에 필요한 패키지 설치  

  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 관리자 권한으로 RGui.exe를 엽니다.  기본값을 사용하여 SQL Server R Services를 설치한 경우 RGui.exe는 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64)에 있습니다.  
  
    또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 다른 R 환경을 설치한 경우(예: RStudio) R 콘솔을 사용하여 명령을 실행할 수 있습니다.  
  
2.  R 프롬프트에서 다음 R 명령을 실행합니다.  
  
    ```  
    install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])  
    install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    ```  
  
**참고:**  
  
-   이 예제에서는 R grep 함수를 사용하여 사용 가능한 경로의 벡터를 검색하고 "program files"에서 하나를 찾습니다. 자세한 내용은 [http://www.rdocumentation.org/packages/base/functions/grep](http://www.rdocumentation.org/packages/base/functions/grep)을 참조하세요.   
  
-   패키지가 이미 설치된 경우 R 함수 `installed.packages()`를 사용하여 설치된 패키지 목록을 확인합니다.  
  
-   클라이언트에서 Program Files의 기본 라이브러리에 쓸 수 없는 경우 사용자 라이브러리를 설치할 수 있습니다. 그러나 SQL Server 컴퓨터에 패키지를 설치할 때 SQL Server R Services에서 사용하는 기본 라이브러리에 설치해야 합니다. 사용자 라이브러리를 사용하지 마세요. 자세한 내용은 [SQL Server에 새 R 패키지 설치](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)를 참조하세요.
      

## <a name="3-run-powershell-script-runsqlrwalkthroughps1"></a>3. Powershell 스크립트 RunSQL_R_Walkthrough.ps1 실행  

솔루션을 빌드할 컴퓨터(예: R 코드를 개발하고 테스트하는 컴퓨터)에서 이 PowerShell 스크립트를 실행할 수 있습니다. 이 컴퓨터에서 명명된 파이프 프로토콜을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 연결할 수 있어야 합니다.  
  
스크립트는 다음과 같은 작업을 수행합니다.  
  
-   SQL Native Client 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 용 명령줄 유틸리티가 설치되어 있는지 확인합니다. 명령줄 도구는 SQL 테이블에 데이터를 빠르게 대량 로드하는 데 사용되는 [bcp 유틸리티](../../tools/bcp-utility.md)를 실행하는 데 필요합니다.    
-   지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결한 다음 데이터베이스를 구성하고 모델 및 데이터를 위한 테이블을 만드는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 실행합니다.    
-   SQL 스크립트를 실행하여 여러 개의 저장 프로시저를 만듭니다.    
-   이전에 다운로드한 데이터를 nyctaxi_sample 테이블에 로드합니다.    
-   지정한 데이터베이스 이름을 사용하도록 R 스크립트 파일의 인수를 다시 작성합니다. 

### <a name="to-run-the-script"></a>스크립트를 실행하려면
  
1.  관리자 권한으로 PowerShell 명령줄을 엽니다.    
  
2.  스크립트를 다운로드한 폴더로 이동한 다음 스크립트 이름을 표시된 대로 입력합니다. Enter 키를 누릅니다.  
  
    ```  
    .\RunSQL_R_Walkthrough.ps1  
    ```  
  
3.  다음 매개 변수를 확인하는 메시지가 각각 표시됩니다.  
  
    - 만들려는 데이터베이스 이름입니다. 
      예를 들어 입력 **Tutorial** 또는 **Taxi**를 입력할 수 있습니다.  
    - 스크립트를 실행할 자격 증명입니다. 옵션에는
        + CREATE DATABASE 권한이 있는 SQL 로그인의 이름을 입력하고 연속된 프롬프트에서 SQL 암호를 제공합니다.
        + Windows ID를 사용할 이름을 입력하지 않고 Enter 키를 누른 다음 Windows 암호를 입력합니다. PowerShell에서는 다른 Windows 사용자 이름을 입력할 수 없습니다. 

          유효한 사용자를 지정하지 않으면 스크립트가 기본적으로 Windows 통합 인증을 사용하도록 설정됩니다.  
  
    -   데이터베이스에 업로드할 csv 파일의 전체 경로입니다.  
  
        스크립트에서 파일을 다운로드하고 데이터베이스에 데이터를 자동으로 로드하지만, 이 작업이 실패할 경우 언제든지 수동으로 데이터를 업로드할 수 있습니다.  
  
4.  Enter 키를 눌러 스크립트를 실행합니다.  
  
## <a name="troubleshooting"></a>문제 해결  
 
 문제가 발생한 경우 PowerShell 스크립트의 줄을 예제로 사용하여 전체 또는 일부 단계를 수동으로 실행할 수 있습니다. 
 

### <a name="the-powershell-script-didnt-download-the-data"></a>PowerShell 스크립트가 데이터를 다운로드하지 않음
  
데이터를 수동으로 다운로드하려면 다음 링크를 마우스 오른쪽 단추로 클릭하고 **다른 이름으로 대상 저장**을 선택합니다.  
  
[http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv](http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv)  
  
다운로드한 데이터 파일의 경로와 데이터가 저장된 파일 이름을 적어둡니다. **bcp**를 사용하여 데이터를 테이블에 로드하려면 경로가 필요합니다.  
  
### <a name="i-was-unable-to-download-the-data"></a>사용자가 데이터를 다운로드할 수 없음
데이터 파일이 큽니다. 인터넷 연결이 양호한 컴퓨터를 사용하세요. 그렇지 않으면 다운로드 시간이 초과될 수 있습니다.  

  
### <a name="could-not-connect-or-script-failed"></a>연결할 수 없거나 스크립트에서 오류가 발생함  
  
+ 인스턴스 이름의 철자를 확인합니다. 
+ 전체 연결 문자열을 확인합니다.    
+ 네트워크 요구 사항에 따라 하나 이상의 서브넷 이름을 사용하여 인스턴스 이름을 한정해야 할 수도 있습니다.  예를 들어 MYSERVER가 작동하지 않는 경우 myserver.subnet.mycompany.com을 사용해 보세요.
  
### <a name="network-error-or-protocol-not-found"></a>네트워크 오류 또는 프로토콜을 찾을 수 없음  
  
+ 인스턴스에서 원격 연결을 지원하는지 확인합니다.    
+ 지정된 SQL 사용자가 원격으로 데이터베이스에 연결할 수 있는지, 인스턴스에서 명명된 파이프가 사용하도록 설정되었는지 확인합니다.    
+ 계정의 사용 권한을 확인합니다. 지정한 계정에 새 데이터베이스를 만들고 데이터를 업로드할 수 있는 권한이 없을 수 있습니다.  

### <a name="bcp-did-not-run"></a>bcp을 실행하지 못함  

+ 컴퓨터에서 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용할 수 있는지 확인합니다. PowerShell 창 또는 Windows 명령 프롬프트에서 bcp를 실행할 수 있습니다.
+ 오류가 발생할 경우 bcp 유틸리티의 위치를 PATH 시스템 환경 변수에 추가한 후 다시 시도합니다.  

### <a name="the-table-schema-was-created-but-there-is-no-data-in-the-table"></a>테이블 스키마가 생성되었지만 테이블에 데이터가 없음

스크립트의 나머지 부분이 문제 없이 실행된 경우 다음과 같이 명령줄에서 **bcp**를 호출하여 수동으로 테이블에 데이터를 업로드할 수 있습니다.  


 
**SQL 로그인 사용**
    
~~~~ 
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U <SQL login> -P <password  
~~~~  
  
**Windows 인증 사용**  

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -T 
~~~~ 
  
  
+ **in** 키워드는 데이터 이동 방향을 지정합니다.  
+ **-f** 인수를 사용하려면 서식 파일의 전체 경로를 지정해야 합니다. **in** 옵션을 사용하는 경우 서식 파일이 필요합니다.
+ SQL 로그인과 함께 bcp를 실행하는 경우 **-U** 및 **-P** 인수를 사용합니다.
+ Windows 통합 인증을 사용하는 경우 **-T** 인수를 사용합니다. 

  
### <a name="how-can-i-run-the-script-without-prompts"></a>프롬프트 없이 스크립트를 실행하는 방법  
  
환경과 관련된 값을 사용하여 모든 매개 변수를 단일 명령줄에서 지정할 수 있습니다. 
  
```  
.\RunSQL_R_Walkthrough.ps1 -server <server address> -dbname <new db name> -u <user name> -p <password> -csvfilepath <path to csv file>  
```  
  
예를 들어 SQL 로그인을 사용하여 스크립트를 실행하려면 다음을 실행합니다.  
  
```  
.\RunSQL_R_Walkthrough.ps1 -server MyServer.subnet.domain.com -dbname MyDB –u SqlUserName –p SqlUsersPassword -csvfilepath C:\temp\nyctaxi1pct.csv  
```  
  
이 예에서는 다음을 수행합니다.  
  
-   *SqlUserName*의 자격 증명을 사용하여 지정된 인스턴스 및 데이터베이스에 연결합니다.  
-   *C:\temp\nyctaxi1pct.csv* 파일에서 데이터를 가져옵니다.  
-   *MyServer*라는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 *MyDB*데이터베이스에 있는 *dbo.nyctaxi_sample* 테이블에 데이터를 로드합니다.  

### <a name="the-data-loaded-but-it-contains-duplicates"></a>데이터가 로드되었지만 중복 항목이 포함되어 있음

기존 테이블이 있고 올바른 스키마를 사용하는 경우 bcp는 계속 실행되지만 기존 데이터를 덮어쓰지 않고 데이터의 새 복사본을 삽입합니다. 이 경우 중복 데이터가 발생합니다.  스크립트를 다시 실행하기 전에 기존 테이블을 잘라야 합니다.

## <a name="what-the-download-includes"></a>다운로드에 포함되는 항목

GitHub 리포지토리에서 파일을 다운로드하는 경우 다음 항목이 포함됩니다.
+ CSV 형식의 데이터
+ 환경을 준비하기 위한 PowerShell 스크립트
+ bcp를 사용하여 SQL Server에 데이터를 가져오기 위한 XML 서식 파일
+ 여러 T-SQL 스크립트
+ 이 연습을 실행하는 데 필요한 모든 R 코드

### <a name="training-and-scoring-data"></a>교육 및 점수 매기기 데이터  
데이터는 각 여정의 요금 및 지불된 팁 금액을 비롯하여 2013년 17,300만 개별 여정의 레코드를 포함하는 뉴욕시 택시 데이터 집합의 대표 샘플링입니다.  이 데이터가 원래 수집된 방법 및 전체 데이터 집합을 가져올 수 있는 방법에 대한 자세한 내용은 다음을 참조하세요.  
[http://chriswhong.com/open-data/foil_nyc_taxi/](http://chriswhong.com/open-data/foil_nyc_taxi/).  
  
데이터를 쉽게 사용할 수 있도록 Microsoft 데이터 과학 팀은 1%의 데이터만 가져오는 다운 샘플링을 수행했습니다.  이 데이터는 Azure의 공용 Blob Storage 컨테이너에서 .CSV 형식으로 공유되었습니다. 원본 데이터는 350MB 미만의 압축되지 않은 파일입니다.  
 
### <a name="files"></a>파일

 
+ **RunSQL_R_Walkthrough.ps1** 먼저 PowerShell을 사용하여 이 스크립트를 실행합니다. SQL 스크립트를 호출하여 데이터베이스에 데이터를 로드합니다.  
    
+ **taxiimportfmt.xml** BCP 유틸리티에서 데이터베이스에 데이터를 로드하는 데 사용하는 형식 정의 파일입니다.
      
+ **RSQL_R_Walkthrough.R** 단원의 나머지 부분에서 데이터 분석 및 모델링에 사용할 핵심 R 스크립트입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 탐색하고, 분류 모델을 작성하고, 그림을 만드는 데 필요한 R 코드를 모두 제공합니다.   
  
### <a name="sql-scripts"></a>SQL 스크립트  
이 PowerShell 스크립트는 서버에서 여러 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 실행합니다. 다음 표에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일이 나와 있습니다.  
  
|SQL 스크립트 파일 이름|수행하는 작업|  
|------------------------|----------------|  
|create-db-tb-upload-data.sql|데이터베이스와 다음 두 개의 테이블을 만듭니다.<br /><br /> *nyctaxi_sample*: 교육 데이터(NYC 택시 데이터 집합의 1% 샘플)를 저장하는 테이블입니다. 저장소 및 쿼리 성능 향상을 위해 클러스터형 columnstore 인덱스가 테이블에 추가됩니다.<br /><br /> *nyc_taxi_models*: 나중에 학습된 분류 모델을 저장하는 데 사용할 빈 테이블입니다.|  
|PredictTipBatchMode.sql|학습된 모델을 호출하여 새 관찰에 대한 레이블을 예측하는 저장 프로시저를 만듭니다. 쿼리를 입력 매개 변수로 허용합니다.|  
|PredictTipSingleMode.sql|학습된 분류 모델을 호출하여 새 관찰에 대한 레이블을 예측하는 저장 프로시저를 만듭니다. 새 관찰의 변수가 인라인 매개 변수로 전달됩니다.|  
|PersistModel.sql|데이터베이스의 테이블에 분류 모델의 이진 표현을 저장하는 데 도움이 되는 저장 프로시저를 만듭니다.|  
|fnCalculateDistance.sql|승하차 위치 사이의 직접 거리를 계산하는 SQL 스칼라 반환 함수를 만듭니다.|  
|fnEngineerFeatures.sql|분류 모델 학습을 위한 기능을 만드는 SQL 테이블 반환 함수를 만듭니다.|  
  
이 연습에 사용된 모든 SQL 쿼리는 테스트되었으며 R 코드에서 있는 그대로 실행할 수 있습니다. 그러나 SQL 쿼리를 사용하여 고유한 솔루션을 개발하거나 추가로 실험하려는 경우 R 코드에 추가하기 전에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 등의 개발 환경을 사용하여 쿼리를 먼저 테스트 및 튜닝하는 것이 좋습니다.  
  
  
## <a name="next-lesson"></a>다음 단원  
[2단원: 데이터 보기 및 탐색&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>이전 단원  
[데이터 과학 종단 간 연습](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)  
  
  
  

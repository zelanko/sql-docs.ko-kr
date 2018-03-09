---
title: "PowerShell를 사용한 데이터 준비(연습) | Microsoft Docs"
ms.custom: 
ms.date: 11/10/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 65fd41d4-c94e-4929-a24a-20e792a86579
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: a1ed4da0aca0b2876e2162c012aabc6c4043c567
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="prepare-the-data-using-powershell-walkthrough"></a>PowerShell를 사용한 데이터 준비(연습)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 시점까지 다음 중 하나를 설치해야 합니다.

+ SQL Server 2016 R Services
+ SQL Server 2017 Machine Learning Services, R 언어 사용

이 단원에서는 Github 리포지토리로부터 연습에 사용되는 데이터, R 패키지 및 R 스크립트를 다운로드합니다. 편의를 위해 PowerShell 스크립트를 사용하여 전체를 다운로드할 수 있습니다.

또한 서버와 R 워크스테이션 모두에 몇 가지 추가 R 패키지를 설치해야 합니다. 단계가 설명됩니다.

그런 다음 두 번째 PowerShell 스크립트인 RunSQL_R_Walkthrought.ps1을 사용해서 모델링과 채점에 사용되는 데이터베이스를 구성합니다. 이 스크립트는 지정한 데이터베이스로 데이터를 대량 로드한 다음 데이터 과학 작업을 단순화하기 위한 몇 가지 SQL 함수와 저장 프로시저를 생성합니다.

이제 시작 하겠습니다.

## <a name="1-download-the-data-and-scripts"></a>1. 데이터와 스크립트를 다운로드 합니다.

필요한 모든 코드가 GitHub 리포지토리에서 제공됩니다. PowerShell 스크립트를 사용하여 파일의 로컬 복사본을 만들 수 있습니다.

1.  데이터 과학 클라이언트 컴퓨터에서 관리자 권한으로 Windows PowerShell 명령 프롬프트를 엽니다.

2. 다운로드 스크립트를 오류 없이 실행하기 위해 아래 명령을 실행합니다. 시스템 기본값을 변경하지 않고 일시적으로 스크립트를 허용합니다.

    ```
    Set-ExecutionPolicy Unrestricted -Scope Process -Force
    ```
      
3.  3.	다음 Powershell 명령을 실행하여 스크립트 파일을 로컬 디렉터리로 다운로드합니다. 디렉터리를 다르게 지정하지 않으면 기본적으로 `C:\tempR` 폴더가 만들어지고 모든 파일이 저장됩니다.
  
    ```
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_R_Walkthrough.ps1'  
    $ps1_dest = "$pwd\Download_Scripts_R_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_R_Walkthrough.ps1 –DestDir 'C:\tempR'
    ```
  
    다른 디렉터리에 파일을 저장하려면 *DestDir* 매개 변수의 값을 편집해서 컴퓨터의 다른 폴더를 지정하십시오. 존재하지 않는 폴더 이름을 입력하면 PowerShell 스크립트가 해당 폴더를 만듭니다.
  
4. 	다운로드는 다소 시간이 걸릴 수 있습니다. 다운로드가 완료된 후 Windows PowerShell 명령 콘솔은 아래와 같이 표시됩니다.
  
    ![PowerShell 스크립트 완료 후](media/rsql-e2e-psscriptresults.PNG "PowerShell 스크립트 완료 후")
  
5.  PowerShell 콘솔에서 `ls` 명령을 실행하여 *DestDir*에 다운로드된 파일 목록을 확인할 수 있습니다.  파일에 대한 설명은 [샘플에 포함된 내용](#What-the-Download-Includes)을 참조합니다.

## <a name="2-install-required-r-packages"></a>2. 필수 R 패키지 설치

이 연습을 수행하려면 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]의 일부로 기본 설치되지 않는 몇 가지 R 라이브러리가 필요합니다. 솔루션을 개발하는 클라이언트와 솔루션을 배포하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 양쪽 모두에 패키지를 설치해야 합니다.

### <a name="install-required-packages-on-the-client"></a>클라이언트에 필수 패키지 설치

다운로드한 R 스크립트에는 이러한 패키지를 다운로드하고 설치하는 명령이 포함되어 있습니다.

1. R 환경에서 스크립트 파일 RSQL_R_Walkthrough.R을 엽니다.

2. 아래 행을 강조 표시하고 실행합니다.
    
    ```
    # Install required R libraries, if they are not already installed.
    if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
    if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
    if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
    if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
    ```
    
    일부 패키지는 필요한 패키지도 설치합니다. 모두 약 32개의 패키지가 필요합니다.

### <a name="install-required-packages-on-the-server"></a>서버에 필수 패키지 설치

SQL Server에 패키지를 설치할 수 있는 여러가지 방법이 있습니다. 예를 들어 SQL Server는 데이터베이스 관리자가 패키지 리포지토리를 만들고 사용자가 자신의 패키지를 설치할 수 있도록 권한을 할당할 수 있는 [패키지 관리](../r/installing-and-managing-r-packages.md) 기능을 제공합니다. 그런데 컴퓨터 관리자의 경우 R을 사용해서 새로운 패키지를 설치할 수도 있습니다.

> [!NOTE]
> 서버에서 메시지가 표시되더라도 사용자 라이브러리에 설치하지 마십시오. 사용자 라이브러리에 설치하지 마십시오. 사용자 라이브러리에 설치하면 SQL Server 인스턴스가 해당 패키지를 찾거나 실행할 수 없습니다. 자세한 내용은 [SQL Server에 새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)를 참조하세요.

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 RGui.exe를 **관리자 권한으로** 엽니다. 기본값으로 SQL Server R Services를 설치한 경우 RGui.exe는 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64)에 있습니다.

2.  R 프롬프트에서 다음 R 명령을 실행합니다.
  
    ```
    install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    ```

    - 이 예제에서는 벡터의 사용 가능한 경로 검색 하 고 "Program Files"를 포함 하는 경로 찾을 R grep 함수를 사용 합니다. 자세한 내용은 [http://www.rdocumentation.org/packages/base/functions/grep](http://www.rdocumentation.org/packages/base/functions/grep)을 참조하세요.

    - 패키지가 이미 설치되었다고 생각되면 `installed.packages()`를 실행하여 설치된 패키지 목록을 확인하십시오.

## <a name="3-prepare-the-environment-using-runsqlrwalkthroughps1"></a>3. RunSQL_R_Walkthrough.ps1으로 환경 준비

다운로드는 데이터 파일, R 스크립트, T-SQL 스크립트와 더불어 PowerShell 스크립트 `RunSQL_R_Walkthrough.ps1`을 포함합니다. 이 스크립트는 다음 작업을 수행합니다.

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 용 SQL Native Client와 명령줄 유틸리티가 설치되어 있는지 확인합니다. 명령줄 도구는 [bcp 유틸리티](../../tools/bcp-utility.md)를 실행하는 데 필요합니다. 이 유틸리티는 SQL 테이블에 데이터를 빠르게 대량 로드하는 데 사용됩니다.

- 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하고 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 실행해서 데이터베이스를 구성하고 모델과 데이터를 위한 테이블을 만듭니다.

- SQL 스크립트를 실행하여 여러 개의 저장 프로시저를 만듭니다.

- 이전에 다운로드한 데이터를 `nyctaxi_sample` 테이블에 로드합니다.

- 지정한 데이터베이스 이름을 사용하도록 R 스크립트 파일의 인수를 다시 씁니다.

솔루션을 작성할 수 있는 컴퓨터에서이 스크립트 실행: 예를 들어의 노트북 개발 하 고 R 코드를 테스트 합니다. 데이터 과학 클라이언트를 호출하게 될 이 컴퓨터에서 명명된 파이프 프로토콜을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 연결할 수 있어야 합니다.

1. PowerShell 명령줄을 **관리자** 권한으로 엽니다.
  
2.  스크립트를 다운로드한 폴더로 이동하고 그림과 같이 스크립트 이름을 입력하십시오. Enter 키를 누릅니다.

    ```
    .\RunSQL_R_Walkthrough.ps1
    ```
  
3. 다음 각 매개변수마다 프롬프트가 표시됩니다.
  
    **데이터베이스 서버 이름**: Machine Learning Services 또는 R Services가 설치된 SQL Server 인스턴스의 이름입니다.

    네트워크 요구 사항에 따라 인스턴스 이름에 하나 이상의 서브넷 이름이 필요할 수도 있습니다. 예를 들어 MYSERVER가 작동하지 않으면  myserver.subnet.mycompany.com을 시도해 보세요.
    
    **만들려는 데이터베이스의 이름**: 예를 들어 **Tutorial** 또는 **Taxi**를 입력할 수 있습니다.

    **사용자 이름**: 데이터베이스 액세스 권한이 있는 계정을 제공합니다. 두 가지 옵션이 있습니다.
    
    + CREATE DATABASE 권한이 있는 SQL 로그인의 이름을 입력하고 이어진 프롬프트에서 SQL 암호를 제공합니다.
    + Windows 인증을 사용하려면 이름 입력없이 ENTER 키를 누른 뒤 보안 프롬프트에서 Windows 암호를 입력합니다. PowerShell에서 다른 Windows 사용자 이름을 입력할 수는 없습니다.
    + 유효한 사용자를 지정하지 않으면 스크립트는 기본적으로 Windows 통합 인증을 사용합니다.
    
      > [!WARNING]
      > PowerShell 스크립트의 프롬프트를 사용하여 자격 증명을 제공하면 업데이트된 스크립트 파일에 일반 텍스트로 암호가 기록됩니다. 필요한 R 개체를 만든 직 후 파일을 편집해서 자격 증명을 제거하십시오.
      
    **csv 파일 경로**: 데이터 파일의 전체 경로를 제공합니다. 기본 경로 및 파일 이름은 `C:\tempR\nyctaxi1pct.csv`입니다.
  
4.  Enter 키를 눌러 스크립트를 실행합니다.

    스크립트에서 파일을 다운로드하고 데이터베이스에 데이터를 자동으로 로드합니다. 이 작업은 다소 시간이 걸릴 수 있습니다. PowerShell 창에서 상태 메시지를 확인합니다.
      
    대량 가져오기 또는 다른 단계가 실패하면 [문제 해결](#bkmk_Troubleshooting) 섹션에 설명된 대로 수동으로 데이터를 로드할 수 있습니다.

**결과(성공적으로 완료)**

```
Execution successful
Completed registering all stored procedures used in this walkthrough.
This step (registering all stored procedures) takes 0.39 seconds.
Plug in the database server name, database name, user name and password into the R script file
This step (plugging in database information) takes 0.48 seconds.
```

다음 단원으로 이동하려면 이 링크 클릭합니다. [SQL을 사용 하여 데이터를 보고 탐색하기](/walkthrough-view-and-explore-the-data.md)

## <a name="bkmk_Troubleshooting"></a>문제 해결

PowerShell 스크립트에 문제가 있다면 수동으로 전체 혹은 일부를 실행할 수 있습니다. 이번 섹션에서 몇 가지 공통적인 문제와 해결 방법을 나열합니다.

### <a name="powershell-script-didnt-download-the-data"></a>PowerShell 스크립트가 데이터를 다운로드하지 않음

데이터를 수동으로 다운로드하려면 다음 링크를 마우스 오른쪽 단추로 클릭하고 **다른 이름으로 대상 저장**을 선택합니다.

[http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv](http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv)

다운로드한 데이터 파일의 경로와 데이터가 저장된 파일 이름을 적어둡니다. **bcp**를 사용하여 테이블에 데이터를 로드하려면 전체 경로가 필요합니다.

### <a name="unable-to-download-the-data"></a>데이터를 다운로드할 수 없음

데이터 파일이 큽니다. 인터넷 연결 상태가 비교적 좋은 컴퓨터를 사용하지 않으면 다운로드가 시간 초과될 수 있습니다.

### <a name="could-not-connect-or-script-failed"></a>연결할 수 없거나 스크립트에 실패

스크립트 중 하나에서 이 오류가 발생할 수 있습니다. *SQL Server에 연결을 설정하는 중에 네트워크 또는 인스턴스 관련 오류가 발생했습니다.*

+ 인스턴스 이름의 철자를 확인합니다.
+ 전체 연결 문자열을 확인합니다.
+ 네트워크 요구 사항에 따라 하나 이상의 서브넷 이름을 사용하여 인스턴스 이름을 한정해야 할 수도 있습니다. 예를 들어 MYSERVER가 작동하지 않는 경우 myserver.subnet.mycompany.com을 사용해 보세요.
+ Windows 방화벽이 SQL Server 연결을 허용하는지 확인합니다.
+ 서버를 등록하고 원격 연결을 허용하는지 확인합니다.
+ 명명된 인스턴스를 사용한다면 SQL Browser 서비스를 켜서 연결을 보다 쉽게 합니다.

### <a name="network-error-or-protocol-not-found"></a>네트워크 오류 또는 프로토콜을 찾을 수 없음

+ 인스턴스가 원격 연결을 지원하는지 확인합니다.
+ 지정된 SQL 사용자가 원격으로 데이터베이스에 연결할 수 있는지 확인합니다.
+ 인스턴스에서 명명된 파이프를 사용하도록 설정합니다.
+ 계정의 사용 권한을 확인합니다. 지정한 계정이 새 데이터베이스를 만들고 데이터를 업로드할 수 있는 권한이 없을 수 있습니다.

### <a name="bcp-did-not-run"></a>bcp를 실행하지 못함

+ 컴퓨터에서 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용할 수 있는지 확인합니다. PowerShell 창 또는 Windows 명령 프롬프트에서 **bcp**를 실행할 수 있습니다.
+ 오류가 발생할 경우 **bcp** 유틸리티의 위치를 PATH 시스템 환경 변수에 추가한 후 다시 시도합니다.

### <a name="the-table-schema-was-created-but-the-table-has-no-data"></a>테이블 스키마가 생성되었지만 테이블에 데이터가 없음

스크립트의 나머지 부분이 문제 없이 실행된 경우 다음과 같이 명령줄에서 **bcp** 를 호출하여 수동으로 테이블에 데이터를 업로드할 수 있습니다.

#### <a name="using-a-sql-login"></a>SQL 로그인 사용

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U <SQL login> -P <password>
~~~~

#### <a name="using-windows-authentication"></a>Windows 인증 사용

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -T
~~~~

+ `in` 키워드는 데이터 이동 방향을 지정합니다.
+ **-f** 인수를 사용하려면 서식 파일의 전체 경로를 지정해야 합니다. **in** 옵션을 사용하는 경우 서식 파일이 필요합니다.
+ SQL 로그인과 함께 bcp를 실행하는 경우 **-U** 및 **-P** 인수를 사용합니다.
+ Windows 통합 인증을 사용하는 경우 **-T** 인수를 사용합니다.

스크립트가 데이터를 로드하지 않으면 구문을 확인하고 서버 이름이 네트워크에 대해 올바르게 지정되었는지 확인합니다. 예를 들어 서브넷을 포함하고 명명된 인스턴스에 연결할 경우 컴퓨터 이름을 포함시킵니다. 대량 업로드를 수행하는 로그인에 권한이 있는지 확인합니다.

### <a name="i-want-to-run-the-script-without-prompts"></a>프롬프트 없이 스크립트를 실행하려고 할 때

다음 템플릿을 사용해서 단일 명령 줄에서 필요한 모든 매개변수를 지정할 수 있습니다.

```
.\RunSQL_R_Walkthrough.ps1 -server <server address> -dbname <new db name> -u <user name> -p <password> -csvfilepath <path to csv file>
```

다음 예제는 SQL 로그인을 사용하여 스크립트를 실행합니다.

```
.\RunSQL_R_Walkthrough.ps1 -server MyServer.subnet.domain.com -dbname MyDB –u SqlUserName –p SqlUsersPassword -csvfilepath C:\temp\nyctaxi1pct.csv
```

-   *SqlUserName*의 자격 증명을 사용하여 지정된 인스턴스 및 데이터베이스에 연결합니다.
-   *C:\temp\nyctaxi1pct.csv*파일에서 데이터를 가져옵니다.
-   *MyServer*라는 *인스턴스의* MyDB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 있는 *dbo.nyctaxi_sample*테이블에 데이터를 로드합니다.

### <a name="the-data-loaded-but-it-contains-duplicates"></a>로드된 데이터에 중복이 있음

데이터베이스에 동일한 이름과 동일한 스키마의 테이블이 존재하는 경우 **bcp**는 기존 데이터를 덮어쓰지 않고 새로운 데이터 사본을 삽입합니다.

중복 데이터를 방지 하려면 스크립트를 다시 실행 하기 전에 기존 테이블을 자릅니다.

## <a name="whats-included-in-the-sample"></a>샘플에 포함된 내용

GitHub 리포지토리에서 파일을 다운로드하면 다음과 같습니다.

+ CSV 형식의 데이터; 자세한 내용은 [학습 및 데이터 채점](#bkmk_data) 을 참조합니다.
+ 환경 준비를 위한 PowerShell 스크립트
+ bcp를 사용하여 SQL Server에 데이터를 가져오기 위한 XML 서식 파일
+ 여러 T-SQL 스크립트
+ 이 연습을 실행하는 데 필요한 모든 R 코드

### <a name="bkmk_data"></a>데이터 학습 및 채점

데이터는 각 여정의 요금 및 지불된 팁 금액을 비롯하여 2013년 17,300만 개별 여정의 레코드를 포함하는 뉴욕시 택시 데이터 집합의 대표 샘플링입니다. 데이터를 쉽게 사용할 수 있도록 Microsoft 데이터 과학 팀은 1%의 데이터만 가져오는 다운 샘플링을 수행했습니다.  이 데이터는 Azure의 공용 Blob Storage 컨테이너에서 .CSV 형식으로 공유되었습니다. 원본 데이터에는 바로 아래 350MB 압축 되지 않은 파일입니다.

+ 공용 데이터 집합: [NYC 택시 및 Limousine Commission] (http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)

+ [뉴욕 택시 데이터 집합에서 Azure ML 모델 만들기] (https://blogs.technet.microsoft.com/machinelearning/2015/04/02/building-azure-ml-models-on-the-nyc-taxi-dataset/

### <a name="powershell-and-r-script-files"></a>PowerShell 및 R 스크립트 파일

+ **RunSQL_R_Walkthrough.ps1** PowerShell을 사용해서 이 스크립트를 먼저 실행합니다. SQL 스크립트로 데이터베이스에 데이터를 로드합니다.

+ **taxiimportfmt.xml** BCP 유틸리티에서 데이터베이스에 데이터를 로드하는 데 사용하는 형식 정의 파일입니다.

+ **RSQL_R_Walkthrough.R** 데이터 분석 및 모델링을 위해 단원의 나머지 부분에서 사용 되는 핵심 R 스크립트입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 탐색하고, 분류 모델을 작성하고, 플롯을 만드는 데 필요한 모든 R 코드를 제공합니다.

### <a name="t-sql-script-files"></a>T-SQL 스크립트 파일

PowerShell 스크립트는 SQL Server 인스턴스에서 여러 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 실행합니다. 다음 표는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트와 용도입니다.

|SQL 스크립트 파일 이름|Description|
|------------------------|----------------|
|create-db-tb-upload-data.sql|데이터베이스와 다음 두 개의 테이블을 만듭니다.<br /><br /> *nyctaxi_sample*: 교육 데이터(NYC 택시 데이터 집합의 1% 샘플)를 저장하는 테이블입니다. 저장소 및 쿼리 성능 향상을 위해 클러스터형 columnstore 인덱스가 테이블에 추가됩니다.<br /><br /> *nyc_taxi_models*: 이진 형식에서 학습 된 모델을 저장 하는 데 사용 되는 테이블입니다.|
|PredictTipBatchMode.sql|새로운 관측(observations)에 대한 레이블(labels)을 예측하기 위해 훈련된 모델을 호출하는 저장 프로시저를 만듭니다. 입력 매개 변수로 쿼리를 받습니다.|
|PredictTipSingleMode.sql|새로운 관측에 대한 레이블을 예측하기 위해 훈련된 분류 모델을 호출하는 저장 프로시저를 만듭니다. 새로운 관측의 변수가 인라인 매개 변수로 전달됩니다.|
|PersistModel.sql|데이터베이스의 테이블에 분류 모델의 이진 표현을 저장하는 데 도움이 되는 저장 프로시저를 만듭니다.|
|fnCalculateDistance.sql|승하차 위치 간의 직접 거리를 계산하는 SQL 스칼라 반환 함수를 만듭니다.|
|fnEngineerFeatures.sql|분류 모델 훈련을 위해 특성(feature)을 만드는 SQL 테이블 반환 함수를 만듭니다.|

이 연습에서 사용된 T-SQL은 검증을 거쳤으며 R 코드에서 그대로 실행될 수 있습니다. 그러나 추가 실험을 원하거나 자체 솔루션을 개발하는 경우엔 전용 SQL 개발 환경에서 쿼리를 검증하고 튜닝한 뒤 R 코드에 추가하는 것을 권장합니다.

+ [Visual Studio Code](https://code.visualstudio.com/)용 [mssql 확장](https://code.visualstudio.com/docs/languages/tsql)은 대부분의 데이터베이스 개발 작업을 지원하는 쿼리를 실행할 수 있는 무료 경량 환경입니다.
+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)는 SQL Server 데이터베이스 개발 및 관리를 위해 제공되는 강력한 무료 도구입니다.

## <a name="next-lesson"></a>다음 단원

[SQL를 사용한 데이터 관찰 및 탐색](/walkthrough-view-and-explore-the-data.md)

## <a name="previous-lesson"></a>이전 단원

[R 및 SQL Server용 데이터 과학 전체 과정 연습](/walkthrough-data-science-end-to-end-walkthrough.md)

[데이터 과학 연습을 위한 필수 조건](walkthrough-prerequisites-for-data-science-walkthroughs.md)

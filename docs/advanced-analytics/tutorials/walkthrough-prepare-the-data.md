---
title: "PowerShell (연습)를 사용 하 여 데이터를 준비 | Microsoft Docs"
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
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 65fd41d4-c94e-4929-a24a-20e792a86579
caps.latest.revision: "30"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 743d7159bd8937fe90be4016ad361d13b7a15c36
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="prepare-the-data-using-powershell-walkthrough"></a>PowerShell (연습)를 사용 하 여 데이터를 준비 합니다.

이 시점에서는 있어야 다음을 설치 중 하나:

+ SQL Server 2016 R Services
+ SQL Server 2017 컴퓨터 학습 서비스를 사용 하도록 설정 하는 R 언어와

이 단원에서는 데이터, R 패키지 및 Github 리포지토리에서 연습에서 사용 되는 R 스크립트를 다운로드 합니다. 편의 위해 PowerShell 스크립트를 사용 하 여 전체를 다운로드할 수 있습니다.

R 워크스테이션 및 서버에서 몇 가지 추가 R 패키지를 설치 해야 합니다. 단계에 설명 되어 있습니다.

그런 다음 모델링 및 점수 매기기에 사용 되는 데이터베이스를 구성 하려면 RunSQL_R_Walkthrough.ps1, 두 번째 PowerShell 스크립트를 사용 합니다. 스크립트는 데이터베이스에 데이터의 대량 로드를 수행을 지정 하 고 몇 가지 SQL 함수 및 데이터 과학 작업을 단순화 하는 저장된 프로시저를 만듭니다.

이제 시작 하겠습니다.

## <a name="1-download-the-data-and-scripts"></a>1. 데이터와 스크립트를 다운로드 합니다.

필요한 모든 코드가 GitHub 리포지토리에 제공 되었습니다. PowerShell 스크립트를 사용하여 파일의 로컬 복사본을 만들 수 있습니다.

1.  데이터 과학 클라이언트 컴퓨터에서 관리자 권한으로 Windows PowerShell 명령 프롬프트를 엽니다.

2.  오류 없이 다운로드 스크립트를 실행할 수 있는지 확인하려면 이 명령을 실행합니다. 시스템 기본값을 변경하지 않고 일시적으로 스크립트를 허용합니다.

    ```
    Set-ExecutionPolicy Unrestricted -Scope Process -Force
    ```
      
3.  다음 Powershell 명령을 실행하여 스크립트 파일을 로컬 디렉터리로 다운로드합니다. 폴더는 기본적으로 다른 디렉터리를 지정 하지 않으면 `C:\tempR` 만들어집니다 및 모든 파일을 저장 합니다.
  
    ```
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_R_Walkthrough.ps1'  
    $ps1_dest = "$pwd\Download_Scripts_R_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_R_Walkthrough.ps1 –DestDir 'C:\tempR'
    ```
  
    다른 디렉터리에 파일을 저장하려는 경우 *DestDir* 매개 변수의 값을 편집하고 컴퓨터의 다른 폴더를 지정합니다. 존재 하지 않는 폴더 이름을 입력 하는 경우 PowerShell 스크립트를 폴더를 만듭니다.
  
4.  다운로드는 다소 시간이 걸릴 수 있습니다. 다운로드가 완료된 후 Windows PowerShell 명령 콘솔은 다음과 같이 표시됩니다.
  
    ![PowerShell 스크립트 완료 후](media/rsql-e2e-psscriptresults.PNG "PowerShell 스크립트 완료 후")
  
5.  PowerShell 콘솔에서 `ls` 명령을 실행하여 *DestDir*에 다운로드된 파일 목록을 확인할 수 있습니다.  파일에 대 한 참조 [포함 된 내용](#What-the-Download-Includes)합니다.

## <a name="2-install-required-r-packages"></a>2. 필요한 R 패키지 설치

이 연습을 수행하려면 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]의 일부로 기본적으로 설치되지 않는 일부 R 라이브러리가 필요합니다. 솔루션을 개발 하 고에서 클라이언트에는 모두 패키지를 설치 해야는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 솔루션을 배포한 컴퓨터입니다.

### <a name="install-required-packages-on-the-client"></a>클라이언트에 필요한 패키지 설치

다운로드한 R 스크립트에는 이러한 패키지를 다운로드 및 설치하는 명령이 포함되어 있습니다.

1. R 환경에서 스크립트 파일 RSQL_R_Walkthrough.R을 엽니다.

2. 해당 줄을 강조 표시하고 실행합니다.
    
    ```
    # Install required R libraries, if they are not already installed.
    if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
    if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
    if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
    if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
    ```
    
    또한 일부 패키지 필요한 패키지를 설치합니다. 모두 32개 정도의 패키지가 필요합니다.

### <a name="install-required-packages-on-the-server"></a>서버에 필요한 패키지 설치

여러 가지 다른 방법으로 SQL Server에 패키지를 설치할 수 있습니다. 예를 들어 SQL Server에서 제공 된 [관리 패키지](../r/installing-and-managing-r-packages.md) 데이터베이스 관리자가 패키지 리포지토리를 만들고 사용자가 자신의 패키지를 설치할 권한을 할당할 수 있는 기능입니다. 그러나 컴퓨터의 관리자 인 경우 올바른 라이브러리를 설치 하면으로 R을 사용 하 여 새 패키지 설치할 수 있습니다.

> [!NOTE]
> 서버에서 **없는** 메시지가 표시 되는 경우에 사용자 라이브러리에 설치 합니다. 사용자 라이브러리에 설치 하는 경우 SQL Server 인스턴스 찾거나 해당 패키지를 실행할 수 없습니다. 자세한 내용은 [SQL Server에 새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)를 참조하세요.

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 RGui.exe를 **관리자 권한으로** 엽니다.  기본값을 사용하여 SQL Server R Services를 설치한 경우 RGui.exe는 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64)에 있습니다.

2.  R 프롬프트에서 다음 R 명령을 실행합니다.
  
    ```
    install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    ```

    - 이 예제에서는 벡터의 사용 가능한 경로 검색 하 고 "Program Files"를 포함 하는 경로 찾을 R grep 함수를 사용 합니다. 자세한 내용은 [http://www.rdocumentation.org/packages/base/functions/grep](http://www.rdocumentation.org/packages/base/functions/grep)을 참조하세요.

    - 패키지가 이미 설치 되어 있다면 설치 된 패키지 목록을 실행 하 여 확인 `installed.packages()`합니다.

## <a name="3-prepare-the-environment-using-runsqlrwalkthroughps1"></a>3. RunSQL_R_Walkthrough.ps1를 사용 하 여 환경을 준비 합니다.

데이터 파일, R 스크립트 및 T-SQL 스크립트와 함께 다운로드는 PowerShell 스크립트를 포함 `RunSQL_R_Walkthrough.ps1`합니다. 스크립트는 다음과 같은 작업을 수행합니다.

- SQL Native Client 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 용 명령줄 유틸리티가 설치되어 있는지 확인합니다. 명령줄 도구는 SQL 테이블에 데이터를 빠르게 대량 로드하는 데 사용되는 [bcp 유틸리티](../../tools/bcp-utility.md)를 실행하는 데 필요합니다.

- 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결한 다음 데이터베이스를 구성하고 모델 및 데이터를 위한 테이블을 만드는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 실행합니다.

- SQL 스크립트를 실행하여 여러 개의 저장 프로시저를 만듭니다.

- 이전에 다운로드한 데이터를 `nyctaxi_sample` 테이블에 로드합니다.

- 지정한 데이터베이스 이름을 사용하도록 R 스크립트 파일의 인수를 다시 작성합니다.

솔루션을 작성할 수 있는 컴퓨터에서이 스크립트 실행: 예를 들어의 노트북 개발 하 고 R 코드를 테스트 합니다. 데이터 과학 클라이언트를 호출하게 될 이 컴퓨터에서 명명된 파이프 프로토콜을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 연결할 수 있어야 합니다.

1. PowerShell 명령줄을 열고 **관리자 권한으로**합니다.
  
2.  스크립트를 다운로드한 폴더로 이동한 다음 스크립트 이름을 표시된 대로 입력합니다. Enter 키를 누릅니다.

    ```
    .\RunSQL_R_Walkthrough.ps1
    ```
  
3.  다음 매개 변수 마다 라는 메시지가 표시 됩니다.
  
    **데이터베이스 서버 이름**: 기계 학습 서비스 또는 R 서비스를 설치한 SQL Server 인스턴스의 이름입니다.

    네트워크 요구 사항에 따라 하나 이상의 서브넷 이름을 사용하여 인스턴스 이름을 한정해야 할 수도 있습니다.  예를 들어 MYSERVER가 작동하지 않는 경우 myserver.subnet.mycompany.com을 사용해 보세요.
    
    **만들려는 데이터베이스의 이름**: 예를 들어 **Tutorial** 또는 **Taxi**를 입력할 수 있습니다.

    **사용자 이름**: 데이터베이스 액세스 권한이 있는 계정을 제공합니다. 옵션에는
    
    + CREATE DATABASE 권한이 있는 SQL 로그인의 이름을 입력하고 연속된 프롬프트에서 SQL 암호를 제공합니다.
    + Windows ID를 사용할 이름을 입력하지 않고 Enter 키를 누른 다음 Windows 암호를 입력합니다. PowerShell에서는 다른 Windows 사용자 이름을 입력할 수 없습니다.
    + 유효한 사용자를 지정 하지 않으면 스크립트 Windows 통합된 인증을 사용 하 여 기본값으로 사용 됩니다.
    
      > [!WARNING]
      > PowerShell 스크립트에서 프롬프트를 사용 하 여 자격 증명을 제공 하는 경우 암호는 업데이트 된 스크립트 파일에 일반 텍스트로에 기록 됩니다. 필요한 R 개체를 만든 후 즉시 자격 증명을 제거하도록 파일을 편집합니다.
      
    **csv 파일 경로**: 데이터 파일의 전체 경로를 제공합니다. 기본 경로 및 파일 이름은 `C:\tempR\nyctaxi1pct.csv`입니다.
  
4.  Enter 키를 눌러 스크립트를 실행합니다.

    스크립트에서 파일을 다운로드하고 데이터베이스에 데이터를 자동으로 로드해야 합니다. 이 작업은 다소 시간이 걸릴 수 있습니다. PowerShell 창에서 상태 메시지를 확인합니다.
      
    대량 가져오기 또는 다른 단계 실패 로드할 수 있습니다에 설명 된 대로 수동으로 데이터는 [문제 해결](#bkmk_Troubleshooting) 섹션.

**결과(성공적으로 완료)**

```
Execution successful
Completed registering all stored procedures used in this walkthrough.
This step (registering all stored procedures) takes 0.39 seconds.
Plug in the database server name, database name, user name and password into the R script file
This step (plugging in database information) takes 0.48 seconds.
```

다음 단원으로 이동 하려면이 링크 클릭: [보기 SQL을 사용 하 여 데이터를 탐색 하 고](/walkthrough-view-and-explore-the-data.md)

## <a name="bkmk_Troubleshooting"></a>문제 해결

PowerShell 스크립트와 함께 문제가 되 면 또는 실행할 수 있습니다 모든 단계를 수동으로 예제로 PowerShell 스크립트의 줄을 사용 하 여 합니다. 이 섹션에는 몇 가지 일반적인 문제 및 해결 방법을 나열합니다.

### <a name="powershell-script-didnt-download-the-data"></a>PowerShell 스크립트가 데이터를 다운로드하지 않음

데이터를 수동으로 다운로드하려면 다음 링크를 마우스 오른쪽 단추로 클릭하고 **다른 이름으로 대상 저장**을 선택합니다.

[http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv](http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv)

다운로드한 데이터 파일의 경로와 데이터가 저장된 파일 이름을 적어둡니다. 전체 경로를 사용 하 여 테이블에 데이터를 로드 해야 **bcp**합니다.

### <a name="unable-to-download-the-data"></a>데이터를 다운로드할 수 없음

데이터 파일이 큽니다. 상대적으로 좋은 인터넷 연결 된 컴퓨터를 사용 해야 하거나 다운로드 시간 초과 될 수 있습니다.

### <a name="could-not-connect-or-script-failed"></a>연결할 수 없거나 스크립트에서 오류가 발생함

스크립트 중 하나를 실행할 때 이 오류가 발생할 수 있습니다. *SQL Server에 연결을 설정하는 중에 네트워크 또는 인스턴스 관련 오류가 발생했습니다.*

+ 인스턴스 이름의 철자를 확인합니다.
+ 전체 연결 문자열을 확인합니다.
+ 네트워크 요구 사항에 따라 하나 이상의 서브넷 이름을 사용하여 인스턴스 이름을 한정해야 할 수도 있습니다.  예를 들어 MYSERVER가 작동하지 않는 경우 myserver.subnet.mycompany.com을 사용해 보세요.
+ Windows 방화벽이 SQL Server를 통한 연결을 허용하는지 확인합니다.
+ 서버를 등록하고 원격 연결을 허용하는지 확인해 보세요.
+ 명명된 인스턴스를 사용할 경우 SQL Browser를 사용하도록 설정하면 더 쉽게 연결할 수 있습니다.

### <a name="network-error-or-protocol-not-found"></a>네트워크 오류 또는 프로토콜을 찾을 수 없음

+ 인스턴스에서 원격 연결을 지원하는지 확인합니다.
+ 지정된 SQL 사용자가 원격으로 데이터베이스에 연결할 수 있는지 확인합니다.
+ 인스턴스에서 명명된 파이프를 사용하도록 설정합니다.
+ 계정의 사용 권한을 확인합니다. 지정한 계정에 새 데이터베이스를 만들고 데이터를 업로드할 수 있는 권한이 없을 수 있습니다.

### <a name="bcp-did-not-run"></a>bcp을 실행하지 못함

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

+ `in` 키워드 데이터 이동의 방향을 지정 합니다.
+ **-f** 인수를 사용하려면 서식 파일의 전체 경로를 지정해야 합니다. **in** 옵션을 사용하는 경우 서식 파일이 필요합니다.
+ SQL 로그인과 함께 bcp를 실행하는 경우 **-U** 및 **-P** 인수를 사용합니다.
+ Windows 통합 인증을 사용하는 경우 **-T** 인수를 사용합니다.

스크립트가 데이터를 로드하지 않으면 구문을 확인하고 네트워크에 대한 서버 이름이 올바르게 지정되었는지 확인합니다. 예를 들어 서브넷을 포함하고 명명된 인스턴스에 연결할 경우 컴퓨터 이름을 포함해야 합니다. 대량 업로드를 수행 하는 기능에는 로그인을 확인 합니다.

### <a name="i-want-to-run-the-script-without-prompts"></a>프롬프트 없이 스크립트를 실행하려고 함

환경과 관련된 값을 사용하여 이 템플릿을 통해 모든 매개 변수를 단일 명령줄에서 지정할 수 있습니다.

```
.\RunSQL_R_Walkthrough.ps1 -server <server address> -dbname <new db name> -u <user name> -p <password> -csvfilepath <path to csv file>
```

다음 예제에서는 SQL 로그인을 사용하여 스크립트를 실행합니다.

```
.\RunSQL_R_Walkthrough.ps1 -server MyServer.subnet.domain.com -dbname MyDB –u SqlUserName –p SqlUsersPassword -csvfilepath C:\temp\nyctaxi1pct.csv
```

-   *SqlUserName*의 자격 증명을 사용하여 지정된 인스턴스 및 데이터베이스에 연결합니다.
-   *C:\temp\nyctaxi1pct.csv*파일에서 데이터를 가져옵니다.
-   *MyServer*라는 *인스턴스의* MyDB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 있는 *dbo.nyctaxi_sample*테이블에 데이터를 로드합니다.

### <a name="the-data-loaded-but-it-contains-duplicates"></a>데이터가 로드되었지만 중복 항목이 포함되어 있음

기존 테이블의 동일한 이름과 동일한 스키마를 데이터베이스에 있으면 **bcp** 덮어쓰기를 기존 데이터 보다는 데이터의 새 복사본을 삽입 합니다.

중복 데이터를 방지 하려면 스크립트를 다시 실행 하기 전에 기존 테이블을 자릅니다.

## <a name="whats-included-in-the-sample"></a>이 샘플에 포함 된 항목

GitHub 리포지토리에서 파일을 다운로드 하는 경우 다음 가져오기:

+ 데이터를 CSV 형식입니다. 참조 [학습 및 데이터 점수 매기기](#bkmk_data) 대 한 자세한 내용은
+ 환경을 준비하기 위한 PowerShell 스크립트
+ bcp를 사용하여 SQL Server에 데이터를 가져오기 위한 XML 서식 파일
+ 여러 T-SQL 스크립트
+ 이 연습을 실행하는 데 필요한 모든 R 코드

### <a name="bkmk_data"></a>학습 및 데이터 점수 매기기

데이터는 각 여정의 요금 및 지불된 팁 금액을 비롯하여 2013년 17,300만 개별 여정의 레코드를 포함하는 뉴욕시 택시 데이터 집합의 대표 샘플링입니다. 데이터를 쉽게 사용할 수 있도록 Microsoft 데이터 과학 팀은 1%의 데이터만 가져오는 다운 샘플링을 수행했습니다.  이 데이터는 Azure의 공용 Blob Storage 컨테이너에서 .CSV 형식으로 공유되었습니다. 원본 데이터에는 바로 아래 350MB 압축 되지 않은 파일입니다.

+ 공용 데이터 집합: [NYC 택시 및 Limousine Commission] (http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)

+ [NYC 택시 데이터 집합에 대해 Azure ML 모델을 작성합니다.] (https://blogs.technet.microsoft.com/machinelearning/2015/04/02/building-azure-ml-models-on-the-nyc-taxi-dataset/ 합니다.

### <a name="powershell-and-r-script-files"></a>PowerShell 및 R 스크립트 파일

+ **RunSQL_R_Walkthrough.ps1** 이 스크립트를 실행할 먼저 PowerShell을 사용 하 여 합니다. SQL 스크립트를 호출하여 데이터베이스에 데이터를 로드합니다.

+ **taxiimportfmt.xml** BCP 유틸리티에서 데이터베이스에 데이터를 로드하는 데 사용하는 형식 정의 파일입니다.

+ **RSQL_R_Walkthrough.R** 데이터 분석 및 모델링을 위해 학습의 나머지 부분에 사용 되는 핵심 R 스크립트입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 탐색하고, 분류 모델을 작성하고, 그림을 만드는 데 필요한 R 코드를 모두 제공합니다.

### <a name="t-sql-script-files"></a>T-SQL 스크립트 파일

PowerShell 스크립트가 실행 된 다중 [!INCLUDE[tsql](../../includes/tsql-md.md)] SQL Server 인스턴스에 대 한 스크립트입니다. 다음 표에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 및 용도입니다.

|SQL 스크립트 파일 이름|Description|
|------------------------|----------------|
|create-db-tb-upload-data.sql|데이터베이스와 다음 두 개의 테이블을 만듭니다.<br /><br /> *nyctaxi_sample*: 교육 데이터(NYC 택시 데이터 집합의 1% 샘플)를 저장하는 테이블입니다. 저장소 및 쿼리 성능 향상을 위해 클러스터형 columnstore 인덱스가 테이블에 추가됩니다.<br /><br /> *nyc_taxi_models*: 이진 형식에서 학습 된 모델을 저장 하는 데 사용 되는 테이블입니다.|
|PredictTipBatchMode.sql|학습된 모델을 호출하여 새 관찰에 대한 레이블을 예측하는 저장 프로시저를 만듭니다. 쿼리를 입력 매개 변수로 허용합니다.|
|PredictTipSingleMode.sql|학습된 분류 모델을 호출하여 새 관찰에 대한 레이블을 예측하는 저장 프로시저를 만듭니다. 새 관찰의 변수가 인라인 매개 변수로 전달됩니다.|
|PersistModel.sql|데이터베이스의 테이블에 분류 모델의 이진 표현을 저장하는 데 도움이 되는 저장 프로시저를 만듭니다.|
|fnCalculateDistance.sql|승하차 위치 사이의 직접 거리를 계산하는 SQL 스칼라 반환 함수를 만듭니다.|
|fnEngineerFeatures.sql|분류 모델 학습을 위한 기능을 만드는 SQL 테이블 반환 함수를 만듭니다.|

이 연습에서 사용 되는 T-SQL 쿼리 테스트를 거쳐으로 실행할 수 있습니다-R 코드에 있습니다. 그러나 고유한 솔루션을 개발하거나 추가로 실험하려는 경우 R 코드에 추가하기 전에 전용 SQL 개발 환경을 사용하여 쿼리를 먼저 테스트 및 튜닝하는 것이 좋습니다.

+ [Visual Studio Code](https://code.visualstudio.com/)용 [mssql 확장](https://code.visualstudio.com/docs/languages/tsql)은 대부분의 데이터베이스 개발 태스크를 지원하는 쿼리를 실행할 수 있는 무료 경량 환경입니다.
+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)는 SQL Server 데이터베이스 개발 및 관리를 위해 제공되는 강력한 무료 도구입니다.

## <a name="next-lesson"></a>다음 단원

[보기 및 R 및 SQL를 사용 하 여 데이터를 탐색 합니다.](/walkthrough-view-and-explore-the-data.md)

## <a name="previous-lesson"></a>이전 단원

[R 및 SQL Server에 대 한 종단 간 데이터 과학 연습](/walkthrough-data-science-end-to-end-walkthrough.md)

[데이터 과학 연습을 위한 필수 조건](walkthrough-prerequisites-for-data-science-walkthroughs.md)

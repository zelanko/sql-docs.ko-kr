---
title: SQL Server 설치를 사용 하 여 R Server 또는 Machine Learning Server (독립 실행형) 설치
description: RevoScaleR, revoscalepy, MicrosoftML 및 기타 패키지를 사용 하 여 R 및 Python 개발에 대해 인스턴스를 인식 하지 않는 독립 실행형 machine learning 서버를 설정 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 94ca7b3646b9005e11b3ee4968cbfaaa65d42264
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715844"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>SQL Server 설치를 사용 하 여 Machine Learning Server (독립 실행형) 또는 R Server (독립 실행형) 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
SQL Server 설치 프로그램에는 SQL Server 외부에서 실행 되는 인스턴스를 인식 하지 않는 독립 실행형 machine learning 서버를 설치 하기 위한 **공유 기능** 옵션이 포함 되어 있습니다. 이를 **Machine Learning Server (독립 실행형)** 이라고 하며 R 및 Python을 포함 합니다. 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server 설치 프로그램에는 SQL Server 외부에서 실행 되는 인스턴스를 인식 하지 않는 독립 실행형 machine learning 서버를 설치 하기 위한 **공유 기능** 옵션이 포함 되어 있습니다. SQL Server 2016에서이 기능을 **R Server (독립 실행형)** 라고 합니다.  
::: moniker-end

SQL Server 설치 프로그램에서 설치 하는 독립 실행형 서버는 다음과 같은 사용 사례 및 시나리오를 지 원하는 SQL 브랜드가 아닌 버전의 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)와 기능적으로 동일 합니다.

+ 원격 실행, 동일한 콘솔에서 로컬 세션과 원격 세션 간 전환
+ 웹 노드 및 계산 노드를 사용 하는 운영 화
+ 웹 서비스 배포: R 및 Python 스크립트를 웹 서비스로 패키지할 수 있습니다.
+ R 및 Python 함수 라이브러리의 전체 컬렉션

SQL Server에서 분리 된 독립 서버는 SQL Server 아닌 독립 실행형 서버에서 제공 되는 기본 운영 체제 및 도구를 사용 하 여 R 및 Python 환경을 구성, 보호 및 액세스 합니다.

SQL Server 보충 모델로으로, 원격 계산 컨텍스트를 사용 하 여 지원 되는 데이터 플랫폼의 전체 범위에 대 한 고성능 기계 학습 솔루션을 개발 해야 하는 경우에는 독립 실행형 서버가 유용 합니다. 로컬 서버에서 Spark 클러스터 또는 다른 SQL Server 인스턴스의 원격 Machine Learning Server로 실행을 전환할 수 있습니다.

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>사전 설치 검사 목록

SQL Server 2016 R Server (독립 실행형) 또는 Microsoft R Server와 같은 이전 버전을 설치한 경우 계속 하기 전에 기존 설치를 제거 합니다.

일반적으로 독립 실행형 서버 및 데이터베이스 엔진 인스턴스 인식 설치를 함께 사용할 수 없는 것으로 간주 하 여 리소스 경합을 방지 하는 것이 좋지만, 리소스가 충분 한 경우에는 금지 동일한 물리적 컴퓨터.

컴퓨터에 독립 실행형 서버를 하나만 포함할 수 있습니다. SQL Server Machine Learning Server (독립 실행형) 또는 SQL Server R 서버 (독립 실행형)입니다. 새 버전을 추가 하기 전에 버전 하나를 제거 해야 합니다.

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>패치 설치 요구 사항 

SQL Server 2016에만 해당: Microsoft는 SQL Server에서 필수 조건으로 설치되는 Microsoft VC++ 2013 런타임 이진 파일의 특정 버전과 관련된 문제를 확인했습니다. VC 런타임 이진 파일에 대한 이 업데이트가 없으면 SQL Server의 특정 시나리오에서 안정성 문제를 발생할 수 있습니다. SQL Server를 설치하기 전에 [SQL Server 릴리스 정보](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) 의 지침에 따라 해당 컴퓨터에 VC 런타임 이진 파일에 대한 패치가 필요한지 확인하세요.  
::: moniker-end

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>설치 프로그램 실행

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. 설치 마법사를 시작 합니다.

2. **설치** 탭을 클릭 하 고 **새 Machine Learning Server (독립 실행형) 설치**를 선택 합니다.
    
     ![Machine Learning Server 독립 실행형 설치](media/2017setup-installation-page-mlsvr.png "Machine Learning Server 독립 실행형 설치 시작")

3. 규칙 확인이 완료 되 면 SQL Server 사용 약관에 동의 하 고 새 설치를 선택 합니다.

4. **기능 선택** 페이지에서 다음 옵션을 이미 선택 해야 합니다.

    - Microsoft Machine Learning Server (독립 실행형)

    - R 및 Python은 모두 기본적으로 선택 됩니다. 두 언어 중 하나를 선택 취소할 수 있지만 지원 되는 언어 중 하나 이상을 설치 하는 것이 좋습니다.

     ![R 또는 Python 기능 선택](media/2017setup-features-page-mlsvr-rpy.png "Machine Learning Server 독립 실행형 설치 시작")
    
    기타 모든 옵션은 무시해야 합니다. 
    
    > [!NOTE]
    > SQL Server 데이터베이스 내 분석을 위해 컴퓨터에 이미 Machine Learning Services 설치 되어 있는 경우 **공유 기능** 을 설치 하지 마세요. 이렇게 하면 중복 된 라이브러리가 생성 됩니다.
    > 
    > 또한 SQL Server에서 실행 되는 R 또는 Python 스크립트는 다른 데이터베이스 엔진 서비스에서 사용 하는 메모리와 충돌 하지 않도록 SQL Server로 관리 되는 반면 독립 실행형 machine learning 서버에는 이러한 제약 조건이 없으며 다른 데이터베이스 작업과 충돌할 수 있습니다. . 마지막으로 운영 화에 자주 사용 되는 RDP 세션을 통한 원격 액세스는 일반적으로 데이터베이스 관리자가 차단 합니다.
    > 
    > 따라서 일반적으로 SQL Server Machine Learning Services에서 별도의 컴퓨터에 Machine Learning Server (독립 실행형)를 설치 하는 것이 좋습니다.

5.  기본 언어 배포를 다운로드 하 고 설치 하기 위한 사용 조건에 동의 합니다. **동의** 단추를 사용할 수 없게 되면 **다음**을 클릭할 수 있습니다. 

     ![Python 사용권 계약](media/2017setup-python-license.png "Python 사용권 계약")

6.  **설치 준비 완료** 페이지에서 선택 내용을 확인하고 **설치**를 클릭합니다.

설치가 완료 되 면 [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md) 에서 오류 또는 경고에 대 한 도움말을 보려면 [업그레이드 및 설치 FAQ-Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md)를 참조 하세요.
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>설치 프로그램 실행

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. 설치 마법사를 시작 합니다.

2. **설치** 탭에서 **새 R Server (독립 실행형) 설치**를 클릭 합니다.
    
     ![R Server 독립 실행형 설치 시작](media/2016-setup-installation-rsvr.png "R Server 독립 실행형 설치 시작")

3. 규칙 확인이 완료 되 면 SQL Server 사용 약관에 동의 하 고 새 설치를 선택 합니다.

4.  **기능 선택** 페이지에서 다음 옵션은 이미 선택되어 있습니다.
    
    **R 서버(독립 실행형)**  
    
    ![R Server 독립 실행형에 대 한 기능 선택](media/2016setup-rserver-features.png "R Server 독립 실행형에 대 한 기능 선택")
    
    기타 모든 옵션은 무시해도 됩니다. 
    
    > [!NOTE]
    > 데이터베이스 내 분석 SQL Server 위해 R 서비스가 이미 설치 된 컴퓨터에서 설치 프로그램을 실행 하는 경우 **공유 기능** 을 설치 하지 마세요. 이렇게 하면 중복 된 라이브러리가 생성 됩니다.
    > 
    > SQL Server에서 실행 되는 R 스크립트는 SQL Server를 통해 관리 되므로 다른 데이터베이스 엔진 서비스에서 사용 하는 메모리와 충돌 하지 않도록 독립 실행형 R 서버에는 이러한 제약 조건이 없으며 다른 데이터베이스 작업에 방해가 될 수 있습니다.
    > 
    > 일반적으로 SQL Server R Services (데이터베이스 내)에서 별도의 컴퓨터에 R Server (독립 실행형)를 설치 하는 것이 좋습니다.

5.  기본 언어 배포를 다운로드 하 고 설치 하기 위한 사용 조건에 동의 합니다. **동의** 단추를 사용할 수 없게 되면 **다음**을 클릭할 수 있습니다. 

6.  **설치 준비 완료** 페이지에서 선택 내용을 확인하고 **설치**를 클릭합니다.

설치가 완료 되 면 [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md) 에서 오류 또는 경고에 대 한 도움말을 보려면 [업그레이드 및 설치 FAQ-Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md)를 참조 하세요.
::: moniker-end

## <a name="set-environment-variables"></a>환경 변수 설정

R 기능 통합의 경우에는 **MKL_CBWR** 환경 변수를 설정 하 여 Intel Mkl (Math Kernel Library) 계산과 일관 되 게 [출력 되도록](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) 해야 합니다.

1. 제어판에서 **시스템 및 보안** > **시스템** > **고급 시스템 설정** > **환경 변수**를 클릭 합니다.

2. 새 사용자 또는 시스템 변수를 만듭니다. 

  + 변수 이름 설정`MKL_CBWR`
  + 변수 값을로 설정 합니다.`AUTO`

3. 서버를 다시 시작합니다.

<a name="install-path"></a>

### <a name="default-installation-folders"></a>기본 설치 폴더

R 및 Python 개발의 경우 동일한 컴퓨터에 여러 버전을 포함 하는 것이 일반적입니다. 설치를 SQL Server 하 여 설치 하는 것 처럼 기본 배포는 설치에 사용한 SQL Server 버전과 연결 된 폴더에 설치 됩니다.

다음 표에서는 Microsoft 설치 관리자에서 만든 R 및 Python 배포에 대 한 경로를 나열 합니다. 완전성을 위해 테이블에는 Microsoft Machine Learning Server에 대 한 독립 실행형 설치 관리자 뿐만 아니라 SQL Server 설정에 의해 생성 된 경로가 포함 됩니다.

|버전| 설치 방법 | 기본 폴더|
|----|----|----|
|SQL Server 2017 Machine Learning Server (독립 실행형) |  SQL Server 2017 설치 마법사 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (독립 실행형) |  Windows 독립 실행형 설치 관리자 |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server Machine Learning Services (데이터베이스 내) |SQL Server 2017 설치 마법사, R 언어 옵션|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R 서버 (독립 실행형) |  SQL Server 2016 설치 마법사 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (데이터베이스 내) |SQL Server 2016 설치 마법사|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>업데이트 적용

데이터베이스 엔진과 machine learning 구성 요소 모두에 최신 누적 업데이트를 적용 하는 것이 좋습니다. 누적 업데이트는 설치 프로그램을 통해 설치 됩니다. 

인터넷에 연결 된 장치에서 자동 압축 풀기 실행 파일을 다운로드할 수 있습니다. 데이터베이스 엔진에 대 한 업데이트를 적용 하면 기존 R 및 Python 기능의 누적 업데이트를 자동으로 가져옵니다. 

연결 되지 않은 서버에서는 추가 단계가 필요 합니다. 기계 학습 기능의 CAB 파일 뿐만 아니라 데이터베이스 엔진에 대 한 누적 업데이트를 가져와야 합니다. 모든 파일을 격리 된 서버로 전송 하 고 수동으로 적용 해야 합니다.

1. 기준 인스턴스를 사용 하 여 시작 합니다. 기존 설치에만 누적 업데이트를 적용할 수 있습니다.

  + SQL Server 2017 최초 릴리스의 Machine Learning Server (독립 실행형)
  + SQL Server 2016 초기 릴리스, SQL Server 2016 SP 1 또는 SQL Server 2016 SP 2에서 R Server (독립 실행형)

2. 열려 있는 R 또는 Python 세션을 닫고 시스템에서 아직 실행 중인 프로세스를 중지 합니다.

3. 웹 서비스 배포를 위해 운영 화를 웹 노드 및 계산 노드로 실행 하도록 설정한 경우에는 **AppSettings** 파일을 예방 조치로 백업 합니다. 2017 CU13 이상을 SQL Server 적용 하면이 파일이 수정 되므로 백업 복사본으로 원래 버전을 유지할 수 있습니다.

4. 인터넷에 연결 된 장치에서 SQL Server 버전에 대 한 누적 업데이트 링크를 클릭 합니다.

  + [SQL Server 2017 업데이트](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [SQL Server 2016 업데이트](https://sqlserverupdates.com/sql-server-2016-updates/)

5. 최신 누적 업데이트를 다운로드 합니다. 실행 파일입니다.

6. 인터넷에 연결 된 장치에서 setup.exe를 두 번 클릭 하 여 설치를 실행 하 고 마법사를 단계별로 실행 하 여 사용 약관에 동의 하 고, 영향을 받는 기능을 검토 하 고, 완료 될 때까지 진행률을 모니터링 합니다

7. 인터넷에 연결 되지 않은 서버:

   + R 및 Python에 해당 하는 CAB 파일을 가져옵니다. 다운로드 링크는 [SQL Server 데이터베이스 내 분석 인스턴스의 누적 업데이트에 대 한 CAB 다운로드](sql-ml-cab-downloads.md)를 참조 하세요.

   + 주 실행 파일 및 CAB 파일의 모든 파일을 오프 라인 컴퓨터의 폴더로 전송 합니다.

   + Setup.exe를 두 번 클릭 하 여 설치를 실행 합니다. 인터넷에 연결 되지 않은 서버에 누적 업데이트를 설치 하는 경우 R 및 Python에 대 한 .cab 파일의 위치를 선택 하 라는 메시지가 표시 됩니다.

8. 사후 설치, 웹 노드 및 계산 노드를 사용 하 여 운영 화를 사용 하도록 설정한 서버에서 **AppSettings**를 편집 하 고 "MMLNativePath" 바로 아래에 "MMLResourcePath" 항목을 추가 합니다.

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [관리 CLI 유틸리티를 실행](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch) 하 여 웹 및 계산 노드를 다시 시작 합니다. 단계 및 구문은 [웹 및 계산 노드 모니터링, 시작 및 중지](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start)를 참조 하세요.

## <a name="development-tools"></a>개발 도구

개발 IDE는 설치의 일부로 설치 되지 않습니다. 개발 환경을 구성 하는 방법에 대 한 자세한 내용은 [R 도구 설정](../r/set-up-a-data-science-client.md) 및 [Python 도구 설정](../python/setup-python-client-tools-sql.md)을 참조 하세요.

## <a name="next-steps"></a>다음 단계

R 개발자는 몇 가지 간단한 예제를 시작 하 고 R이 SQL Server와 작동 하는 방식에 대 한 기본 사항을 배울 수 있습니다. 다음 단계는 다음 링크를 참조 하세요.

+ [자습서: T-sql에서 R 실행](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [자습서: R 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Python 개발자는 다음 자습서를 수행 하 여 SQL Server에서 Python을 사용 하는 방법을 배울 수 있습니다.

+ [자습서: T-sql에서 Python 실행](../tutorials/run-python-using-t-sql.md)
+ [자습서: Python 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

실제 시나리오를 기반으로 하는 기계 학습의 예를 보려면 [machine learning 자습서](../tutorials/machine-learning-services-tutorials.md)를 참조 하세요.

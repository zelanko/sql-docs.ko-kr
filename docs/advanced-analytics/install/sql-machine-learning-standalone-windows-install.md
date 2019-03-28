---
title: R Server 또는 SQL Server 설치 프로그램-SQL Server Machine Learning을 사용 하 여 Machine Learning Server (독립 실행형) 설치
description: RevoScaleR, revoscalepy, MicrosoftML 및 다른 패키지를 사용 하 여 R 및 Python 개발을 위한 독립 실행형 인스턴스 비인식형 machine learning 서버를 설정 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 911086beaaaeb28a036a764e066402d7ba6f1da7
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510880"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>Machine Learning Server (독립 실행형) 또는 SQL Server 설치 프로그램을 사용 하 여 R Server (독립 실행형) 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 설치 프로그램에는 **공유 기능** 를 인스턴스 비인식형를 설치 하기 위한 옵션 SQL Server 외부에서 실행 되는 독립 실행형 machine learning server. 이 기능은 SQL Server 2016에서 이라고 **R Server (독립 실행형)** 합니다. SQL Server 2017에서 라고 **Machine Learning Server (독립 실행형)** R 및 Python을 포함 합니다. 

비 SQL 브랜드 버전의 SQL Server 설치 프로그램으로 설치 된 독립 실행형 서버 기능적으로 동일 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), 사용 사례 및 시나리오를 비롯 한 동일한 지원:

+ 동일한 콘솔에서 로컬 및 원격 세션 간에 전환 하는 원격 실행
+ 웹 노드와 계산 노드를 사용 하 여 운영 화
+ 웹 서비스 배포: R 및 Python 스크립트를 웹 서비스로 패키지 하는 기능
+ R 및 Python 함수 라이브러리의 전체 컬렉션

SQL Server에서 분리 하는 독립 서버와 R 및 Python 환경이 구성, 보안 및 기본 운영 체제 및 SQL Server가 아닌 독립 실행형 서버에서 제공 하는 도구를 사용 하 여 액세스 합니다.

SQL Server의 보충 모델, 독립 실행형 서버는 고속 기계 학습 지원 되는 데이터 플랫폼의 전체 범위 원격 계산 컨텍스트를 사용할 수 있는 솔루션을 개발 해야 하는 경우에 유용 합니다. Spark 클러스터에서 또는 다른 SQL Server 인스턴스에서 원격 Machine Learning Server에 로컬 서버에서 실행을 이동할 수 있습니다.

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>설치 전 검사 목록

SQL Server 2016 R Server (독립 실행형) 또는 Microsoft R Server와 같은 이전 버전을 설치한 경우 계속 하기 전에 기존 설치를 제거 합니다.

일반적으로 좋지만 독립 실행형 서버 및 데이터베이스 엔진 인스턴스 인식형 설치와 상호 배타적 리소스 경합을 방지 하려면 처리를 모두 설치 하는 것에 대 한 대 한 금지 없습니다 방법이 충분 한 리소스에 있는 경우에 동일한 물리적 컴퓨터입니다.

컴퓨터의 한 독립 실행형 서버를 하나만 사용할 수 있습니다: SQL Server 2017의 Machine Learning Server 또는 SQL Server 2016 R Server (독립 실행형). 새 필터를 추가 하기 전에 버전을 제거 해야 합니다.

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>패치 설치 요구 사항 

SQL Server 2016 용만. Microsoft는 SQL Server에서 필수 조건으로 설치되는 Microsoft VC++ 2013 런타임 이진 파일의 특정 버전과 관련된 문제를 확인했습니다. VC 런타임 이진 파일에 대한 이 업데이트가 없으면 SQL Server의 특정 시나리오에서 안정성 문제를 발생할 수 있습니다. SQL Server를 설치하기 전에 [SQL Server 릴리스 정보](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) 의 지침에 따라 해당 컴퓨터에 VC 런타임 이진 파일에 대한 패치가 필요한지 확인하세요.  
::: moniker-end

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>설치 프로그램 실행

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. 설치 마법사를 시작 합니다.

2. 클릭 합니다 **설치** 탭을 선택한 **새 Machine Learning Server (독립 실행형) 설치**합니다.
    
     ![Machine Learning Server 독립 실행형 설치](media/2017setup-installation-page-mlsvr.png "Machine Learning Server 독립 실행형 설치를 시작 합니다.")

3. 규칙 검사를 완료 한 후에 SQL Server 라이선스 약관에 동의 하 고 새로 설치를 선택 합니다.

4. 에 **기능 선택** 페이지에서 다음 옵션은 이미 선택:

    - Microsoft Machine Learning Server (독립 실행형)

    - R 및 Python은 둘 다 기본적으로 선택 됩니다. 두 언어 중 하나를 선택을 취소할 수 있지만 지원 되는 언어 중 하나 이상이 설치 하는 것이 좋습니다.

     ![R 또는 Python 기능을 선택할](media/2017setup-features-page-mlsvr-rpy.png "Machine Learning Server 독립 실행형 설치를 시작 합니다.")
    
    기타 모든 옵션은 무시해야 합니다. 
    
    > [!NOTE]
    > 설치를 방지 합니다 **공유 기능** 컴퓨터에 이미 SQL Server 데이터베이스 내 분석에 대 한 설치 하는 Machine Learning 서비스 하는 경우. 이 중복 된 라이브러리를 만듭니다.
    > 
    > 또한 SQL Server에서 실행 되는 R 또는 Python 스크립트가 관리 하는 SQL Server를 하지 못하도록 다른 데이터베이스 엔진 서비스에서 사용 되는 메모리를 사용 하 여 충돌 하는 반면 독립 실행형 machine learning server에는 이러한 제한이 간섭할 수와 다른 데이터베이스 작업 . 마지막으로, 운영 화를 위한 자주 사용 되는 RDP 세션을 통해 원격 액세스는 일반적으로 데이터베이스 관리자에 의해 차단 됩니다.
    > 
    > 이러한 이유로, 일반적으로 권장 SQL Server Machine Learning Services에서 별도 컴퓨터에 Machine Learning Server (독립 실행형)를 설치 하는 합니다.

5.  다운로드 및 설치는 기본 언어 배포에 대 한 사용 약관에 동의 합니다. **동의** 단추를 사용할 수 없게 되면 **다음**을 클릭할 수 있습니다. 

     ![Python 사용권 계약](media/2017setup-python-license.png "Python 사용권 계약")

6.  **설치 준비 완료** 페이지에서 선택 내용을 확인하고 **설치**를 클릭합니다.

설치가 완료 되 면 참조 [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md) 오류나 경고를 사용 하 여 도움말을 참조 하세요. [업그레이드 및 설치 FAQ-Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md)합니다.
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>설치 프로그램 실행

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. 설치 마법사를 시작 합니다.

2. 에 **설치가** 탭을 클릭 **새 R Server (독립 실행형) 설치**합니다.
    
     ![R Server 독립 실행형 설치 프로그램을 시작한](media/2016-setup-installation-rsvr.png "R 서버 독립 실행형 설치를 시작 합니다.")

3. 규칙 검사를 완료 한 후에 SQL Server 라이선스 약관에 동의 하 고 새로 설치를 선택 합니다.

4.  **기능 선택** 페이지에서 다음 옵션은 이미 선택되어 있습니다.
    
    **R 서버(독립 실행형)**  
    
    ![기능 선택에 대 한 R Server 독립 실행형](media/2016setup-rserver-features.png "R 서버 독립 실행형에 대 한 선택 항목 기능")
    
    기타 모든 옵션은 무시해도 됩니다. 
    
    > [!NOTE]
    > 설치를 방지 합니다 **공유 기능** R Services가 이미 설치 되어 있는 SQL Server 데이터베이스 내 분석에 대 한 컴퓨터에서 설치를 실행 하는 경우. 이 중복 된 라이브러리를 만듭니다.
    > 
    > SQL Server에서 실행 되는 R 스크립트가 관리 하는 SQL Server를 하지 못하도록 다른 데이터베이스 엔진 서비스에서 사용 되는 메모리를 사용 하 여 충돌 하는 반면 독립 실행형 R Server에는 이러한 제한이 및 다른 데이터베이스 작업을 방해할 수 있습니다.
    > 
    > 일반적으로 권장 R Server (독립 실행형)를 설치 하는 별도 컴퓨터에서 SQL Server R Services (In-database).

5.  다운로드 및 설치는 기본 언어 배포에 대 한 사용 약관에 동의 합니다. **동의** 단추를 사용할 수 없게 되면 **다음**을 클릭할 수 있습니다. 

6.  **설치 준비 완료** 페이지에서 선택 내용을 확인하고 **설치**를 클릭합니다.

설치가 완료 되 면 참조 [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md) 오류나 경고를 사용 하 여 도움말을 참조 하세요. [업그레이드 및 설치 FAQ-Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md)합니다.
::: moniker-end

## <a name="set-environment-variables"></a>환경 변수 설정

R 기능 통합만로 설정 해야 합니다 **MKL_CBWR** 환경 변수를 [일관 된 출력을 확인](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) Intel 라이브러리 MKL (Math Kernel) 계산에서 합니다.

1. 제어판에서 클릭 **시스템 및 보안** > **System** > **고급 시스템 설정**  >   **환경 변수**합니다.

2. 새 사용자 또는 시스템 변수를 만듭니다. 

  + 변수 이름 설정 `MKL_CBWR`
  + 변수 값 설정 `AUTO`

3. 서버를 다시 시작합니다.

<a name="install-path"></a>

### <a name="default-installation-folders"></a>기본 설치 폴더

이 R 및 Python 개발을 위해 여러 버전이 같은 컴퓨터에 일반적입니다. SQL Server 설치 프로그램으로 설치, 기본 배포 설치에 사용 하는 SQL Server 버전에 연결 된 폴더에 설치 됩니다.

다음 표에서 Microsoft installer에서 생성 된 R 및 Python 배포에 대 한 경로 나열 합니다. 완성도 위해 테이블은 Microsoft Machine Learning Server에 대 한 독립 실행형 설치 관리자 뿐만 아니라 SQL Server 설치 프로그램에서 생성 하는 경로 포함 합니다.

|버전| 설치 방법 | 기본 폴더|
|----|----|----|
|SQL Server 2017 Machine Learning Server (독립 실행형) |  SQL Server 2017 설치 마법사 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (독립 실행형) |  Windows 독립 실행형 설치 관리자 |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server 2017 Machine Learning Services (In-database) |R 언어 옵션을 사용 하 여 SQL Server 2017 설치 마법사|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server (독립 실행형) |  SQL Server 2016 설치 마법사 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (In-database) |SQL Server 2016 설치 마법사|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>업데이트 적용

데이터베이스 엔진 및 기계 학습 구성 요소 모두에 최신 누적 업데이트를 적용 하는 것이 좋습니다. 누적 업데이트는 설치 프로그램을 통해 설치 됩니다. 

인터넷에 연결 된 장치의 자동 압축 풀기 실행 파일을 다운로드할 수 있습니다. R 및 Python에 대 한 기존 기능에 대 한 누적 업데이트를 가져오는 데이터베이스 엔진에 대 한 업데이트를 자동으로 적용 합니다. 

연결이 끊어진된 서버에 추가 단계가 필요 합니다. 데이터베이스 엔진에 대 한 누적 업데이트와 machine learning 기능에 대 한 CAB 파일을 가져와야 합니다. 모든 파일이 격리 된 서버에 전송 하 고 수동으로 적용 해야 합니다.

1. 기본 인스턴스를 시작 합니다. 기존 설치에만 누적 업데이트를 적용할 수 있습니다.

  + SQL Server 2017 초기 버전에서 machine Learning Server (독립 실행형)
  + SQL Server 2016의 초기 릴리스, SQL Server 2016 SP 1 또는 SQL Server 2016 sp2에서 R Server (독립 실행형)

2. 열려 있는 R 또는 Python 세션을 닫고 시스템에서 여전히 실행 중인 모든 프로세스를 중지 합니다.

3. 웹 서비스 배포에 대 한 웹 노드와 계산으로 실행 되도록 운영 화에 사용 하도록 설정한 경우 백업 합니다 **AppSettings.json** 조치로 파일입니다. 원래 버전을 유지 하기 위해 백업 복사본을 사용할 수 있습니다 SQL Server 2017 CU13 또는 이후 revises이 파일을 적용 합니다.

4. 인터넷 연결된 장치에서의 SQL Server 버전에 대 한 누적 업데이트 링크를 클릭 합니다.

  + [SQL Server 2017 업데이트](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [SQL Server 2016 업데이트](https://sqlserverupdates.com/sql-server-2016-updates/)

5. 최신 누적 업데이트를 다운로드 합니다. 실행 파일입니다.

6. 인터넷에 연결 된 장치에서 설정 및 단계에서 라이선스 조건에 동의 하 고, 영향을 받는 기능을 검토 하 고, 완료 될 때까지 진행 상황을 모니터링 하려면 마법사를 실행 하는.exe를 두 번 클릭 합니다.

7. 인터넷에 연결 되지 않은 서버:

   + R 및 Python에 대 한 해당 CAB 파일을 가져옵니다. 다운로드 링크를 참조 하세요 [CAB 인스턴스를 SQL Server 데이터베이스 내 분석에 누적 업데이트에 대 한 다운로드](sql-ml-cab-downloads.md)합니다.

   + 모든 파일, 주 실행 파일 및 CAB 파일, 오프 라인 컴퓨터의 폴더로 전송 합니다.

   + 설치 프로그램을 실행 하는.exe를 두 번 클릭 합니다. 인터넷에 연결 되지 않은 서버에 누적 업데이트를 설치, R 및 Python에 대 한.cab 파일의 위치를 선택 하 라는 메시지가 표시 됩니다.

8. 설정한 웹 노드와 계산 노드를 사용 하 여 운영 화 하는 서버에서 설치 후 편집 **AppSettings.json**, "MMLNativePath" 바로 아래에 있는 "MMLResourcePath" 항목을 추가 합니다.

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [관리 CLI 유틸리티를 실행](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch) 웹 다시 계산 노드. 단계와 구문을 참조 하세요 [모니터, 시작 및 중지 웹 및 계산 노드와](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start)합니다.

## <a name="development-tools"></a>개발 도구

개발 IDE 설치의 일부로 설치 되지 않았습니다. 개발 환경 구성에 대 한 자세한 내용은 참조 하세요. [R 도구 설정](../r/set-up-a-data-science-client.md) 하 고 [Python 도구 설정](../python/setup-python-client-tools-sql.md)합니다.

## <a name="next-steps"></a>다음 단계

R 개발자가 몇 가지 간단한 예제를 사용 하 여 시작할 수 있습니다 및 SQL Server를 사용 하 여 R을 작동 하는 방법의 기본 사항을 알아봅니다. 다음 단계를 다음 링크를 참조 하세요.

+ [자습서: T-SQL에서 R을 실행 합니다.](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [자습서: R 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Python 개발자는 이러한 자습서를 수행 하 여 SQL Server를 사용 하 여 Python을 사용 하는 방법을 배울 수 있습니다.

+ [자습서: T-sql로 Python 실행](../tutorials/run-python-using-t-sql.md)
+ [자습서: Python 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 [기계 학습 자습서](../tutorials/machine-learning-services-tutorials.md)합니다.

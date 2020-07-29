---
title: Machine Learning Server 설치(독립 실행형)
description: Python 및 R 용도의 독립 실행형 기계 학습 서버를 설치하세요. SQL Server 설치 프로그램을 통해 설치되는 독립 실행형 서버는 SQL 브랜드가 아닌 버전의 Microsoft Machine Learning Server와 기능적으로 동일합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 01/03/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 15280d88b2219587ee63b15e8e98421be2734fab
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85885947"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>SQL Server 설치 프로그램을 사용하여 Machine Learning Server(독립 실행형) 또는 R Server 설치
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
SQL Server 설치 프로그램에는 SQL Server 외부에서 실행되는 독립 실행형 기계 학습 서버 설치를 위한 **공유 기능** 옵션이 포함되어 있습니다. 이 기능은 **Machine Learning Server(독립 실행형)** 라고 하며 Python 및 R을 포함하고 있습니다. 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server 설치 프로그램에는 SQL Server 외부에서 실행되는 독립 실행형 기계 학습 서버 설치를 위한 **공유 기능** 옵션이 포함되어 있습니다. SQL Server 2016에서는 이 기능을 **R Server(독립 실행형)** 라고 합니다.  
::: moniker-end

SQL Server 설치 프로그램을 통해 설치되는 독립 실행형 서버는 SQL 브랜드가 아닌 버전의 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)와 기능적으로 동일하며, 다음을 포함한 동일한 사용 사례 및 시나리오를 지원합니다.

+ 원격 실행, 동일한 콘솔에서 로컬 세션과 원격 세션 간에 전환
+ 웹 노드와 컴퓨팅 노드를 사용하여 운영화
+ 웹 서비스 배포: R 및 Python 스크립트를 웹 서비스로 패키징하는 기능
+ R 및 Python 함수 라이브러리의 전체 컬렉션

SQL Server에서 분리된 독립 서버인 R 및 Python 환경은 SQL Server가 아닌 독립 실행형 서버에서 제공하는 기본 운영 체제 및 도구를 사용하여 구성, 보호 및 액세스됩니다.

SQL Server의 부속 서버인 독립 실행형 서버는 지원되는 데이터 플랫폼의 전체 범위에 원격 컴퓨팅 컨텍스트를 사용할 수 있는 고성능 기계 학습 솔루션을 개발해야 하는 경우에 유용합니다. 로컬 서버에서 Spark 클러스터 또는 다른 SQL Server 인스턴스의 원격 Machine Learning Server로 실행을 전환할 수 있습니다.

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>설치 전 검사 목록

SQL Server 2016 R Server(독립 실행형) 또는 Microsoft R Server 같은 이전 버전을 설치한 경우 계속하기 전에 기존 설치를 제거해야 합니다.

일반적으로 리소스 경합을 방지하기 위해 독립 실행형 서버와 데이터베이스 엔진 인스턴스 인식 설치를 상호 배타적인 것으로 간주하는 것이 좋지만, 리소스가 충분한 경우에는 동일한 물리적 컴퓨터에 두 서버를 모두 설치해도 됩니다.

컴퓨터에 독립 실행형 서버를 하나만(SQL Server Machine Learning Server(독립 실행형) 또는 SQL Server R Server(독립 실행형)) 설치할 수 있습니다. 새 버전을 추가하려면 기존 버전을 제거해야 합니다.

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>패치 설치 요구 사항 

SQL Server 2016만 해당: Microsoft는 SQL Server에서 필수 조건으로 설치되는 Microsoft VC++ 2013 런타임 이진 파일의 특정 버전과 관련된 문제를 확인했습니다. VC 런타임 이진 파일에 대한 이 업데이트가 없으면 SQL Server의 특정 시나리오에서 안정성 문제를 발생할 수 있습니다. SQL Server를 설치하기 전에 [SQL Server 릴리스 정보](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) 의 지침에 따라 해당 컴퓨터에 VC 런타임 이진 파일에 대한 패치가 필요한지 확인하세요.  
::: moniker-end

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>설치 프로그램 실행

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. 설치 마법사를 시작합니다.

2. **설치** 탭을 클릭하고, **새 Machine Learning Server(독립 실행형) 설치**를 선택합니다.
    
   ::: moniker-end
   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![독립 실행형 Machine Learning Server 설치](media/2017setup-installation-page-mlsvr.png "독립 실행형 Machine Learning Server 설치 시작")
   ::: moniker-end
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![독립 실행형 Machine Learning Server 설치](media/2019setup-installation-page-mlsvr.png "독립 실행형 Machine Learning Server 설치 시작")
   ::: moniker-end
   ::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

3. 규칙 검사가 완료되면 SQL Server 사용 약관에 동의하고 새 설치를 선택합니다.

4. **기능 선택** 페이지에서 다음 옵션이 이미 선택되어 있습니다.

    - **Microsoft Machine Learning Server(독립 실행형)**

    - **R** 및 **Python**은 기본적으로 선택됩니다. 두 언어 중 하나를 선택 취소할 수 있지만, 지원되는 언어 중 하나 이상을 설치하는 것이 좋습니다.

   ::: moniker-end
   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![R 또는 Python 기능 선택](media/2017setup-features-page-mlsvr-rpy.png "독립 실행형 Machine Learning Server 설치 시작")
   ::: moniker-end
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![R 또는 Python 기능 선택](media/2019setup-features-page-mlsvr-rpy.png "독립 실행형 Machine Learning Server 설치 시작")
   ::: moniker-end
   ::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
    
   기타 모든 옵션은 무시해야 합니다. 
    
   > [!NOTE]
   > SQL Server 데이터베이스 내 분석을 위해 컴퓨터에 이미 Machine Learning Services가 설치되어 있는 경우 **공유 기능**을 설치하지 마세요. 설치하면 중복 라이브러리가 생성됩니다.
   > 
   > 또한 SQL Server에서 실행되는 R 또는 Python 스크립트는 다른 데이터베이스 엔진 서비스에서 사용하는 메모리와 충돌하지 않도록 SQL Server를 통해 관리되는 반면, 독립 실행형 기계 학습 서버는 이러한 제약 조건이 없으며 다른 데이터베이스 작업과 간섭을 일으킬 수 있습니다. 마지막으로, 운영화에 자주 사용되는 RDP 세션을 통한 원격 액세스는 일반적으로 데이터베이스 관리자에 의해 차단됩니다.
   > 
   > 따라서 일반적으로 SQL Server Machine Learning Services와 분리된 컴퓨터에 Machine Learning Server(독립 실행형)를 설치하는 것이 좋습니다.

5. 기본 언어 배포판을 다운로드하여 설치하려면 사용 조건에 동의합니다. **동의** 단추를 사용할 수 없게 되면 **다음**을 클릭할 수 있습니다. 

6. **설치 준비 완료** 페이지에서 선택 내용을 확인하고 **설치**를 클릭합니다.
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>설치 프로그램 실행

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. 설치 마법사를 시작합니다.

2. **설치** 탭에서 **새 R Server(독립 실행형) 설치**를 클릭합니다.
    
   ![독립 실행형 R Server 설치 시작](media/2016-setup-installation-rsvr.png "독립 실행형 R Server 설치 시작")

3. 규칙 검사가 완료되면 SQL Server 사용 약관에 동의하고 새 설치를 선택합니다.

4. **기능 선택** 페이지에서 다음 옵션은 이미 선택되어 있습니다.
    
   - **R 서버(독립 실행형)**  
    
   ![독립 실행형 R Server의 기능 선택](media/2016setup-rserver-features.png "독립 실행형 R Server의 기능 선택")
    
   기타 모든 옵션은 무시해도 됩니다. 
    
   > [!NOTE]
   > SQL Server 데이터베이스 내 분석을 위해 이미 R Services가 설치되어 있는 컴퓨터에서 설치를 실행하는 경우 **공유 기능**을 설치하지 마세요. 설치하면 중복 라이브러리가 생성됩니다.
   > 
   > SQL Server에서 실행되는 R 스크립트는 다른 데이터베이스 엔진 서비스에서 사용하는 메모리와 충돌하지 않도록 SQL Server를 통해 관리되는 반면, 독립 실행형 R Server는 이러한 제약 조건이 없으며 다른 데이터베이스 작업과 간섭을 일으킬 수 있습니다.
   > 
   > 일반적으로 SQL Server R Services(데이터베이스 내)와 분리된 컴퓨터에 R Server(독립 실행형)를 설치하는 것이 좋습니다.

5. 기본 언어 배포판을 다운로드하여 설치하려면 사용 조건에 동의합니다. **동의** 단추를 사용할 수 없게 되면 **다음**을 클릭할 수 있습니다. 

6. **설치 준비 완료** 페이지에서 선택 내용을 확인하고 **설치**를 클릭합니다.
::: moniker-end

## <a name="set-environment-variables"></a>환경 변수 설정

R 기능 통합의 경우에만 **MKL_CBWR** 환경 변수를 설정하여 Intel MKL(Math Kernel Library) 계산에서 [일관성 있는 출력을 보장](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)해야 합니다.

1. 제어판에서 **시스템 및 보안** > **시스템** > **고급 시스템 설정** > **환경 변수**를 클릭합니다.

2. 새 사용자 또는 시스템 변수를 만듭니다. 

  + 변수 이름을 `MKL_CBWR`로 설정합니다.
  + 변수 값을 `AUTO`로 설정합니다.

3. 서버를 다시 시작합니다.

<a name="install-path"></a>

### <a name="default-installation-folders"></a>기본 설치 폴더

R 및 Python 개발의 경우 동일한 컴퓨터에 여러 버전을 설치하는 것이 일반적입니다. SQL Server 설치 프로그램을 통해 설치되는 기본 배포판은 설치에 사용된 SQL Server 버전과 연결된 폴더에 설치됩니다.

다음 표에는 Microsoft 설치 관리자에서 만든 R 및 Python 배포판의 경로가 나열되어 있습니다. 완전한 정보를 제공하기 위해, 이 표에는 Microsoft Machine Learning Server의 독립 실행형 설치 관리자뿐 아니라 SQL Server 설치 프로그램에서 생성한 경로도 포함되어 있습니다.

|버전| 설치 방법 | 기본 폴더|
|----|----|----|
|SQL Server 2019 Machine Learning Server(독립 실행형) |  SQL Server 2019 설치 마법사 |`C:\Program Files\Microsoft SQL Server\150\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\150\PYTHON_SERVER`|
|SQL Server 2017 Machine Learning Server(독립 실행형) |  SQL Server 2017 설치 마법사 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server(독립 실행형) |  Windows 독립 실행형 설치 관리자 |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server Machine Learning Services(데이터베이스 내) |SQL Server 2019 설치 마법사, R 언어 옵션 포함|`C:\Program Files\Microsoft SQL Server\MSSQL15.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL15.<instance_name>\PYTHON_SERVICES` |
|SQL Server Machine Learning Services(데이터베이스 내) |SQL Server 2017 설치 마법사, R 언어 옵션 포함|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server(독립 실행형) |  SQL Server 2016 설치 마법사 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services(데이터베이스 내) |SQL Server 2016 설치 마법사|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>업데이트 적용

데이터베이스 엔진과 기계 학습 구성 요소 모두에 최신 누적 업데이트를 적용하는 것이 좋습니다. 누적 업데이트는 설치 프로그램을 통해 설치됩니다. 

인터넷에 연결된 디바이스에서 자동 압축 풀기 실행 파일을 다운로드할 수 있습니다. 데이터베이스 엔진의 업데이트를 적용하면 기존 R 및 Python 기능의 누적 업데이트를 자동으로 가져옵니다. 

연결되지 않은 서버에서는 추가 단계가 필요합니다. 기계 학습 기능의 CAB 파일뿐 아니라 데이터베이스 엔진의 누적 업데이트를 가져와야 합니다. 모든 파일을 격리된 서버로 전송하고 수동으로 적용해야 합니다.

1. 기준선 인스턴스를 시작합니다. 기존 설치에만 누적 업데이트를 적용할 수 있습니다.

  + SQL Server 2019 초기 릴리스의 Machine Learning Server(독립 실행형)
  + SQL Server 2017 초기 릴리스의 Machine Learning Server(독립 실행형)
  + SQL Server 2016 초기 릴리스, SQL Server 2016 SP 1 또는 SQL Server 2016 SP 2의 R Server(독립 실행형)

2. 열려 있는 R 또는 Python 세션을 닫고 시스템에서 아직 실행 중인 프로세스를 중지합니다.

3. 웹 서비스 배포를 위해 웹 노드 및 컴퓨팅 노드로 실행되도록 운영화를 설정한 경우 예방 조치로 **AppSettings.json** 파일을 백업합니다. SQL Server 2017 CU13 이상을 적용하면 이 파일이 수정되므로 백업 복사본을 만들어 원래 버전을 유지하는 것이 좋습니다.

4. 인터넷에 연결된 기계를 이용해 [Microsoft SQL Server 최신 업데이트](https://docs.microsoft.com/sql/database-engine/install-windows/latest-updates-for-microsoft-sql-server)에서 버전의 최신 누적 업데이트를 다운로드하세요.

5. 최신 누적 업데이트를 다운로드합니다. 실행 파일입니다.

6. 인터넷에 연결된 디바이스에서 .exe 파일을 두 번 클릭하여 설치 프로그램을 실행하고 마법사를 단계별로 실행하여 사용 약관에 동의하고, 영향을 받는 기능을 검토하고, 완료될 때까지 진행률을 모니터링합니다.

7. 인터넷에 연결되지 않은 서버에서 다음을 수행합니다.

   + R 및 Python에 해당하는 CAB 파일을 가져옵니다. 다운로드 링크는 [SQL Server 데이터베이스 내 분석 인스턴스에 대한 누적 업데이트용 CAB 다운로드](sql-ml-cab-downloads.md)를 참조하세요.

   + 모든 파일, 기본 실행 파일 및 CAB 파일을 오프라인 컴퓨터의 폴더로 전송합니다.

   + .exe 파일을 두 번 클릭하여 설치 프로그램을 실행합니다. 인터넷에 연결되지 않은 서버에 누적 업데이트를 설치하는 경우 R 및 Python에 대한 .cab 파일의 위치를 선택하라는 메시지가 표시됩니다.

8. 설치 후 웹 노드 및 컴퓨팅 노드를 사용하여 배포를 설정한 서버에서 "MMLNativePath" 바로 아래에 "MMLResourcePath" 항목을 추가하여 **AppSettings.json**을 편집합니다. 다음은 그 예입니다.

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [관리 CLI 유틸리티를 실행](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch)하여 웹 및 컴퓨팅 노드를 다시 시작합니다. 단계와 구문은 [웹 및 컴퓨팅 노드의 모니터링, 시작, 중지](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start)를 참조하세요.

## <a name="development-tools"></a>개발 도구

개발 IDE는 설치 프로그램의 일부로 설치되지 않습니다. 개발 환경 구성에 대한 자세한 내용은 [R 도구 설정](../r/set-up-a-data-science-client.md) 및 [Python 도구 설정](../python/setup-python-client-tools-sql.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

R 개발자는 몇 가지 간단한 예제를 시작하고 R이 SQL Server에서 작동하는 방식의 기초를 알아볼 수 있습니다. 다음 단계로 가려면 아래 링크를 참조하세요.

+ [빠른 시작: T-SQL에서 R 사용](../tutorials/quickstart-r-create-script.md)
+ [자습서: R 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Python 개발자는 다음 자습서에 따라 SQL Server에서 Python을 사용하는 방법을 알아볼 수 있습니다.

+ [Python 자습서: SQL Server Machine Learning Services에서 선형 회귀를 사용하여 스키 대여 예측](../tutorials/python-ski-rental-linear-regression-deploy-model.md)
+ [Python 자습서: Categorizing customers using k-means clustering with SQL Server Machine Learning Services](../tutorials/python-clustering-model.md)(SQL Server Machine Learning Services에서 k-평균 클러스터링을 사용하여 고객 분류)
::: moniker-end
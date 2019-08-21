---
title: R 및 Python 구성 요소 업그레이드
description: SQL Server Machine Learning Services에서 R 및 Python을 업그레이드 하거나 sqlbindr .exe를 사용 하 여 Machine Learning Server에 바인딩합니다 SQL Server R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: abc14f78a969abd4adbbb2dcf12b4ee316614d23
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69634545"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>SQL Server 인스턴스에서 machine learning (R 및 Python) 구성 요소 업그레이드
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server의 R 및 Python 통합에는 오픈 소스 및 Microsoft 독점 패키지가 포함 됩니다. 표준 SQL Server 서비스에서 패키지는 현재 버전의 기존 패키지에 대 한 버그 수정과 주 버전 업그레이드는 제공 하지 않고 SQL Server 릴리스 주기에 따라 업데이트 됩니다. 

그러나 많은 데이터 과학자는 사용할 수 있게 되 면 최신 패키지를 사용 하는 데 익숙할 것입니다. SQL Server Machine Learning Services (데이터베이스 내) 및 SQL Server R Services (데이터베이스 내) 모두 **Microsoft Machine Learning Server**에 *바인딩하여* [R 및 Python의 최신 버전](#version-map) 을 가져올 수 있습니다. 

## <a name="what-is-binding"></a>바인딩 이란?

바인딩은 R_SERVICES 및 PYTHON_SERVICES 폴더의 내용을 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)의 최신 실행 파일, 라이브러리 및 도구로 교체 하는 설치 프로세스입니다.

업데이트 된 구성 요소와 함께 서비스 모델에서 스위치가 제공 됩니다. [SQL Server 제품 수명 주기](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017)대신 [SQL Server 누적 업데이트](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions)를 사용 하는 경우 서비스 업데이트가 [최신 수명 주기에](https://support.microsoft.com/help/30881/modern-lifecycle-policy) [Microsoft R Server Machine Learning Server &에 대 한 지원 타임 라인](https://docs.microsoft.com/machine-learning-server/resources-servicing-support) 을 준수 합니다.

구성 요소 버전 및 서비스 업데이트를 제외 하 고 바인딩은 설치의 기본 사항을 변경 하지 않습니다. R 및 Python 통합은 여전히 데이터베이스 엔진 인스턴스의 일부 이며, 라이선스는 변경 되지 않습니다 (바인딩과 관련 된 추가 비용 없음) .이 경우에도 데이터베이스 엔진에 대 한 SQL Server 지원 정책이 유지 됩니다. 이 문서의 나머지 부분에서는 바인딩 메커니즘과 각 버전의 SQL Server에 대해 작동 하는 방식에 대해 설명 합니다.

> [!NOTE]
> 바인딩은 SQL Server 인스턴스에 바인딩된 (데이터베이스 내) 인스턴스에만 적용 됩니다. 바인딩은 (독립 실행형) 설치와 관련이 없습니다.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
**SQL Server 2017 바인딩 고려 사항**

SQL Server Machine Learning Services의 경우 이미가지고 있는 항목에 대 한 추가 패키지 또는 최신 버전을 제공 하기 시작 하는 Microsoft Machine Learning Server 경우에만 바인딩을 고려할 수 있습니다.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**SQL Server 2016 바인딩 고려 사항**

SQL Server 2016 R Services 고객의 경우 바인딩은 업데이트 된 R 패키지, 원래 설치에 포함 되지 않은 새 패키지 ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)) 및 미리 [학습 된 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)을 제공 하며, 이러한 모든 기능은 새로운 주 버전 및 부 버전에서 새로 고칠 수 있습니다. [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index). 바인딩은 SQL Server 2017 기능인 Python 지원을 제공 하지 않습니다.
::: moniker-end

<a name="version-map"></a>

## <a name="version-map"></a>버전 맵

다음 표는 릴리스 차량 전반의 패키지 버전을 보여 주는 버전 맵입니다 .이를 통해 Python 지원 추가를 시작 하기 전에 Microsoft Machine Learning Server (이전에 R Server 라고 함)에 바인딩할 때 잠재적 업그레이드 경로를 확인할 수 있습니다. MLS 9.2.1). 

바인딩은 최신 버전의 R 또는 Anaconda를 보장 하지 않습니다. Microsoft Machine Learning Server (MLS)에 바인딩하는 경우 설치 프로그램을 통해 설치 된 R 또는 Python 버전을 가져올 수 있습니다 .이 버전은 웹에서 사용할 수 있는 최신 버전이 아닐 수 있습니다.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

구성 요소 |초기 릴리스 | [R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
R에 대 한 MRO (Microsoft R Open) | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[사전 학습 된 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[**SQL Server Machine Learning Services**](../install/sql-machine-learning-services-windows-install.md)

구성 요소 |초기 릴리스 | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
R에 대 한 MRO (Microsoft R Open) | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Python 3.5 4.2 Anaconda  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[사전 학습 된 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |
::: moniker-end

## <a name="how-component-upgrade-works"></a>구성 요소 업그레이드 작동 방법 

R 및 Python 라이브러리와 실행 파일은 Machine Learning Server에 기존 R 및 Python 설치를 바인딩할 때 업그레이드 됩니다. 바인딩은 R 또는 Python 통합이 있는 기존 SQL Server 데이터베이스 엔진 인스턴스에서 설치 프로그램을 실행할 때 [Microsoft Machine Learning Server 설치 관리자](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) 에 의해 실행 됩니다. 설치 프로그램에서 기존 기능을 검색 하 고 Machine Learning Server에 다시 바인딩해야 한다는 메시지를 표시 합니다. 

바인딩하는 동안 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES` 및 `\PYTHON_SERVICES` 의 콘텐츠는 및 `\PYTHON_SERVER`의 `C:\Program Files\Microsoft\ML Server\R_SERVER` 최신 실행 파일 및 라이브러리로 덮어쓰여집니다.

동시에 서비스 모델은 SQL Server 업데이트 메커니즘에서 Microsoft Machine Learning Server의 보다 빈번한 주 및 부 릴리스 주기로 대칭 이동 됩니다. 지원 정책을 전환 하는 것은 솔루션에 대 한 최신 세대 R 및 Python 모듈이 필요한 데이터 과학 팀에 게 유용한 옵션입니다. 

+ 바인딩을 사용 하지 않을 경우 SQL Server Service Pack 또는 누적 업데이트 (CU)를 설치 하면 버그 수정을 위해 R 및 Python 패키지가 패치 됩니다. 
+ 바인딩을 사용 하면 최신 [수명 주기 정책](https://support.microsoft.com/help/30881/modern-lifecycle-policy) 및 릴리스 Microsoft Machine Learning Server의 릴리스 일정과는 별도로 최신 패키지 버전을 인스턴스에 적용할 수 있습니다. 최신 수명 주기 지원 정책은 짧은 1 년 동안 더 자주 업데이트를 제공 합니다. 사후 바인딩에서는 Microsoft 다운로드 사이트에서 사용할 수 있게 되는 R 및 Python의 향후 업데이트에 MLS 설치 관리자를 계속 사용할 수 있습니다.

바인딩은 R 및 Python 기능에만 적용 됩니다. 즉, R 및 Python 기능을 위한 오픈 소스 패키지 (Microsoft R Open, Anaconda) 및 독점 패키지 RevoScaleR, revoscalepy 등이 있습니다. 바인딩은 데이터베이스 엔진 인스턴스에 대 한 지원 모델을 변경 하지 않으며 SQL Server 버전을 변경 하지 않습니다.

바인딩을 되돌릴 수 있습니다. [인스턴스를 바인딩](#bkmk_Unbind) 해제 하 고 SQL Server 데이터베이스 엔진 인스턴스를 reparing 하 여 SQL Server 서비스로 되돌릴 수 있습니다.

합계를 계산 하는 단계는 다음과 같습니다.

+ SQL Server R Services 또는 SQL Server Machine Learning Services 기존에 구성 된 설치로 시작 합니다.
+ 사용 하려는 업그레이드 된 구성 요소가 있는 Microsoft Machine Learning Server 버전을 확인 합니다.
+ 해당 버전의 설치 프로그램을 다운로드 하 여 실행 합니다. 설치 프로그램에서 기존 인스턴스를 검색 하 고, 바인딩 옵션을 추가 하 고, 호환 되는 인스턴스 목록을 반환 합니다.
+ 바인딩하려는 인스턴스를 선택 하 고 설치를 완료 하 여 바인딩을 실행 합니다.

사용자 경험을 기준으로 기술은 그대로 사용 됩니다. 유일한 차이점은 최신 버전의 패키지가 있고 원래 SQL Server를 통해 사용할 수 없는 추가 패키지를 사용 한다는 것입니다.

## <a name="bkmk_BindWizard"></a>설치 프로그램을 사용 하 여 MLS에 바인딩

Microsoft Machine Learning 설치 프로그램은 기존 기능 및 SQL Server 버전을 검색 하 고 SqlBindR .exe 라는 유틸리티를 호출 하 여 바인딩을 변경 합니다. 내부적으로 SqlBindR은 설정에 연결 되 고 간접적으로 사용 됩니다. 나중에 명령줄에서 직접 SqlBindR을 호출 하 여 특정 옵션을 연습할 수 있습니다.

1. SSMS에서를 실행 `SELECT @@version` 하 여 서버가 최소 빌드 요구 사항을 충족 하는지 확인 합니다. 

   SQL Server 2016 R Services의 경우 최소는 [서비스 팩 1](https://www.microsoft.com/download/details.aspx?id=54276) 및 [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)입니다.

1. R base 및 RevoScaleR 패키지의 버전을 확인 하 여 기존 버전이 교체할 계획 보다 낮은 지 확인 합니다. 

    ```sql
    EXECUTE sp_execute_external_script
    @language=N'R'
    ,@script = N'str(OutputDataSet);
    packagematrix <- installed.packages();
    Name <- packagematrix[,1];
    Version <- packagematrix[,3];
    OutputDataSet <- data.frame(Name, Version);'
    , @input_data_1 = N''
    WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
    ```

1. SSMS와 SQL Server에 대 한 열린 연결이 있는 기타 도구를 닫습니다. 바인딩은 프로그램 파일을 덮어씁니다. SQL Server 오픈 세션이 있는 경우 바인딩이 실패 하 고 바인드 오류 코드 6이 나타납니다.

1. 업그레이드 하려는 인스턴스가 있는 컴퓨터에 Microsoft Machine Learning Server을 다운로드 합니다. [최신 버전](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)을 권장 합니다.

1. 폴더의 압축을 풀고 MLSWIN93 아래에 있는 ServerSetup를 시작 합니다.

   ![설치 마법사 Microsoft Machine Learning Server](media/mls-921-installer-start.PNG)

1. **설치 구성**에서 업그레이드할 구성 요소를 확인 하 고 호환 되는 인스턴스 목록을 검토 합니다. 

   이 단계는 매우 중요합니다.

   왼쪽에서 유지 하거나 업그레이드 하려는 모든 기능을 선택 합니다. 일부 기능은 업그레이드할 수 없으며 다른 기능으로는 업그레이드할 수 없습니다. 빈 확인란을 선택 하면 해당 기능이 현재 설치 되어 있는 것으로 간주 됩니다. 스크린샷에서 MSSQL13 (SQL Server 2016 R Services) 인스턴스를 지정 하면 R 및 미리 학습 된 모델의 R 버전이 선택 됩니다. 이 구성은 SQL Server 2016에서 R을 지원 하지만 Python은 지원 하지 않기 때문에 유효 합니다.

   SQL Server 2016 R Services의 구성 요소를 업그레이드 하는 경우 Python 기능을 선택 하지 마십시오. Python을 SQL Server 2016 R Services에 추가할 수 없습니다.

   오른쪽에서 인스턴스 이름 옆에 있는 확인란을 선택 합니다. 나열 된 인스턴스가 없으면 호환 되지 않는 조합이 있습니다. 인스턴스를 선택 하지 않으면 Machine Learning Server의 새로운 독립 실행형 설치가 만들어지고 SQL Server 라이브러리는 변경 되지 않습니다. 인스턴스를 선택할 수 없는 경우에는 s p 1이 [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)되지 않을 수 있습니다. 

    ![설치 단계 구성](media/mls-931-installer-mssql13.png)

1. **사용권 계약** 페이지에서 사용 약관에 동의 함을 선택 하 여 Machine Learning Server에 대 한 사용 조건에 동의 합니다. 

1. 연속 된 페이지에서 Microsoft R Open 또는 Python Anaconda 배포와 같이 선택한 모든 오픈 소스 구성 요소에 대 한 추가 라이선스 조건에 동의를 제공 합니다.

1. **거의** 이 페이지에서 설치 폴더를 기록해 둡니다. 기본 폴더는 Files\Microsoft\ML Server입니다.

    설치 폴더를 변경 하려면 **고급** 을 클릭 하 여 마법사의 첫 페이지로 돌아갑니다. 그러나 이전에 선택한 모든 항목을 반복 해야 합니다.

설치 과정에서 SQL Server에서 사용 하는 R 또는 Python 라이브러리가 모두 바뀌고 실행 패드는 최신 구성 요소를 사용 하도록 업데이트 됩니다. 따라서 인스턴스가 이전에 기본 R_SERVICES 폴더의 라이브러리를 사용 하는 경우 업그레이드 후 이러한 라이브러리는 제거 되 고 실행 패드 서비스의 속성이 새 위치의 라이브러리를 사용 하도록 변경 됩니다.

바인딩은 다음 폴더의 내용에 영향을 줍니다. C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library은 C:\Program Files\Microsoft\ML Server\R_SERVER.의 콘텐츠로 바뀝니다. 두 번째 폴더와 해당 콘텐츠는 Microsoft Machine Learning Server 설치 프로그램에 의해 만들어집니다. 

업그레이드가 실패할 경우 [Sqlbindr 오류 코드](#sqlbindr-error-codes) 에서 자세한 내용을 확인 합니다.

## <a name="confirm-binding"></a>바인딩 확인

R 및 RevoScaleR 버전을 다시 확인 하 여 최신 버전이 있는지 확인 합니다. 데이터베이스 엔진 인스턴스에서 R 패키지와 함께 배포 된 R 콘솔을 사용 하 여 패키지 정보를 가져옵니다.

```sql
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
Name <- packagematrix[,1];
Version <- packagematrix[,3];
OutputDataSet <- data.frame(Name, Version);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

Machine Learning Server 9.3에 바인딩된 SQL Server 2016 R 서비스의 경우 R 기본 패키지는 3.4.3이 고, RevoScaleR은 9.3 여야 하며, MicrosoftML 9.3도 있어야 합니다. 

미리 학습 된 모델을 추가 하는 경우 모델은 MicrosoftML 라이브러리에 포함 되며 MicrosoftML 함수를 통해 호출할 수 있습니다. 자세한 내용은 [R samples For MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml)를 참조 하세요.

## <a name="offline-binding-no-internet-access"></a>오프 라인 바인딩 (인터넷 액세스 안 함)

인터넷에 연결 되지 않은 시스템의 경우 인터넷에 연결 된 컴퓨터에 설치 관리자 및 .cab 파일을 다운로드 한 다음 격리 된 서버에 파일을 전송할 수 있습니다. 

설치 관리자 (ServerSetup)에는 Microsoft 패키지 (RevoScaleR, MicrosoftML, olapR, sqlRUtils)가 포함 되어 있습니다. .Cab 파일은 다른 핵심 구성 요소를 제공 합니다. 예를 들어 "SRO" cab는 오픈 소스 R을 배포 하는 Microsoft의 R Open을 제공 합니다.

다음 지침에서는 오프 라인 설치를 위해 파일을 저장 하는 방법을 설명 합니다.

1. MLS 설치 관리자를 다운로드 합니다. 단일 압축 파일로 다운로드 됩니다. [최신 버전](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)을 권장 하지만 [이전 버전](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)을 설치할 수도 있습니다.

1. .Cab 파일을 다운로드 합니다. 9\.3 릴리스에 대 한 링크는 다음과 같습니다. 이전 버전이 필요한 경우 [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)에서 추가 링크를 찾을 수 있습니다. Python/Anaconda는 SQL Server Machine Learning Services 인스턴스에만 추가할 수 있습니다. R 및 Python에 대 한 미리 학습 된 모델이 있습니다. .cab는 사용 중인 언어로 모델을 제공 합니다.

    | 기능 | 다운로드 |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | 미리 학습된 모델 | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. .Zip 및 .cab 파일을 대상 서버로 전송 합니다.

1. 서버에서 실행 명령을 입력 `%temp%` 하 여 임시 디렉터리의 실제 위치를 가져옵니다. 실제 경로는 컴퓨터에 따라 다르지만 일반적으로 `C:\Users\<your-user-name>\AppData\Local\Temp`입니다.

1. % Temp% 폴더에 .cab 파일을 저장 합니다.

1. 설치 관리자의 압축을 풉니다.

1. ServerSetup를 실행 하 고 화면의 지시에 따라 설치를 완료 합니다.

## <a name="bkmk_BindCmd"></a>명령줄 작업

Microsoft Machine Learning Server를 실행 하면 추가 바인딩 작업에 사용할 수 있도록 SqlBindR .exe 라는 명령줄 유틸리티를 사용할 수 있게 됩니다. 예를 들어 바인딩을 되돌려야 하는 경우 설치 프로그램을 다시 실행 하거나 명령줄 유틸리티를 사용할 수 있습니다. 또한이 도구를 사용 하 여 인스턴스 호환성 및 가용성을 확인할 수 있습니다.

> [!TIP]
> SqlBindR을 찾을 수 없습니까? 설치 프로그램을 실행 하지 않았을 수 있습니다. SqlBindR은 Machine Learning Server 설치 프로그램을 실행 한 후에만 사용할 수 있습니다.

1. 관리자 권한으로 명령 프롬프트를 열고 sqlbindr.exe가 포함된 폴더로 이동합니다. 기본 위치는 C:\Program Files\Microsoft\MLServer\Setup

2. 다음 명령을 입력하여 사용 가능한 인스턴스 목록을 표시합니다. `SqlBindR.exe /list`
  
   전체 인스턴스 이름을 나열된 대로 기록해 둡니다. 예를 들어 인스턴스 이름이 MSSQL14 일 수 있습니다. 기본 인스턴스의 경우 MSSQLSERVER 또는 SERVERNAME과 같은 항목입니다. MYNAMEDINSTANCE.

3. */Cinstance* 인수를 사용 하 여 **sqlbindr .exe** 명령을 실행 하 고 이전 단계에서 반환 된 인스턴스 이름을 사용 하 여 업그레이드할 인스턴스의 이름을 지정 합니다.

   예를 들어 기본 인스턴스를 업그레이드 하려면 다음을 입력 합니다.`SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 업그레이드가 완료 되 면 수정 된 인스턴스와 연결 된 실행 패드 서비스를 다시 시작 합니다.

## <a name="bkmk_Unbind"></a>인스턴스 되돌리기 또는 바인딩 해제

바인딩된 인스턴스를 SQL Server 설정으로 설정 된 R 및 Python 구성 요소의 초기 설치로 복원할 수 있습니다. SQL Server 서비스에 다시 되돌리는 세 가지 부분이 있습니다.

+ [1단계: Microsoft Machine Learning Server에서 바인딩 해제](#step-1-unbind)
+ [2단계: 인스턴스를 원래 상태로 복원](#step-2-restore)
+ [3단계: 설치에 추가 된 패키지를 다시 설치 합니다.](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>1단계: 언바인딩

바인딩을 롤백하는 두 가지 옵션이 있습니다. 설치 프로그램을 다시 실행 하거나 SqlBindR 명령줄 유틸리티를 사용 합니다.

#### <a name="bkmk_wizunbind"></a>설치 프로그램을 사용 하 여 바인딩 해제

1. Machine Learning Server에 대 한 설치 관리자를 찾습니다. 설치 관리자를 제거한 경우 다시 다운로드 하거나 다른 컴퓨터에서 복사 해야 할 수 있습니다.
2. 바인딩 해제 하려는 인스턴스가 있는 컴퓨터에서 설치 관리자를 실행 해야 합니다.
2. 설치 관리자에서 바인딩 해제의 대상이 되는 로컬 인스턴스를 식별 합니다.
3. 원래 구성으로 되돌리려는 인스턴스 옆의 확인란을 선택 취소 합니다.
4. 사용권 계약에 동의 합니다. 을 설치 하는 경우에도 사용 약관에 대 한 동의를 나타내야 합니다.
5. **마침**을 클릭합니다. 이 프로세스는 시간이 오래 걸립니다.

#### <a name="bkmk_cmdunbind"></a>명령줄을 사용 하 여 바인딩 해제

1. 이전 섹션에 설명된 대로 명령 프롬프트를 열고 **sqlbindr.exe**가 포함된 폴더로 이동합니다.

2. */unbind* 인수와 함께 **SqlBindR.exe** 명령을 실행하고 인스턴스를 지정합니다.

   예를 들어 다음 명령은 기본 인스턴스를 되돌립니다.
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>2단계: SQL Server 인스턴스 복구

SQL Server 설치 프로그램을 실행 하 여 R 및 Python 기능이 있는 데이터베이스 엔진 인스턴스를 복구 합니다. 기존 업데이트는 유지 되지만 R 및 Python 패키지에 대 한 업데이트를 제공 하는 SQL Server 없는 경우이 단계에서 해당 패치를 적용 합니다.

또는 더 많은 작업을 수행 하지만 데이터베이스 엔진 인스턴스를 완전히 제거 하 고 다시 설치한 다음 모든 서비스 업데이트를 적용할 수도 있습니다.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>3단계: 타사 패키지 추가

패키지 라이브러리에 다른 오픈 소스 또는 타사 패키지를 추가 했을 수 있습니다. 바인딩을 반대로 바꾸는 것은 기본 패키지 라이브러리의 위치를 전환 하기 때문에 R 및 Python에서 현재 사용 하 고 있는 라이브러리에 패키지를 다시 설치 해야 합니다. 자세한 내용은 [R 패키지 정보](../package-management/r-package-information.md) 및 [설치](../package-management/install-additional-r-packages-on-sql-server.md)및 [Python 패키지 정보](../package-management/python-package-information.md) 및 [설치](../package-management/install-additional-python-packages-on-sql-server.md)를 참조 하세요.

## <a name="sqlbindrexe-command-syntax"></a>SqlBindR .exe 명령 구문

### <a name="usage"></a>사용법

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>매개 변수

|이름|설명|
|------|------|
|*list*| 현재 컴퓨터의 모든 SQL Database 인스턴스 ID 목록을 표시합니다.|
|*bind*| 지정된 SQL Database 인스턴스를 최신 버전의 R 서버로 업그레이드하고 인스턴스가 R 서버의 향후 업그레이드를 자동으로 가져오도록 합니다.|
|*unbind*|지정된 SQL Database 인스턴스에서 최신 버전의 R 서버를 제거하고 향후 R 서버 업그레이드가 인스턴스에 영향을 주지 않도록 합니다.|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>바인딩 오류

MLS Installer 및 SqlBindR은 모두 다음 오류 코드와 메시지를 반환 합니다.

|오류 코드  | 메시지           | 세부 정보               |
|------------|-------------------|-----------------------|
|바인딩 오류 0 | 확인 (성공) | 바인딩이 오류 없이 전달 되었습니다. |
|바인딩 오류 1 | 잘못 된 인수 | 구문 오류입니다. |
|바인딩 오류 2 | 잘못 된 작업 | 구문 오류입니다. |
|바인딩 오류 3 | 잘못 된 인스턴스 | 인스턴스가 있지만 바인딩에 적합 하지 않습니다. |
|바인딩 오류 4 | 바인딩할 수 없음 | |
|바인딩 오류 5 | 이미 바인딩 되었습니다. | *bind* 명령을 실행했지만 지정한 인스턴스가 이미 바인딩되어 있습니다. |
|바인딩 오류 6 | 바인딩 실패 | 인스턴스를 바인딩 해제 하는 동안 오류가 발생 했습니다. 기능을 선택 하지 않고 MLS 설치 관리자를 실행 하는 경우이 오류가 발생할 수 있습니다. 바인딩을 사용 하려면 MSSQL 인스턴스와 R 및 Python을 모두 선택 해야 합니다 .이 경우 인스턴스가 2017 SQL Server 된 것으로 가정 합니다. 이 오류는 SqlBindR이 Program Files 폴더에 쓸 수 없는 경우에도 발생 합니다. SQL Server에 대 한 세션 또는 핸들을 열면이 오류가 발생 합니다. 이 오류가 발생 하면 컴퓨터를 다시 부팅 하 고 새 세션을 시작 하기 전에 바인딩 단계를 다시 실행 합니다.|
|바인딩 오류 7 | 바인딩되지 않음 | 데이터베이스 엔진 인스턴스에 R Services 또는 SQL Server Machine Learning Services 있습니다. 인스턴스가 Microsoft Machine Learning Server에 바인딩되어 있지 않습니다. |
|바인딩 오류 8 | 바인딩 해제 실패 | 인스턴스를 바인딩 해제 하는 동안 오류가 발생 했습니다. |
|바인딩 오류 9 | 인스턴스를 찾을 수 없습니다. | 이 컴퓨터에서 데이터베이스 엔진 인스턴스를 찾을 수 없습니다. |

## <a name="known-issues"></a>알려진 문제

이 섹션에서는 SqlBindR .exe 유틸리티의 사용과 관련 하 여 알려진 문제 또는 SQL Server 인스턴스에 영향을 줄 수 있는 Machine Learning Server의 업그레이드에 대해 설명 합니다.

### <a name="restoring-packages-that-were-previously-installed"></a>이전에 설치 된 패키지 복원

Microsoft R Server 9.0.1로 업그레이드 한 경우 해당 버전에 대 한 SqlBindR .exe 버전에서 원래 패키지나 R 구성 요소를 완전히 복원 하지 못해 사용자가 인스턴스에 대 한 복구를 SQL Server 하 고 모든 서비스 릴리스를 적용 한 다음 다시 시작 해야 합니다. 인스턴스입니다.

이후 버전의 SqlBindR은 원래 R 기능을 자동으로 복원 하 여 R 구성 요소를 다시 설치 하거나 서버를 다시 패치할 필요가 없습니다. 그러나 초기 설치 후에 추가 되었을 수 있는 R 패키지 업데이트를 설치 해야 합니다.

패키지 관리 역할을 사용 하 여 패키지를 설치 하 고 공유 하는 경우이 작업은 훨씬 쉽습니다. R 명령을 사용 하 여 설치 된 패키지를 데이터베이스의 레코드를 사용 하 여 파일 시스템에 동기화 하거나 그 반대의 경우도 가능 합니다. 자세한 내용은 [SQL Server에 대 한 R 패키지 관리](../r/install-additional-r-packages-on-sql-server.md)를 참조 하세요.

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>SQL Server에서 여러 업그레이드 문제

이전에 SQL Server 2016 R Services 인스턴스를 9.0.1로 업그레이드 한 경우 Microsoft R Server 9.1.0에 대해 새 설치 관리자를 실행 하면 유효한 모든 인스턴스 목록이 표시 된 다음 기본적으로 이전에 바인딩된 인스턴스를 선택 합니다. 계속 하면 이전에 바인딩된 인스턴스가 바인딩되지 않습니다. 따라서 관련 패키지를 포함 하 여 이전 9.0.1 설치가 제거 되지만 새 버전의 Microsoft R Server (9.1.0)는 설치 되지 않습니다.

해결 방법으로 다음과 같이 기존 R Server 설치를 수정할 수 있습니다.
1. 제어판에서 **프로그램 추가/제거**를 엽니다.
2. Microsoft R Server를 찾고 **변경/수정**을 클릭 합니다.
3. 설치 관리자가 시작 되 면 9.1.0에 바인딩할 인스턴스를 선택 합니다.

Microsoft Machine Learning Server 9.2.1 및 9.3에는이 문제가 없습니다.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>바인딩 또는 바인딩 해제는 여러 임시 폴더를 벗어납니다.

경우에 따라 바인딩 및 바인딩 해제 작업에서 임시 폴더를 정리 하지 못할 수 있습니다.
다음과 같은 이름의 폴더를 찾은 경우 설치가 완료 된 후 제거할 수 있습니다. R_SERVICES_<guid>

> [!NOTE]
> 설치가 완료 될 때까지 기다려야 합니다. 한 버전에 연결 된 R 라이브러리를 제거한 다음 새 R 라이브러리를 추가 하는 데 시간이 오래 걸릴 수 있습니다. 작업이 완료 되 면 임시 폴더가 제거 됩니다.

## <a name="see-also"></a>참조

+ [Windows 용 Machine Learning Server 설치 (인터넷 연결)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Windows 용 Machine Learning Server 설치 (오프 라인)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Machine Learning Server의 알려진 문제](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [이전 R 서버 릴리스의 기능 알림](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [더 이상 사용 되지 않거나, 지원 되지 않거나, 변경 된 기능](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)

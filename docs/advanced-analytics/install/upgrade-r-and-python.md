---
title: R 및 Python 구성 요소 업그레이드
description: sqlbindr.exe를 사용해서 Machine Learning Server에 바인딩하여 SQL Server Machine Learning Services 또는 SQL Server R Services에서 R 및 Python을 업그레이드합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: abc14f78a969abd4adbbb2dcf12b4ee316614d23
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69634545"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>SQL Server 인스턴스에서 Machine Learning(R 및 Python) 구성 요소 업그레이드
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server의 R 및 Python 통합에는 오픈 소스 및 Microsoft 고유 패키지가 포함되어 있습니다. 표준 SQL Server 서비스 중에는 SQL Server 릴리스 주기에 따라 현재 버전에서 기존 패키지에 대한 버그 수정과 함께 패키지가 업데이트되지만, 주 버전 업그레이드는 제공되지 않습니다. 

하지만 많은 데이터 과학자들은 새로운 패키지가 나왔을 때 이를 사용하여 작업하는 데 익숙합니다. SQL Server Machine Learning Services(데이터베이스 내) 및 SQL Server R Services(데이터베이스 내) 모두 **Microsoft Machine Learning Server**에 *바인딩*하여 [새 버전의 R 및 Python](#version-map)을 가져올 수 있습니다. 

## <a name="what-is-binding"></a>바인딩이란?

바인딩은 R_SERVICES 및 PYTHON_SERVICES 폴더 내용을 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)에서 제공되는 새로운 실행 파일, 라이브러리 및 도구들로 바꾸는 설치 프로세스입니다.

업데이트된 구성 요소와 함께 서비스 모델에 스위치가 제공됩니다. [SQL Server 누적 업데이트](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions)의 [SQL Server 제품 수명 주기](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017) 대신, 이제는 [현대식 수명 주기](https://support.microsoft.com/help/30881/modern-lifecycle-policy)의 [Microsoft R Server 및 Machine Learning Server 지원 타임라인](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)에 맞게 서비스 업데이트가 수행됩니다.

구성 요소 버전 및 서비스 업데이트를 제외하고, 바인딩은 기본 설치 요소들을 변경하지 않습니다. R 및 Python 통합이 여전히 데이터베이스 엔진 인스턴스의 일부이고, 라이선스도 변경되지 않고(바인딩 관련 추가 비용 없음), 데이터베이스 엔진에 대한 SQL Server 지원 정책도 그대로 유지됩니다. 이 문서의 나머지 부분에서는 바인딩 메커니즘과 각 버전의 SQL Server에서의 작동 방식을 설명합니다.

> [!NOTE]
> 바인딩은 SQL Server 인스턴스에 바인딩된 (데이터베이스 내) 인스턴스에만 적용됩니다. 바인딩은 (독립형) 설치와 관련이 없습니다.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
**SQL Server 2017 바인딩 고려 사항**

SQL Server Machine Learning Services의 경우, Microsoft Machine Learning Server가 기존 항목에 비해 추가적인 패키지 또는 새 버전을 제공하기 시작할 때만 바인딩을 고려해야 합니다.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**SQL Server 2016 바인딩 고려 사항**

SQL Server 2016 R Services 고객의 경우 바인딩은 업데이트된 R 패키지, 원래 설치에 속하지 않는 새 패키지([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)) 및 [미리 학습된 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)을 제공하며, 이것들은 모두 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)의 새로운 주 및 부 릴리스에서 더 업데이트될 수 있습니다. 바인딩은 SQL Server 2017 기능인 Python 지원을 제공하지 않습니다.
::: moniker-end

<a name="version-map"></a>

## <a name="version-map"></a>버전 요약

다음 표는 Microsoft Machine Learning Server(MLS 9.2.1에서 Python 지원이 추가되기 전까지 R Server라고 부름)에 바인딩할 때 잠재 업그레이드 경로를 확인할 수 있도록 릴리스 매체 간의 패키지 버전을 보여주는 버전 요약 정보입니다. 

바인딩이 항상 R 또는 Anaconda의 최신 버전을 보장하지는 않습니다. Microsoft Machine Learning Server(MLS)에 바인딩하면 설치 과정을 통해 R 또는 Python 버전이 설치됩니다. 하지만 이 버전은 웹에서 제공되는 최신 버전이 아닐 수도 있습니다.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

구성 요소 |초기 릴리스 | [R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
R 기반 Microsoft R Open(MRO) | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[미리 학습된 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[**SQL Server Machine Learning Services**](../install/sql-machine-learning-services-windows-install.md)

구성 요소 |초기 릴리스 | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
R 기반 Microsoft R Open(MRO) | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Python 3.5 기반 Anaconda 4.2  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[미리 학습된 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |
::: moniker-end

## <a name="how-component-upgrade-works"></a>구성 요소 업그레이드 작동 방법 

R 및 Python 라이브러리와 실행 파일은 사용자가 R 및 Python의 기존 설치를 Machine Learning Server에 바인딩할 때 업그레이드됩니다. 바인딩은 R 또는 Python 통합이 포함된 기존 SQL Server 데이터베이스 엔진에서 설치 프로그램을 실행할 때 [Microsoft Machine Learning Server 설치 프로그램](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)에 의해 수행됩니다. 설치 프로그램은 기존 기능을 검색하고 Machine Learning Server에 다시 바인딩하라는 메시지를 표시합니다. 

바인딩 중에는 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES` 및 `\PYTHON_SERVICES` 내용을 `C:\Program Files\Microsoft\ML Server\R_SERVER` 및 `\PYTHON_SERVER`의 새 실행 파일 및 라이브러리로 덮어씁니다.

동시에 서비스 모델이 SQL Server 업데이트 메커니즘에서 더 빈번한 Microsoft Machine Learning Server의 주 및 부 릴리스 주기로 전환됩니다. 솔루션에 더 새로운 세대의 R 및 Python 모듈이 필요한 데이터 과학 팀에게 지원 정책 전환은 매력적인 옵션입니다. 

+ 바인딩을 사용하지 않을 경우 R 및 Python 패키지는 사용자가 SQL Server 서비스 팩 또는 누적 업데이트(CU)를 설치할 때 버그 수정 패치가 적용됩니다. 
+ 바인딩을 사용할 경우에는 CU 릴리스 일정에 관계없이 [현대식 수명 주기](https://support.microsoft.com/help/30881/modern-lifecycle-policy) 및 Microsoft Machine Learning Server 릴리스에 따라 인스턴스에 새로운 패키지 버전을 적용할 수 있습니다. 현대식 수명 주기 지원 정책은 더 짧은 1년 주기의 기간 동안 더 빈번하게 업데이트를 제공합니다. 바인딩 후에도 MLS 설치 프로그램을 계속 사용해서 R 및 Python의 이후 업데이트가 Microsoft 다운로드 사이트에 제공될 때 이를 이용할 수 있습니다.

바인딩은 R 및 Python 기능에만 적용됩니다. 즉, R 및 Python 기능(Microsoft R Open, Anaconda)을 위한 오픈 소스 패키지와 RevoScaleR, revoscalepy 고유 패키지 등에 적용됩니다. 바인딩은 데이터베이스 엔진 인스턴스의 지원 모델을 변경하지 않으며 SQL Server 버전을 변경하지 않습니다.

바인딩은 되돌릴 수 있습니다. [인스턴스를 언바인딩](#bkmk_Unbind)하고 SQL Server 데이터베이스 엔진 인스턴스를 복구하여 SQL Server 서비스로 되돌릴 수 있습니다.

간단히 말해서, 바인딩 단계는 다음과 같습니다.

+ 기존의 구성된 SQL Server R Services 또는 SQL Server Machine Learning Services 설치로 시작합니다.
+ 사용하려는 업그레이드된 구성 요소가 포함된 Microsoft Machine Learning Server 버전을 확인합니다.
+ 해당 버전의 설치 프로그램을 다운로드하고 실행합니다. 설치 프로그램이 기존 인스턴스를 검색하고, 바인딩 옵션을 추가하고, 호환되는 인스턴스 목록을 반환합니다.
+ 바인딩하려는 인스턴스를 선택하고 설치 프로그램을 완료해서 바인딩을 수행합니다.

사용자 환경 측면에서 바인딩을 통한 작업 방식 및 기술은 바뀌지 않습니다. 유일한 차이점은 새로운 버전의 패키지를 사용할 수 있고 원래 SQL Server에서 제공되지 않는 추가 패키지를 이용할 수 있다는 점입니다.

## <a name="bind-to-mls-using-setup"></a><a name="bkmk_BindWizard"></a>설치 프로그램을 사용하여 MLS에 바인딩

Microsoft Machine Learning 설치 프로그램은 기존 기능 및 SQL Server 버전을 검색하고 SqlBindR.exe라는 유틸리티를 호출하여 바인딩을 변경합니다. 내부적으로 SqlBindR은 설치 프로그램에 연결되며, 간접적으로 사용됩니다. 나중에 명령줄에서 SqlBindR을 직접 호출하여 특정 옵션을 실행할 수 있습니다.

1. SSMS에서 `SELECT @@version`을 실행하여 서버가 최소 빌드 요구 사항을 충족하는지 확인합니다. 

   SQL Server 2016 R Services의 경우 최솟값은 [서비스 팩 1](https://www.microsoft.com/download/details.aspx?id=54276) 및 [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)입니다.

1. R Base 및 RevoScaleR 패키지 버전을 확인하여 기존 버전이 바꾸려는 버전보다 낮은지 확인합니다. 

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

1. SSMS를 닫고 SQL Server에 연결된 상태의 다른 도구를 모두 닫습니다. 바인딩하면 프로그램 파일을 덮어씁니다. SQL Server에 열려 있는 세션이 있으면 바인딩 오류 코드 6과 함께 바인딩이 실패합니다.

1. 업그레이드하려는 인스턴스가 포함된 컴퓨터에 Microsoft Machine Learning Server를 다운로드합니다. [최신 버전](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)을 사용하는 것이 좋습니다.

1. 폴더 압축을 풀고 MLSWIN93에 있는 ServerSetup.exe를 시작합니다.

   ![Microsoft Machine Learning Server 설치 마법사](media/mls-921-installer-start.PNG)

1. **설치 구성**에서 업그레이드할 구성 요소를 확인하고 호환되는 인스턴스 목록을 검토합니다. 

   이 단계는 매우 중요합니다.

   왼쪽에서 유지하거나 업그레이드하려는 모든 기능을 선택합니다. 기능에 따라 일부는 업그레이드가 가능하고 일부는 불가능합니다. 확인란이 비어 있으면 해당 기능이 현재 설치된 것으로 간주하고 기능을 제거합니다. 스크린샷에는 SQL Server 2016 R Services(MSSQL13)의 인스턴스, R 및 미리 학습된 모델의 R 버전이 선택되어 있습니다. 이 구성은 SQL Server 2016에서 Python이 아닌 R이 지원되기 때문에 유효합니다.

   SQL Server 2016 R Services에서 구성 요소를 업그레이드할 경우 Python 기능을 선택하지 마십시오. SQL Server 2016 R Services에는 Python을 추가할 수 없습니다.

   오른쪽에서 인스턴스 이름 옆의 확인란을 선택합니다. 인스턴스가 나열되지 않으면 해당 조합이 호환되지 않기 때문입니다. 인스턴스를 선택하지 않으면 Machine Learning Server의 새로운 독립형 설치가 생성되고 SQL Server 라이브러리는 변경되지 않습니다. 인스턴스를 선택할 수 없으면 [SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)에 없는 것일 수 있습니다. 

    ![설치 구성 단계](media/mls-931-installer-mssql13.png)

1. **라이선스 계약** 페이지에서 **사용 조건에 동의함**을 선택하여 Machine Learning Server의 라이선스 조건을 수락합니다. 

1. 이후 페이지에서도 Microsoft R Open 또는 Python Anaconda 배포와 같은 선택한 모든 오픈 소스 구성 요소에 대한 추가 라이선스 조건에 동의합니다.

1. **거의 완료** 페이지에서 설치 폴더 위치를 확인합니다. 기본 폴더는 \Program Files\Microsoft\ML Server입니다.

    설치 폴더를 변경하려면 **고급**을 클릭하여 마법사의 첫 번째 페이지로 돌아갑니다. 하지만 이전의 모든 선택 항목을 다시 반복해야 합니다.

설치 프로세스 동안 SQL Server에서 사용되는 모든 R 또는 Python 라이브러리가 교체되고 새 구성 요소를 사용하도록 실행 패드가 업데이트됩니다. 따라서 기본 R_SERVICES 폴더에 있는 라이브러리가 인스턴스에서 이전에 사용되었다면, 업그레이드 후 이러한 라이브러리가 제거되고 실행 패드 서비스의 속성이 새 위치에 있는 라이브러리를 사용하도록 변경됩니다.

바인딩은 이러한 폴더에 있는 항목들에 영향을 줍니다. C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library는 C:\Program Files\Microsoft\ML Server\R_SERVER에 있는 항목들로 바뀝니다. 두 번째 폴더와 해당 항목들은 Microsoft Machine Learning Server 설치 프로그램에 의해 생성됩니다. 

업그레이드가 실패하면 [SqlBindR 오류 코드](#sqlbindr-error-codes)로 자세한 내용을 확인하세요.

## <a name="confirm-binding"></a>바인딩 확인

R 및 RevoScaleR 버전을 통해 새로운 버전인지 다시 확인합니다. 데이터베이스 엔진 인스턴스에서 R 패키지로 배포된 R 콘솔을 사용하여 패키지 정보를 가져옵니다.

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

Machine Learning Server 9.3에 바인딩된 SQL Server 2016 R Services의 경우, R Base 패키지가 3.4.3, RevoScaleR은 9.3이어야 하고 MicrosoftML 9.3도 있어야 합니다. 

미리 학습된 모델을 추가한 경우 모델이 MicrosoftML 라이브러리에 포함되며, MicrosoftML 함수를 통해 이를 호출할 수 있습니다. 자세한 내용은 [MicrosoftML용 R 샘플](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml)을 참조하세요.

## <a name="offline-binding-no-internet-access"></a>오프라인 바인딩(인터넷 액세스 없음)

인터넷 연결이 없는 시스템의 경우, 설치 프로그램 및 .cab 파일을 인터넷에 연결된 컴퓨터에 다운로드한 후 파일을 격리된 서버로 이동할 수 있습니다. 

설치 프로그램(ServerSetup.exe)에는 Microsoft 패키지(RevoScaleR, MicrosoftML, olapR, sqlRUtils)가 포함됩니다. .cab 파일은 다른 핵심 구성 요소를 제공합니다. 예를 들어 "SRO" cab는 오픈 소스 R의 Microsoft 배포판인 R Open을 제공합니다.

다음 지침에서는 오프라인 설치를 위한 파일 배치 방법을 설명합니다.

1. MLS 설치 프로그램을 다운로드합니다. 이 프로그램은 단일 압축 파일로 다운로드됩니다. [최신 버전](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)이 권장되지만 [이전 버전](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)을 설치할 수도 있습니다.

1. .cab 파일을 다운로드합니다. 다음 링크는 9.3 릴리스용입니다. 이전 버전이 필요한 경우 [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)에서 추가 링크를 찾을 수 있습니다. Python/Anaconda는 SQL Server Machine Learning Services 인스턴스에만 추가할 수 있습니다. 미리 학습된 모델이 R 및 Python 모두 존재하며, .cab는 사용 중인 언어로 모델을 제공합니다.

    | 기능 | 다운로드 |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | 미리 학습된 모델 | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. .zip 및 .cab 파일을 대상 서버로 이동합니다.

1. 서버에서 실행 명령에 `%temp%`를 입력하여 임시 디렉터리의 실제 위치를 가져옵니다. 실제 경로는 컴퓨터에 따라 다르지만 일반적으로 `C:\Users\<your-user-name>\AppData\Local\Temp`입니다.

1. .cab 파일을 %temp% 폴더에 둡니다.

1. 설치 프로그램의 압축을 풉니다.

1. ServerSetup.exe를 실행하고 화면 안내에 따라 설치를 완료합니다.

## <a name="command-line-operations"></a><a name="bkmk_BindCmd"></a>명령줄 작업

Microsoft Machine Learning Server를 실행한 후에는 SqlBindR.exe라는 명령줄 유틸리티를 사용해서 추가 바인딩 작업을 수행할 수 있습니다. 예를 들어 바인딩을 되돌려야 할 경우, 설치 프로그램을 다시 실행하거나 명령줄 유틸리티를 사용하면 됩니다. 또한 이 도구를 사용하여 인스턴스 호환성과 가용성을 확인할 수 있습니다.

> [!TIP]
> SqlBindR을 찾을 수 없습니까? 설치 프로그램을 실행되지 않았기 때문일 수 있습니다. SqlBindR은 Machine Learning Server 설치 프로그램을 실행한 후에만 사용할 수 있습니다.

1. 관리자 권한으로 명령 프롬프트를 열고 sqlbindr.exe가 포함된 폴더로 이동합니다. 기본 위치는 C:\Program Files\Microsoft\MLServer\Setup입니다.

2. 다음 명령을 입력하여 사용 가능한 인스턴스 목록을 표시합니다. `SqlBindR.exe /list`
  
   전체 인스턴스 이름을 나열된 대로 기록해 둡니다. 예를 들어 기본 인스턴스의 이름은 MSSQL14.MSSQLSERVER이거나 SERVERNAME.MYNAMEDINSTANCE와 비슷할 수 있습니다.

3. **SqlBindR.exe** 명령을 */bind* 인수로 실행하고 이전 단계에서 반환된 인스턴스 이름을 사용하여, 업그레이드할 인스턴스 이름을 지정합니다.

   예를 들어 기본 인스턴스를 업그레이드하려면 다음을 입력합니다. `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 업그레이드가 완료되면 수정된 인스턴스와 연관된 실행 패드 서비스를 다시 시작합니다.

## <a name="revert-or-unbind-an-instance"></a><a name="bkmk_Unbind"></a>인스턴스 되돌리기 또는 언바인딩

바인딩된 인스턴스를 SQL Server 설치 프로그램으로 설정되는 R 및 Python 구성 요소의 초기 설치로 복원할 수 있습니다. SQL Server 서비스로 되돌리기 위해서는 세 단계를 수행해야 합니다.

+ [1단계: Microsoft Machine Learning Server에서 언바인딩](#step-1-unbind)
+ [2단계: 인스턴스를 원래 상태로 복원](#step-2-restore)
+ [3단계: 설치에 추가했던 모든 패키지 다시 설치](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>1단계: 바인딩 해제

바인딩 롤백에는 설치 프로그램을 다시 실행하거나 SqlBindR 명령줄 유틸리티를 사용하는 두 가지 옵션이 있습니다.

#### <a name="unbind-using-setup"></a><a name="bkmk_wizunbind"></a> 설치 프로그램을 사용하여 언바인딩

1. Machine Learning Server 설치 프로그램을 찾습니다. 설치 프로그램을 제거한 경우에는 이를 다시 다운로드하거나 다른 컴퓨터에서 복사해야 할 수 있습니다.
2. 언바인딩하려는 인스턴스가 포함된 컴퓨터에서 설치 프로그램을 실행해야 합니다.
2. 설치 프로그램이 언바인딩 후보인 로컬 인스턴스를 식별합니다.
3. 원래 구성으로 되돌리려는 인스턴스 옆에 있는 확인란을 선택 취소합니다.
4. 라이선스 계약에 동의합니다. 설치하는 경우에도 라이선스 조건에 동의해야 합니다.
5. **Finish**를 클릭합니다. 이 프로세스는 시간이 오래 걸립니다.

#### <a name="unbind-using-the-command-line"></a><a name="bkmk_cmdunbind"></a> 명령줄을 사용하여 언바인딩

1. 이전 섹션에 설명된 대로 명령 프롬프트를 열고 **sqlbindr.exe**가 포함된 폴더로 이동합니다.

2. */unbind* 인수와 함께 **SqlBindR.exe** 명령을 실행하고 인스턴스를 지정합니다.

   예를 들어 다음 명령은 기본 인스턴스를 되돌립니다.
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>2단계: SQL Server 인스턴스 복구

SQL Server 설치 프로그램을 실행하여 R 및 Python 기능이 포함된 데이터베이스 엔진 인스턴스를 복구합니다. 기존 업데이트는 보존되지만, R 및 Python 패키지에 대해 누락된 SQL Server 서비스 업데이트가 있으면 이 단계에서 해당 패치가 적용됩니다.

또는 시간이 오래 걸리더라도 데이터베이스 엔진 인스턴스를 완전히 제거한 후 다시 설치하고 모든 서비스 업데이트를 적용할 수도 있습니다.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>3단계: 모든 타사 패키지 추가

패키지 라이브러리에 다른 오픈 소스 또는 타사 패키지가 추가되었을 수도 있습니다. 바인딩을 되돌리면 기본 패키지 라이브러리의 위치가 전환되기 때문에 R 및 Python이 현재 사용 중인 라이브러리에 패키지를 다시 설치해야 합니다. 자세한 내용은 [R 패키지 정보](../package-management/r-package-information.md) 및 [설치](../package-management/install-additional-r-packages-on-sql-server.md), [Python 패키지 정보](../package-management/python-package-information.md) 및 [설치](../package-management/install-additional-python-packages-on-sql-server.md)를 참조하세요.

## <a name="sqlbindrexe-command-syntax"></a>SqlBindR.exe 명령 구문

### <a name="usage"></a>사용

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>매개 변수

|속성|Description|
|------|------|
|*list*| 현재 컴퓨터의 모든 SQL Database 인스턴스 ID 목록을 표시합니다.|
|*bind*| 지정된 SQL Database 인스턴스를 최신 버전의 R 서버로 업그레이드하고 인스턴스가 R 서버의 향후 업그레이드를 자동으로 가져오도록 합니다.|
|*unbind*|지정된 SQL Database 인스턴스에서 최신 버전의 R 서버를 제거하고 향후 R 서버 업그레이드가 인스턴스에 영향을 주지 않도록 합니다.|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>바인딩 오류

MLS 설치 프로그램 및 SqlBindR은 모두 다음 오류 코드와 메시지를 반환합니다.

|오류 코드  | 메시지           | 세부 정보               |
|------------|-------------------|-----------------------|
|바인딩 오류 0 | 확인(성공) | 오류 없이 바인딩이 통과했습니다. |
|바인딩 오류 1 | 잘못된 인수 | 구문 오류입니다. |
|바인딩 오류 2 | 잘못된 작업 | 구문 오류입니다. |
|바인딩 오류 3 | 잘못된 인스턴스 | 인스턴스가 존재하지만 바인딩에 적합하지 않습니다. |
|바인딩 오류 4 | 바인딩할 수 없음 | |
|바인딩 오류 5 | 이미 바인딩됨 | *bind* 명령을 실행했지만 지정한 인스턴스가 이미 바인딩되어 있습니다. |
|바인딩 오류 6 | 바인딩 실패 | 인스턴스를 언바인딩하는 중 오류가 발생했습니다. 기능을 선택하지 않고 MLS 설치 프로그램을 실행하면 이 오류가 발생할 수 있습니다. 바인딩하려면 MSSQL 인스턴스와 R 및 Python을 모두 선택해야 합니다(인스턴스가 SQL Server 2017인 경우). SqlBindR이 Program Files 폴더에 쓰기를 수행할 수 없는 경우에도 이 오류가 발생합니다. SQL Server에 대한 세션 또는 핸들이 열려 있으면 이 오류가 발생합니다. 이 오류가 발생하면 컴퓨터를 다시 부팅하고 새 세션을 시작하기 전에 바인딩 단계를 다시 실행하세요.|
|바인딩 오류 7 | 바인딩되지 않음 | 데이터베이스 엔진 인스턴스에 R Services 또는 SQL Server Machine Learning Services가 있습니다. 인스턴스가 Microsoft Machine Learning Server에 바인딩되지 않았습니다. |
|바인딩 오류 8 | 언바인딩 실패 | 인스턴스를 언바인딩하는 중 오류가 발생했습니다. |
|바인딩 오류 9 | 인스턴스를 찾을 수 없습니다. | 이 컴퓨터에서 데이터베이스 엔진 인스턴스를 찾을 수 없습니다. |

## <a name="known-issues"></a>알려진 문제

이 섹션에서는 SqlBindR.exe 유틸리티 사용 또는 Machine Learning Server 업그레이드와 관련해서 SQL Server 인스턴스에 영향을 줄 수 있는 알려진 문제들을 설명합니다.

### <a name="restoring-packages-that-were-previously-installed"></a>이전에 설치된 패키지 복원

Microsoft R Server 9.0.1로 업그레이드한 경우 해당 버전의 SqlBindR.exe 버전이 원래 패키지 또는 R 구성 요소를 완전히 복원하지 못하며, 사용자가 인스턴스에서 SQL Server 복구를 실행하고 모든 서비스 릴리스를 적용한 후 인스턴스를 다시 시작해야 합니다.

이후 버전의 SqlBindR은 원래 R 기능을 자동으로 복원하므로, R 구성 요소를 다시 설치하거나 서버에 패치를 다시 적용할 필요가 없습니다. 하지만 초기 설치 후 추가되었을 수 있는 R 패키지 업데이트는 설치해야 합니다.

패키지 관리 역할을 사용해서 패키지를 설치 및 공유한 경우, 작업이 더 간편해집니다. 이 경우에는 R 명령을 사용해서 데이터베이스에 있는 레코드를 사용하여 설치 패키지를 파일 시스템으로 또는 그 반대로 동기화할 수 있습니다. 자세한 내용은 [SQL Server에 대한 R 패키지 관리](../r/install-additional-r-packages-on-sql-server.md)를 참조하세요.

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>SQL Server의 여러 업그레이드 문제

이전에 SQL Server 2016 R Services 인스턴스를 9.0.1로 업그레이드한 경우, Microsoft R Server 9.1.0에 대해 새 설치 프로그램을 실행하면 모든 유효한 인스턴스 목록이 표시되고, 기본적으로 이전에 바인딩된 인스턴스가 선택됩니다. 작업을 계속하면 이전에 바인딩된 인스턴스가 언바인딩됩니다. 따라서 관련된 모든 패키지를 포함하여 이전의 9.0.1 설치가 제거되지만 새 버전의 Microsoft R Server(9.1.0)가 설치되지 않습니다.

이를 해결하기 위해서는 다음과 같이 기존 R Server 설치를 수정할 수 있습니다.
1. 제어판에서 **프로그램 추가 또는 제거**를 엽니다.
2. Microsoft R Server를 찾고 **변경/수정**을 클릭합니다.
3. 설치 프로그램이 시작되고 9.1.0에 바인딩하려는 인스턴스를 선택합니다.

Microsoft Machine Learning Server 9.2.1 및 9.3에는 이 문제가 없습니다.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>바인딩 또는 언바인딩하면 임시 폴더가 여러 개 남아 있음

일부 경우에는 바인딩 및 언바인딩 작업이 임시 폴더를 정리하지 못할 수 있습니다.
이름이 다음과 비슷한 임시 폴더가 발견되면 설치가 완료된 후 제거할 수 있습니다. R_SERVICES_<guid>

> [!NOTE]
> 설치가 완료될 때까지 기다려야 합니다. 한 버전과 연결된 R 라이브러리를 제거하고 새로운 R 라이브러리를 추가하기 위해서는 시간이 오래 걸릴 수 있습니다. 작업이 완료되면 임시 폴더가 제거됩니다.

## <a name="see-also"></a>참고 항목

+ [Windows용 Machine Learning Server 설치(인터넷 연결)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Windows용 Machine Learning Server 설치(오프라인)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Machine Learning Server의 알려진 문제](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [이전 R Server 릴리스의 기능 공지](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [사용되지 않거나, 지원이 중단되었거나 변경된 기능](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)

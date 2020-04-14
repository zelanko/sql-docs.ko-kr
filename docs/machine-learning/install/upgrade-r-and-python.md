---
title: Python 및 R 구성 요소 업그레이드
description: sqlbindr.exe를 사용해서 Machine Learning Server에 바인딩하여 SQL Server Machine Learning Services 또는 SQL Server R Services에서 Python 및 R을 업그레이드합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/03/2020
ms.topic: conceptual
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: b2958fcb3d1d64f43f0b463a3145e2c580e6792e
ms.sourcegitcommit: 335d27d0493ddf4ffb770e13f8fe8802208d25ae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2020
ms.locfileid: "81119136"
---
# <a name="upgrade-machine-learning-python-and-r-components-in-sql-server-instances"></a>SQL Server 인스턴스에서 Machine Learning(Python 및 R) 구성 요소 업그레이드
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server의 Python 및 R 통합에는 오픈 소스 및 Microsoft 고유 패키지가 포함되어 있습니다.
                                                                               
표준 SQL Server 서비스:
                                                                               
- 패키지는 SQL Server 릴리스 주기에 따라 업데이트됩니다.
- 버그 수정은 현재 버전에서 기존 패키지에 적용됩니다.
- 주 버전 업그레이드는 없습니다.

**Microsoft Machine Learning Server**에 *바인딩*하여 [최신 버전의 Python 및 R](#version-map)을 가져올 수 있습니다. 버전은 SQL Server Machine Learning Services(데이터베이스 내) 및 SQL Server R Services(데이터베이스 내) 모두에 적용됩니다.

데이터 과학자 같이 데이터 관련 분야에 종사하는 경우 최신 패키지를 가져오는 기능이 선호됩니다.

## <a name="what-is-binding"></a>바인딩이란?

바인딩은 R_SERVICES 및 PYTHON_SERVICES 폴더 내용을 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)에서 제공되는 새로운 실행 파일, 라이브러리 및 도구들로 바꾸는 설치 프로세스입니다.

서비스 모델에 포함된 업로드된 구성 요소가 변경되었습니다.

서비스 업데이트는 [최신 수명 주기](https://support.microsoft.com/help/30881/modern-lifecycle-policy)에서 [Microsoft R Server & Machine Learning Server 지원 타임라인](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)과 일치합니다.

구성 요소 버전 및 서비스 업데이트를 제외하고, 바인딩에서는 설치의 기본 사항을 변경하지 않습니다.

- Python 및 R 통합은 여전히 데이터베이스 엔진 인스턴스의 일부입니다.
- 라이선스는 변경되지 않습니다(바인딩과 관련된 추가 비용 없음).
- 데이터베이스 엔진에 대한 SQL Server 지원 정책은 계속 유지됩니다. 

이 문서의 나머지 부분에서는 바인딩 메커니즘과 각 버전의 SQL Server에서의 작동 방식을 설명합니다.

> [!NOTE]
> 바인딩은 SQL Server 인스턴스에 바인딩된 (데이터베이스 내) 인스턴스에만 적용됩니다. 이 경우 독립 실행형 설치에는 바인딩이 필요하지 않습니다.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**SQL Server 2016 바인딩 고려 사항**

SQL Server 2016 R Services 고객의 경우 바인딩은 다음을 제공합니다.

- 업데이트된 R 패키지.
- 원래 설치의 일부가 아닌 새 패키지([MicrosoftML](https://  docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package))
- 감정 분석 및 이미지 검색을 위한 미리 학습된 기계 학습 [모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models).

모든 바인딩은 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)의 새로운 주/부 릴리스 각각에서 추가로 새로 고쳐질 수 있습니다.
::: moniker-end

## <a name="version-map"></a>버전 요약

다음 표는 버전 맵입니다. 각 맵은 릴리스 간에 패키지 버전을 보여 줍니다. Microsoft Machine Learning Server(Machine Learning Server 9.2.1부터 Python 지원을 추가하기 전에는 R Server라고 함)에 바인딩할 때 업그레이드 경로를 검토할 수 있습니다.

바인딩이 R 또는 Anaconda의 최신 버전을 보장하지는 않습니다. Microsoft Machine Learning Server에 바인딩하면 설치 과정을 통해 R 또는 Python 버전이 설치됩니다. 하지만 이 버전은 웹에서 제공되는 최신 버전이 아닐 수도 있습니다.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

구성 요소 |초기 릴리스 | [R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [Machine Learning Server 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [Machine Learning Server 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
R 기반 Microsoft R Open(MRO) | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[미리 학습된 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
[**SQL Server 2017 Machine Learning Services**](../install/sql-machine-learning-services-windows-install.md)

구성 요소 |초기 릴리스 | Machine Learning Server 9.3 | | | |
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

실행 파일, Python 및 R 라이브러리는 사용자가 기존에 설치된 Python 및 R을 Machine Learning Server에 바인딩할 때 업그레이드됩니다.

바인딩은 Python 또는 R 통합이 포함된 기존 SQL Server 데이터베이스 엔진에서 설치 프로그램을 실행할 때 [Microsoft Machine Learning Server 설치 프로그램](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)에 의해 수행됩니다. 

설치 프로그램은 기존 기능을 검색하고 Machine Learning Server에 다시 바인딩하라는 메시지를 표시합니다.

바인딩하는 동안 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES` 및 `\PYTHON_SERVICES` 내용을 `C:\Program Files\Microsoft\ML Server\R_SERVER` 및 `\PYTHON_SERVER`의 최신 실행 파일 및 라이브러리로 덮어씁니다.

바인딩은 Python 및 R 기능에만 적용됩니다. Python 및 R에 대한 오픈 소스 패키지는 다음으로 구성됩니다.

- Anaconda
- Microsoft R Open
- 전용 패키지 RevoScaleR
- Revoscalepy

바인딩은 데이터베이스 엔진 인스턴스 지원 모델 또는 SQL Server 버전을 변경하지 않습니다.

바인딩은 되돌릴 수 있습니다. [인스턴스를 언바인딩](#bkmk_Unbind)하고 SQL Server 데이터베이스 엔진 인스턴스를 복구하여 SQL Server 서비스로 되돌릴 수 있습니다.

<a name="bkmk_BindWizard"></a>

## <a name="bind-to-machine-learning-server-using-setup"></a>설치 프로그램을 사용하여 Machine Learning Server에 바인딩

설치 프로그램을 사용하여 Microsoft Machine Learning Server에 SQL Server를 바인딩하려면 다음 단계를 수행합니다. 

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

1. **설치 구성**에서 업그레이드할 구성 요소를 확인하고 호환되는 인스턴스 목록을 검토합니다.

1. **라이선스 계약** 페이지에서 **사용 조건에 동의함**을 선택하여 Machine Learning Server의 라이선스 조건을 수락합니다. 

1. 이후 페이지에서도 Microsoft R Open 또는 Python Anaconda 배포와 같은 선택한 모든 오픈 소스 구성 요소에 대한 추가 라이선스 조건에 동의합니다.

1. **거의 완료** 페이지에서 설치 폴더 위치를 확인합니다. 기본 폴더는 \Program Files\Microsoft\ML Server입니다.

    설치 폴더를 변경하려면 **고급**을 클릭하여 마법사의 첫 번째 페이지로 돌아갑니다. 하지만 이전의 모든 선택 항목을 다시 반복해야 합니다.

업그레이드가 실패하면 [SqlBindR 오류 코드](#sqlbindr-error-codes)로 자세한 내용을 확인하세요.

## <a name="offline-binding-no-internet-access"></a>오프라인 바인딩(인터넷 액세스 없음)

인터넷 연결이 없는 시스템의 경우, 설치 프로그램 및 .cab 파일을 인터넷에 연결된 컴퓨터에 다운로드한 후 파일을 격리된 서버로 이동할 수 있습니다.

설치 프로그램(ServerSetup.exe)에는 Microsoft 패키지(RevoScaleR, MicrosoftML, olapR, sqlRUtils)가 포함됩니다. .cab 파일은 다른 핵심 구성 요소를 제공합니다. 예를 들어 "SRO" cab는 오픈 소스 R의 Microsoft 배포판인 R Open을 제공합니다.

다음 지침에서는 오프라인 설치를 위한 파일 배치 방법을 설명합니다.

1. MLSWIN93 설치 프로그램을 다운로드합니다. 이 프로그램은 단일 압축 파일로 다운로드됩니다. [최신 버전](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)이 권장되지만 [이전 버전](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)을 설치할 수도 있습니다.

1. .cab 파일을 다운로드합니다. 다음 링크는 9.3 릴리스용입니다. 이전 버전이 필요한 경우 [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)에서 추가 링크를 찾을 수 있습니다. Python/Anaconda는 SQL Server Machine Learning Services 인스턴스에만 추가할 수 있습니다. 미리 학습된 모델이 Python 및 R 모두 존재하며, .cab은사용 중인 언어로 모델을 제공합니다.

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


> [!TIP]
> SqlBindR을 찾을 수 없습니까? 설치 프로그램을 실행되지 않았기 때문일 수 있습니다.
> SqlBindR은 Machine Learning Server 설치 프로그램을 실행한 후에만 사용할 수 있습니다.

1. 관리자 권한으로 명령 프롬프트를 열고 sqlbindr.exe가 포함된 폴더로 이동합니다. 기본 위치는 C:\Program Files\Microsoft\MLServer\Setup입니다.

2. 다음 명령을 입력하여 사용 가능한 인스턴스 목록을 표시합니다. `SqlBindR.exe /list`
  
   전체 인스턴스 이름을 나열된 대로 기록해 둡니다. 예를 들어 기본 인스턴스의 이름은 MSSQL14.MSSQLSERVER이거나 SERVERNAME.MYNAMEDINSTANCE와 비슷할 수 있습니다.

3. */bind* 인수를 사용하여 **SqlBindR.exe** 명령을 실행합니다. 이전 단계에서 반환된 인스턴스 이름을 사용하여 업그레이드할 인스턴스의 이름을 지정합니다.

   예를 들어 기본 인스턴스를 업그레이드하려면 다음을 입력합니다. `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 업그레이드가 완료되면 수정된 인스턴스와 연관된 실행 패드 서비스를 다시 시작합니다.

## <a name="revert-or-unbind-an-instance"></a><a name="bkmk_Unbind"></a>인스턴스 되돌리기 또는 언바인딩

바인딩된 인스턴스를 SQL Server 설치 프로그램으로 설정되는 Python 및 R 구성 요소의 초기 설치로 복원할 수 있습니다. SQL Server 서비스로 되돌리기 위해서는 세 단계를 수행해야 합니다.

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
4. 모든 라이선스 계약에 동의합니다.
5. **Finish**를 클릭합니다. 이 프로세스는 시간이 오래 걸립니다.

#### <a name="unbind-using-the-command-line"></a><a name="bkmk_cmdunbind"></a> 명령줄을 사용하여 언바인딩

1. 이전 섹션에 설명된 대로 명령 프롬프트를 열고 **sqlbindr.exe**가 포함된 폴더로 이동합니다.

2. */unbind* 인수와 함께 **SqlBindR.exe** 명령을 실행하고 인스턴스를 지정합니다.

   예를 들어 다음 명령은 기본 인스턴스를 되돌립니다.
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>2단계: SQL Server 인스턴스 복구

SQL Server 설치 프로그램을 실행하여 Python 및 R 기능이 포함된 데이터베이스 엔진 인스턴스를 복구합니다. 기존 업데이트는 유지됩니다. 다음 단계는 Python 및 R 패키지에 대한 서비스 업데이트에서 업데이트가 누락된 경우에 적용됩니다.

대체 솔루션: 데이터베이스 엔진 인스턴스를 완전히 제거하고 다시 설치한 후 모든 서비스 업데이트를 적용하세요.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>3단계: 모든 타사 패키지 추가

패키지 라이브러리에 다른 오픈 소스 또는 타사 패키지가 추가되었을 수도 있습니다. 바인딩을 되돌리면 기본 패키지 라이브러리의 위치가 전환되기 때문에 Python 및 R이 현재 사용 중인 라이브러리에 패키지를 다시 설치해야 합니다. 자세한 내용은 [R 패키지 정보](../package-management/r-package-information.md) 및 [설치](../package-management/install-additional-r-packages-on-sql-server.md), [Python 패키지 정보](../package-management/python-package-information.md) 및 [설치](../package-management/install-additional-python-packages-on-sql-server.md)를 참조하세요.

## <a name="sqlbindrexe-command-syntax"></a>SqlBindR.exe 명령 구문

### <a name="usage"></a>사용

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>매개 변수

|속성|Description|
|------|------|
|*list*| 현재 컴퓨터의 모든 SQL Database 인스턴스 ID 목록을 표시합니다.|
|*bind*| 지정된 SQL Database 인스턴스를 최신 버전의 R 서버로 업그레이드하고 인스턴스가 R Server의 향후 업그레이드를 자동으로 가져오도록 합니다.|
|*unbind*|지정된 SQL Database 인스턴스에서 최신 버전의 R Server를 제거하고 향후 R Server 업그레이드가 인스턴스에 영향을 주지 않도록 합니다.|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>바인딩 오류

Machine Learning Server 설치 프로그램 및 SqlBindR은 모두 다음 오류 코드와 메시지를 반환합니다.

|오류 코드  | 메시지           | 세부 정보               |
|------------|-------------------|-----------------------|
|바인딩 오류 0 | 확인(성공) | 오류 없이 바인딩이 통과했습니다. |
|바인딩 오류 1 | 잘못된 인수 | 구문 오류입니다. |
|바인딩 오류 2 | 잘못된 작업 | 구문 오류입니다. |
|바인딩 오류 3 | 잘못된 인스턴스 | 인스턴스가 존재하지만 바인딩에 적합하지 않습니다. |
|바인딩 오류 4 | 바인딩할 수 없음 | |
|바인딩 오류 5 | 이미 바인딩됨 | *bind* 명령을 실행했지만 지정한 인스턴스가 이미 바인딩되어 있습니다. |
|바인딩 오류 6 | 바인딩 실패 | 인스턴스를 언바인딩하는 중 오류가 발생했습니다. 기능을 선택하지 않고 Machine Learning Server 설치 프로그램을 실행하면 이 오류가 발생할 수 있습니다. 바인딩하려면 MSSQL 인스턴스와 Python 및 R을 모두 선택해야 합니다(인스턴스가 SQL Server 2017인 경우). SqlBindR이 Program Files 폴더에 쓰기를 수행할 수 없는 경우에도 이 오류가 발생합니다. SQL Server에 대한 세션 또는 핸들이 열려 있으면 이 오류가 발생합니다. 이 오류가 발생하면 컴퓨터를 다시 부팅하고 새 세션을 시작하기 전에 바인딩 단계를 다시 실행하세요.|
|바인딩 오류 7 | 바인딩되지 않음 | 데이터베이스 엔진 인스턴스에 R Services 또는 SQL Server Machine Learning Services가 있습니다. 인스턴스가 Microsoft Machine Learning Server에 바인딩되지 않았습니다. |
|바인딩 오류 8 | 언바인딩 실패 | 인스턴스를 언바인딩하는 중 오류가 발생했습니다. |
|바인딩 오류 9 | 인스턴스를 찾을 수 없습니다. | 이 컴퓨터에서 데이터베이스 엔진 인스턴스를 찾을 수 없습니다. |

## <a name="known-issues"></a>알려진 문제

이 섹션에서는 SqlBindR.exe 유틸리티 사용 또는 Machine Learning Server 업그레이드와 관련해서 SQL Server 인스턴스에 영향을 줄 수 있는 알려진 문제들을 설명합니다.

### <a name="restoring-packages-that-were-previously-installed"></a>이전에 설치된 패키지 복원

SqlBindR.exe는 Microsoft R Server 9.0.1 업그레이드로 원래 패키지 또는 R 구성 요소를 복원하지 못합니다. 인스턴스에 SQL Server 복구를 사용하고 모든 서비스 릴리스를 적용합니다. 인스턴스를 다시 시작합니다.

이후 버전의 SqlBindR은 원래 R 기능을 자동으로 복원하므로, R 구성 요소를 다시 설치하거나 서버에 패치를 다시 적용할 필요가 없습니다. 하지만 초기 설치 후 추가되었을 수 있는 R 패키지 업데이트는 설치해야 합니다.

R 명령을 사용하여 설치된 패키지를 데이터베이스의 레코드를 사용하는 파일 시스템에 동기화합니다. 자세한 내용은 [SQL Server에 대한 R 패키지 관리](https://docs.microsoft.com/sql/machine-learning/package-management/install-additional-r-packages-on-sql-server)를 참조하세요.

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>SQL Server의 여러 업그레이드 문제

시나리오: 이전에 SQL Server 2016 R Services 인스턴스를 9.0.1로 업그레이드했습니다. Microsoft R Server 9.1.0용 새 설치 프로그램을 실행했습니다. 설치 프로그래이 모든 유효한 인스턴스의 목록을 표시합니다.
기본적으로 설치 프로그램은 이전에 바인딩된 인스턴스를 선택합니다. 작업을 계속하면 이전에 바인딩된 인스턴스가 언바인딩됩니다. 그 결과, 이전 9.0.1 설치 및 모든 관련 패키지는 제거되지만 새 버전의 Microsoft R Server(9.1.0)가 설치되지 않습니다.

이를 해결하기 위해서는 다음과 같이 기존 R Server 설치를 수정할 수 있습니다.
1. 제어판에서 **프로그램 추가 또는 제거**를 엽니다.
2. Microsoft R Server를 찾고 **변경/수정**을 클릭합니다.
3. 설치 프로그램이 시작되고 9.1.0에 바인딩하려는 인스턴스를 선택합니다.

Microsoft Machine Learning Server 9.2.1 및 9.3에는 이 문제가 없습니다.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>바인딩 또는 언바인딩하면 임시 폴더가 여러 개 남아 있음

설치가 완료된 후 임시 폴더를 제거합니다.

> [!NOTE]
> 설치가 완료될 때까지 기다려야 합니다. 한 버전과 연결된 R 라이브러리를 제거하고 새로운 R 라이브러리를 추가하기 위해서는 시간이 오래 걸릴 수 있습니다. 작업이 완료되면 임시 폴더가 제거됩니다.

## <a name="see-also"></a>참고 항목

+ [Windows용 Machine Learning Server 설치(인터넷 연결)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Windows용 Machine Learning Server 설치(오프라인)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Machine Learning Server의 알려진 문제](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [이전 R Server 릴리스의 기능 공지](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [사용되지 않거나 더 이상 지원되지 않거나 변경된 기능](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)

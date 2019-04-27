---
title: R 및 Python 구성 요소-SQL Server Machine Learning Services 업그레이드
description: R 및 Python에서 SQL Server 2016 Services 또는 SQL Server 2017 Machine Learning Services Machine Learning Server 바인딩할 sqlbindr.exe를 사용 하 여 업그레이드 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: da28d6f0ae423ce9cca0c6d571af944a2d7acd3d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642041"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>기계 학습 (R 및 Python) 구성에서 SQL Server 인스턴스 요소를 업그레이드 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server에서 R 및 Python 통합 Microsoft 독점 및 오픈 소스 패키지를 포함합니다. 표준 SQL Server 서비스에서 패키지는 SQL Server 릴리스 주기에서 사용 하 여 현재 버전에만 주 버전 업그레이드 없이 기존 패키지에 대 한 버그 수정에 따라 업데이트 됩니다. 

그러나 많은 데이터 과학자가 사용 가능 해지면 최신 패키지를 사용 하 여 작업에 익숙한 합니다. SQL Server 2017 Machine Learning Services (In-database) 및 SQL Server 2016 R Services (In-database)을 가져올 수 있습니다 [최신 버전의 R 및 Python](#version-map) 하 여 *바인딩* 에 **Microsoft Machine Learning Server**합니다. 

## <a name="what-is-binding"></a>바인딩된 무엇입니까?

바인딩은 최신 실행 파일, 라이브러리를 사용 하 여 R_SERVICES 및 PYTHON_SERVICES 폴더의 내용을 교환 및에서 도구는 설치 프로세스 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)합니다.

와 함께 업데이트 된 구성 요소 모델 서비스에서 스위치를 제공 합니다. 대신 합니다 [SQL Server 제품 수명 주기](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017)를 사용 하 여 [SQL Server 누적 업데이트](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions), 서비스 업데이트에 맞게는 [Microsoft R Server 컴퓨터에 대 한 지원 타임 라인 서버 학습](https://docs.microsoft.com/machine-learning-server/resources-servicing-support) 에 [최신 수명 주기](https://support.microsoft.com/help/30881/modern-lifecycle-policy)합니다.

구성 요소 버전 및 서비스 업데이트를 제외 하 고 바인딩에서는 설치에 대 한 기본적인 변경 되지 않습니다. R 및 Python 통합은 여전히이 데이터베이스 엔진 인스턴스의 일부 라이선스는 변경 되지 않습니다 (추가 비용 없이 바인딩과 연결 된), 및 지원 정책은 SQL Server 데이터베이스 엔진에 대 한 유지 합니다. 이 문서의 나머지 부분에서는 바인딩 메커니즘 및 각 버전의 SQL Server에 대 한 작동 하는 방법을 설명 합니다.

> [!NOTE]
> 바인딩 (In-database) 인스턴스에 SQL Server 인스턴스에 바인딩되는 적용 됩니다. 바인딩 (독립 실행형) 설치에 대 한 관련이 있습니다.

**SQL Server 2017 바인딩 고려 사항**

SQL Server 2017 Machine Learning Services에 대 한 Microsoft Machine Learning Server 추가 패키지를 제공 하기 시작 하거나 작업을 통해 최신 버전을 이미 설치한 경우에 바인딩을 고려할는 있습니다.

**SQL Server 2016 바인딩 고려 사항**

SQL Server 2016 R Services 고객에 대 한 바인딩을 제공 업데이트 된 R 패키지를 새 패키지 원본 설치의 일부가 아닌 ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)), 및 [미리 학습 된 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)를 모두 추가 될 수 있습니다 각 새 주 및 부 버전에서 새로 고칠 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)합니다. 바인딩 얻지 Python 지원 하는 SQL Server 2017 기능입니다. 

<a name="version-map"></a>

## <a name="version-map"></a>버전 맵

다음 표는 Microsoft Machine Learning Server (이전의 R Server를 시작 하는 Python 지원 추가 하기 전에 바인딩하는 경우에 잠재적인 업그레이드 경로 확인할 수 있도록 패키지 버전에서 릴리스 차량 표시 버전 맵을 MLS 9.2.1). 

바인딩 최신 버전의 R 또는 Anaconda를 보장 하지 않습니다 확인 합니다. Microsoft Machine Learning Server (MLS) 하에 바인딩하는 경우 설치 프로그램을 통해 설치 된 최신은 웹에서 확인할 수 없습니다 R 또는 Python 버전을 가져올 수 있습니다.

[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

구성 요소 |초기 릴리스 | [R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
R 통해 Microsoft R Open (MRO) | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[미리 학습 된 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1.0 |  1.0 |  1.0 |  1.0 |


[**SQL Server 2017 Machine Learning Services**](../install/sql-machine-learning-services-windows-install.md)

구성 요소 |초기 릴리스 | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
R 통해 Microsoft R Open (MRO) | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
4.2 anaconda Python 3.5 통해  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[미리 학습 된 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |

## <a name="how-component-upgrade-works"></a>구성 요소 업그레이드의 작동 원리 

Machine Learning Server에 R 및 Python의 기존 설치를 바인딩하는 경우 R 및 Python 라이브러리와 실행 파일로 업그레이드 됩니다. 바인딩을 통해 실행 되는 [Microsoft Machine Learning Server 설치 관리자](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) 기존 SQL Server 데이터베이스 엔진 인스턴스를 2016 또는 2017에서 설치를 실행 하는 경우에 R 또는 Python 통합 필요 합니다. 설치는 기존 기능을 감지 하 고 Machine Learning Server를 다시 바인딩해야 하 라는 메시지가 표시 됩니다. 

바인딩, C:\Program Files\Microsoft SQL Server\MSSQL14 내용의 중 MSSQLSERVER\R_SERVICES 및 \PYTHON_SERVICES 최신 실행 파일 및 C:\Program Files\Microsoft\ML Server\R_SERVER 및 \PYTHON_SERVER 라이브러리를 사용 하 여 덮어씁니다.

동시에, 서비스 모델 또한 대칭 이동 됩니다 SQL Server 업데이트 메커니즘에서 자주 주 및 부 릴리스 주기의 Microsoft Machine Learning Server. 최신 세대 R을 필요로 하는 데이터 과학 팀을 위한 매력적인 옵션 및 해당 솔루션에 대해 Python 모듈은 지원 정책을 전환 합니다. 

+ 바인딩 없이 R 및 Python 패키지는 SQL Server 서비스 팩 또는 누적 업데이트 (CU)를 설치할 때 버그 수정에 대 한 패치 됩니다. 
+ 바인딩을 사용 하 여 최신 패키지 버전에 적용할 수 CU 릴리스 일정을 독립적으로 인스턴스를 아래 합니다 [최신 수명 주기 정책](https://support.microsoft.com/help/30881/modern-lifecycle-policy) Microsoft Machine Learning Server 릴리스의 합니다. 최신 수명 주기 지원 정책을 더 짧은, 1 년 수명을 통해 좀 더 자주 업데이트를 제공합니다. 바인딩 후 계속 사용 가능 해지면 Microsoft 다운로드 사이트에서 R 및 Python의 향후 업데이트에 대 한 MLS 설치 관리자를 사용 합니다.

바인딩 R 및 Python 기능에만 적용 됩니다. 즉, R 및 Python 기능 (Microsoft R Open, Anaconda)에 대 한 오픈 소스 패키지 RevoScaleR 패키지를 소유, revoscalepy, 및 등입니다. 바인딩은 데이터베이스 엔진 인스턴스에 대 한 지원 모델을 변경 되지 않습니다 및 SQL Server의 버전을 변경 하지 않습니다.

바인딩은은 되돌릴 수입니다. SQL Server에서 서비스 되돌릴 수 있습니다 [인스턴스를 바인딩 해제](#bkmk_Unbind) 및 SQL Server 데이터베이스 엔진 인스턴스를 복구 하는 중입니다.

합계, 바인딩에 대 한 단계는 다음과 같습니다.

+ SQL Server 2016 R Services (또는 SQL Server 2017의 Machine Learning Services)으로 구성 된 기존 설치를 시작 합니다.
+ Microsoft Machine Learning Server의 버전에 사용 하려는 업그레이드 된 구성 요소 확인 합니다.
+ 다운로드 하 고 해당 버전에 대 한 설치 프로그램을 실행 합니다. 기존 인스턴스를 검색, 바인딩 옵션을 추가 하는 설정과 호환 인스턴스 목록을 반환 합니다.
+ 바인딩 및 다음 바인딩을 실행 하는 설치를 완료 하려면 원하는 인스턴스를 선택 합니다.

사용자 환경 측면에서 기술과 함께 작동 하는 방법을 변경 되지 않습니다. 유일한 차이점은 최신 버전의 패키지 및 추가 패키지 (예: SQL Server 2016 R Services 고객용 MicrosoftML) SQL Server를 통해 원래 사용할 수 없습니다.

## <a name="bkmk_BindWizard"></a>설치 프로그램을 사용 하 여 MLS에 바인딩

Microsoft Machine Learning 설치 기존 기능 및 SQL Server 버전을 검색 하 고 바인딩을 변경 하는 SqlBindR.exe 라는 유틸리티를 호출 합니다. 내부적으로 SqlBindR 설치에 연결 되며 간접적으로 사용 됩니다. 나중에 특정 옵션을 실행 하려면 명령줄에서 직접 SqlBindR을 호출할 수 있습니다.

1. SSMS에서 실행 `SELECT @@version` 서버 최소 빌드 요구 사항을 충족 확인 합니다. 

   SQL Server 2016 R Services에 대 한 최소값은 [서비스 팩 1](https://www.microsoft.com/download/details.aspx?id=54276) 하 고 [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)합니다.

1. 기본 R 버전을 확인 하 고 기존 버전을 확인 하려면 RevoScaleR 패키지는 바꿀 하려는 것 보다 낮습니다. SQL Server 2016 R Services에 대 한 R 기본 패키지 3.2.2 이며 RevoScaleR 8.0.3 합니다.

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

1. SSMS 및 SQL Server에 연결 된 있는 다른 도구를 닫습니다. 바인딩은 프로그램 파일을 덮어씁니다. SQL Server에 열려 있는 세션 바인딩 바인딩 오류 코드 6 사용 하 여 실패 합니다.

1. 업그레이드 하려는 인스턴스가 있는 컴퓨터에 Microsoft Machine Learning Server를 다운로드 합니다. 권장 합니다 [최신 버전](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)합니다.

1. 폴더 압축을 풀고 ServerSetup.exe, MLSWIN93 아래에 있는 시작 합니다.

   ![Microsoft Machine Learning Server 설치 마법사](media/mls-921-installer-start.PNG)

1. 온 **설치를 구성**를 업그레이드 하려면 구성 요소를 확인 하 고 호환 인스턴스 목록을 검토 합니다. 

   이 단계는 매우 중요합니다.

   왼쪽의 모든 기능을 유지 하거나 업그레이드 하려면를 선택 합니다. 일부 기능 및 다른 것을 업그레이드할 수 없습니다. 비어 있는 확인란이 현재 설치 된 것으로 가정 하는 기능을 제거 합니다. SQL Server 2016 R Services (MSSQL13)의 인스턴스가 지정 된 스크린샷에서 R 및 R 버전 미리 학습된 된 모델의 선택 됩니다. 이 구성은 SQL Server 2016 R 하지만 하지 Python을 지원 하기 때문에 유효 합니다.

   SQL Server 2016 R Services의 구성 요소를 업그레이드 하는 경우에 Python 기능을 선택 하지 마십시오. Python SQL Server 2016 R Services에 추가할 수 없습니다.

   오른쪽의 인스턴스 이름 옆의 확인란을 선택 합니다. 나열 된 인스턴스가 없는 경우는 호환 되지 않는 조합을 해야 합니다. 인스턴스를 선택 하지 않으면 Machine Learning Server는 새 독립 실행형 설치를 만들고 SQL Server 라이브러리 변경 되지 않습니다. 인스턴스를 선택할 수 없습니다, 경우에 없을 수도 있습니다 [SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)합니다. 

    ![설치 단계 구성](media/mls-931-installer-mssql13.png)

1. 에 **사용권 계약** 페이지에서 **이러한 조건에 동의** Machine Learning Server에 대 한 라이선스 사용 조건에 동의 합니다. 

1. 후속 페이지에서 Microsoft R Open 또는 Anaconda Python 배포와 같은 선택한 오픈 소스 구성 요소에 대 한 추가 라이선스 조건에 동의 제공 합니다.

1. 에 **거의** 페이지에서 설치 폴더의 참고를 확인 합니다. 기본 폴더는 \Program Files\Microsoft\ML 서버.

    설치 폴더를 변경 하려면 클릭 **고급** 마법사의 첫 번째 페이지로 돌아갑니다. 그러나 이전에 선택한 모든 항목을 반복 해야 합니다.

설치 과정에서 SQL Server에서 사용 되는 모든 R 또는 Python 라이브러리 바뀝니다 및 실행 패드 최신 구성 요소를 사용 하도록 업데이트 됩니다. 결과적으로, 인스턴스 라이브러리 기본적 R_SERVICES 폴더에서 이전에 사용 하는 경우 업그레이드 후 이러한 라이브러리 제거 되 고 새 위치에 라이브러리를 사용 하는 실행 패드 서비스에 대 한 속성 변경 됩니다.

바인딩 이러한 폴더의 내용을 영향을 줍니다. C:\Program Files\Microsoft SQL Server\MSSQL13입니다. MSSQLSERVER\R_SERVICES\library는 C:\Program Files\Microsoft\ML Server\R_SERVER의 내용으로 바뀝니다. 두 번째 폴더 및 해당 콘텐츠가 Microsoft Machine Learning Server 설치 프로그램에서 생성 됩니다. 

업그레이드에 실패 하면 체크 [SqlBindR 오류 코드](#sqlbindr-error-codes) 자세한 내용은 합니다.

## <a name="confirm-binding"></a>바인딩 확인

최신 버전을 확인 하려면 R 및 RevoScaleR의 버전을 다시 확인 합니다. 데이터베이스 엔진 인스턴스에 R 패키지를 사용 하 여 분산 R 콘솔을 사용 하 여 패키지 정보를 가져오려면:

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

SQL Server 2016 R Services Machine Learning Server 9.3에 바인딩된, R 기본 패키지 3.4.3, RevoScaleR 9.3에 있어야 합니다.이 고 MicrosoftML 9.3 있어야 합니다. 

미리 학습된 된 모델에 추가한 경우에 모델에 MicrosoftML 라이브러리에 포함 되 고 MicrosoftML 함수를 통해 호출할 수 있습니다. 자세한 내용은 [microsoftml R 샘플](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml)합니다.

## <a name="offline-binding-no-internet-access"></a>오프 라인 바인딩 (인터넷 액세스 없음)

시스템의 인터넷 연결 되지 않은 경우 설치 관리자 및.cab 파일에는 인터넷에 연결 된 컴퓨터에 다운로드를 후 격리 된 서버에 파일을 전송 합니다. 

설치 관리자 (ServerSetup.exe) (RevoScaleR, MicrosoftML, olapR, sqlRUtils) Microsoft 패키지를 포함합니다. 기타 핵심 구성 요소를 제공 하는.cab 파일입니다. 예를 들어, "SRO" cab R Open, Microsoft의 배포의 오픈 소스 R 제공

다음 지침을 오프 라인 설치에 대 한 파일을 배치 하는 방법에 설명 합니다.

1. MLS 설치 관리자를 다운로드 합니다. 단일 압축 된 파일로 다운로드합니다. 것이 좋습니다는 [최신 버전](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)를 설치할 수도 있지만 [버전](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)합니다.

1. .Cab 파일을 다운로드 합니다. 다음 링크는 9.3 릴리스에 대 한 합니다. 이전 버전에 필요한 경우 추가 링크에서 찾을 수 있습니다 [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)합니다. 회수 Anaconda Python/SQL Server 2017의 Machine Learning Services 인스턴스를에 추가할 수 있습니다. R 및 Python; 둘 다에 대해 미리 학습 된 모델 존재 .cab은 사용 중인 언어에서 모델을 제공 합니다.

    | 기능 | 다운로드 |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | 미리 학습된 모델 | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. 대상 서버에.zip 및.cab 파일을 전송 합니다.

1. 서버에서 입력 `%temp%` 실행 명령에 임시 디렉터리의 실제 위치를 가져옵니다. 컴퓨터의 실제 경로 달라 지지만 일반적으로 `C:\Users\<your-user-name>\AppData\Local\Temp`입니다.

1. % Temp % 폴더의.cab 파일을 배치 합니다.

1. 설치 관리자를 압축을 풉니다.

1. ServerSetup.exe를 실행 하 고 따릅니다는 설치를 완료 하려면 화면의 지시 합니다.

## <a name="bkmk_BindCmd"></a>명령줄 작업

Microsoft Machine Learning Server를 실행 한 후 SqlBindR.exe 라는 명령줄 유틸리티 추가 바인딩 작업에 사용할 수 있는 사용할 수 있습니다. 예를 들어 역방향 바인딩을 결정 했으면, 없습니다 설치를 다시 실행 하거나 명령줄 유틸리티를 사용 합니다. 또한 예를 들어 호환성 및 가용성을 확인 하려면이 도구를 사용할 수 있습니다.

> [!TIP]
> SqlBindR을 찾을 수 없습니까? 아마도 실행 하지 않은 설치 합니다. SqlBindR은 Machine Learning Server 설치 프로그램을 실행 한 후에 사용할 수 있습니다.

1. 관리자 권한으로 명령 프롬프트를 열고 sqlbindr.exe가 포함된 폴더로 이동합니다. 기본 위치는 C:\Program Files\Microsoft\MLServer\Setup

2. 다음 명령을 입력하여 사용 가능한 인스턴스 목록을 표시합니다. `SqlBindR.exe /list`
  
   전체 인스턴스 이름을 나열된 대로 기록해 둡니다. 예를 들어 인스턴스 이름이 MSSQL14 수 있습니다. 기본 인스턴스의 경우 또는 SERVERNAME와 같은 것에 대 한 MSSQLSERVER입니다. MYNAMEDINSTANCE 합니다.

3. 실행 합니다 **SqlBindR.exe** 명령과 합니다 *바인딩/* 인수를 이전 단계에서 반환 된 인스턴스 이름을 사용 하 여 업그레이드 하려면 인스턴스의 이름을 지정 합니다.

   예를 들어 기본 인스턴스를 업그레이드 하려면 다음을 입력 합니다.  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 업그레이드가 완료 되 면 수정 된 인스턴스와 연결 된 실행 패드 서비스를 다시 시작 합니다.

## <a name="bkmk_Unbind"></a>되돌리거나 인스턴스를 바인딩 해제

R 및 Python 구성 요소, SQL Server 설치 프로그램에서 설정의 초기 설치에 바인딩된 인스턴스를 복원할 수 있습니다. SQL Server 서비스를 다시 되돌리기 세 부분이 있습니다.

+ [1단계: Microsoft Machine Learning Server에서에서 바인딩 해제](#step-1-unbind)
+ [2단계: 인스턴스를 원래 상태로 복원](#step-2-restore)
+ [3단계: 설치에 추가 하는 모든 패키지 다시 설치](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>1단계: 언바인딩

두 가지 바인딩 롤백에 대 한 옵션: 다시 설치를 다시 실행 하거나 SqlBindR 명령줄 유틸리티를 사용 합니다.

#### <a name="bkmk_wizunbind"></a> 설치 프로그램을 사용 하 여 바인딩 해제

1. Machine Learning Server 설치 관리자를 찾습니다. 설치 프로그램을 제거한 경우 다시 다운로드 또는 다른 컴퓨터에서 복사 해야 합니다.
2. 바인딩 해제 하려는 인스턴스가 있는 컴퓨터의 설치 관리자를 실행 해야 합니다.
2. 설치 관리자는 적합 한 바인딩을 해제 하는 것에 대 한 로컬 인스턴스를 식별 합니다.
3. 원래 구성으로 되돌리고 싶은 인스턴스 옆의 확인란을 선택 취소 합니다.
4. 라이선스에 동의 합니다. 설치 하는 경우에 라이선스 약관에 동의 나타내야 합니다.
5. **마침**을 클릭합니다. 프로세스는 시간이 걸립니다.

#### <a name="bkmk_cmdunbind"></a> 명령줄을 사용 하 여 바인딩 해제

1. 이전 섹션에 설명된 대로 명령 프롬프트를 열고 **sqlbindr.exe**가 포함된 폴더로 이동합니다.

2. */unbind* 인수와 함께 **SqlBindR.exe** 명령을 실행하고 인스턴스를 지정합니다.

   예를 들어 다음 명령은 기본 인스턴스를 되돌립니다.
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>2단계: SQL Server 인스턴스에 복구

R 및 Python 기능의 데이터베이스 엔진 인스턴스를 복구 하려면 SQL Server 설치 프로그램을 실행 합니다. 기존 업데이트는 유지 되지만 서비스 R 및 Python 패키지를 업데이트 하는 모든 SQL Server을 놓친 경우이 단계는 이러한 패치 적용 됩니다.

또는 더 많은 작업 이지만 완전히 제거 하 고 데이터베이스 엔진 인스턴스를 다시 설치 하 고 모든 서비스 업데이트를 적용 한 다음 수 없습니다.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>3단계: 모든 타사 패키지를 추가 합니다.

다른 오픈 소스 또는 타사 패키지 패키지 라이브러리에 추가한 수 있습니다. 기본 패키지 라이브러리의 위치를 전환 바인딩의 반대로, 이후 R 및 Python 지금 사용 하는 라이브러리에 패키지를 다시 설치 해야 합니다. 자세한 내용은 [패키지를 기본](installing-and-managing-r-packages.md), [새 R 패키지 설치](install-additional-r-packages-on-sql-server.md), 및 [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)합니다.

## <a name="sqlbindrexe-command-syntax"></a>SqlBindR.exe 명령 구문

### <a name="usage"></a>사용법

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>매개 변수

|이름|Description|
|------|------|
|*list*| 현재 컴퓨터의 모든 SQL Database 인스턴스 ID 목록을 표시합니다.|
|*bind*| 지정된 SQL Database 인스턴스를 최신 버전의 R 서버로 업그레이드하고 인스턴스가 R 서버의 향후 업그레이드를 자동으로 가져오도록 합니다.|
|*unbind*|지정된 SQL Database 인스턴스에서 최신 버전의 R 서버를 제거하고 향후 R 서버 업그레이드가 인스턴스에 영향을 주지 않도록 합니다.|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>바인딩 오류

MLS 설치 관리자 및 SqlBindR 다음 오류 코드 및 메시지를 반환합니다.

|오류 코드  | 메시지           | 설명               |
|------------|-------------------|-----------------------|
|바인딩 오류 | (성공)를 확인 합니다. | 바인딩 오류 없이 전달 합니다. |
|바인딩 오류 1 | 잘못 된 인수 | 구문 오류가 있습니다. |
|바인딩 오류 2 | 잘못 된 작업 | 구문 오류가 있습니다. |
|바인딩 오류 3 | 잘못 된 인스턴스 | 인스턴스는 존재 하지만 바인딩에 적합 하지 않습니다. |
|바인딩 오류 4 | 바인딩할 수 없습니다 | |
|바인딩 오류 5 | 이미 바인딩되어 있습니다. | *bind* 명령을 실행했지만 지정한 인스턴스가 이미 바인딩되어 있습니다. |
|바인딩 오류 6 | 바인드 실패 | 인스턴스를 바인딩 해제 하는 동안 오류가 발생 했습니다. 이 오류는 모든 기능을 선택 하지 않고 MLS 설치 관리자를 실행 하는 경우에 발생할 수 있습니다. 바인딩은 MSSQL 인스턴스 및 R을 선택 하 고 인스턴스를 가정 하는 Python, SQL Server 2017은 필요 합니다. SqlBindR Program Files 폴더에 쓸 수 없습니다 경우에이 오류가 발생 합니다. 열려 있는 세션 또는 SQL Server에 대 한 핸들에는이 오류가 발생 하면 합니다. 이 오류가 발생할 경우 컴퓨터를 다시 부팅 하 고 모든 새 세션을 시작 하기 전에 바인딩 단계를 다시 실행 합니다.|
|바인딩 오류 7 | 바인딩되지 않은 | 데이터베이스 엔진 인스턴스에 R Services 또는 SQL Server Machine Learning Services 있습니다. 인스턴스는 Microsoft Machine Learning Server 바인딩되어 있지 않습니다. |
|바인딩 오류 8 | 바인딩 해제 실패 | 인스턴스를 바인딩 해제 하는 동안 오류가 발생 했습니다. |
|바인딩 오류 9 | 인스턴스를 찾을 수 없습니다. | 이 컴퓨터에 없는 데이터베이스 엔진 인스턴스를 찾을 수 없습니다. |

## <a name="known-issues"></a>알려진 문제

이 섹션에서는 SqlBindR.exe 유틸리티 또는 SQL Server 인스턴스에 영향을 주는 Machine Learning Server의 업그레이드를 사용 하 여 관련 알려진된 문제를 나열 합니다.

### <a name="restoring-packages-that-were-previously-installed"></a>이전에 설치 된 패키지를 복원 합니다.

Microsoft R Server 9.0.1로 업그레이드 하는 경우 해당 버전에 대 한 SqlBindR.exe 버전이 원래 패키지를 복원 하지 못했습니다 또는 R 구성 요소 완전히 사용자 인스턴스에서 SQL Server 복구를 실행 하는 필요한 모든 서비스 릴리스를 적용 하 고 다시 인스턴스입니다.

이후 버전의 SqlBindR 자동으로 R 구성 요소를 다시 설치 하지 않아도 원래 R 기능을 복원 하거나 다시 서버에 패치 합니다. 그러나 초기 설치 후 추가 된 모든 R 패키지 업데이트를 설치 해야 합니다.

패키지 관리 역할을 설치 하 고 패키지 공유를 사용한 경우이 작업은 훨씬 더 쉽게: R 명령을 사용 하 여 데이터베이스에서 레코드를 사용 하 여 파일 시스템에 설치 된 패키지를 동기화 하 고 그 반대의 경우도 마찬가지입니다. 자세한 내용은 [SQL Server에 대 한 R 패키지 관리](install-additional-r-packages-on-sql-server.md)합니다.

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>SQL Server에서 여러 업그레이드 문제

업그레이드 한 경우 이전에 SQL Server 2016 R Services의 인스턴스를 9.0.1, Microsoft R server 9.1.0 새 설치 관리자를 실행 하는 경우, 모든 유효한 인스턴스 목록을 표시 하 고 기본적으로 이전에 바인딩된 인스턴스를 선택 합니다. 계속 하면 이전에 바인딩된 인스턴스를 바인딩 해제 됩니다. 결과적으로 이전 9.0.1 패키지와 관련 된 포함 되지만 Microsoft R Server (9.1.0)의 새 버전이 설치 되어 있지 설치 제거 됩니다.

해결 방법으로 기존 R Server 설치를 다음과 같이 수정할 수 있습니다.
1. 제어판에서 엽니다 **프로그램 추가 / 제거**합니다.
2. Microsoft R Server를 찾아 누릅니다 **변경/수정**합니다.
3. 설치 관리자가 시작 되 면 9.1.0 바인딩할 인스턴스를 선택 합니다.

Microsoft Machine Learning Server 9.2.1 및 9.3에이 문제가 없습니다.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>바인딩 또는 바인딩 해제가 여러 임시 폴더

경우에 따라 바인딩 및 바인딩 해제 작업 임시 폴더 정리에 실패 합니다.
다음과 같은 이름의 폴더를 찾은 경우 설치가 완료 되 면 제거할 수 있습니다. R_SERVICES_<guid>

> [!NOTE]
> 설치가 완료 될 때까지 대기 해야 합니다. R 라이브러리 버전을 사용 하 여 연결을 제거한 다음 새 R 라이브러리를 추가 하는 데 시간이 오래 걸릴 수 있습니다. 작업이 완료 되 면 임시 폴더 제거 됩니다.

## <a name="see-also"></a>참고자료

+ [Machine Learning Server에 대 한 Windows (인터넷 연결)를 설치 합니다.](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Machine Learning Server에 대 한 Windows (오프 라인)를 설치 합니다.](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Machine Learning Server의 알려진된 문제](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [R Server의 이전 릴리스에서 기능 발표](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [사용 되지 않는, 지원 되지 않는 또는 변경 된 기능](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)

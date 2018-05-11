---
title: R 및 Python 구성 요소가 SQL Server R 인스턴스 (컴퓨터 학습 서비스)에서 업그레이드 | Microsoft Docs
description: R 및 SQL Server 2016 R Services 또는 SQL Server 2017 컴퓨터 학습 서비스 컴퓨터 학습 서버 바인딩할 sqlbindr.exe를 사용 하 여 Python 업그레이드 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 716fbd8a105164d40bfa6b3e67d126067174dc5a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>SQL Server 인스턴스에서 컴퓨터 (예: R 및 Python) 학습 구성 업그레이드
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server의 R 및 Python 통합 Microsoft 소유 하 고 오픈 소스 패키지에 포함 됩니다. 표준 SQL Server 서비스에서 R 및 Python 패키지는 SQL Server 릴리스 주기를 현재 버전에서 기존 패키지에 대 한 버그 수정에 따라 업데이트 됩니다. 

대부분 데이터 과학자는 제공 되 면 최신 패키지 사용에 익숙한 합니다. SQL Server 2017 컴퓨터 학습 Services (In-database) 및 SQL Server 2016 R Services (In-database) 모두에 대 한 최신 버전의 R 및 Python을 변경 하 여 가져올 수 있습니다는 *바인딩* 에서 SQL Server 서비스를 [Microsoft 기계 학습 서버](https://docs.microsoft.com/en-us/machine-learning-server/index) 및 [최신 수명 주기 지원 정책](https://support.microsoft.com/help/30881/modern-lifecycle-policy)합니다.

바인딩 설치의 기본 사항을 변경 하지 않습니다: R 및 Python 통합 여전히의 일부인 데이터베이스 엔진 인스턴스를 사용 하는 라이선스는 변경 되지 않습니다 (추가 비용 없이 바인딩과 연결 된)를 누르고 있는 SQL Server 지원 정책 여전히 데이터베이스 엔진입니다. 하지만 R 및 Python 패키지 처리 방법을 변경지 않습니다 다시 바인딩해야 합니다. 이 문서의 나머지 부분에서는 바인딩 메커니즘 및 SQL Server의 각 버전에 대해 작동 방식을 설명 합니다.

> [!NOTE]
> 바인딩 (In-database) 인스턴스에만 적용 됩니다. 바인딩에 (독립 실행형) 설치와 관련이 없습니다.

**SQL Server 2017**

SQL Server 2017 컴퓨터 학습 서비스에 대 한 Microsoft 컴퓨터 학습 서버를 추가 패키지를 제공 하기 시작 되거나 어떤 조치 최신 버전이 이미 있는 경우에 바인딩 라고 생각할.

**SQL Server 2016**

SQL Server 2016 R 서비스 고객에 대 한 방법은 두 가지 새로운 기능과 업데이트를 가져오기 위한 R 패키지 합니다. 하나는 SQL Server 2017;로 업그레이드 두 번째, Microsoft Learning 서버 컴퓨터에 바인딩.

SQL Server 2017로 업그레이드 하면 R 패키지를에 가져옵니다 해당 릴리스 및 Python 기능에 포함 된 버전. 또는 바인딩 가져옵니다 Microsoft 학습 서버 컴퓨터의 각 새로운 주 및 부 버전에서 더 이상 새로 고칠 수 있는 R 패키지를 업데이트 합니다. 

바인딩 얻지 SQL Server 2017 기능인 Python 지원 합니다. 

**Microsoft 컴퓨터 학습 서버를 통해 사용할 수 있는 구성 요소 업그레이드**

다음 표에서 Microsoft 컴퓨터 학습 서버 (이전에 R Server MLS 9.2.1부터 Python 지원 추가 하기 전에)에 바인딩하는 경우 업그레이드 된 SQL Server와 함께 설치 된 버전을 보여 주는 버전 맵입니다. 

바인딩 최신 버전의 R 또는 Anaconda 보장 하지 않습니다 확인 합니다. Microsoft 학습 서버 컴퓨터에 바인딩하는 경우 웹에서 사용 가능한 최신 버전이 아닐 수 있습니다는 설치 프로그램을 통해 설치 된 Python 또는 R 버전을 가져올 수 있습니다.

[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

구성 요소 |초기 릴리스 | R 서버 9.0.1 | R 서버 9.1 | MLS 9.2.1 | MLS 9.3 |
----------|----------------|----------------|--------------|---------|-------|
R 통해 Microsoft R Open (MRO) | R 3.2.2     | 3.3.2 R   |3.3.3 R   | 3.4.1 R  | 3.4.3 R |
[RevoScaleR](https://docs.microsoft.com/achine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[미리 학습 된 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1.0 |  1.0 |  1.0 |  1.0 |


[**SQL Server 2017 컴퓨터 학습 서비스**](../install/sql-machine-learning-services-windows-install.md)

구성 요소 |초기 릴리스 | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
R 통해 Microsoft R Open (MRO) | 3.3.3 R | 3.4.3 R | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Python 3.5 통해 anaconda 4.2  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[미리 학습 된 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |

## <a name="how-component-upgrade-works"></a>구성 요소 업그레이드 작동 방법

구성 요소 업그레이드 방식은 *바인딩* SQL Server 2016 R Services 인스턴스 (또는 SQL Server 2017 컴퓨터 학습 서비스 인스턴스)를 [Microsoft 컴퓨터 학습 서버](https://docs.microsoft.com/machine-learning-server/index)합니다. 

Microsoft, 학습 서버 컴퓨터는 온-프레미스 서버 제품 SQL Server에서 동일한 인터프리터 및 패키지와 구분 합니다. R 패키지 및 Python 패키지 Microsoft 컴퓨터 학습 서버와 함께 출시는 SQL Server가 설치 하는 것 보다 최신를 사용할 수 있도록 SQL Server 서비스 업데이트 메커니즘 교체 바인딩입니다. 정책을 지원 전환는 최신 세대 R을 필요로 하는 데이터 과학 팀에 대해 선택할 수 없었습니다 및 해결 방법에 대 한 Python 모듈입니다. 

바인딩을 통해 실행 되는 [MLS installer](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)합니다. 설치 관리자 특정 R 및 Python 패키지를 업데이트 하지만 연결이 끊어진된 서버 설치 독립 실행형 SQL Server 데이터베이스의 인스턴스를 대체 하지는 않습니다.

+ 바인딩이 없으면 R 및 Python 패키지는 SQL Server 서비스 팩 또는 누적 업데이트 (CU)를 설치할 때 버그 수정에 대 한 패치 됩니다. 
+ 바인딩을 사용할 경우 새 패키지 버전에 적용할 수 CU 릴리스 일정을 독립적으로 해당 인스턴스를 아래에서 [최신 수명 주기 정책](https://support.microsoft.com/help/30881/modern-lifecycle-policy) 및 Microsoft 학습 서버 컴퓨터의 버전입니다. 최신 수명 주기 지원 정책 위에 1 년, 더 짧은 수명이 더 자주 업데이트를 제공합니다. 바인딩 후를 계속 Microsoft 학습 서버 컴퓨터에서에서 제공 되 면 R 및 Python의 향후 업데이트에 대 한 MLS 설치 관리자를 사용 합니다.

바인딩 R 및 Python 기능에 적용 됩니다. 즉, R 및 Python 기능 (Microsoft R Open, Anaconda)에 대 한 오픈 소스 패키지와는 RevoScaleR 패키지를 소유, revoscalepy, 등입니다. 바인딩은 데이터베이스 엔진 인스턴스에 대 한 지원 모델을 변경 되지 않습니다 및 SQL Server의 버전을 변경 하지 않습니다.

바인딩은 복구할 수 없습니다. SQL Server에서 지 원하는 데 되돌릴 수 [인스턴스를 바인딩 해제](#bkmk_Unbind) 및 SQL Server 데이터베이스 엔진 인스턴스를 복구 하는 중입니다.

합계를 계산 바인딩에 대 한 단계는 다음과 같습니다.

+ 기존에 구성 된 설치 된 SQL Server 2016 R Services (또는 SQL Server 2017 컴퓨터 학습 서비스)로 시작 합니다.
+ Microsoft, 학습 서버 컴퓨터의 버전에는 업그레이드 된 구성 요소를 사용 하 여 확인 합니다.
+ 다운로드 하 고 해당 버전에 대 한 설치 프로그램을 실행 합니다. 설치 프로그램이 기존 인스턴스를 찾아냅니다 바인딩 옵션을 더하고 호환 인스턴스 목록을 반환 합니다.
+ 바인딩한 후 바인딩을 실행 하는 설치를 완료 하려면 인스턴스를 선택 합니다.

사용자 환경, 측면에서 기술과 함께 작동 하는 방식 변경 되지 않습니다. 유일한 차이점은 최신 버전의 패키지와 추가 패키지 (예: SQL Server 2016 R 서비스 고객에 대 한 MicrosoftML) SQL Server를 통해 원래 사용할 수 없습니다.

## <a name="bkmk_BindWizard"></a>설치 프로그램을 사용 하 여 MLS에 바인딩

Microsoft Machine Learning 설치는 기존 기능과 SQL Server 버전을 검색 하 고 바인딩을 변경 하는 SqlBindR.exe 라는 유틸리티를 호출 합니다. 내부적으로 SqlBindR 속성 설정에 연결 되며 간접적으로 사용 됩니다. 이상에서는 SqlBindR 특정 옵션을 실행 하려면 명령줄에서 직접 호출할 수 있습니다.

1. 서버는 최소 빌드가 요구 사항을 충족 하는지 확인 합니다. SQL Server 2016 R Services에 대 한 최소값은 [서비스 팩 1](https://www.microsoft.com/download/details.aspx?id=54276) 및 [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)합니다. SSMS에서 실행 `SELECT @@version` 서버 버전 정보를 반환 합니다. 

1. 사용 하 여 대체 하려는 보다 낮은 기존 버전을 확인 하는 R과 RevoScaleR의 버전을 확인 합니다. SQL Server 2016 R Services에 대 한 R 기본 패키지 3.2.2 이며 RevoScaleR 8.0.3 합니다.

    + Files\microsoft SQL Server\MSSQL13로 이동 합니다. MSSQLSERVER\R_SERVICES\bin
    + 두 번 클릭 **R** 콘솔을 엽니다.
    + 패키지 버전을 사용 `library(help="base")` 및 `library(help="RevoScaleR")`합니다. 

1. 업그레이드 하려는 인스턴스가 있는 컴퓨터에 Microsoft 컴퓨터 학습 서버를 다운로드 합니다. 권장 된 [최신 버전](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)합니다.

1. 폴더를 압축 해제 하 고 MLSWIN93 아래에 있는 ServerSetup.exe를 시작 합니다.

   ![Microsoft 컴퓨터 학습 서버 설치 마법사](media/mls-921-installer-start.PNG)

1. **설치를 구성**를 업그레이드 하려면 구성 요소를 확인 하 고 호환 인스턴스 목록을 검토 합니다. 

   왼쪽에 유지 하거나 업그레이드 하려면 모든 기능을 선택 합니다. 일부 기능 중 등을 업그레이드할 수 없습니다. 빈 확인란은 현재 설치 된 것으로 가정 하 고 해당 기능을 제거 합니다. SQL Server 2016 R Services (MSSQL13)의 인스턴스가 스크린샷에서 R 및 R 버전 미리 학습 된 모델의 선택 됩니다. 이 구성은 SQL Server 2016 R 하지만 하지 Python 지원 하기 때문에 유효 합니다.

   오른쪽의 인스턴스 이름 옆의 확인란을 선택 합니다. 인스턴스가 나열 된 경우 호환 되지 않는 조합을 해야 합니다. 인스턴스 선택 하지 않으면 서버를 학습 하는 컴퓨터의 새 독립 실행형 설치 만들어지고 SQL Server 라이브러리는 변경 되지 않습니다. 인스턴스를 선택할 수 없는 경우에 아닐 수 있습니다 [SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)합니다. 

    ![Microsoft 컴퓨터 학습 서버 설치 마법사](media/mls-931-installer-mssql13.png)

1. 에 **사용권 계약** 페이지에서 **이러한 조건에 동의** 학습 서버 컴퓨터에 대 한 라이선스 조건에 동의 합니다. 

1. 연속 페이지에서 선택한 Microsoft R Open 또는 Python Anaconda 배포와 같은 오픈 소스 구성 요소에 대 한 추가 라이선스 조건에 동의 하 게 제공 합니다.

1. 에 **얼마 남지** 페이지에서 설치 폴더를 기록 합니다. 기본 폴더는 \Program Files\Microsoft\ML 서버.

    설치 폴더를 변경 하려면 클릭 **고급** 마법사의 첫 페이지로 돌아갑니다. 그러나 이전에 선택한 항목을 반복 해야 합니다.

설치 과정에서 SQL Server에서 사용 하는 모든 Python 또는 R 라이브러리 대체 하 고 실행 패드 최신 구성 요소를 사용 하도록 업데이트 됩니다. 결과적으로, 인스턴스 라이브러리 기본 R_SERVICES 폴더에 이전에 사용한 경우 업그레이드 후 이러한 라이브러리 제거 되 고 새 위치에 라이브러리를 사용 하는 실행 패드 서비스에 대 한 속성이 변경 됩니다.

바인딩 이러한 폴더의 내용에 영향을 줍니다: C:\Program Files\Microsoft SQL Server\MSSQL13 합니다. MSSQLSERVER\R_SERVICES\library는 C:\Program Files\Microsoft\ML Server\R_SERVER의 내용으로 바뀝니다. 두 번째 폴더와 해당 내용을 Microsoft 컴퓨터 학습 서버 설치 프로그램에서 생성 됩니다. 

업그레이드가 실패 하면 확인 [SqlBindR 오류 코드](#sqlbindr-error-codes) 자세한 정보에 대 한 합니다.

## <a name="confirm-binding"></a>바인딩 확인

최신 버전을 확인 하는 R와 RevoScaleR의 버전을 다시 확인 합니다. 데이터베이스 엔진 인스턴스에서 R 패키지와 함께 배포 하는 R 콘솔을 사용 하 여 패키지 정보를 가져오려면:

+ Files\microsoft SQL Server\MSSQL13로 이동 합니다. MSSQLSERVER\R_SERVICES\bin
+ 두 번 클릭 **R** 콘솔을 엽니다.
+ 패키지 버전을 사용 `library(help="base")` 및 `library(help="RevoScaleR")`합니다. 

SQL Server 2016 R Services 컴퓨터 학습 서버 9.3에 바인딩된, R 기본 패키지 3.4.1 수, RevoScaleR 9.3, 해야 하며 MicrosoftML 9.3이 있어야 합니다. 

미리 학습 된 모델을 추가한 경우에 모델에 MicrosoftML 라이브러리에 포함 되 고 MicrosoftML 함수를 통해 호출할 수 있습니다. 자세한 내용은 참조 [MicrosoftML에 대 한 R 샘플](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml)합니다.

## <a name="offline-no-internet-access"></a>오프 라인 (인터넷 액세스 없음)

인터넷에 연결 되지 않은 시스템의 경우 인터넷에 연결 된 컴퓨터에 설치 관리자 및 cab 파일을 다운로드 하 고 격리 된 서버에 파일을 전송 수 있습니다. 

설치 관리자 (ServerSetup.exe) Microsoft 패키지 (RevoScaleR, MicrosoftML, olapR, sqlRUtils) 포함 되어 있습니다. 다른 핵심 구성 요소를 제공 하는.cab 파일입니다. 예를 들어 "SRO" cab 제공 R Open, Microsoft 웹 배포는 오픈 소스 R입니다.

다음 지침에서는 오프 라인 설치에 대 한 파일을 배치 하는 방법을 설명 합니다.

1. MLS 설치 관리자를 다운로드 합니다. 단일 파일을 zip으로 다운로드합니다. 권장는 [최신 버전](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer), 하지만 설치할 수 [이전 버전](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)합니다.

1. .Cab 파일을 다운로드 합니다. 다음 링크는 9.3 릴리스에 대 한 합니다. 이전 버전을 필요로 하는 경우 추가 링크에서 찾을 수 있습니다 [R 서버 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)합니다. 회수 Python/Anaconda 인스턴스를 SQL Server 2017 컴퓨터 학습 서비스에만 추가할 수 있습니다. R 및 Python; 모두에 대해 미리 학습 된 모델을 배포한 .cab은 사용 중인 언어에서 모델을 제공 합니다.

    | 기능 | 다운로드 |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | 미리 학습 된 모델 | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. 대상 서버에.zip 및.cab 파일을 전송 합니다.

1. 서버에서 입력 `%temp%` 실행 명령의 임시 디렉터리의 실제 위치를 가져옵니다. 컴퓨터의 실제 경로 달라 지지만 일반적으로 `C:\Users\<your-user-name>\AppData\Local\Temp`합니다.

1. % Temp % 폴더에 Place.cab 파일입니다.

1. 설치 관리자를 압축을 풉니다.

1. ServerSetup.exe를 실행 하 고 따릅니다는 설치를 완료 하려면 화면의 지시 합니다.

## <a name="bkmk_BindCmd"></a>명령줄 작업

Microsoft, 학습 서버 컴퓨터를 실행 하면 SqlBindR.exe 라는 명령줄 유틸리티 바인딩 추가 작업에 사용할 수 있습니다 사용할 수 있습니다. 예를 들어 바인딩을 반대로 하도록 결정할 경우, 수 설치를 다시 실행 하거나 명령줄 유틸리티를 사용 합니다. 또한 호환성 및 가용성 예를 들어 확인 하려면이 도구를 사용할 수 있습니다.

> [!TIP]
> SqlBindR를 찾을 수 없나요? 아마도 설치 프로그램을 실행 하지 않은 합니다. SqlBindR를 컴퓨터 학습 서버 설치 프로그램을 실행 한 후에 사용할 수 있습니다.

1. 관리자 권한으로 명령 프롬프트를 열고 sqlbindr.exe가 포함된 폴더로 이동합니다. 기본 위치는 C:\Program Files\Microsoft\MLServer\Setup

2. 다음 명령을 입력하여 사용 가능한 인스턴스 목록을 표시합니다. `SqlBindR.exe /list`
  
   전체 인스턴스 이름을 나열된 대로 기록해 둡니다. 예를 들어 인스턴스 이름이 MSSQL14 수도 있습니다. 기본 인스턴스 또는 다음과 같이 서버 이름에 대 한 MSSQLSERVER입니다. 인스턴스 MYNAMEDINSTANCE 합니다.

3. 실행 된 **SqlBindR.exe** 명령에 *바인딩/* 인수를 하 고 이전 단계에서 반환 된 인스턴스 이름을 사용 하 여를 업그레이드 하려면 인스턴스의 이름을 지정 합니다.

   예를 들어 기본 인스턴스를 업그레이드 하려면 다음을 입력 합니다.  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 업그레이드가 완료 되 면 수정 된 인스턴스와 관련 된 실행 패드 서비스를 다시 시작 합니다.

## <a name="bkmk_Unbind"></a>Revert 또는 인스턴스를 바인딩 해제

SQL Server 설치 프로그램에서 설정한 R 및 Python 구성의 초기 설치에 바인딩된 인스턴스를 복원할 수 있습니다. SQL Server 서비스으로 다시 전환 세 부분이 있습니다.

+ [1 단계: Microsoft 기계 서버 학습에서 바인딩 해제](#step-1-unbind)
+ [2 단계: 인스턴스를 원래 상태로 복원](#step-2-restore)
+ [3 단계: 설치에 추가 하는 모든 패키지를 다시 설치](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>1 단계: 바인딩 해제

두 개의 바인딩 롤백에 대 한 옵션: SqlBindR 명령줄 유틸리티를 사용 하거나 설치를 다시 실행 하십시오.

#### <a name="bkmk_wizunbind"></a> 설치 프로그램을 사용 하 여 바인딩 해제

1. 서버를 학습 하는 컴퓨터에 대 한 설치 관리자를 찾습니다. 설치 프로그램을 제거한 경우 다시 다운로드 하거나 다른 컴퓨터에서 복사를 할 수 있습니다.
2. 바인딩 해제 하려는 인스턴스가 있는 컴퓨터에서 설치 프로그램을 실행 해야 합니다.
2. 설치 프로그램을 바인딩 해제 수 있는 로컬 인스턴스를 식별 합니다.
3. 인스턴스를 원래 구성으로 되돌리려고 옆의 확인란을 선택 취소 합니다.
4. 사용권 계약에 동의 합니다. 설치 하는 경우에 사용 조건 수락을 지정 해야 합니다.
5. **마침**을 클릭합니다. 프로세스 시간이 걸립니다.

#### <a name="bkmk_cmdunbind"></a> 명령줄을 사용 하 여 바인딩 해제

1. 이전 섹션에 설명된 대로 명령 프롬프트를 열고 **sqlbindr.exe**가 포함된 폴더로 이동합니다.

2. */unbind* 인수와 함께 **SqlBindR.exe** 명령을 실행하고 인스턴스를 지정합니다.

   예를 들어 다음 명령은 되돌립니다 기본 인스턴스:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>2 단계: SQL Server 인스턴스를 복구 합니다.

R 및 Python 기능 데이터베이스 엔진 인스턴스를 복구할 SQL Server 설치 프로그램을 실행 합니다. 기존의 업데이트는 유지 되지만 R 및 Python 패키지에 대 한 업데이트를 처리 하는 모든 SQL 서버, 누락 된 경우이 단계는 패치 적용 됩니다.

또는,이 더 많은 작업을 하지만 완전히 제거 하 고 데이터베이스 엔진 인스턴스를 다시 설치 하 고 모든 서비스 업데이트를 적용 한 다음 수 없습니다.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>3 단계: 모든 타사 패키지를 추가 합니다.

패키지 라이브러리에 다른 타사 또는 오픈 소스 패키지 추가 수도 있습니다. 기본 패키지 라이브러리의 위치를 스위치 바인딩 순서를 반대로, 이후 R 및 Python을 사용 하 고 라이브러리에 패키지를 다시 설치 해야 합니다. 자세한 내용은 참조 [패키지 기본](installing-and-managing-r-packages.md), [새 R 패키지 설치](install-additional-r-packages-on-sql-server.md), 및 [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)합니다.

## <a name="known-issues"></a>알려진 문제

이 섹션의 SqlBindR.exe 유틸리티 또는 업그레이드에 영향을 미치는 SQL Server 인스턴스 학습 서버 컴퓨터의 경우에 사용 하 여 관련 알려진된 문제를 나열 합니다.

### <a name="restoring-packages-that-were-previously-installed"></a>이전에 설치 된 패키지를 복원

Microsoft R Server 9.0.1로 업그레이드 한 경우 원래 패키지를 복원 하지 못했습니다 해당 버전에 대 한 SqlBindR.exe의 버전 또는 R 구성 요소 완전히 사용자 SQL Server 복구 인스턴스의 실행 되도록 모든 서비스 릴리스를 적용 하 고 다시 인스턴스입니다.

자동으로 R 구성 요소를 다시 설치 하지 않아도 원래 R 기능을 복원 되거나 다시 서버에 패치를 SqlBindR의 이후 버전입니다. 그러나 초기 설치 후 추가 된 R 패키지 업데이트를 설치 해야 합니다.

이 작업은 훨씬 더 쉽게 패키지 관리 역할 설치 및 패키지 공유를 사용한 경우: R 명령을 사용 하 여 데이터베이스의 레코드를 사용 하 여 파일 시스템에 설치 된 패키지를 동기화 하 하며 그 반대 과정도 수행 합니다. 자세한 내용은 참조 [SQL Server에 대 한 R 패키지 관리](r-package-management-for-sql-server-r-services.md)합니다.

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>SQL Server에서 여러 업그레이드 문제

Microsoft R Server 9.1.0에 대 한 새 설치 관리자를 실행 하면 SQL Server 2016 R Services의 인스턴스를 9.0.1, 업그레이드 이전에 한 경우 모든 유효한 인스턴스 목록을 표시 하 고 기본적으로 이전에 바인딩된 인스턴스를 선택 합니다. 계속 하면 이전에 바인딩된 인스턴스 바인딩 해제 됩니다. 결과적으로 이전 9.0.1 설치한이 제거, 관련 된 패키지를 비롯 하 여 되지만 새 버전의 Microsoft R Server (9.1.0) 설치 되지 않습니다.

이 문제를 해결 기존 R 서버 설치를 다음과 같이 수정할 수 있습니다.
1. 제어판을 열고 **프로그램 추가 / 제거**합니다.
2. Microsoft R Server를 찾아서 클릭 하 여 **변경/수정**합니다.
3. 설치 관리자를 시작할 때 9.1.0 바인딩할 인스턴스를 선택 합니다.

Microsoft 컴퓨터 학습 서버 9.2.1 및 9.3이이 문제를 갖지 않습니다.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>바인딩 또는 바인딩 해제 여러 임시 폴더에 둡니다.

경우에 따라 바인딩 및 바인딩 해제 작업이 임시 폴더를 정리 하려면 실패 합니다.
다음과 같은 이름의 폴더를 찾을 경우 제거할 수 있습니다 설치가 완료 된 후: R_SERVICES_<guid>

> [!NOTE]
> 설치가 완료 될 때까지 대기 해야 합니다. 하나의 버전과 관련 된 R 라이브러리를 제거한 다음 새 R 라이브러리를 추가 하는 데 시간이 오래 걸릴 수 있습니다. 작업이 완료 되 면 임시 폴더 제거 됩니다.

## <a name="sqlbindrexe-command-syntax"></a>SqlBindR.exe 명령 구문

### <a name="usage"></a>사용법

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>매개 변수

|이름|Description|
|------|------|
|*list*| 현재 컴퓨터의 모든 SQL Database 인스턴스 ID 목록을 표시합니다.|
|*bind*| 지정된 SQL Database 인스턴스를 최신 버전의 R 서버로 업그레이드하고 인스턴스가 R 서버의 향후 업그레이드를 자동으로 가져오도록 합니다.|
|*unbind*|지정된 SQL Database 인스턴스에서 최신 버전의 R 서버를 제거하고 향후 R 서버 업그레이드가 인스턴스에 영향을 주지 않도록 합니다.|

< a name = "sqlbinder 오류 코드"<a/>

### <a name="errors"></a>오류

이 도구는 다음과 같은 오류 메시지를 반환합니다.

|오류 코드  | 메시지           | 세부 정보               |
|------------|-------------------|-----------------------|
|바인딩 오류 0 | (성공)를 확인 합니다. | 바인딩 오류 없이 전달 합니다. |
|바인딩 오류 1 | 잘못 된 인수 | 구문 오류가 있습니다. |
|바인딩 오류 2 | 잘못 된 작업 | 구문 오류가 있습니다. |
|바인딩 오류 3 | 잘못 된 인스턴스 | 인스턴스는 존재 하지만 바인딩에 적합 하지 않습니다. |
|바인딩 오류 4 | 바인딩할 수 없습니다 | |
|오류 코드 5에 바인딩 | 이미 바인딩 | *bind* 명령을 실행했지만 지정한 인스턴스가 이미 바인딩되어 있습니다. |
|바인딩 오류 6 | 바인드 실패 | 인스턴스를 바인딩 해제 하는 동안 오류가 발생 했습니다. |
|바인딩 오류 7 | 바인딩되지 않습니다 | 데이터베이스 엔진 인스턴스에 R 서비스 또는 SQL Server 컴퓨터 학습 서비스에 있습니다. 인스턴스는 Microsoft 컴퓨터 학습 서버에 바인딩되지 않습니다. |
|바인딩 오류 8 | 바인딩을 해제 하지 못했습니다. | 인스턴스를 바인딩 해제 하는 동안 오류가 발생 했습니다. |
|바인딩 오류 9 | 인스턴스를 찾을 수 없습니다. | 이 컴퓨터에 인스턴스를 찾지 못했습니다. |


## <a name="see-also"></a>참고 항목

+ [학습 서버에 대 한 Windows 컴퓨터 (인터넷에 연결 된)를 설치 합니다.](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [시스템 학습 Windows 용 서버 설치 (오프 라인)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [서버를 학습 하는 컴퓨터의 알려진된 문제](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [R Server의 이전 릴리스에서 기능 공지 사항](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [사용 되지 않는, 지원 되지 않는 추가 되거나 변경 된 기능](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
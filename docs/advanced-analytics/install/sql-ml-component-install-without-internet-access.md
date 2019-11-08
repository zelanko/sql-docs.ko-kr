---
title: 인터넷에 액세스하지 않고 R 언어 및 Python 구성 요소 설치
description: 네트워크 방화벽 뒤의 격리된 SQL Server 인스턴스에서 기계 학습 R 및 Python을 오프라인 또는 연결 해제 상태에서 설치.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bd1db578d6f1b4900f559c51521d807d7e1ec271
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594358"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>인터넷 액세스가 없는 컴퓨터에 SQL Server 기계 학습 R 및 Python 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

기본적으로 설치 관리자는 Microsoft 다운로드 사이트에 연결하여 SQL Server에 기계 학습을 위한 필수 구성 요소 및 업데이트된 구성 요소를 가져옵니다. 방화벽 제약 조건으로 인해 설치 관리자가 이러한 사이트에 도달하지 못하는 경우 인터넷에 연결된 장치를 사용하여 파일을 다운로드하고 오프라인 서버로 파일을 전송한 다음 설치 프로그램을 실행할 수 있습니다.

데이터베이스 내 분석은 데이터베이스 엔진 인스턴스, 그리고 SQL Server 버전에 따라 R 및 Python 통합을 위한 추가 구성 요소로 구성됩니다. 

+ SQL Server 2019: R, Python 및 Java를 포함
+ SQL Server 2017: R 및 Python을 포함
+ SQL Server 2016: R 전용

격리된 서버에서 기계 학습 및 R/Python 언어 관련 기능은 CAB 파일을 통해 추가됩니다. 

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
## <a name="sql-server-2019-offline-install"></a>SQL Server 2019 오프라인 설치

격리된 서버에 SQL Server Machine Learning Services(R 및 Python)를 설치하려면 먼저 SQL Server 초기 릴리스와 R 및 Python 지원을 위한 해당 CAB 파일을 다운로드합니다. 최신 누적 업데이트를 사용하도록 서버를 즉시 업데이트할 계획인 경우에도 초기 릴리스를 먼저 설치해야 합니다.

> [!Note]
> SQL Server 2019에는 서비스 팩이 없습니다. 초기 릴리스가 누적 업데이트를 통해 서비스를 제공하는 유일한 기준선입니다.

### <a name="1---download-2019-cabs"></a>1 - 2019 CAB 다운로드

인터넷에 연결된 컴퓨터에서 초기 릴리스에 대한 R 및 Python 기능을 제공하는 CAB 파일을 다운로드하고 SQL Server 2019용 설치 미디어를 다운로드합니다.

릴리스  |다운로드 링크  |
---------|---------------|
Microsoft R Open        | [SRO_3.5.2.125_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085686) |
Microsoft R Server      | [SRS_9.4.7.25_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085792) |
Microsoft Python Open   | [SPO_4.5.12.120_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085793) |
Microsoft Python Server | [SPS_9.4.7.25_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085685) |

> [!NOTE]
> Java 기능은 SQL Server 설치 미디어에 포함되어 있으며 별도의 CAB 파일이 필요하지 않습니다.

###  <a name="2---get-sql-server-2019-installation-media"></a>2 - SQL Server 2019 설치 미디어 가져오기

1. 인터넷에 연결된 컴퓨터에서 [SQL Server 2019 설치 프로그램](https://www.microsoft.com/sql-server/sql-server-downloads)을 다운로드합니다. 

2. 설치를 두 번 클릭하고 **미디어 다운로드** 설치 유형을 선택합니다. 이 옵션에서 설치 프로그램은 설치 미디어를 포함하는 로컬 .iso(또는 .cab) 파일을 만듭니다.

   ![미디어 다운로드 설치 유형 선택](media/2019offline-download-tile.png "미디어 다운로드")

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
## <a name="sql-server-2017-offline-install"></a>SQL Server 2017 오프라인 설치

격리된 서버에 SQL Server Machine Learning Services(R 및 Python)를 설치하려면 먼저 SQL Server 초기 릴리스와 R 및 Python 지원을 위한 해당 CAB 파일을 다운로드합니다. 최신 누적 업데이트를 사용하도록 서버를 즉시 업데이트할 계획인 경우에도 초기 릴리스를 먼저 설치해야 합니다.

> [!Note]
> SQL Server 2017에는 서비스 팩이 없습니다. 누적 업데이트를 통해서만 서비스를 제공하는 유일한 기준선으로 초기 릴리스를 사용하는 첫 번째 SQL Server 릴리스입니다. 

### <a name="1---download-2017-cabs"></a>1 - 2017 CAB 다운로드

인터넷에 연결된 컴퓨터에서 초기 릴리스에 대한 R 및 Python 기능을 제공하는 CAB 파일을 다운로드하고 SQL Server 2017용 설치 미디어를 다운로드합니다. 

릴리스  |다운로드 링크  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2 - SQL Server 2017 설치 미디어 가져오기

1. 인터넷에 연결된 컴퓨터에서 [SQL Server 2017 설치 프로그램](https://www.microsoft.com/sql-server/sql-server-downloads)을 다운로드합니다. 

2. 설치를 두 번 클릭하고 **미디어 다운로드** 설치 유형을 선택합니다. 이 옵션에서 설치 프로그램은 설치 미디어를 포함하는 로컬 .iso(또는 .cab) 파일을 만듭니다.

   ![미디어 다운로드 설치 유형 선택](media/offline-download-tile.png "미디어 다운로드")

::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="sql-server-2016-offline-install"></a>SQL Server 2016 오프라인 설치

SQL Server 2016 데이터베이스 내 분석은 R 전용으로, 각각 제품 패키지용 CAB 파일 2개와 Microsoft의 오픈 소스 R 배포를 포함합니다. 다음 릴리스 중 하나를 설치하여 시작합니다. RTM, SP 1, SP 2. 기본 설치가 완료되면 다음 단계로 누적 업데이트를 적용할 수 있습니다.

인터넷에 연결된 컴퓨터에서 설치 프로그램이 SQL Server 2016에 데이터베이스 내 분석을 설치하는 데 사용하는 CAB 파일을 다운로드합니다. 

### <a name="1---download-2016-cabs"></a>1 - 2016 CAB 다운로드

릴리스  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317) |

### <a name="2---get-sql-server-2016-installation-media"></a>2 - SQL Server 2016 설치 미디어 가져오기

대상 컴퓨터에 첫 번째 설치로 SQL Server 2016 RTM, SP 1 또는 SP 2를 설치할 수 있습니다. 이들 버전은 모두 누적 업데이트를 수락할 수 있습니다.

설치 미디어를 포함하는 .iso 파일을 가져오는 한 가지 방법은 [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/)를 통하는 것입니다. 로그인한 다음 **다운로드** 링크를 사용하여 설치하려는 SQL Server 2016 릴리스를 찾습니다. 다운로드는 .iso 파일 형식이며, 오프라인 설치를 위해 대상 컴퓨터에 복사할 수 있습니다.

::: moniker-end

## <a name="transfer-files"></a>파일 전송

SQL Server 설치 미디어(.iso 또는 .cab) 및 데이터베이스 내 분석 CAB 파일을 대상 컴퓨터에 복사합니다. CAB 파일 및 설치 미디어 파일을 대상 컴퓨터의 같은 폴더(예: 설치 사용자의 %TEMP% 폴더)에 저장합니다.

%TEMP% 폴더는 Python CAB 파일에 필요합니다. R의 경우 %TEMP%를 사용하거나 `myrcachedirectory` 매개 변수를 CAB 경로에 설정할 수 있습니다.

## <a name="run-setup"></a>설치 프로그램 실행

인터넷에서 연결되지 않은 컴퓨터에서 SQL Server 설치 프로그램을 실행하면 이전 단계에서 복사한 CAB 파일의 위치를 지정할 수 있도록 **오프라인 설치** 페이지가 마법사에 추가됩니다.

1. 설치를 시작하려면 .iso 또는 .cab 파일을 두 번 클릭하여 설치 미디어에 액세스합니다. **setup.exe** 파일이 보일 것입니다.

2. **setup.exe**를 마우스 오른쪽 단추로 클릭하고 관리자 권한으로 실행합니다.

3. 설치 마법사가 오픈 소스 R 또는 Python 구성 요소에 대한 라이선스 페이지를 표시하면 **수락**을 클릭합니다. 사용 조건에 동의하면 다음 단계를 진행할 수 있습니다.

4. **오프라인 설치** 페이지가 표시되면 **설치 경로**에서 이전에 복사한 CAB 파일이 포함된 폴더를 지정합니다.

5. 계속해서 화면의 지시에 따라 설치를 완료합니다.

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>누적 업데이트 적용

데이터베이스 엔진과 기계 학습 구성 요소 모두에 최신 누적 업데이트를 적용하는 것이 좋습니다. 누적 업데이트는 설치 프로그램을 통해 설치됩니다. 

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
1. 기준선 인스턴스를 사용하여 시작합니다. SQL Server 초기 릴리스의 기존 설치에만 누적 업데이트를 적용할 수 있습니다.

2. 인터넷에 연결된 장치에서 SQL Server 버전에 대한 누적 업데이트 목록으로 이동합니다.

   + SQL Server 2019 업데이트 *(2019용 업데이트는 아직 없음)*
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
1. 기준선 인스턴스를 사용하여 시작합니다. SQL Server 초기 릴리스의 기존 설치에만 누적 업데이트를 적용할 수 있습니다.

2. 인터넷에 연결된 장치에서 SQL Server 버전에 대한 누적 업데이트 목록으로 이동합니다.

   + [SQL Server 2017 업데이트](https://sqlserverupdates.com/sql-server-2017-updates/)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. 기준선 인스턴스를 사용하여 시작합니다. SQL Server 2016 초기 릴리스, SQL Server 2016 SP 1 또는 SQL Server 2016 SP 2의 기존 설치에만 누적 업데이트를 적용할 수 있습니다.

2. 인터넷에 연결된 장치에서 SQL Server 버전에 대한 누적 업데이트 목록으로 이동합니다.

   + [SQL Server 2016 업데이트](https://sqlserverupdates.com/sql-server-2016-updates/)
::: moniker-end

3. 최신 누적 업데이트를 선택하여 실행 파일을 다운로드합니다.

4. R 및 Python에 해당하는 CAB 파일을 가져옵니다. 다운로드 링크는 [SQL Server 데이터베이스 내 분석 인스턴스에 대한 누적 업데이트용 CAB 다운로드](sql-ml-cab-downloads.md)를 참조하세요.

5. 모든 파일, 실행 파일 및 CAB 파일을 오프라인 컴퓨터의 동일한 폴더로 전송합니다.

6. 설치 프로그램을 실행합니다. 사용 조건에 동의하고 기능 선택 페이지에서 누적 업데이트가 적용되는 기능을 검토합니다. 기계 학습 기능을 포함하여 현재 인스턴스에 설치된 모든 기능이 표시되어야 합니다.

   ![기능 트리에서 기능 선택](media/cumulative-update-feature-selection.png "기능 목록")

5. R 및 Python 배포에 대한 사용 조건에 동의하여 마법사를 계속 진행합니다. 설치하는 동안 업데이트된 CAB 파일이 들어 있는 폴더 위치를 선택하라는 메시지가 표시됩니다.

## <a name="set-environment-variables"></a>환경 변수 설정

R 기능 통합의 경우에만 **MKL_CBWR** 환경 변수를 설정하여 Intel MKL(Math Kernel Library) 계산에서 [일관성 있는 출력을 보장](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)해야 합니다.

1. 제어판에서 **시스템 및 보안** > **시스템** > **고급 시스템 설정** > **환경 변수**를 클릭합니다.

2. 새 사용자 또는 시스템 변수를 만듭니다. 

   + 변수 이름을 `MKL_CBWR`로 설정합니다.
   + 변수 값을 `AUTO`로 설정합니다.

이 단계를 수행하려면 서버를 다시 시작해야 합니다. 스크립트 실행을 사용하도록 설정하려는 경우 모든 구성 작업이 완료될 때까지 다시 시작을 보류할 수 있습니다.

## <a name="post-install-configuration"></a>설치 후 구성

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
설치가 완료되면 서비스를 다시 시작하고 스크립트 실행을 사용하도록 서버를 구성합니다.

+ [외부 스크립트 실행을 사용하도록 설정](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)

SQL Server Machine Learning Services의 초기 오프라인 설치에는 다음과 같은 온라인 설치와 동일한 구성이 필요합니다.

+ [설치 확인](sql-machine-learning-services-windows-install.md#verify-installation)
+ [필요에 따른 추가 구성](sql-machine-learning-services-windows-install.md#additional-configuration)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
설치가 완료되면 서비스를 다시 시작하고 스크립트 실행을 사용하도록 서버를 구성합니다.

+ [외부 스크립트 실행을 사용하도록 설정](sql-r-services-windows-install.md#bkmk_enableFeature)

SQL Server R Services의 초기 오프라인 설치에는 다음과 같은 온라인 설치와 동일한 구성이 필요합니다.

+ [설치 확인](sql-r-services-windows-install.md#verify-installation)
+ [필요에 따른 추가 구성](sql-r-services-windows-install.md#bkmk_FollowUp)
::: moniker-end

## <a name="next-steps"></a>다음 단계

인스턴스의 설치 상태를 확인하고 일반적인 문제를 해결하려면 [SQL Server용 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md)를 참조하세요.

익숙하지 않은 메시지 또는 로그 항목에 대한 도움말은 [업그레이드 및 설치 FAQ - Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md)를 참조하세요.

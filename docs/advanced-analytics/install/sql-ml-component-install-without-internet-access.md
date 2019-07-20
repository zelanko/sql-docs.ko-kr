---
title: 인터넷에 액세스 하지 않고 R 언어 및 Python 구성 요소 설치
description: 네트워크 방화벽 뒤에 격리 된 SQL Server 인스턴스에서 R 및 Python 설치 Machine Learning 오프 라인 또는 연결 해제 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1c68ce075c34c6475828e81a66121e21afcf2482
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345015"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>인터넷에 액세스 하지 않고 컴퓨터에 machine learning R 및 Python SQL Server 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

기본적으로 설치 관리자는 Microsoft 다운로드 사이트에 연결 하 여 SQL Server에서 기계 학습을 위한 필수 구성 요소 및 업데이트 된 구성 요소를 가져옵니다. 방화벽 제약 조건으로 인해 설치 관리자가 이러한 사이트에 도달 하지 못하는 경우 인터넷에 연결 된 장치를 사용 하 여 파일을 다운로드 하 고 오프 라인 서버로 파일을 전송 한 다음 설치 프로그램을 실행할 수 있습니다.

데이터베이스 내 분석은 SQL Server 버전에 따라 데이터베이스 엔진 인스턴스와 R 및 Python 통합을 위한 추가 구성 요소로 구성 됩니다. 

+ SQL Server 2017에 R 및 Python 포함 
+ SQL Server 2016은 R 전용입니다.

Isolated 서버에서 기계 학습 및 R/Python 언어 관련 기능은 CAB 파일을 통해 추가 됩니다. 

## <a name="sql-server-2017-offline-install"></a>SQL Server 2017 오프 라인 설치

격리 된 서버에 SQL Server 2017 Machine Learning Services (R 및 Python)를 설치 하려면 먼저 SQL Server 초기 릴리스와 R 및 Python 지원에 해당 하는 CAB 파일을 다운로드 합니다. 최신 누적 업데이트를 사용 하도록 서버를 즉시 업데이트할 계획인 경우에도 초기 릴리스를 먼저 설치 해야 합니다.

> [!Note]
> SQL Server 2017에는 서비스 팩이 없습니다. 누적 업데이트를 통해서만 서비스를 제공 하는 유일한 기본 줄로 초기 릴리스를 사용 하는 SQL Server의 첫 번째 릴리스입니다. 

### <a name="1---download-2017-cabs"></a>1-2017 Cab 다운로드

인터넷에 연결 된 컴퓨터에서 초기 릴리스에 대 한 R 및 Python 기능을 제공 하는 CAB 파일을 다운로드 하 SQL Server 2017에 대 한 설치 미디어를 다운로드 합니다. 

릴리스  |다운로드 링크  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2-SQL Server 2017 설치 미디어 가져오기

1. 인터넷에 연결 된 컴퓨터에서 [SQL Server 2017 설치 프로그램](https://www.microsoft.com/sql-server/sql-server-downloads)을 다운로드 합니다. 

2. 설치를 두 번 클릭 하 고 **다운로드 미디어** 설치 유형을 선택 합니다. 설치 프로그램은이 옵션을 사용 하 여 설치 미디어를 포함 하는 로컬 .iso (또는 .cab) 파일을 만듭니다.

   ![다운로드 미디어 설치 유형 선택](media/offline-download-tile.png "미디어 다운로드")

## <a name="sql-server-2016-offline-install"></a>SQL Server 2016 오프 라인 설치

SQL Server 2016 데이터베이스 내 분석은 각각 제품 패키지에 대 한 두 개의 CAB 파일 및 Microsoft의 오픈 소스 R 배포를 포함 하는 R 전용입니다. 다음 릴리스 중 하나를 설치 하 여 시작 합니다. RTM, SP 1, SP 2. 기본 설치가 준비 되 면 다음 단계로 누적 업데이트를 적용할 수 있습니다.

인터넷에 연결 된 컴퓨터에서 설치 프로그램에서 SQL Server 2016에 데이터베이스 내 분석을 설치 하는 데 사용 하는 CAB 파일을 다운로드 합니다. 

### <a name="1---download-2016-cabs"></a>1-2016 Cab 다운로드

릴리스  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317) |

### <a name="2---get-sql-server-2016-installation-media"></a>2-SQL Server 2016 설치 미디어 가져오기

대상 컴퓨터에 첫 번째 설치로 SQL Server 2016 RTM, SP 1 또는 SP 2를 설치할 수 있습니다. 이러한 버전은 누적 업데이트를 수락할 수 있습니다.

설치 미디어를 포함 하는 .iso 파일을 가져오는 한 가지 방법은 [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/)을 통하는 것입니다. 로그인 하 고 **다운로드** 링크를 사용 하 여 설치 하려는 SQL Server 2016 릴리스를 찾습니다. 다운로드는 .iso 파일 형식으로, 오프 라인 설치를 위해 대상 컴퓨터에 복사할 수 있습니다.

## <a name="transfer-files"></a>파일 전송

SQL Server 설치 미디어 (.iso 또는 .cab) 및 데이터베이스 내 분석 CAB 파일을 대상 컴퓨터에 복사 합니다. CAB 파일 및 설치 미디어 파일을 대상 컴퓨터의 같은 폴더 (예: 설치 사용자의% TEMP * 폴더)에 넣습니다.

% TEMP% 폴더는 Python CAB 파일에 필요 합니다. R의 경우% TEMP%를 사용 하거나 myrcachedirectory 매개 변수를 CAB 경로로 설정할 수 있습니다.

다음 스크린샷은 SQL Server 2017 CAB 및 ISO 파일을 보여 줍니다. SQL Server 2016 다운로드는 서로 다르게 보입니다. 파일 수 (Python 없음)와 설치 미디어 파일 이름은 2016입니다.

![전송할 파일 목록](media/offline-file-list.png "파일 목록")

## <a name="run-setup"></a>설치 프로그램 실행

인터넷에서 연결 되지 않은 컴퓨터에서 설치 프로그램 SQL Server를 실행 하면 이전 단계에서 복사한 CAB 파일의 위치를 지정할 수 있도록 **오프 라인 설치** 페이지가 마법사에 추가 됩니다.

1. 설치를 시작 하려면 .iso 또는 .cab 파일을 두 번 클릭 하 여 설치 미디어에 액세스 합니다. **Setup.exe** 파일이 표시 됩니다.

2. Setup.exe를 마우스 오른쪽 단추로 **클릭 하 고** 관리자 권한으로 실행 합니다.

3. 설치 마법사가 오픈 소스 R 또는 Python 구성 요소에 대 한 라이선스 페이지를 표시 하면 **동의 함**을 클릭 합니다. 사용 조건에 동의 하면 다음 단계를 진행할 수 있습니다.

4. **오프 라인 설치** 페이지로 이동 하면 **설치 경로**에서 이전에 복사한 CAB 파일이 포함 된 폴더를 지정 합니다.

   ![Cab 폴더 선택에 대 한 마법사 페이지](media/screenshot-sql-offline-cab-page.png "CAB 폴더")

5. 화면의 지시에 따라 설치를 완료 합니다.

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>누적 업데이트 적용

데이터베이스 엔진과 machine learning 구성 요소 모두에 최신 누적 업데이트를 적용 하는 것이 좋습니다. 누적 업데이트는 설치 프로그램을 통해 설치 됩니다. 

1. 기준 인스턴스를 사용 하 여 시작 합니다. SQL Server의 기존 설치에만 누적 업데이트를 적용할 수 있습니다.

  + SQL Server 2017 초기 릴리스
  + SQL Server 2016 초기 릴리스, SQL Server 2016 SP 1 또는 SQL Server 2016 SP 2

2. 인터넷에 연결 된 장치에서 SQL Server 버전에 대 한 누적 업데이트 목록으로 이동 합니다.

  + [SQL Server 2017 업데이트](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [SQL Server 2016 업데이트](https://sqlserverupdates.com/sql-server-2016-updates/)

3. 최신 누적 업데이트를 선택 하 여 실행 파일을 다운로드 합니다.

4. R 및 Python에 해당 하는 CAB 파일을 가져옵니다. 다운로드 링크는 [SQL Server 데이터베이스 내 분석 인스턴스의 누적 업데이트에 대 한 CAB 다운로드](sql-ml-cab-downloads.md)를 참조 하세요.

5. 모든 파일, 실행 파일 및 CAB 파일을 오프 라인 컴퓨터의 동일한 폴더로 전송 합니다.

6. 설치 프로그램을 실행합니다. 사용 조건에 동의 하 고 기능 선택 페이지에서 누적 업데이트가 적용 되는 기능을 검토 합니다. 기계 학습 기능을 포함 하 여 현재 인스턴스에 대해 설치 된 모든 기능이 표시 되어야 합니다.

  ![기능 트리에서 기능 선택](media/cumulative-update-feature-selection.png "기능 목록")

5. R 및 Python 배포에 대 한 사용 조건에 동의 하 여 마법사를 계속 진행 합니다. 설치 하는 동안 업데이트 된 CAB 파일이 들어 있는 폴더 위치를 선택 하 라는 메시지가 표시 됩니다.

## <a name="set-environment-variables"></a>환경 변수 설정

R 기능 통합의 경우에는 **MKL_CBWR** 환경 변수를 설정 하 여 Intel Mkl (Math Kernel Library) 계산과 일관 되 게 [출력 되도록](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) 해야 합니다.

1. 제어판에서 **시스템 및 보안** > **시스템** > **고급 시스템 설정** > **환경 변수**를 클릭 합니다.

2. 새 사용자 또는 시스템 변수를 만듭니다. 

  + 변수 이름 설정`MKL_CBWR`
  + 변수 값을로 설정 합니다.`AUTO`

이 단계를 수행 하려면 서버를 다시 시작 해야 합니다. 스크립트 실행을 사용 하도록 설정 하려는 경우 모든 구성 작업이 완료 될 때까지 다시 시작에 대 한 정보를 유지할 수 있습니다.

## <a name="post-install-configuration"></a>설치 후 구성

설치가 완료 되 면 서비스를 다시 시작 하 고 스크립트 실행을 사용 하도록 서버를 구성 합니다.

+ [외부 스크립트 실행 사용 (SQL Server 2017)](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)
+ [외부 스크립트 실행 사용 (SQL Server 2016)](sql-r-services-windows-install.md#bkmk_enableFeature)

SQL Server 2017 Machine Learning Services 또는 SQL Server 2016 R 서비스 중 하나를 초기 오프 라인으로 설치 하려면 온라인 설치와 동일한 구성이 필요 합니다.

+ [설치 확인](sql-machine-learning-services-windows-install.md#verify-installation)  SQL Server 2016의 경우 [여기](sql-r-services-windows-install.md#verify-installation)를 클릭 합니다.
+ [필요에 따라 추가 구성](sql-machine-learning-services-windows-install.md#additional-configuration)  SQL Server 2016의 경우 [여기](sql-r-services-windows-install.md#bkmk_FollowUp)를 클릭 합니다.

## <a name="next-steps"></a>다음 단계

인스턴스의 설치 상태를 확인 하 고 일반적인 문제를 해결 하려면 [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md)를 참조 하세요.

익숙하지 않은 메시지나 로그 항목에 대 한 도움말은 [업그레이드 및 설치 FAQ-Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md)를 참조 하세요.


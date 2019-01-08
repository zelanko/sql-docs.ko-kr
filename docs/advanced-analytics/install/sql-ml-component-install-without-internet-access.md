---
title: R 언어와 SQL Server Machine Learning-인터넷 액세스 없이 Python 구성 요소를 설치 합니다.
description: 오프 라인 상태 이거나 연결이 끊긴 Machine Learning R 및 Python 설치 격리 된 SQL Server 인스턴스에서 네트워크 방화벽으로 보호 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 01f871b6f6a96c053daca13060cac1223415eb20
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596994"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>SQL Server 기계 학습의 R 및 Python 인터넷 액세스 없이 컴퓨터를 설치 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

기본적으로 설치 관리자 필수 가져오려면 Microsoft 다운로드 사이트에 연결 하 고 업데이트 된 구성 요소에 대 한 기계 학습에서 SQL Server입니다. 방화벽 제약 조건을 설치 관리자에서 이러한 사이트에 연결을 방지 하는 경우, 파일을 다운로드 하 고, 오프 라인 서버에 파일을 전송 하 고, 그런 다음 설치 프로그램을 실행 하는 인터넷에 연결 된 장치를 사용할 수 있습니다.

데이터베이스 내 분석 데이터베이스 엔진 인스턴스 및 SQL Server의 버전에 따라 R 및 Python 통합에 대 한 추가 구성 요소 구성 됩니다. 

+ SQL Server 2017에는 R 및 Python 포함 됩니다. 
+ SQL Server 2016은 R 전용입니다. 

격리 된 서버에서 기계 학습 및 R/Python 언어별 기능 CAB 파일을 통해 추가 됩니다. 

## <a name="sql-server-2017-offline-install"></a>SQL Server 2017 오프 라인 설치

격리 된 서버에서 SQL Server 2017 Machine Learning Services (R 및 Python)를 설치 하려면 SQL Server의 초기 릴리스를 다운로드 하 여 시작 하 고 R 및 Python에 대 한 해당 CAB 파일을 지원 합니다. 즉시 최신 누적 업데이트를 사용 하도록 서버를 업데이트 하려는 경우에 초기 릴리스를 먼저 설치 해야 합니다.

> [!Note]
> SQL Server 2017 서비스 팩이 없습니다. 이 초기 릴리스만 누적 업데이트를 통해 서비스와 기준선으로 사용 하도록 SQL Server의 첫 번째 릴리스입니다. 

### <a name="1---download-2017-cabs"></a>1-2017 Cab을 다운로드 합니다.

인터넷 연결 컴퓨터에서 SQL Server 2017에 대 한 초기 릴리스 및 설치 미디어에 대 한 R 및 Python 기능을 제공 CAB 파일을 다운로드 합니다. 

릴리스  |다운로드 링크  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python 열기     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python 서버    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2-SQL Server 2017 설치 미디어 가져오기

1. 인터넷 연결 컴퓨터에 다운로드 합니다 [SQL Server 2017 설치 프로그램](https://www.microsoft.com/sql-server/sql-server-downloads)합니다. 

2. 설치 프로그램을 두 번 클릭 하 고 선택 합니다 **미디어 다운로드** 설치 유형입니다. 이 옵션을 사용 하 여 설치는 설치 미디어에 포함 된 로컬.iso (또는.cab) 파일을 만듭니다.

   ![다운로드 미디어 설치 유형 선택](media/offline-download-tile.png "미디어 다운로드")

## <a name="sql-server-2016-offline-install"></a>SQL Server 2016 오프 라인 설치

SQL Server 2016 데이터베이스 내 분석은 두 가지를 사용 하 여 R 전용 CAB 파일에 대 한 제품 패키지 및 Microsoft의 오픈 소스 R 배포 각각. 이러한 버전 중 하나를 설치 하 여 시작 합니다. RTM에서 SP 1, SP 2입니다. 기본 설치 위치에 있으면 다음 단계로 누적 업데이트를 적용할 수 있습니다.

인터넷 연결 컴퓨터에서 SQL Server 2016에서 데이터베이스 내 분석을 설치 하려면 설치 프로그램에서 사용 되는 CAB 파일을 다운로드 합니다. 

### <a name="1---download-2016-cabs"></a>1-2016 Cab을 다운로드 합니다.

릴리스  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038) |

### <a name="2---get-sql-server-2016-installation-media"></a>2-SQL Server 2016 설치 미디어 가져오기

대상 컴퓨터의 첫 번째 설치와 SQL Server 2016 RTM, SP 1 또는 SP 2를 설치할 수 있습니다. 이러한 버전 중 하나는 누적 업데이트를 사용할 수 있습니다.

.Iso 파일을 가져올 수 설치 미디어를 포함 하는 것 [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/)합니다. 로그인 한 다음 사용 하 여 합니다 **다운로드** 링크를 설치 하려면 SQL Server 2016 릴리스를 찾을 수 있습니다. 오프 라인 설치에 대 한 대상 컴퓨터에 복사할 수 있는.iso 파일의 형태로 시작 됩니다.

## <a name="transfer-files"></a>파일 전송

대상 컴퓨터에 SQL Server 설치 미디어 (.iso 또는.cab) 및 데이터베이스 내 분석 CAB 파일을 복사 합니다. 대상 컴퓨터의 동일한 폴더에 CAB 파일 및 미디어 파일 설치와 같은 배치 **다운로드** 또는 설치 사용자의 %temp * 폴더입니다.

다음 스크린샷은 SQL Server 2017 CAB 및 ISO 파일을 보여 줍니다. SQL Server 2016 다운로드 다르게: 2016에 대 한 설치 미디어 및 파일 수를 줄입니다 (Python 없음)에 해당 하는 파일의 이름은입니다.

![전송할 파일 목록이](media/offline-file-list.png "파일 목록")

## <a name="run-setup"></a>설치 프로그램 실행

인터넷에서 연결이 끊어진 컴퓨터에 SQL Server 설치 프로그램을 실행 하면 설치 프로그램에서 추가 **오프 라인 설치** 마법사 페이지를 이전 단계에서 복사한 CAB 파일의 위치를 지정할 수 있습니다.

1. 설치를 시작 하려면 설치 미디어에 액세스 하려면.iso 또는.cab 파일을 두 번 클릭 합니다. 표시 되어야 합니다 **setup.exe** 파일입니다.

2. 마우스 오른쪽 단추로 클릭 **setup.exe** 하 고 관리자 권한으로 실행 합니다.

3. 설치 마법사에서 오픈 소스 R 또는 Python 구성 요소에 대 한 라이선스 페이지가 표시를 클릭 **Accept**합니다. 라이선스 약관에 동의 사용 하면 다음 단계를 진행할 수 있습니다.

4. 에 **오프 라인 설치** 페이지에서 **설치 경로**, 앞에서 복사한 CAB 파일이 포함 된 폴더를 지정 합니다.

   ![Cab 폴더 선택 마법사 페이지](media/screenshot-sql-offline-cab-page.png "CAB 폴더")

5. 계속 다음의 설치를 완료 하려면 화면의 지시 합니다.

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>누적 업데이트를 적용 합니다.

데이터베이스 엔진 및 기계 학습 구성 요소 모두에 최신 누적 업데이트를 적용 하는 것이 좋습니다. 누적 업데이트는 설치 프로그램을 통해 설치 됩니다. 

1. 기본 인스턴스를 시작 합니다. SQL Server의 기존 설치에만 누적 업데이트를 적용할 수 있습니다.

  + SQL Server 2017 초기 릴리스
  + SQL Server 2016의 초기 릴리스, SQL Server 2016 SP 1 또는 SQL Server 2016 sp2

2. 인터넷 연결된 장치에서의 SQL Server 버전에 대 한 누적 업데이트 목록으로 이동 합니다.

  + [SQL Server 2017 업데이트](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [SQL Server 2016 업데이트](https://sqlserverupdates.com/sql-server-2016-updates/)

3. 실행 파일을 다운로드 하려면 최신 누적 업데이트를 선택 합니다.

4. R 및 Python에 대 한 해당 CAB 파일을 가져옵니다. 다운로드 링크를 참조 하세요 [CAB 인스턴스를 SQL Server 데이터베이스 내 분석에 누적 업데이트에 대 한 다운로드](sql-ml-cab-downloads.md)합니다.

5. 모든 파일, 실행 파일 및 오프 라인 컴퓨터의 같은 폴더에 CAB 파일을 전송 합니다.

6. 설치 프로그램을 실행합니다. 라이선스 조건에 동의 하 고 기능 선택 페이지의 누적 업데이트 적용 되는 기능을 검토 합니다. Machine learning 기능을 포함 하 여 현재 인스턴스에 대해 설치 된 모든 기능에 표시 됩니다.

  ![기능 트리에서 기능 선택](media/cumulative-update-feature-selection.png "기능 목록")

5. R 및 Python 배포에 대 한 라이선스 조건에 동의 하 여 마법사를 진행 합니다. 설치 하는 동안 업데이트 된 CAB 파일이 포함 된 폴더 위치를 선택 하 라는 메시지가 표시 됩니다.

## <a name="set-environment-variables"></a>환경 변수 설정

R 기능 통합만로 설정 해야 합니다 **MKL_CBWR** 환경 변수를 [일관 된 출력을 확인](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) Intel 라이브러리 MKL (Math Kernel) 계산에서 합니다.

1. 제어판에서 클릭 **시스템 및 보안** > **System** > **고급 시스템 설정**  >   **환경 변수**합니다.

2. 새 사용자 또는 시스템 변수를 만듭니다. 

  + 변수 이름 설정 `MKL_CBWR`
  + 변수 값 설정 `AUTO`

이 단계에서는 서버를 다시 시작을 해야 합니다. 스크립트 실행을 사용 하도록 설정 하려는 경우 있습니다 수 보류 다시 시작의 모든 구성 작업이 완료 될 때까지 합니다.

## <a name="post-install-configuration"></a>설치 후 구성

설치가 완료 되 면 서비스를 다시 시작 후 다음 스크립트 실행을 사용 하도록 설정 하려면 서버를 구성 합니다.

+ [외부 스크립트 실행 (SQL Server 2017)를 사용 하도록 설정](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)
+ [외부 스크립트 실행 (SQL Server 2016)를 사용 하도록 설정](sql-r-services-windows-install.md#bkmk_enableFeature)

SQL Server 2017의 Machine Learning Services 또는 SQL Server 2016 R Services의 오프 라인 초기 설치에는 온라인 설치와 같은 구성이 필요합니다.

+ [설치 확인](sql-machine-learning-services-windows-install.md#verify-installation) (SQL Server 2016에 대 한 클릭 [여기](sql-r-services-windows-install.md#verify-installation)).
+ [필요에 따라 추가 구성을](sql-machine-learning-services-windows-install.md#additional-configuration) (SQL Server 2016에 대 한 클릭 [여기](sql-r-services-windows-install.md#bkmk_FollowUp)).

## <a name="next-steps"></a>다음 단계

인스턴스의 설치 상태를 확인 하 고 일반적인 문제 해결, 참조 [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md)합니다.

모든 알 수 없는 메시지 또는 로그 항목을 사용 하 여 도움말을 참조 하세요 [업그레이드 및 설치 FAQ-Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md)합니다.


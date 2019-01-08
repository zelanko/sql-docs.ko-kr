---
title: 자주 묻는 질문 (FAQ)-SQL Server Machine Learning Services 업그레이드 및 설치
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/15/2018
ms.topic: conceptual
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.openlocfilehash: dd92ba0e080da0dd8ed387ae0a9f3d431232c896
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432856"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>R Server 또는 SQL Server Machine Learning에 대 한 업그레이드 및 설치 FAQ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 항목에서는 SQL Server의 기능을 학습 하는 컴퓨터의 설치에 대 한 몇 가지 일반적인 질문에 대 한 답변을 제공 합니다. 또한 업그레이드에 대 한 일반적인 질문에 대해서도 다룹니다.

+ 일부 문제는 시험판 버전에서 업그레이드에만 발생합니다. 따라서는 하면 버전 및 에디션 확인 먼저이 정보를 읽기 전에 하는 것이 좋습니다. 버전 정보를 가져오려면 실행 `@@VERSION` 에서 SQL Server Management Studio에서 쿼리 합니다.
+ 최신 릴리스 또는 최신 릴리스에서 해결 된 문제를 해결 하는 최대한 빨리 서비스 릴리스를 업그레이드 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services (In-database)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>요구 사항 및 이전 버전의 SQL Server 2016에 대 한 제한 

설치 하는 SQL Server의 빌드에 따라 일부는 다음과 같은 제한이 적용 될 수 있습니다.

- SQL Server 2016 R Services의 초기 버전에서 작업 디렉터리를 포함 하는 드라이브에서 8dot3 표기법 필요 했습니다. 시험판 버전을 설치한 경우 SQL Server 2016 서비스 팩 1로 업그레이드 합니다.이 문제를 해결 해야 합니다. 이 요구 사항은 SP1 이후 버전에 적용 되지 않습니다.

- 설치할 수 없는 현재 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 장애 조치 클러스터입니다. 그러나 SQL Server 2019 미리 보기는 테스트 환경에서이 capablity 평가 하려는 경우 장애 조치 지원을 제공 합니다. 자세한 내용은 [What's New](../what-s-new-in-sql-server-machine-learning-services.md)합니다.

- Azure VM에서 몇 가지 추가 구성이 필요할 수 있습니다. 예를 들어, 원격 액세스를 지원 하도록 방화벽 예외를 만들려면 해야 합니다.

- R의 다른 버전 또는 Revolution Analytics의 다른 릴리스를 사용 하 여 side-by-side-설치는 지원 되지 않습니다.

- 설치를 시작 하기 전에 바이러스를 사용 하지 않도록 설정 합니다. 설치가 완료 된 후 사용 하는 폴더에서 바이러스 검사 일시 중단 하는 것이 좋습니다 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]합니다. 가급적 전체에 대 한 검색 일시 중단 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 트리.

 - Windows Core에 설치 된 SQL Server 인스턴스에 Microsoft R Server를 설치 합니다. SQL Server 2016의 RTM 버전을 있었습니다 알려진된 문제를 Windows Server Core 버전 인스턴스에 Microsoft R Server를 추가 하는 경우. 이 문제가 해결되었습니다. 이 문제가 발생 하는 경우에 설명 된 수정 사항을 적용할 수 있습니다 [KB3164398](https://support.microsoft.com/kb/3164398) Windows Server Core의 기존 인스턴스에 R 기능을 추가 합니다. 자세한 내용은 [Windows Server Core 운영 체제에 Microsoft R Server 독립 실행형을 설치할 수 없음](https://support.microsoft.com/kb/3168691)을 참조하세요.


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>지역화 된 버전의 SQL Server 2016에 대 한 기계 학습 구성 요소를 오프 라인 설치

SQL Server 2016의 초기 릴리스 버전 인터넷 연결 없이 오프 라인 설치 하는 동안 로캘별.cab 파일을 설치 하지 못했습니다. 이후 릴리스에서이 문제가 수정 되어 있지만 설치 관리자를 올바른 언어로 설치할 수 없다는 메시지가 반환 하는 경우에 설치를 계속할 수 있도록 파일을 편집할 수 있습니다.

+ 올바른 언어로 설치 되어 있는지 확인 하려면 설치 관리자 파일을 수동으로 편집 합니다. 예를 들어 일본어 버전의 SQL Server를 설치 하는 변경한 파일의 이름을 srs_8.0.3.0_에서**1033**.cab에서 SRS_8.0.3.0_**1041**.cab 합니다.
+ SQL Server 설치 언어와 동일한 machine learning 구성 요소에 사용 되는 언어 식별자 여야 합니다 또는 설치를 완료할 수 없습니다.

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>시험판 버전: 정책, 업그레이드 및 알려진된 문제를 지원 합니다.

모든 시험판 버전의 새 설치 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 는 지원 되지 않습니다. 시험판 버전을 사용 하는 경우 가능한 한 빨리를 업그레이드 합니다.

이 섹션에서는 특정 업그레이드 시나리오에 대 한 자세한 지침을 포함합니다.

### <a name="how-to-upgrade-sql-server"></a>SQL Server를 업그레이드 하는 방법

설치 마법사를 다시 실행 하 여 SQL Server의 버전을 업그레이드할 수 있습니다.

+ [SQL Server 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)
+ [SQL Server 설치 마법사를 사용 하 여 업그레이드](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

방금 기계 학습 구성 요소 바인딩 이라는 프로세스를 사용 하 여 업그레이드할 수 있습니다. 
+ [SqlBindR을 사용 하 여 기계 학습 구성 요소를 업그레이드 합니다.](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>시험판 버전에서 전체 업그레이드에 대 한 지원 종료

SQL Server 2016의 시험판 버전에서 업그레이드를 더 이상 지원 되지. SQL Server 2016 CTP3, CTP3.1, CTP3.2, RC0 또는 RC1이 포함 됩니다.

다음 버전은 SQL Server 2016의 시험판 버전을 사용 하 여 설치 되었습니다.

| 버전 | 빌드         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

사용 중인 버전에 대 한 모든 확실 하지 않은 경우 실행 `@@VERSION` 에서 SQL Server Management Studio에서 쿼리 합니다.

일반적으로 업그레이드 프로세스는 다음과 같습니다.

1. 스크립트 및 데이터를 백업 합니다.
2. 시험판 버전을 제거 합니다.
3. 릴리스 버전을 설치 합니다.

SQL Server의 시험판 버전을 제거 하면 기계 학습 구성 요소 복잡할 수 있으며 특별 한 스크립트를 실행 해야 합니다. 기술 지원 서비스에 문의하십시오.

###  <a name="bkmk_Uninstall"></a> Microsoft R Server의 이전 버전에서 업그레이드 하기 전에 제거

Microsoft R Server 시험판 버전을 설치한 경우 먼저 제거해야 최신 버전으로 업그레이드할 수 있습니다.

1.  **제어판**에서 **프로그램 추가/제거**를 클릭하고 `Microsoft SQL Server 2016 <version number>`을 선택합니다.

2.  구성 요소 **추가**, **복구**또는 **제거** 옵션이 있는 대화 상자에서 **제거**를 선택합니다.
  
3.  **기능 선택** 페이지의 **공유 기능**에서 **R 서버(독립 실행형)** 를 선택합니다. **다음**을 클릭한 다음 **마침** 을 클릭하여 방금 선택한 구성 요소를 제거합니다.

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>R Services 및 R Server (독립 실행형) side-by-side-오류 

SQL Server 2016의 이전 버전에서는 경우에 따라 한 번에 R Server (독립 실행형)와 R Services (In-database) 설치 "액세스 거부" 메시지와 함께 설치가 발생 합니다. 이 문제는 SQL Server 2016 용 서비스 팩 1에서 수정 되었습니다.

이 오류가 발생 하 고 이러한 기능을 업그레이드 해야 하는 경우 SQL Server 2016 sp1 통합 설치를 수행 합니다. 두 가지 문제를 해결 하려면 제거한 둘 다 필요 합니다.

1. R Services (In-database)를 제거 하 고 SQLRUserGroup 사용자 계정을 제거 되었는지 확인 합니다.

2. 서버를 다시 시작 하 고 R Server (독립 실행형)를 다시 설치 하십시오.

3. 실행된 SQL Server 설치를 한 번 선택한이 이번 **기존 SQL Server에 기능 추가**합니다.

4. 인스턴스를 선택 하 고 다음을 선택 합니다 **R Services (In-database)** 추가 하는 옵션입니다.

이 절차를 문제를 해결 하지 못하는 경우 다음 해결 방법을 시도해 보세요.

1. 동시에 R Services (In-database) 및 R Server (독립 실행형)를 제거 합니다.

2. 로컬 사용자 계정 (SQLRUserGroup)를 제거 합니다.

3. 서버를 다시 시작합니다.

4. SQL Server 설치 프로그램을 실행 하 고만 R Services (In-database) 기능을 추가 합니다. 선택 하지 마세요 **R Server (독립 실행형)** 합니다.

일반적으로 좋습니다 R Services (In-database)와 R Server (독립 실행형) 설치 하지 않으면 같은 컴퓨터에서. 그러나 서버에 충분 한 용량이 가정 하 고, R Server 독립 실행형 개발 도구로 유용 확인할 수 있습니다. 다른 가능한 시나리오의 R Server 조작 화 기능을 사용 하지만 데이터 이동 없이 SQL Server 데이터에 액세스 하려고 할 것입니다.

## <a name="incompatible-version-of-r-client-and-r-server"></a>호환되지 않는 버전의 R 클라이언트 및 R 서버

Microsoft R Client를 설치 하 고 원격 SQL Server 계산 컨텍스트에서 R을 실행 하는 경우 다음과 같은 오류가 표시 될 수 있습니다.

*Microsoft R Server 버전 8.0.3과 호환 되지 않는 컴퓨터에 Microsoft R client 버전 9.0.0을 중인 합니다. 호환되는 버전을 다운로드하여 설치하세요.*

SQL Server 2016에서 필수 된 SQL Server R Services에서 실행 중인 R 버전을 동일 하 게 정확 하 게 Microsoft R Client의 라이브러리로 합니다. 이후 버전에서 요구 사항을 제거 되었습니다. 그러나 항상 구성 요소를 학습 하는 컴퓨터의 최신 버전을 다운로드 하는 모든 서비스 팩이 설치는 것이 좋습니다. 

이전 버전의 Microsoft R Server를 Microsoft R Client 9.0.0와의 호환성을 확인 해야 하는 경우이 설명 하는 업데이트를 설치 [지원 문서](https://support.microsoft.com/kb/3210262)합니다.


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>"한 번에 하나의 Revolution Enterprise 제품만 설치할 수 있습니다." 오류가 발생하고 설치에 실패함

Revolution Analytics 제품의 이전 설치 또는 SQL Server R Services 시험판 버전이 있는 경우 이 오류가 발생할 수 있습니다. 먼저 이전 버전을 제거해야 최신 버전의 Microsoft R Server를 설치할 수 있습니다. 다른 버전의 Revolution Enterprise 도구와 함께 설치하는 것은 지원되지 않습니다.

그러나 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 또는 SQL Server 2016과 함께 R 서버 독립 실행형을 사용하는 경우에는 나란히 설치할 수 있습니다.

## <a name="registry-cleanup-to-uninstall-older-components"></a>이전 구성 요소를 제거 하는 레지스트리 정리

이전 버전을 제거하는 데 문제가 있는 경우 레지스트리를 편집하여 관련 키를 제거해야 할 수도 있습니다.

> [!IMPORTANT]
> 이 문제는 Microsoft R Server 시험판 버전 또는 SQL Server 2016 R Services CTP 버전을 설치한 경우에만 적용됩니다.
  
1. Windows 레지스트리를 열고 `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`키를 찾습니다.
2. 다음 항목이 있고 키에 `sEstimatedSize2`값만 포함된 경우에는 모두 삭제합니다.
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (8.0.2의 경우)
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (8.0.1의 경우)
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (8.0.0의 경우)
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (7.5.0의 경우)

## <a name="see-also"></a>참고자료

 [SQL Server Machine Learning Services (In-database)](../r/sql-server-r-services.md)

 [SQL Server Machine Learning Server (독립 실행형)](../r/r-server-standalone.md)

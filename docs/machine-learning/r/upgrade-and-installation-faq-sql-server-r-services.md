---
title: 업그레이드 및 설치 FAQ
description: SQL Server의 기계 학습 기능 설치에 대한 일반적인 질문에 대한 답변입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
ms.author: davidph
author: dphansen
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 66b973a91d1b45832f75df6c2896e05f4f4eb85a
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117216"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>SQL Server Machine Learning 또는 R Server 업그레이드 및 설치에 대한 FAQ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 토픽에서는 SQL Server의 기계 학습 기능 설치에 대한 일반적인 질문에 대답합니다. 또한 업그레이드에 대한 일반적인 질문을 다룹니다.

+ 일부 문제는 시험판 버전에서 업그레이드할 때만 발생합니다. 따라서 이 정보를 읽기 전에 버전 및 에디션을 먼저 확인하는 것이 좋습니다. 버전 정보를 보려면 SQL Server Management Studio의 쿼리에서 `@@VERSION`을 실행합니다.
+ 최신 릴리스에서 수정된 문제를 해결하는 가장 빠른 방법은 최대한 빨리 최신 릴리스 또는 서비스 릴리스로 업그레이드하는 것입니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server Machine Learning Services(데이터베이스 내)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>SQL Server 2016 이전 버전의 요구 사항 및 제한 사항 

설치하려는 SQL Server 빌드에 따라 다음 제한 사항이 적용될 수 있습니다.

- SQL Server 2016 R Services 초기 버전에서는 작업 디렉터리가 포함된 드라이브에 8dot3 표기법이 필요했습니다. 시험판 버전을 설치한 경우 SQL Server 2016 서비스 팩 1로 업그레이드하면 이 문제가 해결됩니다. SP1 이후의 릴리스에는 이 요구 사항이 적용되지 않습니다.

- SQL Server 2016의 장애 조치(Failover) 클러스터에는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 설치할 수 없습니다. 그러나 SQL Server 2019는 장애 조치(failover) 지원을 제공합니다. 자세한 내용은 [새로운 기능](../what-s-new-in-sql-server-machine-learning-services.md)을 참조하세요.

- Azure VM은 경우에 따라 추가 구성이 필요할 수 있습니다. 예를 들어 원격 액세스를 지원하기 위해 방화벽 예외를 만들어야 할 수 있습니다.

- R의 다른 버전 또는 Revolution Analytics의 다른 릴리스를 병렬로 설치하는 것은 지원되지 않습니다.

- 설치를 시작하기 전에 바이러스 검사를 해제하세요. 설치가 완료되면 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]에서 사용하는 폴더에 대한 바이러스 검사를 일시 중단하는 것이 좋습니다. 원한다면 전체 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 트리에서 검사를 일시 중단해도 됩니다.

 - Windows Core에 설치된 SQL Server 인스턴스에 Microsoft R Server 설치 SQL Server 2016 RTM 버전에서는 Windows Server Core 버전의 인스턴스에 Microsoft R Server를 추가하는 경우 알려진 문제가 있었습니다. 이 문제가 해결되었습니다. 이 문제가 발생하는 경우 [KB3164398](https://support.microsoft.com/kb/3164398)에 설명된 수정 사항을 적용하여 Windows Server Core의 기존 인스턴스에 R 기능을 추가할 수 있습니다. 자세한 내용은 [Windows Server Core 운영 체제에 Microsoft R Server 독립 실행형을 설치할 수 없음](https://support.microsoft.com/kb/3168691)을 참조하세요.


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>지역화된 SQL Server 2016 버전의 기계 학습 구성 요소를 오프라인으로 설치

SQL Server 2016 초기 릴리스 버전에서는 인터넷에 연결하지 않고 오프라인 설치 중에 로캘별 .cab 파일을 설치할 수 없었습니다. 이 문제는 이후 릴리스에서 수정되었지만, 설치 관리자가 올바른 언어를 설치할 수 없다는 메시지를 반환하는 경우 설치를 계속할 수 있도록 파일 이름을 편집할 수 있습니다.

+ 올바른 언어가 설치되도록 설치 관리자 파일을 수동으로 편집하세요. 예를 들어 일본어 버전의 SQL Server를 설치하려면 파일 이름을 SRS_8.0.3.0_**1033**.cab에서 SRS_8.0.3.0_**1041**.cab로 변경합니다.
+ 기계 학습 구성 요소에 사용되는 언어 식별자는 SQL Server 설치 프로그램 언어와 같아야 합니다. 같지 않으면 설치를 완료할 수 없습니다.

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>시험판 버전: 지원 정책, 업그레이드 및 알려진 이슈

더 이상 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 시험판 버전을 새로 설치할 수 없습니다. 시험판 버전을 사용 중인 경우 최대한 빨리 업그레이드하세요.

이 섹션에는 특정 업그레이드 시나리오에 대한 구체적인 지침이 포함되어 있습니다.

### <a name="how-to-upgrade-sql-server"></a>SQL Server를 업그레이드하는 방법

설치 마법사를 다시 실행하여 SQL Server 버전을 업그레이드할 수 있습니다.

+ [SQL Server 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)
+ [설치 마법사를 사용하여 SQL Server 업그레이드](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

바인딩이라는 프로세스를 사용하여 기계 학습 구성 요소만 업그레이드할 수 있습니다. 
+ [SqlBindR을 사용하여 기계 학습 구성 요소 업그레이드](../install/upgrade-r-and-python.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>시험판 버전에서 현재 위치 업그레이드 지원 종료

더 이상 SQL Server 2016 시험판 버전에서 업그레이드할 수 없습니다. 여기에는 SQL Server 2016 CTP3, CTP3.1, CTP3.2, RC0 또는 RC1이 포함됩니다.

다음 버전은 SQL Server 2016 시험판 버전과 함께 설치되었습니다.

| 버전 | 빌드         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

사용 중인 버전을 확신할 수 없는 경우 SQL Server Management Studio의 쿼리에서 `@@VERSION`을 실행합니다.

일반적으로 업그레이드 프로세스는 다음과 같습니다.

1. 스크립트 및 데이터를 백업합니다.
2. 시험판 버전을 제거합니다.
3. 릴리스 버전을 설치합니다.

SQL Server 기계 학습 구성 요소의 시험판 버전을 제거하는 작업은 복잡할 수 있으며 특수 스크립트를 실행해야 할 수도 있습니다. 기술 지원 서비스에 문의하십시오.

###  <a name="uninstall-prior-to-upgrading-from-an-older-version-of-microsoft-r-server"></a><a name="bkmk_Uninstall"></a> 이전 버전의 Microsoft R Server에서 업그레이드하기 전에 설치 제거

Microsoft R Server 시험판 버전을 설치한 경우 먼저 제거해야 최신 버전으로 업그레이드할 수 있습니다.

1.  **제어판**에서 **프로그램 추가/제거**를 클릭하고 `Microsoft SQL Server 2016 <version number>`을 선택합니다.

2.  구성 요소 **추가**, **복구**또는 **제거** 옵션이 있는 대화 상자에서 **제거**를 선택합니다.
  
3.  **기능 선택** 페이지의 **공유 기능**에서 **R 서버(독립 실행형)** 를 선택합니다. **다음**을 클릭한 다음 **마침** 을 클릭하여 방금 선택한 구성 요소를 제거합니다.

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>R Services 및 R Server(독립 실행형) 병렬 오류 

이전 버전의 SQL Server 2016에서는 R Server(독립 실행형)와 R Services(데이터베이스 내)를 동시에 설치하면 "액세스 거부됨" 메시지와 함께 설치가 실패하는 경우가 가끔 있었습니다. 이 이슈는 SQL Server 2016 서비스 팩 1에서 해결되었습니다.

이 오류가 발생했는데 이러한 기능을 업그레이드해야 하는 경우 SQL Server 2016과 SP1의 통합 설치 설치를 수행합니다. 이 이슈를 해결하는 두 가지 방법이 있으며, 두 방법 모두 제거 후 다시 설치해야 합니다.

1. R Services(데이터베이스 내)를 제거하고, SQLRUserGroup의 사용자 계정이 제거되었는지 확인합니다.

2. 서버를 다시 시작한 다음, R Server(독립 실행형)를 다시 설치합니다.

3. SQL Server 설치 프로그램을 한 번 더 실행하고, 이번에는 **기존 SQL Server에 기능 추가**를 선택합니다.

4. 인스턴스를 선택한 다음, **R Services(데이터베이스 내)** 옵션을 선택하여 추가합니다.

이 절차를 수행해도 문제가 해결되지 않으면 다음 해결 방법을 시도합니다.

1. R Services(데이터베이스 내)와 R Server(독립 실행형)를 동시에 제거합니다.

2. 로컬 사용자 계정(SQLRUserGroup)을 제거합니다.

3. 서버를 다시 시작합니다.

4. SQL Server 설치 프로그램을 실행하고, R Services(데이터베이스 내) 기능만 추가합니다. **R Server(독립 실행형)** 를 선택하지 마세요.

일반적으로 R Services(데이터베이스 내)와 R Server(독립 실행형)를 같은 컴퓨터에 모두 설치하지 않는 것이 좋습니다. 그러나 서버의 용량이 충분하다면 R Server 독립 실행형을 유용한 개발 도구로 활용할 수도 있습니다. 또 다른 시나리오는 R Server의 운영 기능을 사용해야 하지만, 데이터 이동 없이 SQL Server 데이터에 액세스해야 하는 상황입니다.

## <a name="incompatible-version-of-r-client-and-r-server"></a>호환되지 않는 버전의 R 클라이언트 및 R 서버

Microsoft R Client를 설치하고 원격 SQL Server 컴퓨팅 컨텍스트에서 R을 실행하는 데 사용하는 경우 다음과 같은 오류가 발생할 수 있습니다.

*컴퓨터에서 Microsoft R Server 버전 8.0.3과 호환되지 않는 Microsoft R Client 버전 9.0.0을 실행 중입니다. 호환되는 버전을 다운로드하여 설치하세요.*

SQL Server 2016에서는 SQL Server R Services에서 실행되는 R 버전이 Microsoft R Client의 라이브러리와 정확히 일치해야 했습니다. 이후 버전에서는 이 요구 사항이 제거되었습니다. 그러나 항상 최신 버전의 기계 학습 구성 요소를 가져오고 모든 서비스 팩을 설치하는 것이 좋습니다. 

이전 버전의 Microsoft R Server를 사용 중이고 Microsoft R Client 9.0.0과 호환되어야 하는 경우 이 [지원 문서](https://support.microsoft.com/kb/3210262)에 설명된 업데이트를 설치하세요.


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>"한 번에 하나의 Revolution Enterprise 제품만 설치할 수 있습니다." 오류가 발생하고 설치에 실패함

Revolution Analytics 제품의 이전 설치 또는 SQL Server R Services 시험판 버전이 있는 경우 이 오류가 발생할 수 있습니다. 먼저 이전 버전을 제거해야 최신 버전의 Microsoft R Server를 설치할 수 있습니다. 다른 버전의 Revolution Enterprise 도구와 함께 설치하는 것은 지원되지 않습니다.

그러나 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 또는 SQL Server 2016과 함께 R 서버 독립 실행형을 사용하는 경우에는 나란히 설치할 수 있습니다.

## <a name="registry-cleanup-to-uninstall-older-components"></a>레지스트리를 정리하여 이전 구성 요소 제거

이전 버전을 제거하는 데 문제가 있는 경우 레지스트리를 편집하여 관련 키를 제거해야 할 수도 있습니다.

> [!IMPORTANT]
> 이 문제는 Microsoft R Server 시험판 버전 또는 SQL Server 2016 R Services CTP 버전을 설치한 경우에만 적용됩니다.
  
1. Windows 레지스트리를 열고 `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`키를 찾습니다.
2. 다음 항목이 있고 키에 `sEstimatedSize2`값만 포함된 경우에는 모두 삭제합니다.
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (8.0.2의 경우)
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (8.0.1의 경우)
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (8.0.0의 경우)
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (7.5.0의 경우)

## <a name="see-also"></a>참고 항목

 [SQL Server Machine Learning Services(데이터베이스 내)](../r/sql-server-r-services.md)

 [SQL Server Machine Learning Server(독립 실행형)](../r/r-server-standalone.md)

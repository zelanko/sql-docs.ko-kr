---
title: SQL Server 기계 학습에 대 한 업그레이드 및 설치 FAQ | Microsoft Docs
ms.date: 03/15/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 288c764a56cb7a97774e26645f175e912b56b2a7
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>SQL Server 기계 학습 또는 R 서버에 대 한 업그레이드 및 설치 FAQ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 항목에서는 SQL Server의 기능을 학습 하는 컴퓨터의 설치에 대 한 몇 가지 일반적인 질문에 대 한 답을 제공 합니다. 또한 업그레이드에 대 한 일반적인 질문을 다룹니다.

+ 일부 문제는 시험판 버전에서 업그레이드 에서만 발생합니다. 따라서 정확히 파악 버전 및 에디션 먼저 이러한 정보를 읽어야 하는 것이 좋습니다. 버전 정보를 얻으려면 실행 `@@VERSION` 에서 SQL Server Management Studio에서 쿼리 합니다.
+ 최신 릴리스에서 수정 된 모든 문제를 해결 하려면 가장 최근 릴리스가 또는 가능한 한 빨리 서비스 릴리스 업그레이드 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 Services (In-database)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>요구 사항 및 이전 버전의 SQL Server 2016에 대 한 제한 

설치 하는 SQL Server의 빌드에 따라 다음과 같은 제한 사항에 해당할 수 있습니다.

- SQL Server 2016 R Services의 초기 버전에서 8.3 형식이 표기법 작업 디렉터리를 포함 하는 드라이브에 필요 합니다. 시험판 버전을 설치한 경우 SQL Server 2016 서비스 팩 1로 업그레이드 합니다.이 문제를 수정 해야 합니다. 이 요구 사항은 SP1 이후 버전에 적용 되지 않습니다.

- Side-by-side-r을 다른 버전 또는 Revolution Analytics의 다른 릴리스를 설치할 수 없습니다.

- 바이러스 설치 프로그램을 시작 하기 전에 검사를 사용 하지 않도록 설정 합니다. 바이러스 검색에서 사용 하는 폴더에 일시 중단 설치가 완료 된 후 권장 [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]합니다. 가급적 전체에서 검색 일시 중단 [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] 트리 합니다.

 - Windows Core에 설치 된 SQL Server의 인스턴스에서 Microsoft R Server를 설치 합니다. SQL Server 2016 RTM 버전 있었습니다 알려진된 문제를 Microsoft R Server Windows Server Core edition의 인스턴스에 추가 하는 경우. 이 문제가 해결되었습니다. 이 문제가 발생 하는 경우에에 설명 된 수정 프로그램을 적용할 수 있습니다 [KB3164398](https://support.microsoft.com/kb/3164398) 를 Windows Server Core에서 기존 인스턴스에 R 기능을 추가 합니다. 자세한 내용은 [Windows Server Core 운영 체제에 Microsoft R Server 독립 실행형을 설치할 수 없음](https://support.microsoft.com/kb/3168691)을 참조하세요.


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>지역화 된 버전의 SQL Server 2016에 대 한 컴퓨터 학습 구성 요소를 오프 라인 설치

SQL Server 2016의 초기 릴리스 버전 인터넷 연결 없이 오프 라인 설치 하는 동안 로캘 관련.cab 파일을 설치 하지 못했습니다. 이 문제는 이후 릴리스에서 수정 되었습니다 있지만 올바른 언어를 설치할 수 없습니다 되었다는 메시지를 반환 하는 설치 관리자 설치를 계속 하도록 파일 이름을 편집할 수 있습니다.

+ 올바른 언어로 설치 되어 있는지 확인 하려면 설치 관리자 파일을 수동으로 편집 합니다. 예를 들어 일본어 버전의 SQL Server를 설치 하는 파일의 이름에서에서 변경한 SRS_8.0.3.0_**1033**SRS_8.0.3.0_에.cab**1041**.cab 합니다.
+ 기계 학습 구성 요소에 사용 되는 언어 식별자를 사용 해야 SQL Server 설치 언어와 동일 하거나 설치를 완료할 수 없습니다.

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>시험판 버전: 정책, 업그레이드 및 알려진된 문제를 지원 합니다.

모든 시험판 버전의 새 설치 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 더 이상 지원 합니다. 시험판 버전을 사용 하는 경우 가능한 한 빨리를 업그레이드 합니다.

이 섹션에는 특정 업그레이드 시나리오에 대 한 자세한 지침은 포함 되어 있습니다.

### <a name="how-to-upgrade-sql-server"></a>SQL Server를 업그레이드 하는 방법

설치 마법사를 다시 실행 하 여 SQL Server의 버전을 업그레이드할 수 있습니다.

+ [SQL Server 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)
+ [SQL Server 설치 마법사를 사용 하 여 업그레이드](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

방금 기계 학습 구성 요소 바인딩 프로세스를 사용 하 여 업그레이드할 수 있습니다. 
+ [SqlBindR를 사용 하 여 컴퓨터 학습 구성 요소를 업그레이드 하려면](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>시험판 버전에서 전체 업그레이드에 대 한 지원의 끝

SQL Server 2016의 시험판 버전에서 업그레이드 이상 지원 되지 않습니다. SQL Server 2016 CTP3, CTP3.1, c t p 3.2, RC0 또는 r c 1이 포함 됩니다.

다음 버전 시험판 버전의 SQL Server 2016 설치 되었습니다.

| 버전 | 빌드         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

사용 중인 버전에 대 한 확실 하지 않을 경우 실행 `@@VERSION` 에서 SQL Server Management Studio에서 쿼리 합니다.

일반적으로 업그레이드 프로세스는 다음과 같습니다.

1. 스크립트 및 데이터를 백업 합니다.
2. 시험판 버전을 제거 합니다.
3. 릴리스 버전을 설치 합니다.

SQL Server의 시험판 버전을 제거 하 컴퓨터 학습 구성 요소의 복잡 하 고는 특별 한 스크립트를 실행 해야 합니다. 기술 지원 서비스에 문의하십시오.

###  <a name="bkmk_Uninstall"></a> Microsoft R Server의 이전 버전에서 업그레이드 하기 전에 제거

Microsoft R Server 시험판 버전을 설치한 경우 먼저 제거해야 최신 버전으로 업그레이드할 수 있습니다.

1.  **제어판**에서 **프로그램 추가/제거**를 클릭하고 `Microsoft SQL Server 2016 <version number>`을 선택합니다.

2.  구성 요소 **추가**, **복구**또는 **제거** 옵션이 있는 대화 상자에서 **제거**를 선택합니다.
  
3.  **기능 선택** 페이지의 **공유 기능**에서 **R 서버(독립 실행형)**를 선택합니다. **다음**을 클릭한 다음 **마침** 을 클릭하여 방금 선택한 구성 요소를 제거합니다.

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>R 서비스 및 R Server (독립 실행형) side-by-side-오류 

SQL Server 2016의 이전 버전의 경우에 따라 같은 시간에 R Server (독립 실행형)와 R Services (In-database) 설치 발생 "액세스 거부" 메시지는 실패 하 고 설치 합니다. 이 문제는 SQL Server 2016 용 서비스 팩 1에서 수정 되었습니다.

이 오류가 발생 했습니다. 이러한 기능을 업그레이드 해야 하는 경우 s p 1의 SQL Server 2016의 통합 설치를 수행 합니다. 제거 및 다시 설치 해야는 문제를 해결 하려면 두 가지가 있습니다.

1. R Services (In-database)를 제거 하 고 SQLRUserGroup에 대 한 사용자 계정을 제거 되 고 있는지 확인 합니다.

2. 서버를 다시 다음 R Server (독립 실행형)를 다시 설치 하십시오.

3. SQL Server를 실행된, 한 번 설정 하 고이 시간 선택 **기존 SQL Server에 기능 추가**합니다.

4. 인스턴스를 선택 하 고 다음 선택에서 **R Services (In-database)** 추가 하는 옵션입니다.

이 절차에이 문제를 해결 하지 못하는 경우 다음 해결 방법을 시도해 보십시오.

1. 동시에 R Services (In-database) 및 R Server (독립 실행형)를 제거 합니다.

2. 로컬 사용자 계정 (SQLRUserGroup)를 제거 합니다.

3. 서버를 다시 시작합니다.

4. SQL Server 설치 프로그램을 실행 하 고 전용 R Services (In-database) 기능을 추가 합니다. 선택 하지 않으면 **R Server (독립 실행형)**합니다.

일반적으로 권장 R Services (In-database)와 R Server (독립 실행형) 설치 하지 않으면 같은 컴퓨터에 있습니다. 그러나 서버에 충분 한 용량을 가정할 서버 독립 실행형 R 개발 도구로 유용할 수 있습니다 발견할 수 있습니다. 다른 시나리오를 R Server의 화 기능을 사용 하 고 싶을 데이터 이동 없이 SQL Server 데이터에 액세스 해야 하는입니다.

## <a name="incompatible-version-of-r-client-and-r-server"></a>호환되지 않는 버전의 R 클라이언트 및 R 서버

Microsoft R 클라이언트를 설치 하 고 사용 하 여 원격 SQL Server 계산 컨텍스트에서 R을 실행할 경우 다음과 같은 오류가 발생할 수 있습니다.

*9.0.0 버전의 Microsoft R 클라이언트가 8.0.3 버전의 Microsoft R Server와 호환 되지 않는 컴퓨터에 실행 합니다. 호환되는 버전을 다운로드하여 설치하세요.*

SQL Server 2016에서 필수 된 SQL Server R Services에서 실행 중인 R의 버전 수 정확 하 게 Microsoft R 클라이언트에서 라이브러리와 동일 합니다. 이후 버전에서 해당 요구 사항을 제거 되었습니다. 그러나 항상 가져올 구성 요소를 학습 하는 컴퓨터의 최신 버전을 설치 하는 모든 서비스 팩 것이 좋습니다. 

이전 버전의 Microsoft R Server가 설치 하 고 Microsoft R 9.0.0 클라이언트와의 호환성을 위해 필요한 경우이 설명 하는 업데이트를 설치 [지원 문서](https://support.microsoft.com/kb/3210262)합니다.


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>"한 번에 하나의 Revolution Enterprise 제품만 설치할 수 있습니다." 오류가 발생하고 설치에 실패함

Revolution Analytics 제품의 이전 설치 또는 SQL Server R Services 시험판 버전이 있는 경우 이 오류가 발생할 수 있습니다. 먼저 이전 버전을 제거해야 최신 버전의 Microsoft R Server를 설치할 수 있습니다. 다른 버전의 Revolution Enterprise 도구와 함께 설치하는 것은 지원되지 않습니다.

그러나 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 또는 SQL Server 2016과 함께 R 서버 독립 실행형을 사용하는 경우에는 나란히 설치할 수 있습니다.

## <a name="registry-cleanup-to-uninstall-older-components"></a>오래 된 구성 요소를 제거 하는 레지스트리 정리

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

 [SQL Server 컴퓨터 학습 Services (In-database)](../r/sql-server-r-services.md)

 [SQL Server 컴퓨터 (독립 실행형) 서버를 학습 합니다.](../r/r-server-standalone.md)

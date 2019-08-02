---
title: 업그레이드 및 설치 FAQ (질문과 대답)
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
ms.author: davidph
author: dphansen
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fe196a82badcab9ebe05004ee05cd67131942dd1
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715608"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>SQL Server Machine Learning 또는 R Server에 대 한 업그레이드 및 설치 FAQ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 항목에서는 SQL Server의 기계 학습 기능 설치와 관련 된 몇 가지 일반적인 질문에 대 한 답변을 제공 합니다. 또한 업그레이드에 대 한 일반적인 질문을 다룹니다.

+ 일부 문제는 시험판 버전에서 업그레이드 하는 경우에만 발생 합니다. 따라서 이러한 정보를 읽기 전에 먼저 버전 및 에디션을 확인 하는 것이 좋습니다. 버전 정보를 가져오려면 SQL Server Management Studio의 `@@VERSION` 쿼리에서를 실행 합니다.
+ 최신 릴리스에서 수정 된 문제를 해결 하기 위해 최대한 빨리 최신 릴리스 또는 서비스 릴리스로 업그레이드 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server Machine Learning Services (데이터베이스 내)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>이전 버전의 SQL Server 2016에 대 한 요구 사항 및 제한 사항 

설치 하는 SQL Server 빌드에 따라 다음과 같은 제한 사항이 적용 될 수 있습니다.

- SQL Server 2016 R Services의 초기 버전에서는 작업 디렉터리가 포함 된 드라이브에 8.3 표기법이 필요 했습니다. 시험판 버전을 설치한 경우 SQL Server 2016 서비스 팩 1로 업그레이드 하면이 문제를 해결 해야 합니다. S p 1 이후의 릴리스에는이 요구 사항이 적용 되지 않습니다.

- 현재는 장애 조치 ( [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] failover) 클러스터에을 설치할 수 없습니다. 그러나 테스트 환경에서이 기능을 평가 하려는 경우에는 SQL Server 2019 미리 보기에서 장애 조치 (failover)를 지원 합니다. 자세한 내용은 [새로운 기능](../what-s-new-in-sql-server-machine-learning-services.md)을 참조 하세요.

- Azure VM에서 몇 가지 추가 구성이 필요할 수 있습니다. 예를 들어 원격 액세스를 지원 하기 위해 방화벽 예외를 만들어야 할 수 있습니다.

- 다른 버전의 R과 함께 설치 하거나 혁명 분석의 다른 릴리스와 함께 설치 하는 것은 지원 되지 않습니다.

- 설치를 시작 하기 전에 바이러스 검색을 사용 하지 않도록 설정 합니다. 설치가 완료 되 면에서 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]사용 하는 폴더에 대 한 바이러스 검색을 일시 중단 하는 것이 좋습니다. 경우에 따라 전체 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 트리에서 검색을 일시 중단 합니다.

 - Windows Core에 설치 된 SQL Server 인스턴스에 Microsoft R Server를 설치 합니다. SQL Server 2016의 RTM 버전에서는 Windows Server Core 버전의 인스턴스에 Microsoft R Server를 추가할 때 알려진 문제가 있었습니다. 이 문제가 해결되었습니다. 이 문제가 발생 하는 경우 [KB3164398](https://support.microsoft.com/kb/3164398) 에 설명 된 수정 사항을 적용 하 여 Windows Server Core의 기존 인스턴스에 R 기능을 추가할 수 있습니다. 자세한 내용은 [Windows Server Core 운영 체제에 Microsoft R Server 독립 실행형을 설치할 수 없음](https://support.microsoft.com/kb/3168691)을 참조하세요.


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>SQL Server 2016의 지역화 된 버전에 대 한 machine learning 구성 요소 오프 라인 설치

SQL Server 2016의 초기 릴리스 버전에서는 인터넷에 연결 하지 않고 오프 라인 설치 중에 로캘별 .cab 파일을 설치 하지 못했습니다. 이 문제는 이후 릴리스에서 수정 되었지만 설치 관리자에서 올바른 언어를 설치할 수 없다는 메시지를 반환 하는 경우 설치를 계속할 수 있도록 파일 이름을 편집할 수 있습니다.

+ 설치 관리자 파일을 수동으로 편집 하 여 올바른 언어가 설치 되어 있는지 확인 합니다. 예를 들어 SQL Server 일본어 버전을 설치 하려면 파일 이름을 SRS_ 8.0.3.0 _**1033**에서 srs_ 8.0.3.0 _**1041**로 변경 합니다.
+ 기계 학습 구성 요소에 사용 되는 언어 식별자는 SQL Server 설치 언어와 동일 해야 합니다. 그렇지 않으면 설치를 완료할 수 없습니다.

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>시험판 버전: 지원 정책, 업그레이드 및 알려진 문제

의 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 시험판 버전을 새로 설치 하는 것은 더 이상 지원 되지 않습니다. 시험판 버전을 사용 하는 경우 최대한 빨리 업그레이드 하세요.

이 섹션에는 특정 업그레이드 시나리오에 대 한 자세한 지침이 포함 되어 있습니다.

### <a name="how-to-upgrade-sql-server"></a>SQL Server 업그레이드 하는 방법

설치 마법사를 다시 실행 하 여 SQL Server 버전을 업그레이드할 수 있습니다.

+ [SQL Server 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)
+ [설치 마법사를 사용 하 여 SQL Server 업그레이드](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

바인딩 이라는 프로세스를 사용 하 여 machine learning 구성 요소만 업그레이드할 수 있습니다. 
+ [SqlBindR을 사용 하 여 기계 학습 구성 요소 업그레이드](../install/upgrade-r-and-python.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>시험판 버전에서 현재 위치의 업그레이드 지원 종료

SQL Server 2016의 시험판 버전에서 업그레이드는 더 이상 지원 되지 않습니다. 여기에는 SQL Server 2016 CTP3, CTP 3.1, CTP 3.2, RC0 또는 RC1이 포함 됩니다.

다음 버전은 SQL Server 2016의 시험판 버전과 함께 설치 되었습니다.

| 버전 | 빌드         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

사용 중인 버전에 대해 잘 모르겠으면 SQL Server Management Studio에서 쿼리를 실행 `@@VERSION` 합니다.

일반적으로 업그레이드 프로세스는 다음과 같습니다.

1. 스크립트 및 데이터를 백업 합니다.
2. 시험판 버전을 제거 합니다.
3. 릴리스 버전을 설치 합니다.

SQL Server machine learning 구성 요소의 시험판 버전을 제거 하는 것은 복잡할 수 있으므로 특수 스크립트를 실행 해야 할 수 있습니다. 기술 지원 서비스에 문의하십시오.

###  <a name="bkmk_Uninstall"></a>이전 버전의 Microsoft R Server에서 업그레이드 하기 전에 제거

Microsoft R Server 시험판 버전을 설치한 경우 먼저 제거해야 최신 버전으로 업그레이드할 수 있습니다.

1.  **제어판**에서 **프로그램 추가/제거**를 클릭하고 `Microsoft SQL Server 2016 <version number>`을 선택합니다.

2.  구성 요소 **추가**, **복구**또는 **제거** 옵션이 있는 대화 상자에서 **제거**를 선택합니다.
  
3.  **기능 선택** 페이지의 **공유 기능**에서 **R 서버(독립 실행형)** 를 선택합니다. **다음**을 클릭한 다음 **마침** 을 클릭하여 방금 선택한 구성 요소를 제거합니다.

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>R Services 및 R Server (독립 실행형) side-by-side 오류 

이전 버전의 SQL Server 2016에서 R Server (독립 실행형) 및 R Services (데이터베이스 내)를 동시에 설치 하면 "액세스 거부" 메시지가 발생 하 여 설치가 실패 하는 경우가 있습니다. 이 문제는 2016 SQL Server 서비스 팩 1에서 해결 되었습니다.

이 오류가 발생 하 고 이러한 기능을 업그레이드 해야 하는 경우 SQL Server 2016 s p 1의 통합 설치 설치를 수행 합니다. 두 가지 방법으로 문제를 해결할 수 있습니다. 두 가지 방법 모두를 제거 하 고 다시 설치 해야 합니다.

1. R Services (데이터베이스 내)를 제거 하 고 SQLRUserGroup의 사용자 계정이 제거 되었는지 확인 합니다.

2. 서버를 다시 시작한 다음 R 서버 (독립 실행형)를 다시 설치 합니다.

3. 나중에 SQL Server 설치를 실행 하 고 이번 **에는 기존 SQL Server에 기능 추가**를 선택 합니다.

4. 인스턴스를 선택한 다음 추가할 **R Services (데이터베이스 내)** 옵션을 선택 합니다.

이 절차를 수행 하 여 문제가 해결 되지 않으면 다음 해결 방법을 시도 하십시오.

1. R Services (데이터베이스 내) 및 R Server (독립 실행형)를 동시에 제거 합니다.

2. 로컬 사용자 계정 (SQLRUserGroup)을 제거 합니다.

3. 서버를 다시 시작합니다.

4. SQL Server 설치를 실행 하 고 R Services (데이터베이스 내) 기능만 추가 합니다. **R 서버 (독립 실행형)** 를 선택 하지 마십시오.

일반적으로 동일한 컴퓨터에 R Services (데이터베이스 내)와 R 서버 (독립 실행형)를 둘 다 설치 하지 않는 것이 좋습니다. 그러나 서버에 충분 한 용량이 있다고 가정 하면 R Server 독립 실행형을 개발 도구로 활용할 수 있습니다. 또 다른 가능한 시나리오는 R Server의 운영 화 기능을 사용 해야 하 고 데이터 이동 없이도 SQL Server 데이터에 액세스 하는 것입니다.

## <a name="incompatible-version-of-r-client-and-r-server"></a>호환되지 않는 버전의 R 클라이언트 및 R 서버

Microsoft R Client를 설치 하 고이를 사용 하 여 원격 SQL Server 계산 컨텍스트에서 R을 실행 하는 경우 다음과 같은 오류가 발생할 수 있습니다.

*컴퓨터에서 Microsoft R client 버전 9.0.0을 실행 하 고 있습니다 .이 버전은 Microsoft R Server 버전 8.0.3과와 호환 되지 않습니다. 호환되는 버전을 다운로드하여 설치하세요.*

SQL Server 2016에서는 SQL Server R Services에서 실행 되는 R 버전이 Microsoft R Client의 라이브러리와 정확히 일치 해야 했습니다. 이 요구 사항은 이후 버전에서 제거 되었습니다. 그러나 항상 최신 버전의 machine learning 구성 요소를 가져오고 모든 서비스 팩을 설치 하는 것이 좋습니다. 

이전 버전의 Microsoft R Server 있고 Microsoft R Client 9.0.0와의 호환성을 보장 해야 하는 경우이 [지원 문서](https://support.microsoft.com/kb/3210262)에 설명 된 업데이트를 설치 합니다.


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>"한 번에 하나의 Revolution Enterprise 제품만 설치할 수 있습니다." 오류가 발생하고 설치에 실패함

Revolution Analytics 제품의 이전 설치 또는 SQL Server R Services 시험판 버전이 있는 경우 이 오류가 발생할 수 있습니다. 먼저 이전 버전을 제거해야 최신 버전의 Microsoft R Server를 설치할 수 있습니다. 다른 버전의 Revolution Enterprise 도구와 함께 설치하는 것은 지원되지 않습니다.

그러나 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 또는 SQL Server 2016과 함께 R 서버 독립 실행형을 사용하는 경우에는 나란히 설치할 수 있습니다.

## <a name="registry-cleanup-to-uninstall-older-components"></a>이전 구성 요소를 제거 하기 위한 레지스트리 정리

이전 버전을 제거하는 데 문제가 있는 경우 레지스트리를 편집하여 관련 키를 제거해야 할 수도 있습니다.

> [!IMPORTANT]
> 이 문제는 Microsoft R Server 시험판 버전 또는 SQL Server 2016 R Services CTP 버전을 설치한 경우에만 적용됩니다.
  
1. Windows 레지스트리를 열고 `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`키를 찾습니다.
2. 다음 항목이 있고 키에 `sEstimatedSize2`값만 포함된 경우에는 모두 삭제합니다.
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (8.0.2의 경우)
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (8.0.1의 경우)
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (8.0.0의 경우)
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (7.5.0의 경우)

## <a name="see-also"></a>참조

 [SQL Server Machine Learning Services (데이터베이스 내)](../r/sql-server-r-services.md)

 [SQL Server Machine Learning Server (독립 실행형)](../r/r-server-standalone.md)

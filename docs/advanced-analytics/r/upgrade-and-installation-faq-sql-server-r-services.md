---
title: "SQL Server 기계 학습에 대 한 업그레이드 및 설치 FAQ | Microsoft Docs"
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: "59"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 137889dae328d3f780082ca5837717017b66867d
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning"></a>SQL Server 기계 학습에 대 한 업그레이드 및 설치 FAQ

이 항목에서는 SQL Server의 기능을 학습 하는 컴퓨터의 설치에 대 한 몇 가지 일반적인 질문에 대 한 답을 제공 합니다. 또한 업그레이드에 대 한 일반적인 질문을 다룹니다.

+ 일부 문제는 시험판 버전에서 업그레이드 에서만 발생합니다. 따라서 정확히 파악 버전 및 에디션 먼저 이러한 정보를 읽어야 하는 것이 좋습니다.
+ 최신 릴리스에서 수정 된 모든 문제를 해결 하려면 가장 최근 릴리스가 또는 가능한 한 빨리 서비스 릴리스 업그레이드 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 Services (In-database)

## <a name="performing-setup-for-the-first-time"></a>처음으로 설치를 수행합니다.

설정 하기 위한 절차에 따라 [!INCLUDE[sscurrent_md](../../includes/sscurrent_md.md)] 및 R 구성 요소 설명에 따라: 

+ [SQL Server R Services 또는 시스템 학습 서비스 In-database 설정](../r/set-up-sql-server-r-services-in-database.md)
+ [Python SQL Server 2017 설정](../python/setup-python-machine-learning-services.md)
+ [독립 실행형 R Server 만들기](../r/create-a-standalone-r-server.md)

> [!IMPORTANT]
> 
> SQL Server 및 Python 또는 R 스크립트를 사용 하려면 먼저 기능을 학습 하는 컴퓨터를 설치한 후 몇 가지 추가 구성 단계를 완료 해야 합니다. 외부 스크립트 실행 기능을 기본적으로 해제 때문입니다.

### <a name="requirements-and-restrictions"></a>요구 사항 및 제한 사항

설치 하는 SQL Server의 빌드에 따라 다음과 같은 제한 사항에 해당할 수 있습니다.

- SQL Server 2016 R Services의 초기 버전에서 8.3 형식이 표기법 작업 디렉터리를 포함 하는 드라이브에 필요 합니다. 시험판 버전을 설치한 경우 SQL Server 2016 서비스 팩 1로 업그레이드 합니다.이 문제를 수정 해야 합니다. 이 요구 사항은 SP1 이후 버전에 적용 되지 않습니다.

- 설치할 수 없는 현재 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 장애 조치 클러스터에 있습니다. 

- Azure VM에서 몇 가지 추가 구성이 필요할 수 있습니다. 예를 들어 원격 액세스를 지원 하도록 방화벽 예외를 만들려고 할 수 있습니다.

- Side-by-side-r을 다른 버전 또는 Revolution Analytics의 다른 릴리스를 설치할 수 없습니다.

- [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 시험판 버전의 새로운 설치는 더 이상 지원되지 않습니다. 시험판 버전을 사용 하는 경우 가능한 한 빨리를 업그레이드 합니다.

- 바이러스 설치 프로그램을 시작 하기 전에 검사를 사용 하지 않도록 설정 합니다. 바이러스 검색에서 사용 하는 폴더에 일시 중단 설치가 완료 된 후 권장 [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]합니다. 가급적 전체에서 검색 일시 중단 [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] 트리 합니다.

### <a name="licensing-agreements-for-unattended-installs"></a>무인된 설치에 대 한 사용권 계약

SQL Server의 인스턴스를 업그레이드 하려면 명령줄을 사용 하는 경우 명령줄 모두 포함 되어 있는지 확인은 [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] 계약 매개 변수 및 새 사용권 계약 매개 변수 R 및 Python에 대 한 라이선스.

### <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server"></a>지역화 된 버전의 SQL Server에 대 한 컴퓨터 학습 구성 요소를 오프 라인 설치

설치 하는 경우 [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] 컴퓨터 학습 인터넷 액세스가 없는 컴퓨터에 구성 요소를 몇 가지 추가 단계를 수행 해야 합니다.

+ SQL Server 설치 프로그램을 실행 하기 전에 로컬 폴더에 있는 Python 또는 R 구성 요소 설치 관리자를 다운로드 합니다.
+ 경우에 따라 올바른 언어로 설치 되어 있는지 확인 하려면 설치 관리자 파일을 편집 해야 합니다.
+ 기계 학습 구성 요소에 사용 되는 언어 식별자를 사용 해야 SQL Server 설치 언어와 동일 하거나 설치를 완료할 수 없습니다.

자세한 내용은 참조 [인터넷 연결 되지 않은 컴퓨터 학습 구성 요소 설치](../r/installing-ml-components-without-internet-access.md)합니다.

## <a name="post-installation-configuration"></a>설치 후 구성

기계 학습에서 Python 또는 R을 사용 하려면 몇 가지 추가 구성이 SQL Server 설치 프로그램을 실행 한 후 필요 합니다. 필요한 정확한 단계는 서버 및 SQL Server 인스턴스 및 데이터베이스 구성 방법의 보안 수준에 따라 달라 집니다.

사용자 환경에는 추가 단계가 필요할 수를 확인 하려면 설치 후 지침의 목록에서 모든 옵션을 검토 합니다.

+ [데이터베이스에서 학습 하는 SQL Server 컴퓨터를 설정](set-up-sql-server-r-services-in-database.md) 

## <a name="upgrades-or-uninstallation"></a>업그레이드 또는 제거

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

| 버전 옵션 | 빌드         |
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

### <a name="support-for-slipstream-upgrades"></a>통합 설치 업그레이드 지원

통합 설치는 실패한 인스턴스 설치에 패치나 업데이트를 적용하여 기존 문제를 해결하는 기능을 말합니다. 이 방법의 장점은 SQL Server 수행 하는 설치 프로그램을 나중에 별도 컴퓨터를 다시 시작을 방지 하는 동시에 업데이트 됩니다.

서버에 인터넷에 액세스 하는 경우에 SQL Server 설치 관리자를 다운로드 해야 합니다. 또한 업데이트 프로세스를 시작하기 *전에* R 구성 요소 설치 관리자의 일치하는 버전을 별도로 다운로드해야 합니다. 

다운로드 위치에 대 한 참조 [인터넷 연결 되지 않은 컴퓨터 학습 구성 요소 설치](installing-ml-components-without-internet-access.md)합니다.

모든 설치 파일이 로컬 디렉터리로 복사되면 명령줄에서 SETUP.EXE를 입력하여 설치 유틸리티를 시작합니다.

- 사용 하 여는 */UPDATESOURCE* 인수는 누적 업데이트 또는 서비스 팩 릴리스의 비롯 하 여 SQL Server 업데이트를 포함 하는 로컬 파일의 위치를 지정 합니다.

- 사용 하 여는 */MRCACHEDIRECTORY* 인수 R 구성 요소 CAB 파일을 포함 하는 폴더를 지정 합니다.

자세한 내용은 지원 팀이 블로그를 참조 하십시오: [인터넷 액세스가 없는 컴퓨터에 R 서비스 배포](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)합니다.

### <a name="get-machine-learning-components-for-offline-installs"></a>오프 라인 설치에 대 한 컴퓨터 학습 구성 요소 가져오기

를 설치 하거나 인터넷에 연결 되어 있지 않은 서버를 업그레이드 하는 경우 새로 고침을 시작 하기 전에 구성 요소를 수동으로 학습 하는 컴퓨터의 업데이트 된 버전을 다운로드 해야 합니다. 

+ [인터넷 연결 되지 않은 컴퓨터 학습 구성 요소 설치](../../advanced-analytics/r/installing-ml-components-without-internet-access.md)합니다.

### <a name="support-policy-and-schedule-for-update-of-machine-learning-components"></a>시스템 학습 구성 요소 업데이트에 대 한 지원 정책 및 일정

핫픽스 또는 SQL Server의 향상 된 기능 출시 되 면 컴퓨터 학습 구성 요소가 자동으로 업그레이드 되었거나 인스턴스에 기능을 이미 포함 하는 경우 새로 고침 합니다.

2016 년 12 월을 기준으로 SQL Server 릴리스 주기 보다 더 빠른 주기로 컴퓨터 학습 구성 요소를 업그레이드할 수 있습니다. 이렇게 하려면 *바인딩* 최신 소프트웨어 수명 주기 정책에 SQL Server의 인스턴스. 새 버전의 기계 학습 도구는 개발 팀을 학습 하는 컴퓨터에서 출시 되 면 때마다 최신 버전을 다운로드 하 고 기계 학습에 사용 되는 SQL Server 인스턴스에 적용 합니다.

참조 항목:

+ [Microsoft R Server 및 학습 서버 컴퓨터에 대 한 지원 타임 라인](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)
+ [SQL Server의 인스턴스를 업그레이드 하려면 SqlBindR를 사용 하 여](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

## <a name="r-server-standalone"></a>R Server (Standalone)

이 섹션에서는 SQL Server 2016 설치 프로그램을 사용 하는 Microsoft R server (독립 실행형) 설치 관련 문제를 설명 합니다. 

서버를 학습 하는 컴퓨터에 R Server에서 업그레이드와 관련 된 문제에 대 한 참조 [Windows 용 컴퓨터 학습 서버 설치](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)합니다.

### <a name="problems-when-r-services-and-r-server-standalone-are-installed-on-the-same-computer"></a>R 서비스 및 서버 독립 실행형 R 동일한 컴퓨터에 설치 된 경우의 문제

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

## <a name="see-also"></a>관련 항목:

 [SQL Server R Services 시작](../r/getting-started-with-sql-server-r-services.md)

 [Microsoft R Server 독립 실행형 시작](../r/getting-started-with-microsoft-r-server-standalone.md)

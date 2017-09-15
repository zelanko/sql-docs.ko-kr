---
title: "업그레이드 및 설치 FAQ (SQL Server R Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: 59
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: 395554af6b9d014d560d8b6520d032966630c5b2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/08/2017

---
# <a name="upgrade-and-installation-faq-sql-server-r-services"></a>업그레이드 및 설치 FAQ (SQL Server R Services)

이 항목에서는 SQL Server의 기능을 학습 하는 컴퓨터의 설치에 대 한 몇 가지 일반적인 질문에 대 한 답을 제공 합니다. 또한 업그레이드에 대 한 일반적인 질문을 다룹니다. 일부 문제는 시험판 버전에서 업그레이드 에서만 발생합니다. 따라서, 버전 및 에디션 첫 번째 및 가장 최근 릴리스가 또는 서비스 릴리스 업그레이드을 가능한 한 빨리 확인 하는 것이 좋습니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 Services (In-database)

## <a name="performing-setup-for-the-first-time"></a>처음으로 설치를 수행합니다.

설정 하기 위한 절차에 따라 [! INCLUDEssCurrent] 및 R 구성 요소 설명에 따라: 

+ [SQL Server R Services 또는 시스템 학습 서비스 In-database 설정](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)
+ [Python SQL Server 2017 설정](../python/setup-python-machine-learning-services.md)
+ [독립 실행형 R 서버 만들기](create-a-standalone-r-server.md)

외부 Python 또는 R 스크립트를 사용 하려면 SQL Server를 설치한 후에 몇 가지 추가 구성을 마쳐야 합니다. 외부 스크립트 실행 기능을 기본적으로 해제 때문입니다.

> [!NOTE]
> SQL Server 2016에 대 한 공개 하기 전에 게시 된 설치 지침을 사용 하지 마십시오. 설치 프로세스를 완전히 초기 릴리스 및 공식 릴리스 버전 간의 변경 합니다. 

### <a name="requirements-and-restrictions"></a>요구 사항 및 제한 사항

R services를 설치 하는 빌드에 따라 다음과 같은 제한 사항에 해당할 수 있습니다.

- SQL Server 2016 R Services의 초기 버전에서 8.3 형식이 표기법 작업 디렉터리를 포함 하는 드라이브에 필요 합니다. 시험판 버전을 설치한 경우이 요구 사항을 제거 해야 SQL Server 2016 서비스 팩 1로 업그레이드 합니다.

- 장애 조치(Failover) 클러스터에는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 를 설치할 수 없습니다. 

- Azure VM에서 몇 가지 추가 구성이 필요할 수 있습니다. 예를 들어 원격 액세스를 지원 하도록 방화벽 예외를 만들려고 할 수 있습니다.

- Side-by-side-r을 다른 버전 또는 Revolution Analytics의 다른 릴리스를 설치할 수 없습니다.

- [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 시험판 버전의 새로운 설치는 더 이상 지원되지 않습니다. 시험판 버전을 사용 하는 경우 가능한 한 빨리를 업그레이드 합니다.

- 바이러스 설치 프로그램을 시작 하기 전에 검사를 사용 하지 않도록 설정 합니다. 설치가 완료 된 후에 SQL Server (가급적 속한 전체 형식 트리)에서 사용 되는 폴더에 바이러스 검사를 일시 중단 하는 것이 좋습니다.

### <a name="licensing-agreements-for-unattended-installs"></a>무인된 설치에 대 한 사용권 계약

SQL Server의 인스턴스를 업그레이드 하려면 명령줄을 사용 하는 경우 새 사용권 계약 매개 변수는 명령줄에 포함 되는지 확인 */IACCEPTROPENLICENSEAGREEMENT*합니다. 이 매개 변수를 사용 하지 않는 경우 설치가 실패할 수 있습니다.

### <a name="offline-installation-of-r-components-for-a-localized-version-of-sql-server"></a>R 구성 요소 지역화 된 버전의 SQL Server에 대 한 오프 라인 설치

인터넷에 연결 되지 않은 컴퓨터에 R Services를 설치할 때 두 가지 추가 단계를 수행 해야 합니다. SQL Server 설치 프로그램을 실행 하 고 올바른 언어로 설치 되어 있는지 확인 하려면 설치 관리자 파일을 편집 하기 전에 로컬 폴더에 R 구성 요소 설치 관리자를 다운로드 합니다.

SQL Server 설치 언어와 동일한 R 구성 요소에 사용 되는 언어 식별자 여야 합니다 또는 **다음** 단추가 비활성화 되 고 설치를 완료할 수 없습니다.

자세한 내용은 참조 [인터넷에 액세스 하지 않고 R 구성 요소 설치](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md)합니다.

## <a name="post-installation-configuration"></a>설치 후 구성

기계 학습에서 Python 또는 R을 사용 하려면 몇 가지 추가 구성이 SQL Server 설치 프로그램을 실행 한 후 필요 합니다. 추가 단계는 서버 및 SQL Server 인스턴스 및 데이터베이스의 보안 수준에 따라 필요할 수 있습니다. 설치 지침에는 추가 구성이 필요할 경우 확인부터 이러한 단계를 검토 합니다.

[SQL Server R Services에서-데이터베이스 설정](set-up-sql-server-r-services-in-database.md)

- Python 또는 R 등의 외부 스크립트를 실행할 수 있도록 지원 하는 기능 데이터베이스 보안을 위해 기본적으로 비활성화 되 고 사용할 수 있어야 합니다.

- Python 또는 R 실행 하려면 실행 패드에서 사용 되는 작업자 계정 인스턴스에 대 한 액세스 권한이 있는지 확인 합니다.

- SQL Server와 인바운드 통신을 허용 하는 방화벽 규칙을 만들거나 서버에서 원격 액세스를 사용 해야 합니다.

- 계획 된 작업 부하에 따라 기계 학습 작업에 대 한 서버를 최적화 하기 위해 할 수 있습니다. 

## <a name="upgrades-or-uninstallation"></a>업그레이드 또는 제거

이 섹션에는 특정 업그레이드 시나리오에 대 한 자세한 지침은 포함 되어 있습니다.

SQL Server 2016 R Services의 시험판 버전에서 업그레이드는 지원 더 이상 사용 되지 않습니다. 시험판 버전을 제거한 후 릴리스 버전을 가능한 한 빨리 설치 하는 것이 좋습니다.

### <a name="support-for-slipstream-upgrades"></a>통합 설치 업그레이드 지원

통합 설치는 실패한 인스턴스 설치에 패치나 업데이트를 적용하여 기존 문제를 해결하는 기능을 말합니다. 이 방법의 장점은 SQL Server 수행 하는 설치 프로그램을 나중에 별도 컴퓨터를 다시 시작을 방지 하는 동시에 업데이트 됩니다.

서버에 인터넷에 액세스 하는 경우에 SQL Server 설치 관리자를 다운로드 해야 합니다. 또한 업데이트 프로세스를 시작하기 *전에* R 구성 요소 설치 관리자의 일치하는 버전을 별도로 다운로드해야 합니다. 

다운로드 위치에 대 한 참조 [설치 R components without](installing-ml-components-without-internet-access.md)합니다.

모든 설치 파일이 로컬 디렉터리로 복사되면 명령줄에서 SETUP.EXE를 입력하여 설치 유틸리티를 시작합니다.

- 사용 하 여는 */UPDATESOURCE* 인수는 누적 업데이트 또는 서비스 팩 릴리스의 비롯 하 여 SQL Server 업데이트를 포함 하는 로컬 파일의 위치를 지정 합니다.

- 사용 하 여는 */MRCACHEDIRECTORY* 인수 R 구성 요소 CAB 파일을 포함 하는 폴더를 지정 합니다.

자세한 내용은 지원 팀이 블로그를 참조 하십시오: [인터넷 액세스가 없는 컴퓨터에 R 서비스 배포](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)합니다.

### <a name="upgrade-r-components-offline"></a>R 구성 요소를 오프 라인으로 업그레이드

를 설치 하거나 인터넷에 연결 되어 있지 않은 서버를 업그레이드 하는 경우 새로 고침을 시작 하기 전에 업데이트 된 버전의 R 구성 요소를 수동으로 다운로드 해야 있습니다. 자세한 내용은 참조 [설치 R components without](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md)합니다.

### <a name="schedule-for-update-of-r-components"></a>R 구성 요소 업데이트에 대 한 일정

핫픽스 또는 SQL Server 2016의 향상 된 기능 출시 되 면 R 구성 요소는 업그레이드 하거나 인스턴스에 R 서비스 기능을 이미 포함 하는 경우 새로 고칠 수도 있습니다.

SQL Server 2017을 사용 하는 R 구성 요소에 대 한 업그레이드 자동으로 설치 됩니다.

2016 년 12 월을 기준으로 SQL Server 릴리스 주기 보다 더 빠른 주기로 R 구성 요소를 업그레이드할 수 있습니다. 이렇게 하려면 *바인딩* 최신 소프트웨어 수명 주기 정책에 R Services의 인스턴스. 현재 지원은 2016 인스턴스를 업그레이드에 대해서만 제공 됩니다. 새 버전의 R Server 출시 되 면도 2017 인스턴스를 업그레이드할 수 있습니다.

자세한 내용은 참조 [SQL Server R Services의 인스턴스를 업그레이드 하려면 사용 하 여 SqlBindR](../../advanced-analytics/r-services/use-sqlbindr-exe-to-upgrade-an-instance-of-r-services.md)합니다.

### <a name="upgrade-from-a-pre-release-version-of-sql-server-2016"></a>SQL Server 2016의 시험판 버전에서 업그레이드

일반적으로 전체 업그레이드는 시험판 버전에 대 한 지원 되지 않습니다.

이전 버전을 제거 해야 R 서비스를 성공적으로 설치 하려면 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 및 관련된 R 구성 요소입니다. SQL Server 2016 CTP3, CTP3.1, c t p 3.2, RC0 또는 r c 1이 포함 됩니다.

시험판 버전을 제거 하 복잡 한 수 있으며 특별 한 스크립트를 실행 해야 합니다. 기술 지원 서비스에 문의하십시오.

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

사용 중인 버전에 대 한 확실 하지 않을 경우 실행 `@@VERSION` SQL Server Management Studio에서.

### <a name="problems-with-setup-of-r-server-standalone"></a>R server (독립 실행형) 설치에 문제가 있습니다.

이 섹션에서는 SQL Server 2016 설치 프로그램을 사용 하는 Microsoft R server (독립 실행형) 설치 관련 문제를 설명 합니다. R 서버 업그레이드와 관련 된 일반적인 문제에 대 한 참조 [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/) msdn 합니다.

#### <a name="failure-to-install-localized-versions"></a>지역화 된 버전 설치 실패

R 서버를 오프 라인으로 설치할 때 시험판 버전 하지 못하게 지역화 된 언어를 사용할 수 있습니다.

일반적으로 서버에 인터넷 액세스가 없는 경우 설치 프로그램을 실행 하기 전에 다운로드 해야 설치 패키지를 모든 R 서버에 대 한 합니다. 그런 다음 설치 하는 동안 파일의 위치를 지정합니다.

그러나 설치 관리자 패키지와 관련 된 언어 식별자를 없는 경우 SQL Server 설치 언어와 동일한 문제가 발생 합니다. R 구성 요소 설치에 대 한 페이지에 도달 하면는 **다음** 단추가 비활성화 되 고 설치를 진행할 수 없습니다. 이 문제를 해결 일치 하는 식별자를 사용 하려면 패키지 이름을 바꿀 수 있습니다.

예를 들어, 설치 패키지의 이름 수 있습니다 `SRO_3.2.2.0_1031.cab`합니다.
SQL Server에서 104 언어를 설치 하려면 파일을 이름 `SRO_3.2.2.0_1041.cab`합니다.

#### <a name="installing-r-services-and-r-server-standalone-on-the-same-computer"></a>R 서비스와 동일한 컴퓨터에 R Server 독립 실행형 설치

일반적으로 있습니다 설치 하지 마십시오 R Services (In-database)와 R Server (독립 실행형)를 모두 동일한 컴퓨터에서. 그러나 서버에 충분 한 용량이 있으면 서버 독립 실행형 R 개발 도구로 유용할 수 있습니다. R 서버의 화 기능을 사용 하 고 데이터 이동 없이 R 서버에서 SQL Server 데이터 액세스를 할 수도 있습니다.

동일한 컴퓨터에 R 서버와 R Services를 설치 하는 경우 두 개의 별도 동일한 R 라이브러리 집합이 설치 되어 있는지 확인 합니다. 하나는 SQL Server 인스턴스에서 사용 하기 위해 고 하나는 개발을 사용 하거나 R 서버에서 사용 합니다.

SQL Server 2016의 이전 버전에서 동시에 R Server (독립 실행형)와 R Services (In-database) 설치 "액세스 거부" 메시지와 함께 오류가 발생할 수 있습니다. 이 문제는 SQL Server 2016 용 서비스 팩 1에서 수정 되었습니다.

이 오류가 발생 했습니다. 이러한 기능을 업그레이드 해야 하는 경우 s p 1의 SQL Server 2016의 통합 설치를 수행 합니다. 제거 및 다시 설치 해야는 문제를 해결 하려면 두 가지가 있습니다.

1. R Services (In-database)를 제거 하 고 SQLRUserGroup에 대 한 사용자 계정을 제거 되 고 있는지 확인 합니다.

2. 서버를 다시 다음 R Server (독립 실행형)를 다시 설치 하십시오.

3. SQL Server를 실행된, 한 번 설정 하 고이 시간 선택 **기존 SQL Server에 기능 추가**합니다.

4. 인스턴스를 선택 하 고 다음 선택에서 **R Services (In-database)** 추가 하는 옵션입니다.

이 절차는 경우에 따라 문제를 해결 하려면 실패 합니다. 다음 해결 방법을 시도해 보십시오.

1. 동시에 R Services (In-database) 및 R Server (독립 실행형)를 제거 합니다.

2. 로컬 사용자 계정 (SQLRUserGroup)를 제거 합니다.

3. 서버를 다시 시작합니다.

4. SQL Server 설치 프로그램을 실행 하 고 전용 R Services (In-database) 기능을 추가 합니다. 선택 하지 않으면 **R Server (독립 실행형)**합니다.

## <a name="see-also"></a>참고 항목

 [SQL Server R Services 시작](../r/getting-started-with-sql-server-r-services.md)

 [Microsoft R Server 독립 실행형 시작](../r/getting-started-with-microsoft-r-server-standalone.md)


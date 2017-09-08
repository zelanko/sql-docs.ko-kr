---
title: "업그레이드 및 설치 FAQ(SQL Server R Services) | Microsoft 문서"
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fa3cf5a36af30be655286a2e883d2408a6a3de90
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="upgrade-and-installation-faq-sql-server-r-services"></a>업그레이드 및 설치 FAQ(SQL Server R Services)

이 항목에서는 기계 학습에서 SQL Server 서비스의 설치에 대 한 몇 가지 일반적인 질문에 대 한 답을 제공 합니다. 또한 업그레이드에 대 한 일반적인 질문을 다룹니다. 일부 문제는 시험판 버전에서 업그레이드 에서만 발생합니다. 따라서, 버전 및 에디션 첫 번째 및 가장 최근 릴리스가 또는 서비스 릴리스 업그레이드을 가능한 한 빨리 확인 하는 것이 좋습니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 Services (In-database)

## <a name="performing-setup-for-the-first-time"></a>처음으로 설치를 수행합니다.

설정 하기 위한 절차에 따라 [! INCLUDEssCurrent] 및 여기에 설명 된 대로 R 구성 요소: 

+ [SQL Server R Services 또는 시스템 학습 서비스 In-database 설정](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)
+ [Python SQL Server 2017 설정](../python/setup-python-machine-learning-services.md)
+ [독립 실행형 R 서버 만들기](create-a-standalone-r-server.md)

외부 Python 또는 R 스크립트를 사용 하려면 SQL Server를 설치한 후에 몇 가지 추가 구성 단계를 수행 해야 합니다. 즉, 외부 스크립트 실행 기능 노출 영역을 줄이기 위해 기본적으로 활성화 되어 있지 않으므로 합니다.

> [!NOTE]
> SQL Server 2016에 대 한 공개 하기 전에 게시 된 설치 지침을 사용 하지 마십시오. 설치 프로세스를 완전히 초기 릴리스 및 공식 릴리스 버전 간의 변경 합니다. 

### <a name="requirements-and-restrictions"></a>요구 사항 및 제한 사항

R services를 설치 하는 빌드에 따라 일부 다음과 같은 제한 사항이 적용 될 수 있습니다.

- SQL Server 2016 R Services의 초기 버전에서 8.3 형식이 표기법 작업 디렉터리를 포함 하는 드라이브에 필요 합니다. 시험판 버전을 설치한 경우이 요구 사항을 제거 해야 SQL Server 2016 서비스 팩 1로 업그레이드 합니다.

- 장애 조치(Failover) 클러스터에는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 를 설치할 수 없습니다. 

- Azure VM에서 몇 가지 추가 구성이 필요할 수 있습니다. 예를 들어 원격 액세스를 지원 하도록 방화벽 예외를 만들려고 할 수 있습니다.

- Side-by-side-r을 다른 버전 또는 Revolution Analytics의 다른 릴리스를 설치할 수 없습니다.

- [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 시험판 버전의 새로운 설치는 더 이상 지원되지 않습니다. 시험판 버전을 사용 하는 경우 가능한 한 빨리를 업그레이드 합니다.

- 바이러스 설치 프로그램을 시작 하기 전에 검사를 사용 하지 않도록 설정 합니다. 설치가 완료 된 후에 바이러스 검사에서 SQL Server, 전체 트리 가급적 사용 하는 폴더에 일시 중단 하는 것이 좋습니다.

### <a name="licensing-agreements-for-unattended-installs"></a>무인된 설치에 대 한 사용권 계약

SQL Server의 인스턴스를 업그레이드 하려면 명령줄을 사용 하는 경우 새 사용권 계약 매개 변수는 명령줄에 포함 되는지 확인 */IACCEPTROPENLICENSEAGREEMENT*합니다. 올바른 인수를 사용 하려면 설치 프로그램이 실패 않을 수 있습니다.

### <a name="offline-installation-of-r-components-for-localized-version-of-sql-server"></a>지역화된 버전의 SQL Server에 대한 R 구성 요소의 오프라인 설치

두 개의 추가 단계를 수행 해야 인터넷에 연결 되지 않은 컴퓨터에 R 서비스를 설치 하는 경우: R 구성 요소 설치 관리자를 실행 하면 SQL Server를 설치 하기 전에 로컬 폴더에 다운로드 해야 하 고 올바른 l 되도록 설치 관리자 파일을 편집 해야 합니다 언어 설치 되어 있습니다.

SQL Server 설치 언어와 동일한 R 구성 요소에 사용 되는 언어 식별자 여야 합니다 또는 **다음** 단추가 비활성화 됩니다 하 고 설치를 완료할 수 없습니다.

자세한 내용은 [인터넷에 연결하지 않고 R 구성 요소 설치](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md)를 참조하세요.

## <a name="post-installation-configuration"></a>설치 후 구성

기계 학습에서 Python 또는 R을 사용 하려면 몇 가지 추가 구성이 SQL Server 설치 프로그램을 실행 한 후 필요 합니다. 추가 단계는 서버 및 SQL Server 인스턴스 및 데이터베이스의 보안 수준에 따라 필요할 수 있습니다. 설치 지침에는 추가 구성이 필요할 경우 확인부터 이러한 단계를 검토 합니다.

[Sql Server R Services에서-데이터베이스 설정](set-up-sql-server-r-services-in-database.md)

- Python 또는 R 등의 외부 스크립트를 실행할 수 있도록 지원 하는 기능 데이터베이스 보안을 위해 기본적으로 비활성화 되 고 사용할 수 있어야 합니다.

- Python 또는 R 실행 하려면 실행 패드에서 사용 되는 작업자 계정 인스턴스에 대 한 액세스 권한이 있는지 확인 합니다. [실행 패드 계정 그룹에 대 한 묵시적된 인증을 사용]를 참조 하십시오.

- SQL Server와 인바운드 통신을 허용 하는 방화벽 규칙을 만들거나 서버에서 원격 액세스를 사용 해야 합니다.

- 계획 된 작업 부하에 따라 기계 학습 작업에 대 한 서버를 최적화 하기 위해 할 수 있습니다. 

## <a name="upgrades-or-uninstallation"></a>업그레이드 또는 제거

이 섹션에는 특정 업그레이드 시나리오에 대 한 자세한 지침은 포함 되어 있습니다.

SQL Server 2016 R Services의 시험판 버전에서 업그레이드는 지원 더 이상 사용 되지 않습니다. 제거 하 고 다음 가능한 빨리 릴리스 버전을 설치 하는 것이 좋습니다.

### <a name="support-for-slipstream-upgrades"></a>통합 설치 업그레이드 지원

통합 설치는 실패한 인스턴스 설치에 패치나 업데이트를 적용하여 기존 문제를 해결하는 기능을 말합니다. 이 방법은 설치를 수행할 때 동시에 SQL Server가 업데이트되므로 이후에 별도로 다시 시작할 필요가 없는 장점이 있습니다.

서버가 인터넷에 연결되어 있지 않으면 SQL Server 설치 관리자를 다운로드해야 합니다. 또한 업데이트 프로세스를 시작하기 **전에** R 구성 요소 설치 관리자의 일치하는 버전을 별도로 다운로드해야 합니다. 

다운로드 위치는 [인터넷에 연결하지 않고 R 구성 요소 설치](installing-ml-components-without-internet-access.md)를 참조하세요.

모든 설치 파일이 로컬 디렉터리로 복사되면 명령줄에서 SETUP.EXE를 입력하여 설치 유틸리티를 시작합니다.

- */UPDATESOURCE* 인수를 사용하여 누적 업데이트 또는 서비스 팩 릴리스와 같은 SQL Server 업데이트가 포함된 로컬 파일의 위치를 지정합니다.

- */MRCACHEDIRECTORY* 인수를 사용하여 R 구성 요소 CAB 파일이 포함된 폴더를 지정합니다.

자세한 내용은 지원 팀이 블로그를 참조 하십시오: [인터넷 액세스가 없는 컴퓨터에 R 서비스 배포](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)

### <a name="upgrading-r-components-offline"></a>R 구성 요소를 오프 라인으로 업그레이드

인터넷에 연결되지 않은 서버를 설치하거나 업그레이드하는 경우 새로 고침을 시작하기 전에 업데이트된 버전의 R 구성 요소를 수동으로 다운로드해야 합니다. 자세한 내용은 [인터넷에 연결하지 않고 R 구성 요소 설치](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md)를 참조하세요.

### <a name="schedule-for-update-of-r-components"></a>R 구성 요소 업데이트에 대 한 일정

핫픽스 또는 SQL Server 2016의 향상 된 기능 출시 되 면 R 구성 요소 업그레이드 되었거나 인스턴스에 R 서비스 기능을 이미 포함 하는 경우도 새로 고쳐집니다.

SQL Server 2017을 사용 하는 R 구성 요소에 대 한 업그레이드 자동으로 설치 됩니다.

2016 년 12 월을 기준으로 것도 가능 R 구성 요소를 업그레이드 하는 SQL Server 릴리스 주기 보다 더 빠른 주기로 여 *바인딩* 최신 소프트웨어 수명 주기 정책에 R Services의 인스턴스. 현재 지원은 2016 인스턴스를 업그레이드에 대해서만 제공 됩니다. 그러나 새 버전의 R Server를 놓을 때에 업그레이드 된 2017 인스턴스를 수 있습니다.

자세한 내용은 [SqlBindR을 사용하여 SQL Server R Services 인스턴스 업그레이드](../../advanced-analytics/r-services/use-sqlbindr-exe-to-upgrade-an-instance-of-r-services.md)를 참조하세요.

### <a name="upgrading-from-a-pre-release-version-of-sql-server-2016"></a>SQL Server 2016의 시험판 버전에서 업그레이드

일반적으로 전체 업그레이드는 시험판 버전에 대 한 지원 되지 않습니다.

이전 버전을 제거 해야 R 서비스를 성공적으로 설치 하려면 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 및 관련된 R 구성 요소, SQL Server 2016 CTP3, CTP3.1, c t p 3.2, RC0 또는 r c 1을 포함 합니다.

복잡 한 수 있고; 특수 스크립트를 실행 해야 시험판 버전의 제거 기술 지원에 문의 하는 것이 좋습니다.

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

이 섹션에서는 SQL Server 2016 설치 프로그램을 사용 하 여 Microsoft R server (독립 실행형) 설치와 관련 된 문제를 설명 합니다. R 서버 업그레이드와 관련 된 일반적인 문제에 대 한 MSDN 사이트를 참조 하세요. [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/)합니다.

#### <a name="failure-to-install-localized-versions"></a>지역화 된 버전 설치 실패

오프 라인 수행 R server를 설치 하는 경우 시험판 버전 하지 못하게 지역화 된 언어를 사용할 수 있습니다.

일반적으로 서버 설치 프로그램을 실행 하기 전에 인터넷 액세스가 없는 경우 R 서버에 대 한 모든 설치 패키지 다운로드를 설치 하는 동안 파일의 위치를 지정 합니다.

그러나 언어 식별자와 관련 된 설치 관리자 패키지 없으면 SQL Server 설치 언어와 동일한 R 구성 요소 설치에 대 한 페이지에 도달 하면는 **다음** 단추가 비활성화 되 고 계속할 수 없습니다는 설치 합니다. 이 문제를 해결 일치 하는 식별자를 사용 하려면 패키지 이름을 바꿀 수 있습니다.

예를 들어, 설치 패키지의 이름 수 있습니다 `SRO_3.2.2.0_1031.cab`합니다.
SQL Server에서 104 언어를 설치 하려면 파일을 이름 `SRO_3.2.2.0_1041.cab`합니다.

#### <a name="installing-r-services-and-r-server-standalone-on-the-same-computer"></a>R 서비스와 동일한 컴퓨터에 R Server 독립 실행형 설치

일반적으로 동일한 컴퓨터에 R Services (In-database)와 R Server (독립 실행형)를 설치 하지 좋습니다. 그러나 서버에 충분 한 용량이 있으면 서버 독립 실행형 R 개발 도구로 유용할 수 있습니다. R 서버의 화 기능을 사용 하 고 데이터 이동 없이 R 서버에서 SQL Server 데이터 액세스를 할 수도 있습니다.

동일한 컴퓨터에 R 서버와 R Services를 설치 하는 경우 두 개의 별도 동일한 R 라이브러리 집합이 설치 되어 있는지 확인:에서 SQL server 인스턴스를 사용 하기 위해 각각와 개발에 사용 하거나 R 서버에서 사용 합니다.

SQL Server 2016의 이전 버전에서 동시에 R Server (독립 실행형)와 R Services (In-database) 설치 "액세스 거부" 메시지와 함께 오류가 발생할 수 있습니다. 이 문제는 SQL Server 2016 용 서비스 팩 1에서 수정 되었습니다.

이 오류가 발생 했습니다. 이러한 기능을 업그레이드 해야 하는 경우에 s p 1의 SQL Server 2016의 통합 설치를 수행 하는 것이 좋습니다. 기능을 모두 제거 해야 하 고 다시 설치는 문제를 해결 하는 방법은 두 가지가 있습니다.

1. R Services (In-database)를 제거 하 고 SQLRUserGroup에 대 한 사용자 계정을 제거 되 고 있는지 확인 합니다.

2. 서버를 다시 다음 R Server (독립 실행형)를 다시 설치 하십시오.

3. SQL Server를 실행된, 한 번 설정 하 고이 시간 선택 **기존 SQL Server에 기능 추가**합니다.

4. 인스턴스를 선택 하 고 다음 선택에서 **R Services (In-database)** 추가 하는 옵션입니다.

경우에 따라 실패 한 이전 설치를 정리 하기 위해이 절차가 실패 합니다. 이 경우 해야 제거한 다시 설치 하면 다음과 같습니다.

1. 동시에 R Services (In-database) 및 R Server (독립 실행형)를 제거 합니다.

2. 로컬 사용자 계정 (SQLRUserGroup)를 제거 합니다.

3. 서버를 다시 시작합니다.

4. SQL Server 설치 프로그램을 실행 하 고 전용 R Services (In-database) 기능을 추가 합니다. 선택 하지 않으면 **R Server (독립 실행형)**합니다.

## <a name="see-also"></a>관련 항목:

 [SQL Server R Services 시작](../r/getting-started-with-sql-server-r-services.md)

 [Microsoft R Server 독립 실행형 시작](../r/getting-started-with-microsoft-r-server-standalone.md)


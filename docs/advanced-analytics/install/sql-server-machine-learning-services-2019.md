---
title: Windows에 대한 격리 변경 내용
description: 이 문서에서는 Windows의 SQL Server 2019에서 사용되는 Machine Learning Services의 격리 메커니즘 변경 내용을 설명합니다. 이러한 변경 내용은 SQLRUserGroup, 방화벽 규칙, 파일 사용 권한 및 묵시적 인증에 영향을 줍니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4fae460e78682263c604d8e1e86ca40b7b62df97
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69531042"
---
# <a name="sql-server-2019-on-windows-isolation-changes-for-machine-learning-services"></a>Windows의 SQL Server 2019: Machine Learning Services에 대한 격리 변경 내용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 Windows의 SQL Server 2019에서 사용되는 Machine Learning Services의 격리 메커니즘 변경 내용을 설명합니다. 이러한 변경 내용은 **SQLRUserGroup**, 방화벽 규칙, 파일 사용 권한 및 묵시적 인증에 영향을 줍니다.

자세한 내용은 [Windows에 SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md) 설치 방법을 참조하세요.

## <a name="changes-to-isolation-mechanism"></a>격리 메커니즘의 변경 내용

Windows에서 SQL Server 2019 설치 프로그램은 외부 프로세스에 대한 격리 메커니즘을 변경합니다. 이 변경 내용은 로컬 작업자 계정을 Windows에서 실행되는 클라이언트 애플리케이션에 대한 격리 기술인 [AppContainer](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)로 바꿉니다. 

이러한 수정 때문에 관리자가 구체적으로 수행할 작업 항목은 없습니다. 새 서버 또는 업그레이드된 서버에서 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)로부터 실행되는 모든 외부 스크립트와 코드는 자동으로 새 격리 모델을 따릅니다. 

요약하자면, 이 릴리스의 주요 차이점은 다음과 같습니다.

+ **SQL 제한된 사용자 그룹(SQLRUserGroup)** 의 로컬 사용자 계정은 더 이상 외부 프로세스를 실행하기 위해 생성되거나 사용되지 않습니다. AppContainer가 이를 대신합니다.
+ **SQLRUserGroup** 멤버 자격이 변경되었습니다. 멤버 자격은 여러 로컬 사용자 계정 대신, SQL Server 실행 패드 서비스 계정으로만 구성됩니다. R 및 Python 프로세스는 이제 AppContainer를 통해 격리된 실행 패드 서비스 ID에서 실행됩니다.

격리 모델이 변경되었지만 설치 마법사와 명령줄 매개 변수는 SQL Server 2019에서 동일하게 유지됩니다. 설치 지원이 필요한 경우 [SQL Server Machine Learning Services 설치](sql-machine-learning-services-windows-install.md)를 참조하세요.

## <a name="about-appcontainer-isolation"></a>AppContainer 격리 정보

이전 릴리스의 **SQLRUserGroup**에는 외부 프로세스를 격리하고 실행하는 데 사용되는 로컬 Windows 사용자 계정(MSSQLSERVER00-MSSQLSERVER20) 풀이 포함되어 있습니다. 외부 프로세스가 필요한 경우 SQL Server 실행 패드 서비스는 사용 가능한 계정을 가져와 프로세스를 실행하는 데 사용합니다. 

SQL Server 2019에서 설치 프로그램은 더 이상 로컬 작업자 계정을 생성하지 않습니다. 대신 [AppContainer](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)를 통해 격리가 진행됩니다. 런타임에 저장 프로시저 또는 쿼리에서 포함된 스크립트나 코드가 감지되면 SQL Server는 확장별 시작 관리자를 요청하여 실행 패드를 호출합니다. 실행 패드는 해당 ID를 사용해 프로세스에서 적절한 런타임 환경을 호출하고, 이를 포함할 AppContainer를 인스턴스화합니다. 이러한 변경은 로컬 계정 및 암호 관리가 더 이상 필요하지 않기 때문에 유용합니다. 또한 로컬 사용자 계정이 금지된 설치에서 로컬 사용자 계정 종속성을 제거하면 이 기능을 사용할 수 있습니다.

SQL Server에서 구현되므로 AppContainer는 내부 메커니즘입니다. 프로세스 모니터에서 AppContainer의 물리적 증거는 표시되지 않지만 설치 프로그램에서 프로세스의 네트워크 호출 수행을 방지하기 위해 만든 아웃바운드 방화벽 규칙에 표시될 수 있습니다.

## <a name="firewall-rules-created-by-setup"></a>설치 프로그램에서 만든 방화벽 규칙

기본적으로 SQL Server는 방화벽 규칙을 만들어 아웃바운드 연결을 사용하지 않도록 설정합니다. 이전에는 이러한 규칙이 로컬 사용자 계정을 기준으로 했습니다. 이 경우 설치 프로그램은 해당 멤버에 대한 네트워크 액세스를 거부하는 **SQLRUserGroup**에 대한 아웃바운드 규칙을 하나 만들었습니다(각 작업자 계정은 rule_에 적용되는 로컬 주체로 나열됨). 

AppContainer로 전환하는 과정에서 AppContainer SID를 기준으로 새로운 방화벽 규칙이 생성되었습니다. 각 규칙은 SQL Server 설치 프로그램에서 만든 20개의 AppContainer 각각에 해당합니다. 방화벽 규칙 이름에 대한 명명 규칙은 **SQL Server 인스턴스 MSSQLSERVER에서 AppContainer-00에 대한 네트워크 액세스 차단**입니다. 여기서 00은 AppContainer의 번호(기본적으로 00-20)이고 MSSQLSERVER는 SQL Server 인스턴스의 이름입니다. 

> [!Note]
> 네트워크 호출이 필요한 경우 Windows 방화벽에서 아웃바운드 규칙을 사용하지 않도록 설정할 수 있습니다.

## <a name="program-file-permissions"></a>프로그램 파일 사용 권한

이전 릴리스와 마찬가지로 **SQLRUserGroup**은 SQL Server **Binn**, **R_SERVICES**및 **PYTHON_SERVICES** 디렉터리의 실행 파일에 대해 읽기 및 실행 권한을 계속 제공합니다. 이 릴리스에서는 **SQLRUserGroup**의 멤버가 SQL Server 실행 패드 서비스 계정 뿐입니다.  실행 패드 서비스가 R 또는 Python 실행 환경을 시작하면 프로세스는 실행 패드 서비스로 실행됩니다.

## <a name="implied-authentication"></a>암시적 인증

이전처럼, 스크립트나 코드에서 신뢰할 수 있는 인증을 사용하여 데이터 또는 리소스를 검색하기 위해 SQL Server에 다시 연결해야 하는 *암시적 인증*에는 여전히 추가 구성이 필요합니다. 추가 구성에는 **SQLRUserGroup**에 대한 데이터베이스 로그인을 만드는 작업이 포함되며, 이에 대한 유일한 멤버는 여러 작업자 계정 대신, 단일 SQL Server 실행 패드 서비스 계정입니다. 이 태스크에 대한 자세한 내용은 [SQLRUserGroup을 데이터베이스 사용자로 추가](../security/create-a-login-for-sqlrusergroup.md)를 참조하세요.


## <a name="symbolic-link-created-by-setup"></a>설치 프로그램에서 만든 심볼 링크

심볼 링크는 SQL Server 설치 프로그램의 일부로 현재 기본 **R_SERVICES** 및 **PYTHON_SERVICES**에 생성됩니다. 이 링크를 만들지 않으려는 경우에는 대신, 해당 폴더까지의 계층 구조에 대한 읽기 권한을 '모든 애플리케이션 패키지'에 부여하는 것이 좋습니다.


## <a name="see-also"></a>관련 항목:

+ [Windows에서 SQL Server Machine Learning Services 설치](sql-machine-learning-services-windows-install.md)
+ [Linux에서 SQL Server Machine Learning Services 설치](../../linux/sql-server-linux-setup-machine-learning.md)

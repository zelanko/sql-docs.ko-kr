---
title: SQL Server 2019의 차이점
description: SQL Server 2019 preview 릴리스에서 SQL Server machine learning 확장의 R 및 Python에 대 한 새로운 기능을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8996d47c58841f668813c8ff344683150e456fb3
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345001"
---
# <a name="differences-in-sql-server-machine-learning-services-installation-in-sql-server-2019"></a>SQL Server 2019의 SQL Server Machine Learning Services 설치의 차이점  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Windows에서 SQL Server 2019 설치 프로그램은 외부 프로세스에 대 한 격리 메커니즘을 변경 합니다. 이 변경 내용은 Windows에서 실행 되는 클라이언트 응용 프로그램에 대 한 격리 기술인 로컬 작업자 계정을 [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)으로 바꿉니다. 

수정의 결과로 관리자에 대 한 특정 작업 항목이 없습니다. 새 서버 또는 업그레이드 된 서버에서 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 에서 실행 되는 모든 외부 스크립트와 코드는 새 격리 모델을 자동으로 따릅니다. 

요약 하자면,이 릴리스의 주요 차이점은 다음과 같습니다.

+ **SQL 제한 된 사용자 그룹 (SQLRUserGroup)** 의 로컬 사용자 계정은 더 이상 생성 되거나 외부 프로세스를 실행 하는 데 사용 되지 않습니다. AppContainers를 바꿉니다.
+ **SQLRUserGroup** 멤버 자격이 변경 되었습니다. 멤버 자격은 여러 로컬 사용자 계정 대신 SQL Server 실행 패드 서비스 계정 으로만 구성 됩니다. R 및 Python 프로세스는 이제 AppContainers를 통해 격리 된 실행 패드 서비스 id로 실행 됩니다.

격리 모델이 변경 되었지만 설치 마법사와 명령줄 매개 변수는 SQL Server 2019에서 동일 하 게 유지 됩니다. 설치에 대 한 도움말은 [SQL Server Machine Learning Services 설치](sql-machine-learning-services-windows-install.md)를 참조 하세요.

## <a name="about-appcontainer-isolation"></a>AppContainer 격리 정보

이전 릴리스에서 **SQLRUserGroup** 에는 외부 프로세스를 분리 하 고 실행 하는 데 사용 되는 로컬 Windows 사용자 계정 (MSSQLSERVER00-MSSQLSERVER20)의 풀이 포함 되어 있습니다. 외부 프로세스가 필요한 경우 SQL Server 실행 패드 서비스는 사용 가능한 계정을 가져와 프로세스를 실행 하는 데 사용 합니다. 

SQL Server 2019에서 설치 프로그램은 더 이상 로컬 작업자 계정을 생성 하지 않습니다. 대신 [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)를 통해 격리 됩니다. 런타임에 저장 프로시저 또는 쿼리에서 포함 된 스크립트나 코드가 검색 되 면 확장 프로그램에 대 한 요청에 대 한 요청으로 실행 패드를 호출 SQL Server 합니다. 실행 패드는 해당 id로 프로세스에서 적절 한 런타임 환경을 호출 하 고,이를 포함 하는 AppContainer를 인스턴스화합니다. 이러한 변경은 로컬 계정 및 암호 관리가 더 이상 필요 하지 않기 때문에 유용 합니다. 또한 로컬 사용자 계정이 금지 된 설치에서 로컬 사용자 계정 종속성을 제거 하면이 기능을 사용할 수 있습니다.

SQL Server에 의해 구현 되는 AppContainers는 내부 메커니즘입니다. 프로세스 모니터에 AppContainers의 물리적 증거는 표시 되지 않지만 설치 프로그램에서 만든 아웃 바운드 방화벽 규칙에 따라 프로세스가 네트워크 호출을 수행 하지 못하게 할 수 있습니다.

## <a name="firewall-rules-created-by-setup"></a>설치 프로그램에서 만든 방화벽 규칙

기본적으로 SQL Server는 방화벽 규칙을 만들어 아웃 바운드 연결을 사용 하지 않도록 설정 합니다. 이전에 이러한 규칙은 로컬 사용자 계정을 기반으로 하며,이 규칙은 설치 프로그램에서 해당 멤버에 대 한 네트워크 액세스를 거부 한 **SQLRUserGroup** 에 대 한 아웃 바운드 규칙 하나를 만들었습니다 (각 작업자 계정은 rule_에 적용 되는 로컬 주체로 나열 됨). 

AppContainers로 이동 하는 과정의 일환으로, AppContainer Sid를 기반으로 하는 새 방화벽 규칙이 있습니다. 하나는 SQL Server 설치 프로그램에서 만든 20 AppContainers 각각에 해당 합니다. 방화벽 규칙 이름에 대 한 명명 규칙은 **SQL Server 인스턴스 MSSQLSERVER의 appcontainer-00에 대 한 네트워크 액세스를 차단**합니다. 여기서 00은 appcontainer의 수 (00-20)입니다. MSSQLSERVER는 SQL Server 인스턴스의 이름입니다. 

> [!Note]
> 네트워크 호출이 필요한 경우 Windows 방화벽에서 아웃 바운드 규칙을 사용 하지 않도록 설정할 수 있습니다.

## <a name="program-file-permissions"></a>프로그램 파일 사용 권한

이전 릴리스와 마찬가지로 **SQLRUserGroup** 는 SQL Server **Binn**, **R_SERVICES**및 **PYTHON_SERVICES** 디렉터리의 실행 파일에 대 한 읽기 및 실행 권한을 계속 제공 합니다. 이 릴리스에서는 **SQLRUserGroup** 의 유일한 멤버가 SQL Server 실행 패드 서비스 계정입니다.  실행 패드 서비스에서 R 또는 Python 실행 환경을 시작할 때 프로세스가 실행 패드 서비스로 실행 됩니다.

## <a name="implied-authentication"></a>암시적 인증

이전 처럼 스크립트나 코드에서 신뢰할 수 있는 인증을 사용 하 여 데이터 나 리소스를 검색 하는 SQL Server에 다시 연결 해야 하는 경우에는 *묵시적 인증* 에 대 한 추가 구성이 필요 합니다. 추가 구성에는 **SQLRUserGroup**에 대 한 데이터베이스 로그인을 만드는 작업이 포함 됩니다. 여기에는 단일 구성원이 여러 작업자 계정 대신 단일 SQL Server 실행 패드 서비스 계정입니다. 이 태스크에 대 한 자세한 내용은 [SQLRUserGroup를 데이터베이스 사용자로 추가](../security/create-a-login-for-sqlrusergroup.md)를 참조 하세요.


## <a name="symbolic-link-created-by-setup"></a>설치 프로그램에서 만든 기호화 된 링크

기호화 된 링크가 SQL Server 설정의 일부로 현재 기본 **R_SERVICES** 및 **PYTHON_SERVICES** 에 만들어집니다. 이 링크를 만들지 않으려는 경우에는 폴더에 대 한 계층 구조에 ' 모든 응용 프로그램 패키지 ' 읽기 권한을 부여 하는 것이 좋습니다.


## <a name="see-also"></a>참조

+ [Windows에 SQL Server Machine Learning Services 설치](sql-machine-learning-services-windows-install.md)

+ [Linux에 SQL Server 2019 Machine Learning Services 설치](../../linux/sql-server-linux-setup-machine-learning.md)

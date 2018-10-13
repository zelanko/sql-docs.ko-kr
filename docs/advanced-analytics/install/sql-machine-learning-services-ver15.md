---
title: SQL Server 2019 Machine Learning Services 설치의 차이점 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/08/2018
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2bd03c4c1dfb019238785b5284b4cceffc95c3a2
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48878156"
---
# <a name="differences-in-sql-server-machine-learning-services-installation-in-sql-server-2019"></a>SQL Server 2019에 SQL Server Machine Learning Services 설치의 차이점  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Windows, SQL Server 2019 설치 외부 프로세스에 대 한 격리 메커니즘을 변경합니다. 이 변경은 로컬 작업자 계정을 사용 하 여 대체 [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation), 클라이언트 응용 프로그램의 Windows에서 실행 되는 격리 기술 합니다. 

수정 결과로 관리자에 대 한 특정 작업 항목이 없습니다. 새 패키지나 업그레이드 된 서버, 모든 외부 스크립트 및 코드에서 실행할 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 새 격리 모델을 자동으로 따릅니다. 이 R, Python 및 SQL Server 2019에 도입 된 새 Java 언어 확장에 적용 됩니다.

이 릴리스의 주요 차이점은 요약:

+ 로컬 사용자 계정 **SQL 제한 된 사용자 그룹 (SQLRUserGroup)** 는 더 이상 만들거나 외부 프로세스를 실행 하는 데 사용 됩니다. AppContainers 바꿔야 합니다.
+ **SQLRUserGroup** 멤버 자격 변경 되었습니다. 여러 로컬 사용자 계정 대신 멤버 자격만 SQL Server 실행 패드 서비스 계정으로 구성 됩니다. 이제 R, Python 및 Java 프로세스 격리 AppContainers 통해 실행 패드 서비스 id로 실행 합니다.

격리 모델을 변경 하지만 설치 마법사 및 명령줄 매개 변수를 SQL Server 2019에 동일 하 게 유지 합니다. 설치 도움말을 참조 하세요 [SQL Server Machine Learning Services 설치](sql-machine-learning-services-windows-install.md)합니다.

## <a name="about-appcontainer-isolation"></a>AppContainer 격리에 대 한

이전 릴리스에서 **SQLRUserGroup** 로컬 Windows 사용자 계정 (MSSQLSERVER00 MSSQLSERVER20)는 격리 및 실행 중인 외부 프로세스에 사용 되는 하나의 풀을 포함 합니다. 외부 프로세스 필요 했습니다 SQL Server 실행 패드 서비스는 사용할 수 있는 계정 수행 하 고 사용 하 여 프로세스를 실행 합니다. 

설치 프로그램은 SQL Server 2019에 더 이상 로컬 작업자 계정을 만듭니다. 격리를 통해 구현 되는 대신 [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)합니다. 런타임에 포함 된 스크립트 또는 코드 감지 되 면 저장된 프로시저 또는 쿼리를 SQL Server는 요청을 사용 하 여 실행 패드는 확장 프로그램별 시작 관리자에 대 한 호출 합니다. 실행 패드는 해당 id로 프로세스에서 적절 한 런타임 환경을 호출 하 고 포함 하기 위해 AppContainer를 인스턴스화합니다. 이 변경은 로컬 계정 및 암호 관리는 더 이상 필요 하기 때문에 유용 합니다. 또한 로컬 사용자 계정을 사용할 수 없습니다는 설치 시 로컬 사용자 계정 종속성 제거 의미이 기능을 이제 사용할 수 있습니다.

SQL Server에 의해 구현 된 대로 AppContainers는는 내부 메커니즘입니다. 실제 증빙 AppContainers 프로세스 모니터에 표시 되지 않습니다, 하지만 프로세스가 네트워크 호출을 수행 하지 못하게 하기 위해 설치 프로그램에서 생성 된 아웃 바운드 방화벽 규칙에서 찾을 수 있습니다.

## <a name="firewall-rules-created-by-setup"></a>설치 프로그램에서 만든 방화벽 규칙

기본적으로 SQL Server 방화벽 규칙을 만들어 아웃 바운드 연결을 해제 합니다. 이전에 이러한 규칙 설정에 대 한 아웃 바운드 규칙이 만들어진 로컬 사용자 계정에 기반한 **SQLRUserGroup** 해당 멤버에 대 한 네트워크 액세스를 거부 하는 (각 작업자 계정은 rule_ 적용 로컬 원칙으로 나열 되었습니다. 

AppContainers 이동의 일부로, 가지 AppContainer Sid에 따라 새 방화벽 규칙: SQL Server 설치 프로그램을 만들어 각각 20 AppContainers에 대 한 합니다. 방화벽 규칙 이름에 대 한 명명 규칙이 **SQL Server 인스턴스 MSSQLSERVER의에서 AppContainer 00에 대 한 네트워크 액세스를 차단**, 여기서 00입니다 (00-20 기본적으로)을 AppContainer 및 SQL의 이름인 MSSQLSERVER 서버 인스턴스입니다. 

> [!Note]
> 네트워크 호출이 필요한 경우에 Windows 방화벽의 아웃 바운드 규칙을 비활성화할 수 있습니다.

## <a name="program-file-permissions"></a>프로그램 파일 사용 권한

이전 릴리스와 마찬가지로 합니다 **SQLRUserGroup** 읽기를 제공 하 고 SQL Server에서 실행 파일에 대 한 실행을 계속 **Binn**합니다 **R_SERVICES**, 및  **PYTHON_SERVICES** 디렉터리입니다. 이 릴리스에서 유일한 구성원 **SQLRUserGroup** SQL Server 실행 패드 서비스 계정입니다.  실행 패드 서비스에는 R, Python 또는 Java 실행 환경을 시작 되 면 프로세스는 실행 패드 서비스로 실행 됩니다.

## <a name="implied-authentication"></a>암시적 인증

추가 구성은 여전히 필요 이전 처럼 *묵시적된 인증* 신뢰할 수 있는 인증을 사용 하 여 데이터 또는 리소스를 검색 하는 SQL Server에 다시 연결 하는 스크립트나 코드에 있는 경우에서. 추가 구성에 대 한 데이터베이스 로그인을 만들어야 **SQLRUserGroup**, 유일한 멤버를 가진 여러 작업자 계정 대신 단일 SQL Server 실행 패드 서비스 계정이 됩니다. 이 태스크에 대 한 자세한 내용은 참조 하세요. [SQLRUserGroup을 데이터베이스 사용자로 추가](../security/add-sqlrusergroup-to-database.md)합니다.


## <a name="symbolic-link-created-by-setup"></a>설치 프로그램에서 생성 하는 기호화 된 링크

기호화 된 링크를 현재 기본값으로 만들어집니다 **R_SERVICES** 하 고 **PYTHON_SERIVCES** SQL Server 설치의 일부로. 이 링크를 만들려면 않으려면 대안 폴더에 이르는 계층에 '모든 응용 프로그램 패키지' 읽기 권한을 부여 하는 것입니다.


## <a name="see-also"></a>참고자료

+ [SQL Server Machine Learning에서 Windows 서비스를 설치 합니다.](sql-machine-learning-services-windows-install.md)

+ [Linux에서 SQL Server 2019 Machine Learning Services 설치](../../linux/sql-server-linux-setup-machine-learning.md)

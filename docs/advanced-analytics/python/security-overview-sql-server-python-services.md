---
title: SQL Server Machine Learning에서 Python에 대 한 보안 개요 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a33701283635327fcaac4a9629cb02044b30dda8
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43890059"
---
# <a name="security-overview-for-python-in-sql-server-machine-learning"></a>SQL Server Machine Learning에서 Python에 대 한 보안 개요
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

연결에 사용 되는 보안 아키텍처에 설명 합니다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 데이터베이스 엔진 및 Python 구성 요소입니다. 두 가지 일반적인 시나리오에 보안 프로세스의 예가 제공 됩니다: 저장된 프로시저를 사용 하 고 원격 계산 컨텍스트를 SQL Server를 사용 하 여 Python을 실행 하는 SQL Server에서 Python을 실행 합니다.

## <a name="security-overview"></a>보안 개요

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 로그인 또는 Windows 사용자 계정이 SQL Server에서 Python 스크립트를 실행 하려면 필요 합니다. 이러한 *보안 주체* 인스턴스 및 데이터베이스 수준에서 관리 됩니다 및 데이터베이스에 연결, 데이터 읽기 및 쓰기, 권한이 있는 사용자를 식별 하거나 테이블 또는 저장된 프로시저와 같은 데이터베이스 개체를 만듭니다. 또한 Python 스크립트를 실행 하는 사용자 데이터베이스 수준에서 외부 스크립트를 실행할 수 있는 권한이 있어야 합니다.

사용자가 Python 코드에서 데이터베이스 또는 access 데이터베이스 개체 및 데이터를 실행 해야 하는 경우에 외부 도구에서 Python을 사용 하는 사용자 로그인 또는 데이터베이스에서 계정에 매핑해야 합니다. Python 스크립트를 원격 데이터 과학 클라이언트에서 보낸 여부는 T-SQL 저장 프로시저를 사용 하 여 시작에 동일한 권한이 필요.

예를 들어 랩톱에서 실행 되는 Python 스크립트를 작성 하 고 코드를 실행 하려는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다. 다음 조건이 충족되는지 확인해야 합니다.

+ 데이터베이스에서 원격 연결을 허용합니다.
+ SQL 로그인 또는 데이터베이스 액세스에 사용 된 Windows 계정에 추가 되었습니다는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스 수준에서.
+ SQL 로그인 또는 Windows 사용자에게 외부 스크립트를 실행할 권한이 부여되어야 합니다. 일반적으로 이 권한은 데이터베이스 관리자만 추가할 수 있습니다.
+ SQL 로그인 또는 Window 사용자는 이러한 작업 중 하나는 Python 스크립트를 수행 하는 각 데이터베이스에서 적절 한 권한이 있는 사용자로 추가 되어야 합니다.
    + 데이터 검색
    + 데이터 쓰기 또는 업데이트
    + 테이블 또는 저장 프로시저 등의 새 개체 만들기

로그인 또는 Windows 사용자 계정을 프로 비전 하 고 필요한 권한이 부여에서 Python 코드를 실행할 수 있습니다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 에서 제공 하는 데이터 원본 개체를 사용 하 여 합니다 **revoscalepy** 라이브러리 또는 저장을 호출 하 여 Python 스크립트를 포함 하는 프로시저입니다.

Python 스크립트를 시작할 때마다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 데이터베이스 엔진 보안 작업을 시작한 사용자 또는 보안 개체에 대 한 로그인의 매핑을 관리 사용자의 보안 컨텍스트를 가져옵니다.

따라서 원격 클라이언트에서 시작 되는 모든 Python 스크립트는 연결 문자열의 일부로 로그인 또는 사용자 정보를 지정 해야 합니다.

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>상호 작용 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 보안 및 실행 패드 보안

Python 스크립트의 컨텍스트에서 실행 되는 시기를 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스 외부 프로세스에 대해 설정할 작업자 계정의 풀에서 사용 가능한 작업자 계정 (로컬 사용자 계정)를 가져오고 해당 작업자 계정을 사용 하 여 관련된 태스크를 수행 합니다.

예를 들어, Windows 도메인 자격 증명에서 Python 스크립트를 시작 합니다. SQL Server 자격 증명을 가져옵니다 및 사용할 수 있는 실행 패드 작업자 계정에는 작업을 같은 매핑합니다 *SQLRUser01*합니다.

> [!NOTE]
> 작업자 계정 그룹의 이름은 R 또는 Python을 사용 중인지 여부에 관계 없이 동일 합니다. 그러나 모든 외부 언어를 활성화 하는 각 인스턴스에 대 한 별도 그룹이 생성 됩니다.

작업 계정에 매핑된 후 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]는 프로세스를 시작하는 데 사용되는 사용자 토큰을 만듭니다. 

모든 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 작업이 완료되면 사용자 작업자 계정은 사용 가능으로 표시되고 풀로 반환됩니다.

서비스에 대 한 자세한 내용은 참조 하세요. [Extensibility framework](../concepts/extensibility-framework.md)합니다.

### <a name="implied-authentication"></a>암시적 인증

**묵시적된 인증** 용어는 SQL Server 사용자를 가져옵니다 프로세스에 대 한 자격 증명 하 고 다음 사용자는 데이터베이스에 대 한 올바른 권한을 가정 하 고 사용자를 대신 하 여 모든 외부 스크립트 작업을 실행 합니다. 묵시적 인증이 Python 스크립트를 SQL Server 데이터베이스 외부 ODBC 호출을 수행 해야 하는 경우에 특히 중요 합니다. 예를 들어, 코드는 스프레드시트 또는 기타 원본의 요인의 짧은 목록을 검색할 수 있습니다.

성공 하려면 이러한 루프백 호출에 대 한 SQLRUserGroup 작업자 계정이 포함 된 그룹에는 "로컬 로그온 허용" 권한이 있어야 합니다. 기본적으로이 권한은 모든 새 로컬 사용자에 게 제공 됩니다 되지만 일부 조직에서는 더 엄격한 그룹 정책이 적용 될 수 있습니다.

![R에 대 한 암시적된 인증](media/implied-auth-python2.png)

## <a name="security-of-worker-accounts"></a>작업자 계정의 보안

외부 Windows 사용자 또는 작업자 계정에 올바른 SQL 로그인의 매핑을 Python 스크립트를 실행 하는 SQL의 수명 동안 저장 프로시저에 대해서만 유효 합니다.

같은 로그인의 병렬 쿼리는 같은 사용자의 작업자 계정에 매핑됩니다.

프로세스에 사용 되는 디렉터리에서 관리 되는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], 및 디렉터리에 대 한 액세스 제한 합니다. Python PythonLauncher이이 작업을 수행합니다. 각 개별 작업자 계정을 자체 폴더로 제한 되 고 자체 수준 상위 폴더의에서 파일에 액세스할 수 없습니다. 그러나 작업자 계정 수 읽기, 쓰기 또는 만들어진 세션 작업 폴더 아래에 자식을 삭제 합니다.

작업자 계정, 계정 이름 또는 계정 암호의 수를 변경 하는 방법에 대 한 자세한 내용은 참조 하세요. [SQL Server machine learning 위한 사용자 계정 풀 수정](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)합니다.


## <a name="security-isolation-for-multiple-external-scripts"></a>여러 외부 스크립트에 대 한 보안 격리

격리 메커니즘은 실제 사용자 계정을 기반으로 합니다. 특정 위성 런타임에 대한 위성 프로세스가 시작될 때 각 위성 태스크는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]에서 지정된 작업자 계정을 사용합니다. 태스크에 여러 위성이 필요한 경우(예: 병렬 쿼리) 모든 관련 태스크에 단일 작업자 계정이 사용됩니다.

작업자 계정은 다른 작업자 계정이 사용하는 파일을 보거나 조작할 수 있습니다.

컴퓨터의 관리자는 각 프로세스에 대해 만들어진 디렉터리를 볼 수 있습니다. 각 디렉터리는 세션 GUID로 식별됩니다.

## <a name="see-also"></a>관련 항목

[아키텍처 개요](../../advanced-analytics/python/architecture-overview-sql-server-python.md)

---
title: R 및 Python 확장-SQL Server Machine Learning에 대 한 보안 개요
description: SQL Server Machine Learning Services의 확장성 프레임 워크에 대 한 보안 개요입니다. 로그인 및 사용자 계정, SQL Server 실행 패드 서비스, 여러 스크립트 및 파일 권한을 실행 하는 작업자 계정에 대 한 보안.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: f9f5552a106d0549aaf3b5e9ae291ebe3b534543
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963049"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services의 확장성 프레임 워크에 대 한 보안 개요

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 확장성 프레임 워크를 사용 하 여 SQL Server 데이터베이스 엔진 및 관련된 구성 요소를 통합 하는 데 사용 되는 전반적인 보안 아키텍처를 설명 합니다. 보안 개체, 서비스, 프로세스 id 및 사용 권한을 검사합니다. 주요 개념 및 SQL Server의 확장성 구성 요소에 대 한 자세한 내용은 참조 하세요. [SQL Server Machine Learning Services의 확장성 아키텍처](extensibility-framework.md)].

## <a name="securables-for-external-script"></a>외부 스크립트에 대 한 보안 개체

R 또는 Python으로 작성 된 외부 스크립트를 입력된 매개 변수로 제출 되는 [시스템 저장 프로시저](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 이 목적을 위해 만들거나 정의 하는 저장된 프로시저에 래핑됩니다. 또는 미리 학습 된 및 T-SQL에서 호출할 수는 데이터베이스 테이블에서 이진 형식으로 저장 된 모델 있을 [PREDICT](../../t-sql/queries/predict-transact-sql.md) 함수입니다.

스크립트는 기존 데이터베이스 스키마 개체, 저장된 프로시저 및 테이블을 통해 제공 된 대로 가지 새 [보안 개체](../../relational-databases/security/securables.md) SQL Server Machine Learning Services에 대 한 합니다.

스크립트를 사용 하는 방법 또는 무엇으로 구성 됩니다에 관계 없이 데이터베이스 개체 생성 되 고 아마도 저장 되지만 스크립트를 저장 하기 위한 도입 된 새 개체 유형이 없습니다. 결과적으로,를 사용 하는 기능을 만들고 데이터베이스 사용 권한을 사용자에 대해 이미 정의에 크게 종속 개체 데이터베이스 저장 합니다.

<a name="permissions"></a>

## <a name="permissions"></a>사용 권한

데이터베이스 로그인 및 역할의 데이터 보안 모델을 SQL Server의 R 및 Python 스크립트를 확장 합니다. SQL Server 로그인 또는 Windows 사용자 계정을 사용 하는 SQL Server 데이터 또는 SQL Server 계산 컨텍스트를 사용 하 여 실행 되는 외부 스크립트를 실행 하려면 필요 합니다. 임시 쿼리를 실행 하는 권한을 가진 데이터베이스 사용자는 R 또는 Python 스크립트에서 동일한 데이터를 액세스할 수 있습니다.

로그인 또는 사용자 계정을 식별 하는 *보안 주체*, 여러 수준의 외부 스크립트 요구 사항에 따라 액세스 해야 할 수 있는 사용자:

+ 외부 스크립트는 사용할 수 있는 데이터베이스에 액세스할 수 있는 권한입니다.
+ 테이블과 같은 보안된 개체에서 데이터를 읽을 권한입니다.
+ 모델 또는 점수 매기기 결과 같은 테이블에 새 데이터를 쓸 수 있습니다.
+ 테이블과 같은 새 개체를 만들 수는 저장 프로시저 외부 스크립트를 사용 하거나 사용자 지정 함수를 사용 하 여 R 또는 Python 작업 합니다.
+ SQL Server 컴퓨터의 새 패키지를 설치 하거나 사용자 그룹에 제공 하는 패키지를 사용 하 여 권한입니다.

SQL Server를 사용 하 여 실행 컨텍스트로 외부 스크립트를 실행 하는 각 사용자 데이터베이스의 사용자를 매핑해야 합니다. 대신 개별적으로 데이터베이스 사용자 권한 설정, 사용 권한 집합을 관리 및 이러한 역할에 사용자를 할당 하지 않고 개별적으로 설정 된 사용자 권한 역할을 만들 수 있습니다.

자세한 내용은 [SQL Server Machine Learning Services 하도록 사용자 권한 부여](../../advanced-analytics/security/user-permission.md)합니다.

## <a name="permissions-when-using-an-external-client-tool"></a>외부 클라이언트 도구를 사용 하는 경우 사용 권한

외부 클라이언트 도구를에서 R 또는 Python을 사용 하는 사용자가 로그인 또는 외부 스크립트에서 데이터베이스 또는 access 데이터베이스 개체 및 데이터를 실행 하는 경우 사용자 데이터베이스에 매핑된 계정이 있어야 합니다. 권한인을 필수 원격 데이터 과학 클라이언트에서 외부 스크립트를 전송 하는 여부 또는 T-SQL 저장 프로시저를 사용 하 여 실행 합니다.

SQL Server에서 해당 스크립트를 실행 하려는 고 예를 들어, 로컬 컴퓨터에서 실행 되는 외부 스크립트를 만든를 가정 합니다. 다음 조건이 충족되는지 확인해야 합니다.

+ 데이터베이스에서 원격 연결을 허용합니다.
+ SQL 로그인 또는 데이터베이스 액세스에 사용 된 Windows 계정 인스턴스 수준에서 SQL Server에 추가 되었습니다.
+ SQL 로그인 또는 Windows 사용자를 외부 스크립트를 실행할 권한이 있어야 합니다. 일반적으로 이 권한은 데이터베이스 관리자만 추가할 수 있습니다.
+ SQL 로그인 또는 Window 사용자는 이러한 작업의 외부 스크립트를 수행 하는 각 데이터베이스에서 적절 한 권한이 있는 사용자로 추가 되어야 합니다.
  + 데이터를 검색합니다.
  + 데이터 쓰기 또는 업데이트 합니다.
  + 테이블 또는 저장된 프로시저 등의 새 개체를 만드는 중입니다.

로그인 또는 Windows 사용자 계정을 프로 비전 하 고 필요한 권한이 부여, 있습니다 수 외부 스크립트를 SQL Server에서 실행 R에서 데이터 원본 개체를 사용 하 여 또는 **revoscalepy** Python 또는 저장을 호출 하 여 라이브러리 외부 스크립트를 포함 하는 프로시저입니다.

외부 스크립트를 SQL Server에서 시작 될 때마다 데이터베이스 엔진 보안 작업을 시작한 사용자 또는 보안 개체에 대 한 로그인의 매핑을 관리 사용자의 보안 컨텍스트를 가져옵니다.

따라서 연결 문자열의 일부로 원격 클라이언트에서 시작 되는 모든 외부 스크립트의 로그인 또는 사용자 정보를 지정 해야 합니다.

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>외부 처리 (실행 패드)에 사용 된 서비스

하나의 새 NT 서비스를 추가 하는 확장성 프레임 워크를 [서비스 목록을](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details) SQL Server 설치에서: [**SQL Server 실행 패드 (MSSSQLSERVER)** ](extensibility-framework.md#launchpad)합니다.

데이터베이스 엔진이 별도 프로세스로 R 또는 Python 세션을 인스턴스화하기 위해 SQL Server 실행 패드 서비스를 사용 합니다. 낮은 권한 계정을; 프로세스 실행 SQL Server, 자체 실행 패드 및 저장된 프로시저 또는 호스트 쿼리가 실행 되는 사용자 id에서 고유 합니다. 낮은 권한 계정으로 별도 프로세스에서 스크립트를 실행 중인 R 및 Python에서 SQL Server에 대 한 보안 및 격리 모델의 기반이 됩니다.

외부 프로세스를 시작 하는 것 외에도 실행 패드 프로세스를 시작 하는 데 사용 하는 권한이 낮은 작업자 계정에 해당 id를 매핑 및 호출 하는 사용자의 id를 추적 하는 일을 담당 이기도 합니다. 일부 시나리오에서는 스크립트 또는 코드 호출 하는 경우 다시 SQL server 데이터 및 작업, 실행 패드는 일반적으로 identity 전송을 원활 하 게 관리할 수 있습니다. 스크립트 함수 및 다른 프로그래밍 개체 호출 또는 SELECT 문을 포함 하는 호출 사용자에 게 충분 한 권한이 있는 경우에 일반적으로 성공할 수 있습니다.

> [!NOTE]
> 기본적으로 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 에서 실행 되도록 구성 됩니다 **NT Service\MSSQLLaunchpad**는 외부 스크립트를 실행 하는 데 필요한 모든 권한이 프로 비전 됩니다. 구성 가능한 옵션에 대 한 자세한 내용은 참조 하세요. [SQL Server 실행 패드 서비스 구성을](../security/sql-server-launchpad-service-account.md)합니다.

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>(SQLRUserGroup) 처리에 사용 되는 id

**SQLRUserGroup** (SQL 제한 된 사용자 그룹)는 SQL Server 설치 프로그램에서 만들어지고 낮은 권한 로컬 Windows 사용자 계정 풀을 포함 합니다. 외부 프로세스에 필요한 경우 실행 패드 사용 가능한 작업자 계정을 사용 하 고 프로세스를 실행 하는 데 사용 합니다. 보다 구체적으로, 실행 패드 사용 가능한 작업자 계정을 활성화 하는 호출 하는 사용자의 id로 매핑합니다 및 작업자 계정으로 스크립트를 실행 합니다.

+ **SQLRUserGroup** 특정 인스턴스에 연결 됩니다. 컴퓨터에 학습에 사용 하도록 설정한 각 인스턴스에 대 한 별도 풀 작업자 계정에 필요 합니다. 인스턴스 간에 계정을 공유할 수 없습니다.

+ 사용자 계정 풀의 크기에는 정적 이며 기본값은 20 이며, 20 동시 세션을 지. 이 사용자 계정 풀의 크기에 따라 동시에 시작할 수 있는 외부 런타임 세션 수가 제한 됩니다. 

+ 풀의 작업자 계정 이름은 sqlinstancename 가지*nn*합니다. 기본 인스턴스의 경우에 예를 들어 **SQLRUserGroup** MSSQLSERVER01, MSSQLSERVER02 등과에서 MSSQLSERVER20 최대 명명 된 계정을 포함 합니다.

병렬화 된 작업에 추가 계정을 사용 하지 않습니다. 예를 들어 사용자가 병렬 처리를 사용 하는 점수 매기기 작업을 실행 하는 경우 모든 스레드에 대해 같은 작업자 계정이 재사용 됩니다. Machine learning의 과도 한 사용 하려는 경우에 외부 스크립트를 실행 하는 데 사용 되는 계정의 수를 늘릴 수 있습니다. 자세한 내용은 [machine learning 위한 사용자 계정 풀 수정](../../advanced-analytics/administration/modify-user-account-pool.md)합니다.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>SQL Server 2019 AppContainer 격리

SQL Server 2019에서 설치 프로그램에서는 더 이상에 대 한 작업자 계정 **SQLRUserGroup**합니다. 격리를 통해 구현 되는 대신 [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)합니다. 외부 스크립트를 저장된 프로시저 또는 쿼리의 발견 된 경우, 런타임 시 SQL Server는 요청을 사용 하 여 실행 패드는 확장 프로그램별 시작 관리자에 대 한 호출 합니다. 실행 패드는 해당 id로 프로세스에서 적절 한 런타임 환경을 호출 하 고 포함 하기 위해 AppContainer를 인스턴스화합니다. 이 변경은 로컬 계정 및 암호 관리는 더 이상 필요 하기 때문에 유용 합니다. 또한 로컬 사용자 계정을 사용할 수 없습니다는 설치 시 로컬 사용자 계정 종속성 제거 의미이 기능을 이제 사용할 수 있습니다.

SQL Server에 의해 구현 된 대로 AppContainers는는 내부 메커니즘입니다. 실제 증빙 AppContainers 프로세스 모니터에 표시 되지 않습니다, 하지만 프로세스가 네트워크 호출을 수행 하지 못하게 하기 위해 설치 프로그램에서 생성 된 아웃 바운드 방화벽 규칙에서 찾을 수 있습니다. 자세한 내용은 [SQL Server Machine Learning Services에 대 한 방화벽 구성](../../advanced-analytics/security/firewall-configuration.md)합니다.

> [!Note]
> SQL Server 2019 **SQLRUserGroup** 단일 SQL Server 실행 패드 서비스 계정이 여러 작업자 계정 대신 현재는 하나의 멤버가 합니다.
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>SQLRUserGroup에 부여 된 권한

기본적으로 멤버인 **SQLRUserGroup** 읽기 및 SQL Server의 파일에 대 한 실행 **Binn**, **R_SERVICES**, 및 **PYTHON_SERVICES** 실행 파일, 라이브러리 및 SQL Server와 함께 설치 된 R 및 Python 배포판에 기본 제공 데이터 집합에 대 한 액세스를 사용 하 여 디렉터리에 있습니다. 

SQL Server에서 중요 한 리소스를 보호 하려면 정의할 수 있습니다 필요에 따라는 ACL (액세스 제어 목록)에 대 한 액세스를 거부 하는 **SQLRUserGroup**합니다. 반대로, SQL Server 자체 외에도 호스트 컴퓨터에 있는 로컬 데이터 리소스에 대 한 사용 권한을 부여 될 수 있습니다. 

설계상 **SQLRUserGroup** 데이터베이스 로그인 또는 모든 데이터에 권한이 없습니다. 특정 상황에서는 연결을 허용 하도록 루프 백, 특히 경우 신뢰할 수 있는 Windows id를 호출 하는 사용자 로그인을 만드는 데는 것이 좋습니다. 이 기능은 이라고 [ *묵시적된 인증*](#implied-authentication)합니다. 자세한 내용은 [SQLRUserGroup을 데이터베이스 사용자로 추가](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)합니다.

## <a name="identity-mapping"></a>Id 매핑

세션은 시작 하는 경우 실행 패드 작업자 계정에 호출 하는 사용자의 id를 매핑합니다. 외부 Windows 사용자 또는 작업자 계정에 올바른 SQL 로그인의 매핑은 외부 스크립트를 실행 하는 SQL의 수명 동안 저장 프로시저에 대해서만 유효 합니다. 같은 로그인의 병렬 쿼리는 같은 사용자의 작업자 계정에 매핑됩니다.

실행 중 실행 패드를 세션 데이터를 저장할 임시 폴더 세션을 완료 하는 경우 삭제할 만듭니다. 디렉터리는 액세스가 제한 됩니다. R에 대 한 RLauncher이이 작업을 수행합니다. Python PythonLauncher이이 작업을 수행합니다. 각 개별 작업자 계정을 자체 폴더로 제한 되 고 자체 수준 상위 폴더의에서 파일에 액세스할 수 없습니다. 그러나 작업자 계정 수 읽기, 쓰기 또는 만들어진 세션 작업 폴더 아래에 자식을 삭제 합니다. 컴퓨터의 관리자는 각 프로세스에 대해 만들어진 디렉터리를 볼 수 있습니다. 각 디렉터리는 세션 GUID로 식별됩니다.

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>묵시적된 인증 (루프 백 요청)

*묵시적된 인증* 는 권한이 낮은 작업자 계정에 SQL Server에 신뢰할 수 있는 사용자 id로 표시 됩니다 실행 하는 외부 프로세스 루프 백 요청 데이터 또는 작업에 대 한 연결 요청 동작을 설명 합니다. 개념상으로 묵시적된 인증은 R 또는 Python 스크립트와 같은 외부 프로세스에서 시작 된 요청에 트러스트 된 연결을 지정 하는 SQL Server 연결 문자열에서 Windows 인증으로 고유 합니다. 수도 이라고 하는 *루프 백*합니다.

신뢰할 수 있는 연결은 추가 구성만 사용 하 여 R 및 Python 스크립트에서 작동 합니다. 확장성 아키텍처에 R 및 Python 프로세스는 부모 로부터 사용 권한을 상속 하는 작업자 계정으로 실행 **SQLRUserGroup**합니다. 연결 문자열을 지정 하는 경우 `Trusted_Connection=True`, SQL Server에 기본적으로 알 수 없는 연결 요청을 작업자 계정의 id를 표시 됩니다.

연결을 신뢰할 수 있는, 성공적인 수에 대 한 데이터베이스 로그인을 만들어야 합니다 **SQLRUserGroup**합니다. 이렇게 한 다음, 모든 트러스트 된 연결에서의 모든 멤버가 **SQLRUserGroup** SQL Server에 대 한 로그인 권한이 있습니다. 단계별 지침은 [데이터베이스 로그인에 대 한 SQLRUserGroup 추가](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)합니다.

트러스트 된 연결의 연결 요청을 가장 널리 사용 되는 구성 않습니다. 연결을 지정 하는 R 또는 Python 스크립트를 더 많이 ODBC 데이터 원본에 연결 되는 경우 SQL 로그인을 완전히 지정 된 사용자 이름 및 암호 사용 수 있습니다.

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>R 및 Python 세션용 어떻게 묵시적된 인증의 작동 방식

다음 다이어그램은 R 런타임 및 r 묵시적된 인증을 수행 하는 방법을 사용 하 여 SQL Server 구성 요소의 상호 작용을 보여 줍니다.

![R에 대 한 암시적된 인증](../security/media/implied-auth-rsql.png)

다음 다이어그램에는 SQL Server 구성 요소 및 상호 작용 Python 런타임에서 Python에 대 한 묵시적된 인증을 수행 하는 방법을 보여 줍니다.

![Python에 대 한 암시적된 인증](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>Rest에서 투명 한 데이터 암호화에 대 한 지원 되지 않습니다

[Transparent Data Encryption (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) 외부 스크립트 런타임에서 주고 받는 데이터에 대 한 지원 되지 않습니다. 외부 프로세스 (R 또는 Python) SQL Server 프로세스 외부에서 실행 되는 이유 때문입니다. 따라서 외부 런타임에서 사용 되는 데이터는 데이터베이스 엔진의 암호화 기능을 통해 보호 되지 않습니다. 이 동작은 데이터베이스에서 데이터를 읽고 복사 하는 SQL Server 컴퓨터에서 실행 하는 다른 모든 클라이언트에 차이가 없습니다.

따라서 TDE **아닙니다** R 또는 Python 스크립트에서 사용 하는 모든 데이터 또는 영구 저장된 된 중간 결과 또는 디스크에 저장 하는 모든 데이터에 적용 합니다. 그러나 다른 유형의 암호화, 파일 또는 폴더 수준에서 적용 하는 Windows BitLocker 암호화 또는 제 3 자 암호화 같은 여전히 유효 합니다.

경우 [Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md), 외부 런타임 암호화 키에 대 한 액세스 권한이 없습니다. 따라서 스크립트에 데이터를 보낼 수 없습니다.

## <a name="next-steps"></a>다음 단계

이 문서에서는 구성 요소 배웠습니다 및 보안 아키텍처의 상호 작용 모델에는 기본 제공 되는 [확장성 프레임 워크](../../advanced-analytics/concepts/extensibility-framework.md)합니다. 이 문서에서 다루는 주요 사항을 실행 패드, SQLRUserGroup 및 작업자 계정의 목적은 R 및 Python 사용자 id 작업자 계정에 매핑되는 방식을 프로세스 격리를 포함 합니다. 

다음 단계에 대 한 지침을 검토 하세요 [권한 부여](../../advanced-analytics/security/user-permission.md)합니다. Windows 인증을 사용 하는 서버에 대 한도 검토 해야 [데이터베이스 로그인에 대 한 SQLRUserGroup 추가](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md) 에 추가 구성이 필요한 경우에 대해 알아봅니다.
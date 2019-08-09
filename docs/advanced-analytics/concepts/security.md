---
title: R 및 Python 확장에 대 한 보안 개요
description: SQL Server Machine Learning Services의 확장성 프레임 워크에 대 한 보안 개요 로그인 및 사용자 계정, SQL Server 실행 패드 서비스, 작업자 계정, 여러 스크립트 실행 및 파일 사용에 대 한 보안입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f5b0af74633fb13b9cfd0b187bc2b180d7fd87b4
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715857"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services 확장성 프레임 워크에 대 한 보안 개요

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 SQL Server 데이터베이스 엔진 및 관련 구성 요소를 확장성 프레임 워크와 통합 하는 데 사용 되는 전체 보안 아키텍처에 대해 설명 합니다. 보안 개체, 서비스, 프로세스 id 및 사용 권한을 검사 합니다. SQL Server 확장성의 핵심 개념과 구성 요소에 대 한 자세한 내용은 [SQL Server Machine Learning Services 의 확장성 아키텍처](extensibility-framework.md)를 참조 하세요.

## <a name="securables-for-external-script"></a>외부 스크립트에 대 한 보안 개체

R 또는 Python으로 작성 된 외부 스크립트는이 목적을 위해 생성 된 [시스템 저장 프로시저](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 에 입력 매개 변수로 제출 되거나 사용자가 정의 하는 저장 프로시저에 래핑됩니다. 또는 데이터베이스 테이블에서 미리 학습 되 고 이진 형식으로 저장 된 모델을 포함 하 여 T-sql [PREDICT](../../t-sql/queries/predict-transact-sql.md) 함수에서 호출할 수 있습니다.

기존 데이터베이스 스키마 개체, 저장 프로시저 및 테이블을 통해 스크립트가 제공 되므로 SQL Server Machine Learning Services에 대 한 새 [보안 개체](../../relational-databases/security/securables.md) 없습니다.

스크립트나 스크립트를 사용 하는 방법에 관계 없이 데이터베이스 개체가 생성 되 고 저장 될 수 있지만 스크립트 저장을 위해 새 개체 형식이 도입 되지는 않습니다. 따라서 데이터베이스 개체를 사용 하 고 만들고 저장 하는 기능은 주로 사용자에 대해 정의 된 데이터베이스 사용 권한에 따라 달라 집니다.

<a name="permissions"></a>

## <a name="permissions"></a>사용 권한

데이터베이스 로그인 및 역할의 SQL Server 데이터 보안 모델이 R 및 Python 스크립트로 확장 됩니다. SQL Server 로그인 또는 Windows 사용자 계정은 SQL Server 데이터를 사용 하거나 SQL Server에서 계산 컨텍스트로 실행 되는 외부 스크립트를 실행 하는 데 필요 합니다. 임시 쿼리를 실행할 권한이 있는 데이터베이스 사용자는 R 또는 Python 스크립트에서 동일한 데이터에 액세스할 수 있습니다.

로그인 또는 사용자 계정은 외부 스크립트 요구 사항에 따라 여러 수준의 액세스가 필요할 수 있는 *보안 주체*를 식별 합니다.

+ 외부 스크립트를 사용 하는 데이터베이스에 액세스할 수 있는 권한
+ 테이블과 같은 보안 개체의 데이터를 읽을 수 있는 권한
+ 모델 또는 점수 매기기 결과와 같은 테이블에 새 데이터를 쓸 수 있습니다.
+ 테이블, 외부 스크립트를 사용 하는 저장 프로시저 또는 R 또는 Python 작업을 사용 하는 사용자 지정 함수 등의 새 개체를 만들 수 있습니다.
+ SQL Server 컴퓨터에 새 패키지를 설치 하거나 사용자 그룹에 제공 된 패키지를 사용할 수 있는 권한입니다.

실행 컨텍스트로 SQL Server를 사용 하 여 외부 스크립트를 실행 하는 각 사용자는 데이터베이스의 사용자에 게 매핑되어야 합니다. 데이터베이스 사용자 권한을 개별적으로 설정 하는 대신 역할을 만들어 권한 집합을 관리 하 고 사용자에 게 개별적으로 설정 하는 대신 해당 역할에 사용자를 할당할 수 있습니다.

자세한 내용은 [사용자에 게 Machine Learning Services SQL Server 대 한 사용 권한 부여](../../advanced-analytics/security/user-permission.md)를 참조 하세요.

## <a name="permissions-when-using-an-external-client-tool"></a>외부 클라이언트 도구를 사용 하는 경우 사용 권한

외부 클라이언트 도구에서 R 또는 Python을 사용 하는 사용자는 데이터베이스 내에서 외부 스크립트를 실행 하거나 데이터베이스 개체 및 데이터에 액세스 해야 하는 경우 데이터베이스의 사용자에 게 매핑된 로그인 이나 계정이 있어야 합니다. 외부 스크립트가 원격 데이터 과학 클라이언트에서 전송 되거나 T-sql 저장 프로시저를 사용 하 여 실행 되는지 여부에 관계 없이 동일한 권한이 필요 합니다.

예를 들어 로컬 컴퓨터에서 실행 되는 외부 스크립트를 만들었으며 SQL Server에서 해당 스크립트를 실행 하려고 한다고 가정 합니다. 다음 조건이 충족되는지 확인해야 합니다.

+ 데이터베이스에서 원격 연결을 허용합니다.
+ 데이터베이스 액세스에 사용 되는 SQL 로그인 또는 Windows 계정이 인스턴스 수준에서 SQL Server에 추가 되었습니다.
+ SQL 로그인 또는 Windows 사용자에 게는 외부 스크립트를 실행할 수 있는 권한이 있어야 합니다. 일반적으로 이 권한은 데이터베이스 관리자만 추가할 수 있습니다.
+ SQL 로그인 또는 창 사용자는 외부 스크립트가 다음 작업을 수행 하는 각 데이터베이스에서 적절 한 권한이 있는 사용자로 추가 되어야 합니다.
  + 데이터를 검색 하는 중입니다.
  + 데이터를 작성 하거나 업데이트 하는 중입니다.
  + 테이블이 나 저장 프로시저와 같은 새 개체 만들기

로그인 또는 Windows 사용자 계정이 프로 비전 되 고 필요한 사용 권한이 부여 된 후에는 R의 데이터 원본 개체 또는 Python의 **revoscalepy** 라이브러리를 사용 하거나 저장 프로시저를 호출 하 여 SQL Server에서 외부 스크립트를 실행할 수 있습니다. 외부 스크립트를 포함 합니다.

SQL Server에서 외부 스크립트가 시작 될 때마다 데이터베이스 엔진 보안은 작업을 시작한 사용자의 보안 컨텍스트를 가져오며 보안 개체에 대 한 사용자 또는 로그인의 매핑을 관리 합니다.

따라서 원격 클라이언트에서 시작 된 모든 외부 스크립트는 연결 문자열의 일부로 로그인 또는 사용자 정보를 지정 해야 합니다.

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>외부 처리에 사용 되는 서비스 (실행 패드)

확장성 프레임 워크는 SQL Server 설치의 [서비스 목록](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details) 에 하나의 새 NT 서비스를 추가 합니다. [**SQL Server 실행 패드 (MSSSQLSERVER)** ](extensibility-framework.md#launchpad).

데이터베이스 엔진은 SQL Server 실행 패드 서비스를 사용 하 여 R 또는 Python 세션을 별도의 프로세스로 인스턴스화합니다. 프로세스는 낮은 권한 계정으로 실행 됩니다. SQL Server, 실행 패드 자체, 저장 프로시저 또는 호스트 쿼리가 실행 된 사용자 id를 구분 합니다. 별도의 프로세스에서 낮은 권한 계정으로 스크립트를 실행 하는 것은 SQL Server의 R 및 Python에 대 한 보안 및 격리 모델의 기반이 됩니다.

실행 패드는 외부 프로세스를 실행 하는 것 외에도 호출 하는 사용자의 id를 추적 하 고 해당 id를 프로세스를 시작 하는 데 사용 되는 낮은 권한 작업자 계정에 매핑하는 작업을 담당 합니다. 스크립트나 코드가 데이터 및 작업에 대 한 SQL Server를 다시 호출 하는 일부 시나리오에서 실행 패드는 일반적으로 id 전송을 원활 하 게 관리할 수 있습니다. 호출 하는 사용자에 게 충분 한 권한이 있는 경우에는 SELECT 문 또는 호출 함수와 기타 프로그래밍 개체가 포함 된 스크립트가 일반적으로 성공 합니다.

> [!NOTE]
> 기본적 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 으로는 외부 스크립트를 실행 하는 데 필요한 모든 권한으로 프로 비전 된 **NT Service\MSSQLLaunchpad**에서 실행 되도록 구성 됩니다. 구성 가능한 옵션에 대 한 자세한 내용은 [SQL Server 실행 패드 서비스 구성](../security/sql-server-launchpad-service-account.md)을 참조 하세요.

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>처리에 사용 되는 id (SQLRUserGroup)

**SQLRUserGroup** (SQL 제한 된 사용자 그룹)은 SQL Server 설정에 따라 만들어지며 낮은 권한의 로컬 Windows 사용자 계정 풀을 포함 합니다. 외부 프로세스가 필요한 경우 실행 패드는 사용 가능한 작업자 계정을 받아서이를 사용 하 여 프로세스를 실행 합니다. 구체적으로 말하면 실행 패드는 사용 가능한 작업자 계정을 활성화 하 고 호출 하는 사용자의 id에 매핑한 다음 작업자 계정으로 스크립트를 실행 합니다.

+ **SQLRUserGroup** 은 특정 인스턴스에 연결 됩니다. 기계 학습을 사용 하도록 설정 된 각 인스턴스에 대해 별도의 작업자 계정 풀이 필요 합니다. 인스턴스 간에 계정을 공유할 수 없습니다.

+ 사용자 계정 풀의 크기는 정적이 고 기본값은 20 이며 동시 세션 20 개를 지원 합니다. 동시에 시작할 수 있는 외부 런타임 세션 수는이 사용자 계정 풀의 크기에 따라 제한 됩니다. 

+ 풀의 작업자 계정 이름은 SQLInstanceName*nn*형식입니다. 예를 들어 기본 인스턴스에서 **SQLRUserGroup** 에는 MSSQLSERVER01, mssqlserver02 등과 등의 계정이 포함 됩니다.

병렬화 한 작업은 추가 계정을 사용 하지 않습니다. 예를 들어 사용자가 병렬 처리를 사용 하는 점수 매기기 작업을 실행 하는 경우 모든 스레드에 대해 동일한 작업자 계정이 다시 사용 됩니다. 기계 학습을 과도 하 게 사용 하려는 경우 외부 스크립트를 실행 하는 데 사용 되는 계정 수를 늘릴 수 있습니다. 자세한 내용은 [machine learning에 대 한 사용자 계정 풀 수정](../../advanced-analytics/administration/modify-user-account-pool.md)을 참조 하세요.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>SQL Server 2019의 AppContainer 격리

SQL Server 2019에서 설치 프로그램은 더 이상 **SQLRUserGroup**에 대 한 작업자 계정을 생성 하지 않습니다. 대신 [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)를 통해 격리 됩니다. 런타임에 저장 프로시저 또는 쿼리에서 외부 스크립트가 검색 되 면 확장 프로그램에 대 한 요청으로 실행 패드를 호출 SQL Server 합니다. 실행 패드는 해당 id로 프로세스에서 적절 한 런타임 환경을 호출 하 고,이를 포함 하는 AppContainer를 인스턴스화합니다. 이러한 변경은 로컬 계정 및 암호 관리가 더 이상 필요 하지 않기 때문에 유용 합니다. 또한 로컬 사용자 계정이 금지 된 설치에서 로컬 사용자 계정 종속성을 제거 하면이 기능을 사용할 수 있습니다.

SQL Server에 의해 구현 되는 AppContainers는 내부 메커니즘입니다. 프로세스 모니터에 AppContainers의 물리적 증거는 표시 되지 않지만 설치 프로그램에서 만든 아웃 바운드 방화벽 규칙에 따라 프로세스가 네트워크 호출을 수행 하지 못하게 할 수 있습니다. 자세한 내용은 [SQL Server Machine Learning Services에 대 한 방화벽 구성](../../advanced-analytics/security/firewall-configuration.md)을 참조 하세요.

> [!Note]
> SQL Server 2019에서 **SQLRUserGroup** 에는 여러 작업자 계정 대신 단일 SQL Server 실행 패드 서비스 계정인 하나의 멤버만 있습니다.
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>SQLRUserGroup에 부여 된 사용 권한

기본적으로 **SQLRUserGroup** 의 멤버에는 R의 실행 파일, 라이브러리 및 기본 제공 데이터 집합에 대 한 액세스 권한이 있는 SQL Server **Binn**, **R_SERVICES**및 **PYTHON_SERVICES** 디렉터리의 파일에 대 한 읽기 및 실행 권한이 있습니다. SQL Server와 함께 설치 되는 Python 배포. 

SQL Server에서 중요 한 리소스를 보호 하기 위해 필요에 따라 **SQLRUserGroup**에 대 한 액세스를 거부 하는 ACL (액세스 제어 목록)을 정의할 수 있습니다. 반대로, 호스트 컴퓨터에 존재 하는 로컬 데이터 리소스에 대 한 사용 권한을 SQL Server 자체와 별도로 부여할 수도 있습니다. 

기본적으로 **SQLRUserGroup** 에는 데이터베이스 로그인 또는 데이터에 대 한 사용 권한이 없습니다. 특정 상황에서는 특히 신뢰할 수 있는 Windows id가 호출 하는 사용자 인 경우 루프 백 연결을 허용 하는 로그인을 만들려고 할 수 있습니다. 이 기능을 [*묵시적 인증*](#implied-authentication)이라고 합니다. 자세한 내용은 [데이터베이스 사용자로 SQLRUserGroup 추가](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)를 참조 하세요.

## <a name="identity-mapping"></a>Id 매핑

세션이 시작 되 면 실행 패드는 호출 하는 사용자의 id를 작업자 계정에 매핑합니다. 외부 Windows 사용자 또는 유효한 SQL 로그인을 작업자 계정에 매핑하는 작업은 외부 스크립트를 실행 하는 SQL 저장 프로시저의 수명 동안만 유효 합니다. 같은 로그인의 병렬 쿼리는 같은 사용자의 작업자 계정에 매핑됩니다.

실행 패드는 실행 중에 세션 데이터를 저장 하는 임시 폴더를 만들어 세션이 종료 될 때 삭제 합니다. 디렉터리는 액세스가 제한 되어 있습니다. R의 경우 RLauncher 관리자가이 작업을 수행 합니다. Python의 경우 PythonLauncher에서이 작업을 수행 합니다. 각 개별 작업자 계정은 자체 폴더로 제한 되며, 자신의 수준 위의 폴더에 있는 파일에는 액세스할 수 없습니다. 그러나 작업자 계정은 생성 된 세션 작업 폴더에서 자식을 읽거나, 쓰고, 삭제할 수 있습니다. 컴퓨터의 관리자는 각 프로세스에 대해 만들어진 디렉터리를 볼 수 있습니다. 각 디렉터리는 세션 GUID로 식별됩니다.

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>묵시적 인증 (루프 뒤로 요청)

*묵시적 인증* 은 낮은 권한 작업자 계정으로 실행 되는 외부 프로세스가 데이터 나 작업에 대 한 루프 백 요청을 SQL Server 하는 신뢰할 수 있는 사용자 id로 제공 되는 연결 요청 동작을 설명 합니다. 개념에 따라 묵시적 인증은 R 또는 Python 스크립트와 같은 외부 프로세스에서 시작 되는 요청에 대해 트러스트 된 연결을 지정 하는 SQL Server 연결 문자열에서 Windows 인증에 고유 합니다. *루프*라고도 하는 경우도 있습니다.

트러스트 된 연결은 R 및 Python 스크립트에서 작동 하 고 추가 구성 으로만 작동 합니다. 확장성 아키텍처에서 R 및 Python 프로세스는 작업자 계정에서 실행 되 고 부모 **SQLRUserGroup**에서 사용 권한을 상속 합니다. 연결 문자열에서를 지정 `Trusted_Connection=True`하면 작업자 계정의 id가 연결 요청에 표시 되며,이는 기본적으로 SQL Server에 대해 알 수 없습니다.

트러스트 된 연결을 성공적으로 수행 하려면 **SQLRUserGroup**에 대 한 데이터베이스 로그인을 만들어야 합니다. 이렇게 한 후 **SQLRUserGroup** 의 모든 구성원 으로부터 트러스트 된 연결에는 SQL Server에 대 한 로그인 권한이 있습니다. 단계별 지침은 [데이터베이스 로그인에 SQLRUserGroup 추가](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)를 참조 하세요.

트러스트 된 연결은 가장 널리 사용 되는 연결 요청 공식화 아닙니다. R 또는 Python 스크립트에서 연결을 지정 하는 경우 SQL 로그인을 사용 하는 것이 더 일반적 이거나 ODBC 데이터 원본에 연결 된 경우에는 완전히 지정 된 사용자 이름 및 암호를 사용 하는 것이 더 일반적입니다.

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>R 및 Python 세션에서 묵시적 인증이 작동 하는 방식

다음 다이어그램에서는 R 런타임과 SQL Server 구성 요소의 상호 작용 및 R에 대 한 묵시적 인증을 수행 하는 방법을 보여 줍니다.

![R에 대 한 묵시적 인증](../security/media/implied-auth-rsql.png)

다음 다이어그램은 Python 런타임과 SQL Server 구성 요소의 상호 작용 및 Python에 대 한 묵시적 인증을 수행 하는 방법을 보여 줍니다.

![Python에 대 한 묵시적 인증](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>휴지 상태의 투명한 데이터 암호화 지원 안 함

[TDE (투명한 데이터 암호화)](../../relational-databases/security/encryption/transparent-data-encryption.md) 는 외부 스크립트 런타임에서 보내거나 받는 데이터에 대해서는 지원 되지 않습니다. 외부 프로세스 (R 또는 Python)가 SQL Server 프로세스 외부에서 실행 되기 때문입니다. 따라서 외부 런타임에서 사용 하는 데이터는 데이터베이스 엔진의 암호화 기능으로 보호 되지 않습니다. 이 동작은 데이터베이스에서 데이터를 읽고 복사본을 만드는 SQL Server 컴퓨터에서 실행 되는 다른 클라이언트와는 다릅니다.

결과적으로 TDE는 R 또는 Python 스크립트에서 사용 하는 데이터 나 디스크에 저장 된 데이터 또는 지속형 중간 결과에는 적용 **되지 않습니다** . 그러나 Windows BitLocker 암호화 또는 파일 또는 폴더 수준에서 적용 되는 타사 암호화와 같은 다른 유형의 암호화도 적용 됩니다.

[Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)경우에는 외부 런타임이 암호화 키에 액세스할 수 없습니다. 따라서 스크립트에 데이터를 보낼 수 없습니다.

## <a name="next-steps"></a>다음 단계

이 문서에서는 [확장성 프레임 워크](../../advanced-analytics/concepts/extensibility-framework.md)에 기본 제공 되는 보안 아키텍처의 구성 요소 및 상호 작용 모델을 배웠습니다. 이 문서에서 다루는 핵심 사항에는 실행 패드의 용도, SQLRUserGroup 및 작업자 계정, R 및 Python의 프로세스 격리, 사용자 id가 작업자 계정에 매핑되는 방법이 포함 됩니다. 

다음 단계로 [권한 부여](../../advanced-analytics/security/user-permission.md)에 대 한 지침을 검토 합니다. Windows 인증을 사용 하는 서버의 경우 추가 구성이 필요한 경우에 알아보려면 [데이터베이스 로그인에 SQLRUserGroup 추가](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md) 도 검토 해야 합니다.
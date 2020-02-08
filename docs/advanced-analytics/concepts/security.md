---
title: 확장성에 대한 보안 개요
description: SQL Server Machine Learning Services의 확장성 프레임워크에 대한 보안 개요. 로그인 및 사용자 계정, SQL Server 실행 패드 서비스, 작업자 계정, 여러 스크립트 실행 및 파일 권한에 대한 보안.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f2e2d696a09e5b5bb321da583efd76f580759ce6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727670"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services의 확장성 프레임워크에 대한 보안 개요

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 SQL Server 데이터베이스 엔진 및 관련 구성 요소를 확장성 프레임워크와 통합하는 데 사용되는 전체 보안 아키텍처에 대해 설명합니다. 또한 보안 개체, 서비스, 프로세스 ID 및 사용 권한을 살펴봅니다. SQL Server 확장성의 주요 개념 및 구성 요소에 대한 자세한 내용은 [SQL Server Machine Learning Services의 확장성 아키텍처](extensibility-framework.md)를 참조하세요.

## <a name="securables-for-external-script"></a>외부 스크립트에 대한 보안 개체

R 또는 Python으로 작성된 외부 스크립트는 이 용도로 만들어진 [시스템 저장 프로시저](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 입력 매개 변수로 제출되거나 사용자가 정의하는 저장 프로시저에 래핑됩니다. T-SQL [PREDICT](../../t-sql/queries/predict-transact-sql.md) 함수에서 호출할 수 있으며 미리 학습되고 데이터베이스 테이블에 이진 형식으로 저장되는 모델이 있을 수도 있습니다.

기존 데이터베이스 스키마 개체, 저장 프로시저 및 테이블을 통해 스크립트가 제공되므로 SQL Server Machine Learning Services를 위한 새로운 [보안 개체](../../relational-databases/security/securables.md)가 없습니다.

스크립트를 어떻게 사용하고 있는지 또는 무엇으로 구성되는지에 관계없이 데이터베이스 개체가 만들어지고 저장되지만 스크립트 저장을 위한 새로운 개체 형식이 추가되지는 않습니다. 따라서 데이터베이스 개체를 사용하고 만들고 저장하는 기능은 사용자에 대해 이미 정의된 데이터베이스 권한에 따라 크게 달라집니다.

<a name="permissions"></a>

## <a name="permissions"></a>사용 권한

데이터베이스 로그인 및 역할에 대한 SQL Server의 데이터 보안 모델이 R 및 Python 스크립트로 확장됩니다. SQL Server 데이터를 사용하거나 SQL Server에서 컴퓨팅 컨텍스트로 실행되는 외부 스크립트를 실행하려면 SQL Server 로그인 또는 Windows 사용자 계정이 필요합니다. 임시 쿼리를 실행할 권한이 있는 데이터베이스 사용자는 R 또는 Python 스크립트에서 동일한 데이터에 액세스할 수 있습니다.

다음과 같은 외부 스크립트 요구 사항에 따라 로그인 또는 사용자 계정에서 여러 수준의 액세스가 필요할 수 있는 *보안 주체*를 식별합니다.

+ 외부 스크립트가 사용되는 데이터베이스에 액세스할 수 있는 권한
+ 테이블과 같은 보안 개체의 데이터를 읽을 수 있는 권한
+ 모델 또는 채점 결과 등의 새 데이터를 테이블에 쓰는 기능
+ 테이블, 외부 스크립트를 사용하는 저장 프로시저, R 또는 Python 작업을 사용하는 사용자 지정 함수 등의 새 개체를 만드는 기능
+ SQL Server 컴퓨터에 새 패키지를 설치하거나 사용자 그룹에 제공되는 패키지를 사용할 수 있는 권한

SQL Server를 실행 컨텍스트로 사용하여 외부 스크립트를 실행하는 각 사용자를 데이터베이스의 사용자에게 매핑해야 합니다. 데이터베이스 사용자 권한을 개별적으로 설정하는 대신 사용 권한 집합을 관리하는 역할을 만들고 사용자를 해당 역할에 할당할 수 있습니다.

자세한 내용은 [사용자에게 SQL Server Machine Learning Services 사용 권한 부여](../../advanced-analytics/security/user-permission.md)를 참조하세요.

## <a name="permissions-when-using-an-external-client-tool"></a>외부 클라이언트 도구를 사용할 때 사용 권한

외부 클라이언트 도구에서 R 또는 Python을 사용하는 경우 데이터베이스 내에서 외부 스크립트를 실행하거나 데이터베이스 개체와 데이터에 액세스하려면 데이터베이스에 사용자에게 매핑된 로그인이나 계정이 있어야 합니다. 외부 스크립트가 원격 데이터 과학 클라이언트에서 전송되는지 아니면 T-SQL 저장 프로시저를 사용하여 실행되는지에 관계없이 동일한 권한이 필요합니다.

예를 들어, 로컬 컴퓨터에서 실행되는 외부 스크립트를 만들었으며 SQL Server에서 해당 스크립트를 실행하려는 경우 다음 조건이 충족되는지 확인해야 합니다.

+ 데이터베이스에서 원격 연결을 허용합니다.
+ 데이터베이스 액세스에 사용한 SQL 로그인 또는 Windows 계정이 인스턴스 수준에서 SQL Server에 추가되었습니다.
+ SQL 로그인 또는 Windows 사용자에게 외부 스크립트를 실행할 수 있는 권한이 있어야 합니다. 일반적으로 이 권한은 데이터베이스 관리자만 추가할 수 있습니다.
+ 외부 스크립트가 다음 작업을 수행하는 각 데이터베이스에서 SQL 로그인 또는 Window 사용자를 적절한 권한을 가진 사용자로 추가해야 합니다.
  + 데이터 검색
  + 데이터 쓰기 또는 업데이트
  + 테이블 또는 저장 프로시저 등의 새 개체 만들기

로그인 또는 Windows 사용자 계정이 프로비저닝되고 필요한 사용 권한이 부여된 후에는 R의 데이터 원본 개체 또는 Python의 **revoscalepy** 라이브러리를 사용하거나 외부 스크립트를 포함 하는 저장 프로시저를 호출하여 SQL Server에서 외부 스크립트를 실행할 수 있습니다.

외부 스크립트가 SQL Server에서 시작될 때마다 데이터베이스 엔진 보안은 작업을 시작한 사용자의 보안 컨텍스트를 가져오고 보안 개체에 대한 사용자 또는 로그인의 매핑을 관리합니다.

따라서 원격 클라이언트에서 시작된 모든 외부 스크립트는 로그인 또는 사용자 정보를 연결 문자열의 일부로 지정해야 합니다.

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>외부 처리에 사용되는 서비스(실행 패드)

확장성 프레임워크는 SQL Server 설치의 [서비스 목록](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details)에 하나의 새 NT 서비스를 추가합니다. [**SQL Server 실행 패드(MSSSQLSERVER)** ](extensibility-framework.md#launchpad).

데이터베이스 엔진은 SQL Server 실행 패드 서비스를 사용하여 R 또는 Python 세션을 별도의 프로세스로 인스턴스화합니다. SQL Server, 실행 패드 자체 및 저장 프로시저나 호스트 쿼리가 실행된 사용자 ID와 달리 권한이 낮은 계정으로 프로세스가 실행됩니다. SQL Server의 R 및 Python에 대한 보안 및 격리 모델에서는 기본적으로 별도의 프로세스에서 권한이 낮은 계정으로 스크립트를 실행합니다.

실행 패드는 외부 프로세스를 실행하는 것 외에도 호출하는 사용자의 ID를 추적하고 해당 ID를 프로세스 시작에 사용되는 권한이 낮은 작업자 계정에 매핑하는 작업을 수행합니다. 데이터와 작업을 위해 스크립트나 코드가 SQL Server로 콜백하는 일부 시나리오에서 실행 패드는 일반적으로 ID 전송을 원활하게 관리할 수 있습니다. 호출하는 사용자에게 충분한 사용 권한이 있는 경우 SELECT 문 또는 호출 함수와 기타 프로그래밍 개체가 포함된 스크립트는 대개 성공합니다.

> [!NOTE]
> 기본적으로 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]는 외부 스크립트를 실행하는 데 필요한 모든 권한으로 프로비저닝된 **NT Service\MSSQLLaunchpad**에서 실행되도록 구성됩니다. 구성 가능한 옵션에 대한 자세한 내용은 [SQL Server 실행 패드 서비스 구성](../security/sql-server-launchpad-service-account.md)을 참조하세요.

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>처리에 사용되는 ID(SQLRUserGroup)

**SQLRUserGroup**(SQL Restricted User Group)은 SQL Server 설치 프로그램에 의해 만들어지며 권한이 낮은 로컬 Windows 사용자 계정의 풀을 포함합니다. 외부 프로세스가 필요한 경우 실행 패드가 사용 가능한 작업자 계정을 가져와서 프로세스를 실행하는 데 사용합니다. 좀 더 구체적으로 설명하면 실행 패드가 사용 가능한 작업자 계정을 활성화하고 호출하는 사용자의 ID에 매핑한 다음, 해당 작업자 계정으로 스크립트를 실행합니다.

+ **SQLRUserGroup**은 특정 인스턴스에 연결됩니다. 기계 학습이 사용되는 각 인스턴스에 대해 별도의 작업자 계정 풀이 필요합니다. 인스턴스 간에 계정을 공유할 수 없습니다.

+ 사용자 계정 풀의 크기는 정적이고 기본값은 20으로, 20개의 동시 세션을 지원합니다. 동시에 시작될 수 있는 외부 런타임 세션 수는 이 사용자 계정 풀의 크기에 따라 제한됩니다. 

+ 풀의 작업자 계정 이름은 SQLInstanceName*nn* 형식입니다. 예를 들어, 기본 인스턴스에서 **SQLRUserGroup**은 이름이MSSQLSERVER01, MSSQLSERVER02......MSSQLSERVER20인 계정을 포함합니다.

병렬화된 작업은 추가 계정을 사용하지 않습니다. 예를 들어, 사용자가 병렬 처리를 사용하는 채점 작업을 실행하는 경우 모든 스레드에 동일한 작업자 계정이 다시 사용됩니다. 기계 학습을 많이 사용하려는 경우 외부 스크립트를 실행하는 데 사용되는 계정 수를 늘릴 수 있습니다. 자세한 내용은 [기계 학습의 사용자 계정 풀 수정](../../advanced-analytics/administration/modify-user-account-pool.md)을 참조하세요.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>SQL Server 2019의 AppContainer 격리

SQL Server 2019에서는 설치 프로그램이 더 이상 **SQLRUserGroup**에 대한 작업자 계정을 만들지 않습니다. 대신 [AppContainer](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)를 통해 격리가 이루어집니다. 런타임에 저장 프로시저 또는 쿼리에서 외부 스크립트가 감지되면 SQL Server는 확장별 시작 관리자를 요청하여 실행 패드를 호출합니다. 실행 패드는 해당 ID를 사용하여 프로세스에서 적절한 런타임 환경을 호출하고, 이를 포함할 AppContainer를 인스턴스화합니다. 이러한 변경은 로컬 계정 및 암호 관리가 더 이상 필요하지 않기 때문에 유용합니다. 또한 로컬 사용자 계정이 금지된 설치에서 로컬 사용자 계정 종속성을 제거하면 이 기능을 사용할 수 있습니다.

SQL Server에서 구현되므로 AppContainer는 내부 메커니즘입니다. 프로세스 모니터에서 AppContainer의 물리적 증거는 표시되지 않지만 설치 프로그램에서 프로세스의 네트워크 호출 수행을 방지하기 위해 만든 아웃바운드 방화벽 규칙에 표시될 수 있습니다. 자세한 내용은 [SQL Server Machine Learning Services에 대한 방화벽 구성](../../advanced-analytics/security/firewall-configuration.md)을 참조하세요.

> [!Note]
> SQL Server 2019에서 **SQLRUserGroup**의 구성원은 여러 작업자 계정이 아닌 단일 SQL Server 실행 패드 서비스 계정 하나뿐입니다.
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>SQLRUserGroup에 부여된 사용 권한

기본적으로 **SQLRUserGroup**의 구성원에게는 SQL Server와 함께 설치되는 R 및 Python 배포의 실행 파일, 라이브러리 및 기본 제공 데이터 세트에 대한 액세스 권한과 함께 SQL Server **Binn**, **R_SERVICES** 및 **PYTHON_SERVICES** 디렉터리의 파일에 대한 읽기 및 실행 권한이 있습니다. 

SQL Server의 중요한 리소스를 보호하기 위해 필요에 따라 **SQLRUserGroup**에 대한 액세스를 거부하는 ACL(액세스 제어 목록)을 정의할 수 있습니다. 반대로, SQL Server 자체와 별도로 호스트 컴퓨터에 있는 로컬 데이터 리소스에 대한 사용 권한을 부여할 수도 있습니다. 

설계상 **SQLRUserGroup**에는 데이터베이스 로그인이나 데이터에 대한 사용 권한이 없습니다. 특정 상황, 특히 신뢰할 수 있는 Windows ID가 호출하는 사용자인 경우 루프 백 연결을 허용하기 위해 로그인을 만들고자 할 수 있습니다. 이 기능을 [*묵시적 인증*](#implied-authentication)이라고 합니다. 자세한 내용은 [데이터베이스 사용자로 SQLRUserGroup 추가](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)를 참조하세요.

## <a name="identity-mapping"></a>ID 매핑

세션이 시작되면 실행 패드는 호출하는 사용자의 ID를 작업자 계정에 매핑합니다. 작업자 계정에 대한 외부 Windows 사용자 또는 유효한 SQL 로그인의 매핑은 외부 스크립트를 실행하는 SQL 저장 프로시저의 수명 동안만 유효합니다. 같은 로그인의 병렬 쿼리는 같은 사용자의 작업자 계정에 매핑됩니다.

실행 패드는 실행 중 세션 데이터를 저장할 임시 폴더를 만들고 세션이 종료되면 삭제합니다. 디렉터리는 액세스가 제한됩니다. R의 경우 RLauncher가 이 작업을 수행합니다. Python의 경우 PythonLauncher가 이 작업을 수행합니다. 각 개별 작업자 계정은 자체 폴더로 제한되며, 자신보다 높은 수준의 폴더에 있는 파일에 액세스할 수 없습니다. 그러나 작업자 계정은 생성된 세션 작업 폴더 아래의 자식 요소를 읽거나, 쓰거나, 삭제할 수 있습니다. 컴퓨터의 관리자는 각 프로세스에 대해 만들어진 디렉터리를 볼 수 있습니다. 각 디렉터리는 세션 GUID로 식별됩니다.

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>묵시적 인증(루프 백 요청)

*묵시적 인증*은 데이터 또는 작업에 대한 루프 백 요청에서 권한이 낮은 작업자 계정으로 실행되는 외부 프로세스가 SQL Server에 신뢰할 수 있는 사용자 ID로 제공되는 연결 요청 동작을 설명합니다. 개념적으로 묵시적 인증은 R 또는 Python 스크립트와 같은 외부 프로세스에서 요청이 시작되는 경우 신뢰할 수 있는 연결을 지정하는 SQL Server 연결 문자열의 Windows 인증에 고유합니다. 이를 *루프 백*이라고도 합니다.

신뢰할 수 있는 연결은 R 및 Python 스크립트에서 작동하지만 추가 구성이 필요합니다. 확장성 아키텍처에서 R 및 Python 프로세스는 작업자 계정으로 실행되고 부모 **SQLRUserGroup**으로부터 사용 권한을 상속 합니다. 연결 문자열에서 `Trusted_Connection=True`를 지정하면 연결 요청에서 작업자 계정의 ID가 제공되지만 SQL Sever에서는 기본적으로 이를 알 수 없습니다.

신뢰할 수 있는 연결이 성공하려면 **SQLRUserGroup**에 대한 로그인을 만들어야 합니다. 그러면 **SQLRUserGroup** 구성원의 신뢰할 수 있는 연결에 SQL Server에 대한 로그인 권한이 부여됩니다. 단계별 지침은 [데이터베이스 로그인에 SQLRUserGroup 추가](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)를 참조하세요.

신뢰할 수 있는 연결이 가장 널리 사용되는 연결 요청 구성은 아닙니다. R 또는 Python 스크립트에서 연결을 지정하는 경우 SQL 로그인을 사용하는 것이 더 일반적이며, ODBC 데이터 원본에 연결하는 경우에는 완전하게 지정된 사용자 이름과 암호를 사용하는 것이 더 일반적입니다.

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>R 및 Python 세션에서 묵시적 인증의 작동 방식

다음 다이어그램에서는 R 런타임과 SQL Server 구성 요소의 상호 작용과 이를 통해 어떻게 R에 대한 묵시적 인증이 수행되는지 보여줍니다.

![R에 대한 묵시적 인증](../security/media/implied-auth-rsql.png)

다음 다이어그램에서는 Python 런타임과 SQL Server 구성 요소의 상호 작용과 이를 통해 어떻게 Python에 대한 묵시적 인증이 수행되는지 보여줍니다.

![Python에 대한 묵시적 인증](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>미사용 시 투명한 데이터 암호화 지원 안 함

외부 스크립트 런타임에서 보내거나 받는 데이터에 대해서는 [TDE(투명한 데이터 암호화)](../../relational-databases/security/encryption/transparent-data-encryption.md)가 지원되지 않습니다. 외부 프로세스(R 또는 Python)가 SQL Server 프로세스 외부에서 실행되기 때문입니다. 따라서 외부 런타임에서 사용하는 데이터가 데이터베이스 엔진의 암호화 기능으로 보호되지 않습니다. 데이터베이스에서 데이터를 읽고 복사본을 만드는 SQL Server 컴퓨터에서 실행 중인 다른 클라이언트의 경우도 마찬가지입니다.

따라서 R 또는 Python 스크립트에서 사용하는 데이터, 디스크에 저장된 데이터 또는 영구 저장된 중간 결과에 TDE가 적용되지 **않습니다**. 그러나 Windows BitLocker 암호화나 파일 또는 폴더 수준에서 적용되는 타사 암호화를 비롯한 다른 유형의 암호화는 적용됩니다.

[Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)를 사용하는 경우 외부 런타임에서 암호화 키에 액세스할 수 없습니다. 따라서 스크립트에 데이터를 보낼 수 없습니다.

## <a name="next-steps"></a>다음 단계

이 문서에서는 [확장성 프레임워크](../../advanced-analytics/concepts/extensibility-framework.md)에 기본 제공되는 보안 아키텍처의 구성 요소와 상호 작용 모델에 대해 알아보았습니다. 실행 패드의 용도, SQLRUserGroup 및 작업자 계정, R 및 Python의 프로세스 격리, 사용자 ID가 작업자 계정에 매핑되는 방법을 중점적으로 다루었습니다. 

다음 단계로 [권한 부여](../../advanced-analytics/security/user-permission.md)에 대한 지침을 검토합니다. Windows 인증을 사용하는 서버의 경우 [데이터베이스 로그인에 SQLRUserGroup 추가](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)도 검토하여 언제 추가 구성이 필요한지 알아보아야 합니다.
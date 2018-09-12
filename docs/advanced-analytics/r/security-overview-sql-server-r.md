---
title: SQL Server machine learning 및 R에 대 한 보안 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c04670464d23f0951a957df945a2e81b817ae134
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889189"
---
# <a name="security-for-sql-server-machine-learning-and-r"></a>SQL Server machine learning 및 R에 대 한 보안
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 연결에 사용 되는 전반적인 보안 아키텍처를 설명 합니다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 데이터베이스 엔진 및 R 런타임 관련된 구성 요소입니다. 보안 프로세스의 예제는 엔터프라이즈 환경에서 R 사용에 대 한 이러한 일반적인 시나리오에 대해 제공 됩니다.

+ 데이터 과학 클라이언트에서 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]의 RevoScaleR 함수 실행
+ 저장 프로시저를 사용하여 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 직접 R 실행

## <a name="security-overview"></a>보안 개요

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 로그인 또는 Windows 사용자 계정을 사용 하는 SQL Server 데이터 또는 SQL Server 계산 컨텍스트를 사용 하 여 실행 되는 R 스크립트를 실행 하려면 필요 합니다. 이 요구 사항은 모두 적용 됩니다 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 및 SQL Server 2017 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]합니다.

로그인 또는 사용자 계정을 식별 하는 *보안 주체*, 여러 수준의 R 스크립트 요구 사항에 따라 액세스 해야 할 수 있는 사용자:

+ R이 사용 되는 데이터베이스에 액세스 하는 권한
+ 테이블과 같은 보안된 개체에서 데이터를 읽을 권한
+ 모델 또는 점수 매기기 결과 같은 테이블에 새 데이터를 쓸 수
+ 테이블과 같은 새 개체를 만들 수는 저장 프로시저는 R 스크립트를 사용 하 여 또는 사용자 지정 함수를 사용 하 여 R 작업
+ SQL Server 컴퓨터 또는 사용자 그룹에 제공 하는 r 패키지를 새 패키지 설치 권한입니다. 

따라서 각 사람에 게 사용 하 여 R 코드 실행 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 실행 하는 것 컨텍스트 데이터베이스의 로그인에 매핑된 해야 합니다. SQL Server 보안 사용 권한 집합을 관리 및 이러한 역할에 사용자를 할당 하지 않고 개별적으로 설정 된 사용자 권한 역할을 만드는 가장 쉬운 방법은 일반적으로 됩니다. 

예를 들어 랩톱에서 실행 되는 일부 R 코드를 생성 하 고 코드를 실행 하려는 가정 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다. 이러한 조건이 충족 될 경우에이 수행할 수 있습니다.

+ 데이터베이스에서 원격 연결을 허용합니다.
+ R 코드에서 사용한 이름 및 암호를 사용한 SQL 로그인이 인스턴스 수준에서 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에 추가되었습니다. 또는 Windows 통합 인증을 사용 중인 경우 연결 문자열에 지정된 Windows 사용자가 인스턴스에서 사용자로 추가되어야 합니다.
+ SQL 로그인 또는 Windows 사용자를 외부 스크립트를 실행할 권한이 있어야 합니다. 일반적으로 이 권한은 데이터베이스 관리자만 추가할 수 있습니다.
+ SQL 로그인 또는 Window 사용자는 R 작업이 다음 작업을 수행하는 각 데이터베이스에서 적절한 권한을 가진 사용자로 추가되어야 합니다.
    + 데이터 검색
    + 데이터 쓰기 또는 업데이트 
    + 테이블 또는 저장 프로시저 등의 새 개체 만들기

로그인 또는 Windows 사용자 계정을 프로 비전 되었으며 필요한 권한이 부여, 후 R 코드를 실행할 수 있습니다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] R 데이터 원본 개체를 사용 하 여 또는 저장된 프로시저를 호출 하 여 합니다. R 시작 될 때마다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 데이터베이스 엔진 보안 R 작업을 시작 또는 저장된 프로시저를 실행 하 고, 사용자 또는 보안 개체에 대 한 로그인의 매핑을 관리 사용자의 보안 컨텍스트를 가져옵니다. 

따라서 원격 클라이언트에서 시작 되는 모든 R 작업은 연결 문자열의 일부로 로그인 또는 사용자 정보를 지정 해야 합니다.

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>상호 작용 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 보안 및 실행 패드 보안

R 스크립트가 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터의 컨텍스트에서 실행되면 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스는 외부 프로세스용으로 설정된 작업 계정 풀에서 사용 가능한 작업자 계정(로컬 사용자 계정)을 가져오고 해당 작업자 계정을 사용하여 관련 태스크를 수행합니다. 

예를 들어 Windows 도메인 자격 증명으로 R 작업을 시작할 경우 계정은 실행 패드 작업자 계정 *SQLRUser01*에 매핑될 수 있습니다.

작업 계정에 매핑된 후 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]는 프로세스를 시작하는 데 사용되는 사용자 토큰을 만듭니다. 

모든 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 작업이 완료되면 사용자 작업자 계정은 사용 가능으로 표시되고 풀로 반환됩니다.

서비스에 대 한 자세한 내용은 참조 하세요. [Extensibility framework](../concepts/extensibility-framework.md)합니다. 

### <a name="implied-authentication"></a>암시적 인증

**묵시적된 인증** 용어는 SQL Server 사용자를 가져옵니다 프로세스에 대 한 자격 증명 하 고 다음 사용자는 데이터베이스에 대 한 올바른 권한을 가정 하 고 사용자를 대신 하 여 모든 외부 스크립트 작업을 실행 합니다. 묵시적된 인증이 R 스크립트에서 데이터베이스 외부의 SQL Server ODBC 호출을 수행 해야 하는 경우에 특히 중요 합니다. 예를 들어, 코드는 스프레드시트 또는 기타 원본의 요인의 짧은 목록을 검색할 수 있습니다.

성공 하려면 이러한 루프백 호출에 대 한 SQLRUserGroup 작업자 계정이 포함 된 그룹에는 "로컬 로그온 허용" 권한이 있어야 합니다. 기본적으로이 권한은 모든 새 로컬 사용자에 게 제공 됩니다 되지만 일부 조직에서는 더 엄격한 그룹 정책이 적용 될 수 있습니다.

![R에 대 한 암시적된 인증](media/implied-auth-rsql.png)

## <a name="security-of-worker-accounts"></a>작업자 계정의 보안

외부 Windows 사용자 또는 작업자 계정에 올바른 SQL 로그인 매핑은 R 스크립트를 실행 하는 SQL 쿼리의 수명 동안에만 유효 합니다.

같은 로그인의 병렬 쿼리는 같은 사용자의 작업자 계정에 매핑됩니다.

프로세스에 사용되는 디렉터리는 RLauncher를 통해 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]에서 관리되고 디렉터리는 액세스가 제한됩니다. 작업자 계정은 상위 폴더의 파일에 액세스할 수 없지만 R 스크립트를 사용하여 SQL 쿼리에 대해 만들어진 세션 작업 폴더에서 자식을 읽거나, 쓰거나, 삭제할 수 있습니다.

작업자 계정, 계정 이름 또는 계정 암호의 수를 변경 하는 방법에 대 한 자세한 내용은 참조 하세요. [SQL Server machine learning 위한 사용자 계정 풀 수정](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)합니다.

## <a name="security-isolation-for-multiple-external-scripts"></a>여러 외부 스크립트에 대 한 보안 격리

격리 메커니즘은 실제 사용자 계정을 기반으로 합니다. 특정 위성 런타임에 대한 위성 프로세스가 시작될 때 각 위성 태스크는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]에서 지정된 작업자 계정을 사용합니다. 태스크에 여러 위성이 필요한 경우(예: 병렬 쿼리) 모든 관련 태스크에 단일 작업자 계정이 사용됩니다.

작업자 계정은 다른 작업자 계정이 사용하는 파일을 보거나 조작할 수 있습니다.
 
컴퓨터의 관리자는 각 프로세스에 대해 만들어진 디렉터리를 볼 수 있습니다. 각 디렉터리는 세션 GUID로 식별됩니다.

## <a name="see-also"></a>참고자료

[SQL Server machine learning 위한 아키텍처 개요](../../advanced-analytics/r/architecture-overview-sql-server-r.md)

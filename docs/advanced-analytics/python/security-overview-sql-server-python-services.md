---
title: "보안 개요(SQL Server R Services) | Microsoft 문서"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6ddfc3ccb67d017dc618cfbb7e7680c0164f3a21
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="security-overview"></a>보안 개요

이 항목에 연결 하는 데 사용 되는 보안 아키텍처에 설명 된 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 데이터베이스 엔진 및 Python 구성 요소입니다. 보안 프로세스의 예는 두 가지 일반적인 시나리오에 대해 제공 됩니다: SQL Server 저장된 프로시저를 사용 하 고 원격 연산 컨텍스트로 SQL Server와 Python 실행에서 Python을 실행 합니다.

## <a name="security-overview"></a>보안 개요

A [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 로그인 또는 Windows 사용자 계정이 SQL Server에서 Python 스크립트를 실행 하려면 필요 합니다. 로그인 또는 사용자 계정을 식별 하는 *보안 주체*에서 데이터를 검색 하는 데이터베이스에 액세스할 수 있는 권한을 보유 해야 합니다. 여부 Python 스크립트 개체를 새로 만듭니다 또는 새 데이터 기록에 따라 사용자는 테이블을 만들거나 데이터를 쓰는, 사용자 정의 함수 또는 저장된 프로시저를 만들 권한이 필요할 수도 있습니다.

따라서 것이 엄격한 요구 사항이 있는 Python 코드를 실행 하는 각 사용자에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 로그인 또는 데이터베이스의 계정에 매핑되어야 합니다. 이 제한은 스크립트 원격 데이터 과학 클라이언트에서 보낸 여부에 관계 없이 적용 하거나 T-SQL 저장 프로시저를 사용 하 여 시작 합니다.

예를 들어 랩톱에서 실행 되는 Python 스크립트를 생성 하 고 코드를 실행 하려면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다. 다음 조건이 충족되는지 확인해야 합니다.

+ 데이터베이스에서 원격 연결을 허용합니다.
+ SQL 로그인 또는 데이터베이스 액세스에 사용 된 Windows 계정에 추가 되었습니다는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스 수준에서 합니다.
+ SQL 로그인 또는 Windows 사용자에게 외부 스크립트를 실행할 권한이 부여되어야 합니다. 일반적으로 이 권한은 데이터베이스 관리자만 추가할 수 있습니다.
+ SQL 로그인 또는 창 사용자 Python 스크립트를 수행 하는 이러한 작업 중 하나는 각 데이터베이스에서 적절 한 권한이 있는 사용자로 추가 해야 합니다.
    + 데이터 검색
    + 데이터 쓰기 또는 업데이트
    + 테이블 또는 저장 프로시저 등의 새 개체 만들기

로그인 또는 Windows 사용자 계정을 프로 비전 하 고 후에 필요한 사용 권한이 부여에서 Python 코드를 실행할 수 있습니다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 에서 제공 하는 데이터 원본 개체를 사용 하 여는 **revoscalepy** 라이브러리에 저장 하는 호출 하 여 Python 스크립트를 포함 하는 프로시저입니다.

Python 스크립트를 시작할 때마다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 데이터베이스 엔진 보안 작업을 시작 하 고 사용자 또는 보안 개체에는 로그인의 매핑을 관리 하는 사용자의 보안 컨텍스트를 가져옵니다.

따라서 원격 클라이언트에서 시작 되는 모든 Python 스크립트를 연결 문자열의 일부로 로그인 또는 사용자 정보를 지정 해야 합니다.


## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 보안 및 실행 패드 보안의 상호 작용

Python 스크립트의 컨텍스트에서 실행 될 때는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스 외부 프로세스에 설정 된 작업자 계정의 풀에서 사용 가능한 작업자 계정 (로컬 사용자 계정)를 가져오고 작업자 계정으로 사용 하 여 관련된 태스크를 수행 합니다.

예를 들어, Windows 도메인 자격 증명에서 Python 스크립트를 실행 합니다. SQL Server 자격 증명을 가져오고을 사용할 수 있는 실행 패드 작업자 계정에 같은 매핑 *SQLRUser01*합니다.

> [!NOTE]
> 작업자 계정의 그룹 이름은 R, Python 사용 여부에 관계 없이 동일 합니다. 그러나 모든 외부 언어를 사용 하면 각 인스턴스에 대해 별도 그룹이 만들어집니다.

작업 계정에 매핑된 후 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]는 프로세스를 시작하는 데 사용되는 사용자 토큰을 만듭니다. 

모든 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 작업이 완료되면 사용자 작업자 계정은 사용 가능으로 표시되고 풀로 반환됩니다.

에 대 한 자세한 내용은 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], 참조 [Python의 통합을 원하는 SQL Server에서 새 구성 요소](../../advanced-analytics/python/new-components-in-sql-server-to-support-python-integration.md)합니다.

> [!NOTE]
> 실행 패드 작업자 계정을 관리 하 고 실행할 Python 작업, 작업자 계정이 포함 된 그룹에 대 한 *SQLRUserGroup*, "로컬 로그온 허용" 권한을; 있어야 합니다. 그렇지 않은 경우 Python 런타임은 시작 되지 합니다. 기본적으로이 권한은 모든 새 로컬 사용자에 게 제공 됩니다 되지만 일부 조직에서는 그룹 정책을 더 엄격한 수 적용할 수, 근로자 계정을 Python 작업에 SQL Server에 연결 하지 못하도록 방지 하는.

## <a name="security-of-worker-accounts"></a>작업자 계정의 보안

외부 Windows 사용자 또는 작업자 계정에 올바른 SQL 로그인의 매핑을 Python 스크립트를 실행 하는 SQL의 수명을 저장 프로시저에 대해서만 유효 합니다.

같은 로그인의 병렬 쿼리는 같은 사용자의 작업자 계정에 매핑됩니다.

프로세스에 사용 되는 디렉터리에서 관리 되는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], 및 디렉터리 액세스를 제한 합니다. Python PythonLauncher이이 작업을 수행합니다. 각 개별 작업자 계정을 자체 폴더로 제한 되 고 자체 수준 이상의 폴더에 있는 파일에 액세스할 수 없습니다. 그러나 작업자 수 읽기, 쓰기 또는 생성 된 세션 작업 폴더 아래에 자식을 삭제 합니다.

작업자 계정, 계정 이름 또는 계정 암호 수를 변경하는 방법에 대한 자세한 내용은 [SQL Server R Services용 사용자 계정 풀 수정](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)을 참조하세요.


## <a name="security-isolation-for-multiple-external-scripts"></a>여러 외부 스크립트에 대한 보안 격리

격리 메커니즘은 실제 사용자 계정을 기반으로 합니다. 특정 위성 런타임에 대한 위성 프로세스가 시작될 때 각 위성 태스크는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]에서 지정된 작업자 계정을 사용합니다. 태스크에 여러 위성이 필요한 경우(예: 병렬 쿼리) 모든 관련 태스크에 단일 작업자 계정이 사용됩니다.

작업자 계정은 다른 작업자 계정이 사용하는 파일을 보거나 조작할 수 있습니다.

컴퓨터의 관리자는 각 프로세스에 대해 만들어진 디렉터리를 볼 수 있습니다. 각 디렉터리는 세션 GUID로 식별됩니다.

## <a name="see-also"></a>관련 항목:

[아키텍처 개요](../../advanced-analytics/python/architecture-overview-sql-server-python.md)


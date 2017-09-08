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
ms.openlocfilehash: 8388d7c9d22a49a49a1a45a6fa6b479107f9ccae
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="security-overview-sql-server-r-services"></a>보안 개요(SQL Server R Services)

이 항목에서는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 데이터베이스 엔진 및 관련 구성 요소를 R 런타임에 연결하는 데 사용되는 전체 보안 아키텍처를 설명합니다. 엔터프라이즈 환경에서 R을 사용하는 두 가지 일반적인 시나리오에 대한 보안 프로세스의 예제가 제공됩니다.

+ 데이터 과학 클라이언트에서 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]의 RevoScaleR 함수 실행
+ 저장 프로시저를 사용하여 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 직접 R 실행

## <a name="security-overview"></a>보안 개요

A [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 로그인 또는 Windows 사용자 계정을 사용 하는 SQL Server 데이터 또는 SQL Server 계산 컨텍스트로 써으로 실행 하는 R 스크립트를 실행 하려면 필요 합니다. 이 요구 사항은 둘 다에 적용 됩니다. [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 및 SQL Server 2017 컴퓨터 학습 서비스입니다. 

로그인 또는 사용자 계정 식별는 *보안 주체*, 여러 수준의 R 스크립트 요구 사항에 따라 액세스 해야 하는 수 있습니다.
+ R 사용 하도록 설정 하 고 데이터베이스에 액세스할 수 있는 권한
+ 테이블과 같은 보안 된 개체에서 데이터를 읽어 사용 권한
+ 모델 또는 결과 점수 매기기 같은 테이블에 새 데이터를 쓸 수
+ 사용자 정의 함수를 사용 하 여 R 작업 또는 테이블과 같은 새 개체를 만들 수는 저장 프로시저를 R 스크립트를 사용 하 여
+ SQL Server 컴퓨터 또는 사용자 그룹에 제공 된 R 사용 하 여 패키지에 새 패키지를 설치 하려면 권한입니다. 

따라서 각각의 사용자가 사용 하 여 R 코드 실행 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 실행으로 컨텍스트 데이터베이스의 로그인에 매핑되어 있어야 합니다. SQL Server 보안이 일반적으로 가장 쉽게 사용 권한 집합을 관리 하 고 해당 역할에 사용자를 할당 하지 않고 사용자 사용 권한을 개별적으로 설정 하는 역할을 만들 수 있습니다. 

예를 들어 랩톱에서 실행 되는 몇 가지 R 코드를 생성 하 고 코드를 실행 하려면 가정 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다. 이러한 조건이 충족 될 경우에 수행할 수 있습니다.

+ 데이터베이스에서 원격 연결을 허용합니다.
+ R 코드에서 사용한 이름 및 암호를 사용한 SQL 로그인이 인스턴스 수준에서 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에 추가되었습니다. 또는 Windows 통합 인증을 사용 중인 경우 연결 문자열에 지정된 Windows 사용자가 인스턴스에서 사용자로 추가되어야 합니다.
+ Windows 사용자 또는 SQL 로그인 한 외부 스크립트를 실행할 수 있는 권한이 있어야 합니다. 일반적으로 이 권한은 데이터베이스 관리자만 추가할 수 있습니다.
+ SQL 로그인 또는 Window 사용자는 R 작업이 다음 작업을 수행하는 각 데이터베이스에서 적절한 권한을 가진 사용자로 추가되어야 합니다.
    + 데이터 검색
    + 데이터 쓰기 또는 업데이트 
    + 테이블 또는 저장 프로시저 등의 새 개체 만들기

R 코드를 실행할 수 로그인 또는 Windows 사용자 계정을 프로 비전 하 고 후에 필요한 사용 권한이 부여, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] R 데이터 원본 개체를 사용 하 여 또는 저장된 프로시저를 호출 하 여 합니다. R에서 시작 될 때마다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 데이터베이스 엔진 보안 R 작업을 시작 또는 저장된 프로시저를 실행 하 고, 사용자 또는 보안 개체에는 로그인의 매핑을 관리 하는 사용자의 보안 컨텍스트를 가져옵니다. 

따라서 원격 클라이언트에서 시작 하는 모든 R 작업은 연결 문자열의 일부로 로그인 또는 사용자 정보를 지정 해야 합니다.

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 보안 및 실행 패드 보안의 상호 작용

R 스크립트가 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터의 컨텍스트에서 실행되면 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스는 외부 프로세스용으로 설정된 작업 계정 풀에서 사용 가능한 작업자 계정(로컬 사용자 계정)을 가져오고 해당 작업자 계정을 사용하여 관련 태스크를 수행합니다. 

예를 들어 Windows 도메인 자격 증명으로 R 작업을 시작할 경우 계정은 실행 패드 작업자 계정 *SQLRUser01*에 매핑될 수 있습니다.

작업 계정에 매핑된 후 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]는 프로세스를 시작하는 데 사용되는 사용자 토큰을 만듭니다. 

모든 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 작업이 완료되면 사용자 작업자 계정은 사용 가능으로 표시되고 풀로 반환됩니다.

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]에 대한 자세한 내용은 [R 통합을 지원하기 위한 SQL Server의 새 구성 요소](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r.md)를 참조하세요.

> [!NOTE]
실행 패드에서 작업자 계정을 관리하고 R 작업을 실행하려면 작업자 계정이 포함된 그룹 SQLRUserGroup에 "로컬 로그온 허용" 권한이 있어야 합니다. 이 권한이 없으면 R Services가 작동하지 않을 수 있습니다. 기본적으로 이 권한은 모든 로컬 사용자에게 부여되지만 일부 조직에서는 더 엄격한 그룹 정책이 적용되어 작업자 계정이 R 작업을 수행하기 위해 SQL Server에 연결할 수 없습니다.  

## <a name="security-of-worker-accounts"></a>작업자 계정의 보안

외부 Windows 사용자 또는 작업자 계정에 올바른 SQL 로그인의 매핑을 R 스크립트를 실행 하는 SQL 쿼리가의 수명 기간에만 유효 합니다. 

같은 로그인의 병렬 쿼리는 같은 사용자의 작업자 계정에 매핑됩니다.

프로세스에 사용되는 디렉터리는 RLauncher를 통해 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]에서 관리되고 디렉터리는 액세스가 제한됩니다. 작업자 계정은 상위 폴더의 파일에 액세스할 수 없지만 R 스크립트를 사용하여 SQL 쿼리에 대해 만들어진 세션 작업 폴더에서 자식을 읽거나, 쓰거나, 삭제할 수 있습니다.

작업자 계정, 계정 이름 또는 계정 암호 수를 변경하는 방법에 대한 자세한 내용은 [SQL Server R Services용 사용자 계정 풀 수정](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)을 참조하세요.


## <a name="security-isolation-for-multiple-external-scripts"></a>여러 외부 스크립트에 대한 보안 격리

격리 메커니즘은 실제 사용자 계정을 기반으로 합니다. 특정 위성 런타임에 대한 위성 프로세스가 시작될 때 각 위성 태스크는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]에서 지정된 작업자 계정을 사용합니다. 태스크에 여러 위성이 필요한 경우(예: 병렬 쿼리) 모든 관련 태스크에 단일 작업자 계정이 사용됩니다.

작업자 계정은 다른 작업자 계정이 사용하는 파일을 보거나 조작할 수 있습니다.
 
컴퓨터의 관리자는 각 프로세스에 대해 만들어진 디렉터리를 볼 수 있습니다. 각 디렉터리는 세션 GUID로 식별됩니다.

## <a name="see-also"></a>관련 항목:
[아키텍처 개요](../../advanced-analytics/r-services/architecture-overview-sql-server-r.md)


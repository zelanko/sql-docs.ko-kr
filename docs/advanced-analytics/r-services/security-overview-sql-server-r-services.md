---
title: "보안 개요 (SQL Server R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# 보안 개요 (SQL Server R Services)

이 항목에 연결 하는 데 사용 되는 전반적인 보안 아키텍처에 설명 된 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 데이터베이스 엔진 및 R 런타임에 관련된 구성 요소입니다. 보안 프로세스의 예는 엔터프라이즈 환경에서 R 사용에 대 한 일반적인 두 가지 시나리오에 제공 됩니다.

+ RevoScaleR 함수를 실행 하면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 데이터 과학 클라이언트에서
+ R에서 직접 실행 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 저장된 프로시저를 사용 하 여

## 보안 개요

A [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 로그인 또는 Windows 사용자 계정을 사용 하는 모든 R 작업 실행 하는 데 필요한는 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]합니다. 로그인 또는 사용자 계정을 식별 하는 *보안 주체*, 테이블과 같은 보안된 개체에서 데이터를 읽는 또는 새 데이터를 쓰거나 R 작업에 필요한 경우 새 개체를 추가 하는 권한 뿐 아니라 R 실행 되는 위치, 데이터베이스 액세스 권한을 보유 해야 합니다.

따라서 것이 엄격한 요구 사항이 있는 R 코드를 실행 하는 각 사용자에 대해 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 여부에 관계 없이 해당 코드 RevoScaleR 함수를 사용 하 여 원격 데이터 과학 클라이언트에서 전송 되는 T-SQL 저장 프로시저를 사용 하 여 시작 데이터베이스의 로그인에 매핑되어야 합니다. 

예를 들어 랩톱에서 실행 되는 일부 R 코드를 생성 하 고 코드를 실행 하려면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다. 다음 조건이 충족 되어 있는지 확인 해야 합니다.

+ 데이터베이스 원격 연결을 허용합니다.
+ 이름 및 R 코드에 사용 되는 암호를 사용 하 여 SQL 로그인에 추가 되었습니다는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스 수준입니다. 또는 Windows 통합된 인증을 사용 하는 경우 연결 문자열에 지정 된 Windows 사용자 인스턴스에 대 한 사용자로 추가 해야 합니다.
+ SQL 로그인 또는 Windows 사용자는 외부 스크립트를 실행할 수 있는 권한이 부여 되어야 합니다. 일반적으로 데이터베이스 관리자가이 권한을 추가할 수만 있습니다.
+ SQL 로그인 또는 창 사용자는 이러한 작업 중 하나는 R 작업 수행 하는 각 데이터베이스에서 적절 한 권한이 있는 사용자로 추가 되어야 합니다.
    + 데이터 검색
    + 작성 하거나 데이터를 업데이트 합니다. 
    + 테이블 또는 저장된 프로시저와 같은 새 개체 만들기

로그인 또는 Windows 사용자 계정을 프로 비전 하 고 후에 필요한 사용 권한을 부여에서 R 코드를 실행할 수 있습니다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] R 데이터 원본 개체를 사용 하 여 또는 저장된 프로시저를 호출 하 여 합니다. R에서 시작 될 때마다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 데이터베이스 엔진 보안 R 작업을 시작 하 고 사용자 또는 보안 개체에는 로그인의 매핑을 관리 하는 사용자의 보안 컨텍스트를 가져옵니다. 

따라서 원격 클라이언트에서 시작 하는 모든 R 작업은 연결 문자열의 일부로 로그인 또는 사용자 정보를 지정 해야 합니다.


## 상호 작용 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 보안 및 실행 패드 보안

R 스크립트의 컨텍스트에서 실행 되는 경우는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스는 외부 프로세스에 설정 된 작업자 계정의 풀에서 사용 가능한 작업자 계정 (로컬 사용자 계정)를 가져옵니다 하 고 관련된 작업을 수행 하려면 해당 작업자 계정을 사용 합니다. 

예를 들어 Windows 도메인 자격 증명에서 R 작업을 시작 하는 경우 계정 수 계정에 매핑할 수는 실행 패드 작업자 *SQLRUser01*합니다.

작업자 계정에 매핑 후 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 프로세스를 시작 하는 데 사용 되는 사용자 토큰을 만듭니다. 

경우 모든 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 작업이 완료, 사용자 작업자 계정이 자유형으로 표시 된 고 풀으로 반환 합니다.

에 대 한 자세한 내용은 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], 참조 [R 통합 지원 기능이 SQL Server에서 새 구성 요소](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)합니다.

## 작업자 계정 보안
이 매핑은 외부 Windows 사용자 또는 올바른 SQL 계정에 로그인 하는 작업자의 R 스크립트를 실행 하는 SQL 쿼리의 수명 기간 동안에 유효 합니다. 

동일한 로그인에서 병렬 쿼리는 동일한 사용자 작업자 계정에 매핑됩니다.

프로세스에 사용 되는 디렉터리에서 관리 되는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] RLauncher를 사용 하 여 및 디렉터리 액세스를 제한 합니다. 작업자 계정이 자체적으로 위의 폴더의 모든 파일을 액세스할 수 없지만 수 읽기, 쓰기 또는 R 스크립트를 사용 하 여 SQL 쿼리를 위해 생성 된 세션 작업 폴더 아래에 자식을 삭제 합니다.

작업자 계정, 계정 이름 또는 계정 암호의 수를 변경 하는 방법에 대 한 자세한 내용은 참조 [SQL Server R 서비스에 대 한 사용자 계정 풀 수정](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)합니다.


## 여러 외부 스크립트에 대 한 보안 격리

격리 메커니즘은 실제 사용자 계정에 기반 합니다. 각 위성 작업 지정 하는 작업자 계정을 사용 하 여 특정 언어 런타임에 대 한 위성 프로세스를 시작 하는 대로 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]합니다. 작업을 여러 위성이 필요한 경우 예를 들어 병렬 쿼리의 경우 단일 작업자 계정이 사용 됩니다 모든 관련된 작업에 대해.

작업자 계정이 없으면 참조 하거나 다른 작업자 계정을 사용 하는 파일을 조작할 수 있습니다.
 
컴퓨터의 관리자 인 경우에 각 프로세스에 대해 생성 된 디렉터리를 볼 수 있습니다. 각 디렉터리는 세션 GUID로 식별 됩니다.

## 참고 항목
[아키텍처 개요](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)
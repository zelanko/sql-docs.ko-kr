---
title: SQL Server의 기계 학습에 대 한 보안 고려 사항 | Microsoft Docs
ms.date: 02/01/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: bd695d866479b88f139011ff4f7760b4c0565734
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="security-considerations-for-machine-learning-in-sql-server"></a>SQL Server의 기계 학습에 대 한 보안 고려 사항
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 관리자 또는 설계자 명심 해야 컴퓨터 학습 서비스를 사용 하는 경우 보안 고려 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스

## <a name="use-a-firewall-to-restrict-network-access"></a>방화벽을 사용 하 여의 네트워크 액세스 제한

기본 설치에서 Windows 방화벽 규칙을 사용 하 여 외부 런타임 프로세스에서 모든 아웃 바운드 네트워크 액세스를 차단 하 합니다. 패키지를 다운로드 하거나 악의적일 수 있는 기타 네트워크 호출을 수행 합니다. 외부 런타임 프로세스를 방지 하기 위해 방화벽 규칙을 만들어야 합니다.

다른 방화벽 프로그램을 사용 하는 경우에 사용자 계정 풀이 나타내는 그룹 또는 로컬 사용자 계정에 대 한 규칙을 설정 하 여 외부 런타임에 대 한 아웃 바운드 네트워크 연결을 차단 하는 규칙을 만들 수 있습니다.

Python 또는 R 런타임에 무제한 네트워크 액세스를 방지 하기 위해 Windows 방화벽 (또는 원하는 다른 방화벽)에서 설정 하는 것이 좋습니다.

## <a name="authentication-methods-supported-for-remote-compute-contexts"></a>원격 계산 컨텍스트를 지 원하는 인증 방법

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] Windows 통합 인증 및 SQL 로그인 간의 연결을 만들 때 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 원격 데이터 과학 클라이언트입니다.

예를 들어 랩톱에서 R 솔루션을 개발 하는 및를 SQL Server 컴퓨터에 계산을 수행 합니다. 사용 하 여 R에서 SQL Server 데이터 소스를 만드는 것은 **rx** Windows 자격 증명을 기반으로 함수 및 연결 문자열을 정의 합니다.

변경 될 때는 _계산 컨텍스트_ 랩톱에 SQL Server 컴퓨터에서 모든 R 코드는 실행 SQL Server 컴퓨터에 Windows 계정에 필요한 권한이 있으면 합니다. 또한, R 코드의 일부로 실행 되는 모든 SQL 쿼리도 자격 증명에서 실행 됩니다.

SQL 로그인을 사용 하는이 시나리오 에서도 지원 됩니다. 그러나이 위해서는 SQL Server 인스턴스가 혼합된 모드 인증을 허용 하도록 구성할 수 있습니다.

### <a name="implied-authentication"></a>암시적 인증

 일반적으로 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 외부 스크립트 런타임을 시작 하 고는 자체 계정에서 스크립트를 실행 합니다. 그러나, 외부 런타임은 ODBC 호출을 수행 하는 경우는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] ODBC 호출 발생 하지 않도록 하는 명령을 전송 하는 사용자의 자격 증명을 가장 합니다. 이를 *암시적 인증*이라고 합니다.
 
 > [!IMPORTANT]
 > 묵시적된 인증을 성공적으로 작업자 계정이 포함 된 Windows 사용자 그룹에 대 한 (기본적으로 **SQLRUserGroup**) 해야 수 있는 권한이 부여 되어야 인스턴스와이 계정에 대 한 계정이 master 데이터베이스에 있어야 인스턴스에 연결 합니다.
 > 
 > 그룹 **SQLRUserGroup** Python 스크립트를 실행 하는 경우에 사용 됩니다. 

일반적으로 RODBC 또는 다른 라이브러리를 사용 하 여 데이터 읽기를 시도 하기 보다는 먼저 SQL Server에 더 큰 데이터 집합을 이동 하는 것이 좋습니다. 또한 사용 하 여 SQL Server 쿼리 또는 뷰, 주 데이터 원본으로 성능 향상을 위해 합니다. 

예를 들어 SQL Server에서 학습 데이터 (일반적으로 가장 큰 데이터)를 가져올 수도 있으며 외부 소스에서 같은 요소의 목록을 가져올 수 있습니다. 대부분의 ODBC 데이터 원본에서 데이터를 가져오는 연결된 된 서버를 정의할 수 있습니다. 자세한 내용은 참조 [연결된 된 서버 만들기](https://docs.microsoft.com/sql/relational-databases/linked-servers/create-linked-servers-sql-server-database-engine)합니다.

ODBC 호출을 외부 데이터 원본에 대 한 종속성을 최소화 하려면 수 또한 데이터 엔지니어링 팀을 별도 프로세스를 수행 하 고 결과 테이블에 저장 또는 T-SQL을 사용 하 여 합니다. SQL vs에서 엔지니어링 팀에 데이터의 좋은 예에 대 한이 자습서를 참조 하십시오. R: [T-SQL을 사용 하 여 데이터 기능을 만드는](../tutorials/sqldev-create-data-features-using-t-sql.md)합니다.

## <a name="no-support-for-encryption-at-rest"></a>휴지 암호화 지원 되지 않음

[투명 한 데이터 암호화 (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption) 로 전송 되거나 외부 스크립트 런타임에서 받은 데이터에 대 한 지원 되지 않습니다. SQL Server 프로세스; 외부 R (또는 Python)에서 실행 하는 이유는 따라서 외부 런타임에서 사용 되는 데이터는 데이터베이스 엔진의 암호화 기능에 의해 보호 되지 않습니다.  이 동작은 데이터베이스에서 데이터를 읽고 복사 하는 SQL Server 컴퓨터에서 실행 중인 다른 모든 클라이언트는 방법과 다르지 않습니다.

따라서 TDE **않습니다** 디스크 또는 영구 저장 된 모든 중간 결과 저장 된 데이터 또는 Python 또는 R 스크립트에서 사용 하는 모든 데이터에 적용 합니다. 그러나 다른 유형의 암호화, 파일 또는 폴더 수준에서 적용 된 Windows BitLocker 암호화 또는 제 3 자 암호화와 같은 여전히 적용 됩니다.

경우 [항상 암호화](https://docs.microsoft.com/sql/relational-databases/security/encryption/overview-of-key-management-for-always-encrypted), 외부 런타임 암호화 키에 액세스할 필요는 없으며, 따라서 스크립트에서 데이터를 보낼 수 없습니다.

## <a name="resources"></a>리소스

시스템 학습 스크립트를 실행 하는 데 사용자 계정을 프로 비전 하는 방법에 대 한 서비스를 관리 하는 방법에 대 한 자세한 내용은 참조 [구성 및 고급 분석 확장 관리](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)합니다.

에 대 한 설명은 일반 보안 아키텍처 참조:

+ [R에 대 한 보안 개요](security-overview-sql-server-r.md)
+ [Python에 대 한 보안 개요](../python/security-overview-sql-server-python-services.md)

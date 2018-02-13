---
title: "SSMS를 사용 하 여 Linux에서 SQL Server 관리 | Microsoft Docs"
description: 
author: rothja
ms.author: jroth
manager: craigg
ms.date: 08/23/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.technology: database-engine
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.custom: sql-linux
ms.workload: On Demand
ms.openlocfilehash: 31bff0cb43048585fb03246b683ad71e673bb7f4
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/13/2018
---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>Windows에서 SQL Server Management Studio를 사용 하 여 Linux에서 SQL Server 관리

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 소개 [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) 과정을 안내 하는 몇 가지 일반 작업 및 합니다. SSMS는 Windows 응용 프로그램, 따라서 Linux에서 원격 SQL Server 인스턴스에 연결할 수 있는 Windows 컴퓨터는 경우 SSMS를 사용 합니다.

[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) 무료로 개발 및 관리 요구 사항에 대 한 Microsoft 서비스를 해제 하는 SQL 도구 제품군의 일부입니다. SSMS는 액세스, 구성, 관리, 관리, 운영 및 온-프레미스를 실행 중인 SQL server 또는 Linux, Windows 또는 macOS 및 Azure SQL 데이터베이스에는 Docker 및 Azure SQL 데이터 웨어하우스 클라우드의 모든 구성 요소를 개발 하기 위한 통합된 환경. SSMS 다양 한 개발자와 모든 기술 수준의 관리자에 SQL Server에 대 한 액세스를 제공 하기 위해 풍부한 스크립트 편집기와 광범위 한 그래픽 도구 그룹을 결합 합니다.

SSMS는 도구를 비롯 하 여 SQL Server에 대 한 다양 한 개발 및 관리 기능 집합을 제공 합니다.

- 구성, 모니터링 및 단일 컴퓨터 또는 SQL Server의 여러 인스턴스를 관리 합니다.
- 배포, 모니터링 및 데이터 계층 구성 요소와 같은 업그레이드 데이터베이스 및 데이터 웨어하우스
- 데이터베이스 백업 및 복원
- 빌드 및 T-SQL 쿼리 및 스크립트를 실행 및 결과 참조 하십시오.
- 데이터베이스 개체에 대 한 T-SQL 스크립트를 생성 합니다.
- 데이터베이스의 데이터 보기 및 편집
- T-SQL 쿼리 및 뷰, 테이블 및 저장된 프로시저와 같은 데이터베이스 개체를 시각적으로 디자인

참조 [사용 하 여 SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/ms174173.aspx) 자세한 정보에 대 한 합니다.

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)의 최신 버전 설치

SQL Server를 사용할 때는 항상 최신 버전의 SQL Server Management Studio (SSMS)를 사용 해야 합니다. 최신 버전의 SSMS 지속적으로 업데이트 되 고 최적화 된와 현재 SQL Server on 2017 Linux 합니다. 참조를 다운로드 하 여 최신 버전을 설치 하려면 [SQL Server Management Studio 다운로드](../ssms/download-sql-server-management-studio-ssms.md)합니다. 최신 상태로 유지, 최신 버전의 SSMS 묻는 메시지를 다운로드 하는 새 버전이 있는 경우. 

## <a name="before-you-begin"></a>시작하기 전 주의 사항
- 참조 [Linux에서 SQL Server에 연결 하는 Windows에서 사용 하 여 SSMS](sql-server-linux-develop-use-ssms.md) SSMS를 사용 하 여 쿼리 및 연결 하는 방법에 대 한
- 읽기는 [알려진 문제](sql-server-linux-release-notes.md) for SQL Server 2017 Linux

## <a name="create-and-manage-databases"></a>만들기 및 데이터베이스 관리
에 연결 된 상태는 *마스터* 데이터베이스 서버에 데이터베이스를 만들 하 고 수정 하거나 수 있습니다 기존 데이터베이스를 삭제 합니다. 다음 단계에서는 Management Studio를 통해 일반적인 몇 가지 데이터베이스 관리 태스크를 수행 하는 방법에 설명 합니다. 이러한 작업을 수행 하려면 반드시 연결한는 *마스터* SQL Server 2017 linux를 설정할 때 만든 서버 수준 보안 주체 로그인을 사용 하 여 데이터베이스입니다.

### <a name="create-a-new-database"></a>새 데이터베이스 만들기

1. SSMS를 시작 하 고 SQL Server 2017 linux에 서버에 연결

2. 개체 탐색기에서 마우스 오른쪽 단추로 클릭는 *데이터베이스* 폴더를 마우스 클릭 * 새 데이터베이스... "

3. 에 *새 데이터베이스* 대화 상자에서 새 데이터베이스에 대 한 이름을 입력 한 다음 클릭 *확인*

새 데이터베이스 서버에 성공적으로 만들어집니다. T-SQL을 사용 하 여 새 데이터베이스를 만들려면 다음을 참조 하는 경우 [CREATE DATABASE (SQL Server Transact SQL)](../t-sql/statements/create-database-sql-server-transact-sql.md)합니다.

### <a name="drop-a-database"></a>데이터베이스 삭제

1. SSMS를 시작 하 고 SQL Server 2017 linux에 서버에 연결

2. 개체 탐색기에서 확장 된 *데이터베이스* 폴더를 서버에 모든 데이터베이스의 목록입니다.

3. 개체 탐색기에서 삭제 하려는 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 클릭 *삭제*

4. 에 *개체 삭제* 대화 상자에서 확인 *기존 연결 닫기* 클릭 한 다음 *확인*

데이터베이스 서버에서 성공적으로 삭제 됩니다. T-SQL을 사용 하 여 데이터베이스를 삭제 하려면 다음을 참조 하면 [DROP DATABASE (SQL Server Transact SQL)](../t-sql/statements/drop-database-transact-sql.md)합니다.

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>작업 모니터를 사용 하 여 SQL Server 작업에 대 한 정보를 보려면

[작업 모니터](../relational-databases/performance-monitor/activity-monitor.md) 도구는 SQL Server Management Studio (SSMS)에 기본적으로 제공 하 고 SQL Server 프로세스와 이러한 프로세스가 현재 SQL Server 인스턴스의 미치는 영향에 대 한 정보를 표시 합니다.

1. SSMS를 시작 하 고 SQL Server 2017 linux에 서버에 연결

2. 개체 탐색기에서 마우스 오른쪽 단추로 클릭는 *서버* 노드를 차례로 클릭 한 다음 *작업 모니터*

작업 모니터에서는 확장 및 축소 가능한 창이 다음에 대 한 정보를 보여 줍니다.
- 개요
- 프로세스
- 리소스 대기
- 데이터 파일 I/O
- 비용이 드는 최근 쿼리
- 비용이 드는 활성 쿼리

창을 확장 하면 작업 모니터는 인스턴스에서 정보를 쿼리 합니다. 창을 축소하면 해당 창에 대한 모든 쿼리 작업이 중지됩니다. 하나 이상의 창을 인스턴스에서 여러 종류의 작업을 보려면를 동시에 확장할 수 있습니다.

## <a name="see-also"></a>참고 항목
- [SQL Server Management Studio 사용](https://msdn.microsoft.com/en-us/library/ms174173.aspx)
- [SSMS 사용 하 여 데이터베이스를 내보내고](sql-server-linux-migrate-ssms.md)
- [자습서: SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/bb934498.aspx)
- [자습서: Transact-SQL 문 작성](../t-sql/tutorial-writing-transact-sql-statements.md)
- [서버 성능 및 작업 모니터링](../relational-databases/performance/server-performance-and-activity-monitoring.md)

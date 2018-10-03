---
title: SSMS를 사용 하 여 Linux의 SQL Server 관리 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/21/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.custom: sql-linux
ms.openlocfilehash: 5de8172a38cfb547315c2cf65c470b019b7227eb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47723201"
---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>Windows에서 SQL Server Management Studio를 사용 하 여 Linux의 SQL Server 관리

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 소개 [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) 몇 가지 일반적인 작업을 안내 합니다. SSMS는 Windows 응용 프로그램, 따라서 SSMS를 사용 하 여 Linux에서 원격 SQL Server 인스턴스에 연결할 수 있는 Windows 컴퓨터의 경우.

> [!TIP]
> Windows 컴퓨터에서 SSMS를 실행 하도록가 없는 경우 새 고려 [Azure Data Studio](../azure-data-studio/index.md)합니다. SQL Server를 관리 하기 위한 그래픽 도구를 제공 하 고 Linux와 Windows 모두에서 실행 됩니다.

[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) 은 Microsoft 제품 개발 및 관리 요구 사항에 맞게 한 무료 SQL 도구 제품군의 일부입니다. SSMS는 액세스, 구성, 관리, 관리 및 SQL Server의 모든 구성 요소를 개발 하는 통합된 환경입니다. 실행 중인 SQL Server 플랫폼에서 모두 온-프레미스 및 클라우드에서 Docker 컨테이너에 연결할 수 있습니다. 또한 Azure SQL Database 및 Azure SQL Data Warehouse에 연결 합니다. SSMS는 다양 한 개발자와 모든 수준의 관리자 SQL server 액세스를 제공 하기 위해 풍부한 스크립트 편집기를 사용 하 여 광범위 한 그래픽 도구 그룹을 결합 합니다.

SSMS는 도구를 포함 하 여 SQL Server에 대 한 광범위 한 개발 및 관리 기능을 제공 합니다.

- 구성, 모니터링 및 단일 또는 SQL Server의 여러 인스턴스를 관리 합니다.
- 배포, 모니터링 및 데이터 계층 구성 요소와 같은 업그레이드 데이터베이스 및 데이터 웨어하우스
- 데이터베이스 백업 및 복원
- 빌드 및 T-SQL 쿼리 및 스크립트 실행 결과 참조 하세요.
- 데이터베이스 개체에 대 한 T-SQL 스크립트를 생성 합니다.
- 데이터베이스에서 데이터 보기 및 편집
- T-SQL 쿼리 및 뷰, 테이블 및 저장된 프로시저와 같은 데이터베이스 개체를 시각적으로 디자인

참조 [SSMS 란?](../ssms/sql-server-management-studio-ssms.md) SSMS에 대 한 자세한 내용은 합니다.

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>최신 버전의 SQL Server Management Studio (SSMS)를 설치 합니다.

SQL Server에서 작업할 때 항상 최신 버전의 SQL Server Management Studio (SSMS)를 사용 해야 합니다. 최신 버전의 SSMS는 지속적으로 업데이트 하 고 최적화 하 고 현재 Linux에서 SQL Server를 사용 하 여 작동 합니다. 다운로드 하 고 최신 버전 설치를 참조 하세요 [SQL Server Management Studio 다운로드](../ssms/download-sql-server-management-studio-ssms.md)합니다. 최신, 최신 버전의 SSMS 묻는 새 버전을 다운로드할 수 있으면 됩니다.

> [!NOTE]
> Linux를 관리 하려면 SSMS를 사용 하기 전에 검토 합니다 [알려진 문제](sql-server-linux-release-notes.md) Linux에서 SSMS에 대 한 합니다.

## <a name="connect-to-sql-server-on-linux"></a>Linux의 SQL Server에 연결

연결 하려면 다음 기본 단계를 사용 합니다.

1. 입력 하 여 SSMS를 시작할 **Microsoft SQL Server Management Studio** 검색 상자에는 Windows 및 데스크톱 앱을 클릭 합니다.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png)

1. 에 **서버에 연결** 창에서 다음 정보를 입력 (SSMS 이미 실행 중인 경우 클릭 **연결 > 데이터베이스 엔진** 열려는 **서버에 연결** window):

   | 설정 | Description |
   |-----|-----|
   | **서버 유형** | 기본값은 데이터베이스 엔진입니다. 이 값을 변경 하지 마십시오. |
   | **서버 이름** | 대상 Linux SQL Server 컴퓨터의 IP 주소 이름을 입력 합니다. |
   | **인증** | Linux의 SQL Server를 사용 하 여 **SQL Server 인증**합니다. |
   | **로그인** | 서버의 데이터베이스에 액세스할 수 있는 사용자의 이름을 입력 (예를 들어 기본값 **SA** 설치 중에 만든 계정). |
   | **암호** | 지정된 된 사용자에 대 한 암호를 입력 (에 대 한 합니다 **SA** 계정을 만든이 설치 하는 동안). |

    ![SQL Server Management Studio: SQL Database 서버에 연결](./media/sql-server-linux-manage-ssms/connect.png)

1. **연결**을 클릭합니다.

    > [!TIP]
    > 연결 오류가 발생하는 경우 먼저 오류 메시지에서 문제를 진단합니다. 그런 다음 [connection troubleshooting recommendations](sql-server-linux-troubleshooting-guide.md#connection)(연결 문제 해결 권장 사항)를 검토합니다.
 
1. SQL 서버에 연결 **개체 탐색기** 열리고 하면 이제 액세스할 수 있습니다 데이터베이스 관리 작업을 수행 하거나 데이터를 쿼리 합니다.

## <a name="run-transact-sql-queries"></a>TRANSACT-SQL 쿼리를 실행 합니다.

서버에 연결한 후에 데이터베이스에 연결 하 고 TRANSACT-SQL 쿼리를 실행할 수 있습니다. 거의 모든 데이터베이스 작업에 대 한 TRANSACT-SQL 쿼리를 사용할 수 있습니다.

1. **개체 탐색기**, 서버에서 대상 데이터베이스로 이동 합니다. 예를 들어, 확장 **시스템 데이터베이스** 사용 하 여 **마스터** 데이터베이스.

1. 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 선택한 **새 쿼리**합니다.

1. 쿼리 창에서 반환을 선택 하는 TRANSACT-SQL 쿼리를 서버의 모든 데이터베이스의 이름을 작성.

   ```sql
   SELECT [Name]
   FROM sys.Databases
   ```

   쿼리를 작성 하는 데 처음 이라면 참조 [TRANSACT-SQL 문 작성](../t-sql/tutorial-writing-transact-sql-statements.md)합니다.

1. 클릭 합니다 **Execute** 단추 쿼리를 실행 하 고 결과 확인 합니다.

   ![성공했습니다. SQL Database 서버에 연결: SQL Server Management Studio](./media/sql-server-linux-manage-ssms/execute-query.png)

TRANSACT-SQL 쿼리를 사용 하 여 모든 관리 작업 거의 할 수 있지만 SSMS는 그래픽 도구를 SQL Server를 관리 하기가입니다. 다음 섹션에서는 그래픽 사용자 인터페이스를 사용 하 여 몇 가지 예제를 제공 합니다.

## <a name="create-and-manage-databases"></a>데이터베이스 만들기 및 관리

에 연결 된 상태를 *마스터* 데이터베이스 서버에서 데이터베이스 만들기 및 수정 하거나 수 기존 데이터베이스를 삭제 합니다. 다음 단계는 Management Studio를 통해 여러 일반 데이터베이스 관리 작업을 수행 하는 방법을 설명 합니다. 이러한 작업을 수행 하려면 해야 연결한 합니다 *마스터* Linux의 SQL Server를 설정할 때 만든 서버 수준 보안 주체 로그인을 사용 하 여 데이터베이스입니다.

### <a name="create-a-new-database"></a>새 데이터베이스 만들기

1. SSMS를 시작 하 고 Linux의 SQL Server에서 서버에 연결

2. 개체 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 *데이터베이스* 폴더를 마우스 클릭 * 새 데이터베이스... "

3. 에 *새 데이터베이스* 대화 상자에서 새 데이터베이스의 이름을 입력 한 다음 클릭 *확인*

새 데이터베이스 서버에 성공적으로 만들어집니다. T-SQL을 사용 하 여 새 데이터베이스를 만들려면 다음을 참조 하는 경우 [CREATE DATABASE (SQL Server TRANSACT-SQL)](../t-sql/statements/create-database-sql-server-transact-sql.md)합니다.

### <a name="drop-a-database"></a>데이터베이스 삭제

1. SSMS를 시작 하 고 Linux의 SQL Server에서 서버에 연결

2. 개체 탐색기에서 확장을 *데이터베이스* 서버의 모든 데이터베이스의 목록을 보려면 폴더입니다.

3. 개체 탐색기에서 데이터베이스를 삭제 하려면 마우스 오른쪽 단추로 클릭 하 고 클릭 *삭제*

4. 에 *개체 삭제* 대화 상자에서 *기존 연결 닫기* 클릭 하 고 *확인*

데이터베이스 서버에서 성공적으로 삭제 됩니다. T-SQL을 사용 하 여 데이터베이스를 삭제 하려면 다음을 참조 하는 경우 [DROP DATABASE (SQL Server TRANSACT-SQL)](../t-sql/statements/drop-database-transact-sql.md)합니다.

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>작업 모니터를 사용 하 여 SQL Server 작업에 대 한 정보를 참조 하세요.

합니다 [작업 모니터](../relational-databases/performance-monitor/activity-monitor.md) 도구는 SQL Server Management Studio (SSMS)를 빌드하고 SQL Server 프로세스와 이러한 프로세스가 현재 인스턴스의 SQL Server에 미치는 영향에 대 한 정보를 표시 합니다.

1. SSMS를 시작 하 고 Linux의 SQL Server에서 서버에 연결

1. 개체 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 *server* 노드를 차례로 클릭 한 다음 *작업 모니터*

작업 모니터에는 다음 정보를 사용 하 여 확장 및 축소 가능한 창이 보여 줍니다.

- 개요
- 프로세스
- 리소스 대기
- 데이터 파일 I/O
- 비용이 드는 최근 쿼리
- 비용이 드는 활성 쿼리

창이 확장 되 면 작업 모니터는 인스턴스에서 정보를 쿼리 합니다. 창을 축소하면 해당 창에 대한 모든 쿼리 작업이 중지됩니다. 하나 이상의 창을 동시 인스턴스에서 다른 종류의 작업 보기를 확장할 수 있습니다.

## <a name="see-also"></a>참고자료
- [SSMS란 무엇인가요?](../ssms/sql-server-management-studio-ssms.md)
- [SSMS 사용 하 여 데이터베이스를 내보내고](sql-server-linux-migrate-ssms.md)
- [자습서: SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)
- [자습서: Transact-SQL 문 작성](../t-sql/tutorial-writing-transact-sql-statements.md)
- [서버 성능 및 작업 모니터링](../relational-databases/performance/server-performance-and-activity-monitoring.md)

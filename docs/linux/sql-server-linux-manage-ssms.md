---
title: SSMS를 사용하여 SQL Server on Linux 관리
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 05/21/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.openlocfilehash: 753845d41c946d955b80a927901f827ee4643567
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68000098"
---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>Windows에서 SQL Server Management Studio를 사용하여 SQL Server on Linux 관리

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 [SSMS(SQL Server Management Studio)](../ssms/sql-server-management-studio-ssms.md)를 소개하고 몇 가지 일반적인 작업을 안내합니다. SSMS는 Windows 애플리케이션이므로 Linux의 원격 SQL Server 인스턴스에 연결할 수 있는 Windows 머신이 있는 경우 SSMS를 사용합니다.

> [!TIP]
> SSMS를 실행할 Windows 머신이 없는 경우 새 [Azure Data Studio](../azure-data-studio/index.md)을 고려합니다. 이 항목은 SQL Server를 관리하기 위한 도구를 제공하고 Linux 및 Windows에서 실행됩니다.

[SSMS(SQL Server Management Studio)](../ssms/sql-server-management-studio-ssms.md)는 Microsoft에서 개발 및 관리를 위해 체험용으로 제공하는 SQL 도구 모음의 일부입니다. SSMS는 SQL Server의 모든 구성 요소를 액세스, 구성, 관리, 운영 및 개발하기 위한 통합 환경입니다. 온-프레미스, Docker 컨테이너 및 클라우드의 모든 플랫폼에서 실행되는 SQL Server에 연결할 수 있습니다. 또한 Azure SQL Database 및 Azure SQL Data Warehouse에 연결합니다. SSMS는 수많은 풍부한 스크립트 편집기와 광범위한 그래픽 도구 그룹을 결합하여 기술 수준에 상관없이 모든 개발자와 관리자에게 SQL Server에 대한 액세스 권한을 제공합니다.

SSMS는 다음과 같은 도구를 비롯하여 SQL Server에 대한 다양한 개발 및 관리 기능 세트를 제공합니다.

- 단일 또는 여러 SQL Server 인스턴스 구성, 모니터링 및 관리
- 데이터베이스 및 데이터 웨어하우스와 같은 데이터 계층 구성 요소 배포, 모니터링 및 업그레이드
- 데이터베이스 백업 및 복원
- T-SQL 쿼리 및 스크립트 작성 및 실행, 결과 확인
- 데이터베이스 개체에 대한 T-SQL 스크립트 생성
- 데이터베이스의 데이터 보기 및 편집
- 뷰, 테이블 및 저장 프로시저와 같은 T-SQL 쿼리 및 데이터베이스 개체를 시각적으로 디자인

SSMS에 대한 자세한 내용은 [SSMS란?](../ssms/sql-server-management-studio-ssms.md)을 참조하세요.

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>최신 버전의 SSMS(SQL Server Management Studio) 설치

SQL Server로 작업하는 경우 항상 최신 버전의 SSML(SQL Server Management Studio)를 사용해야 합니다. 최신 버전의 SSMS는 지속적으로 업데이트되고 최적화되며 현재 SQL Server on Linux에서 작동합니다. 최신 버전을 다운로드하고 설치하려면 [SQL Server Management Studio 다운로드](../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요. 최신 상태를 유지하기 위해 최신 버전의 SSMS는 다운로드할 수 있는 새 버전이 있는 경우 메시지를 표시합니다.

> [!NOTE]
> SSMS를 사용하여 Linux를 관리하기 전에 Linux의 SSMS에 대한 [알려진 문제](sql-server-linux-release-notes.md)를 검토합니다.

## <a name="connect-to-sql-server-on-linux"></a>SQL Server on Linux에 연결

다음 기본 단계를 사용하여 연결합니다.

1. Windows 검색 상자에 **Microsoft SQL Server Management Studio**를 입력하여 SSMS를 시작한 다음, 데스크톱 앱을 클릭합니다.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png)

1. **서버에 연결** 창에서 다음 정보를 입력합니다(SSMS가 이미 실행 중인 경우 **연결 > 데이터베이스 엔진**을 클릭하여 **서버에 연결** 창 열기).

   | 설정 | 설명 |
   |-----|-----|
   | **서버 유형** | 기본값은 데이터베이스 엔진입니다. 이 값을 변경하지 마세요. |
   | **서버 이름** | 대상 Linux SQL Server 머신의 이름 또는 IP 주소를 입력합니다. |
   | **인증** | SQL Server on Linux의 경우 **SQL Server 인증**을 사용합니다. |
   | **로그인** | 서버의 데이터베이스에 대한 액세스 권한이 있는 사용자의 이름을 입력합니다(예: 설치하는 동안 생성된 기본 **SA** 계정). |
   | **암호** | 지정된 사용자의 암호를 입력합니다(**SA** 계정의 경우 설치하는 동안 이 암호를 만들었음). |

    ![SQL Server Management Studio: SQL Database 서버에 연결](./media/sql-server-linux-manage-ssms/connect.png)

1. **연결**을 클릭합니다.

    > [!TIP]
    > 연결 오류가 발생하는 경우 먼저 오류 메시지에서 문제를 진단합니다. 그런 다음 [connection troubleshooting recommendations](sql-server-linux-troubleshooting-guide.md#connection)(연결 문제 해결 권장 사항)를 검토합니다.
 
1. SQL Server에 성공적으로 연결한 후 **개체 탐색기**가 열리며 이제 데이터베이스에 액세스하여 관리 작업을 수행하거나 데이터를 쿼리할 수 있습니다.

## <a name="run-transact-sql-queries"></a>Transact-SQL 쿼리 실행

서버에 연결한 후 데이터베이스에 연결하고 Transact-SQL 쿼리를 실행할 수 있습니다. Transact-SQL 쿼리는 거의 모든 데이터베이스 작업에 사용할 수 있습니다.

1. **개체 탐색기**에서 서버의 대상 데이터베이스로 이동합니다. 예를 들어 **시스템 데이터베이스**를 확장하여 **master** 데이터베이스로 작업합니다.

1. 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.

1. 쿼리 창에서 Transact-SQL 쿼리를 작성하여 서버에 있는 모든 데이터베이스의 이름을 반환하도록 선택합니다.

   ```sql
   SELECT [Name]
   FROM sys.Databases
   ```

   쿼리를 처음 작성하는 경우 [Transact-SQL 문 작성](../t-sql/tutorial-writing-transact-sql-statements.md)을 참조하세요.

1. **실행** 단추를 클릭하여 쿼리를 실행하고 결과를 확인합니다.

   ![성공했습니다. SQL Database 서버에 연결: SQL Server Management Studio](./media/sql-server-linux-manage-ssms/execute-query.png)

Transact-SQL 쿼리를 사용하여 거의 모든 관리 작업을 수행할 수 있지만, SSMS는 SQL Server을 보다 쉽게 관리할 수 있는 그래픽 도구입니다. 다음 섹션에서는 그래픽 사용자 인터페이스 사용에 대한 몇 가지 예제를 제공합니다.

## <a name="create-and-manage-databases"></a>데이터베이스 만들기 및 관리

*master* 데이터베이스에 연결되어 있는 동안 서버에 데이터베이스를 만들고 기존 데이터베이스를 수정하거나 삭제할 수 있습니다. 다음 단계에서는 Management Studio를 통해 여러 가지 일반적인 데이터베이스 관리 작업을 수행하는 방법을 설명합니다. 이 작업을 수행하려면 SQL Server on Linux를 설치할 때 만든 서버 수준 보안 주체 로그인을 사용하여 *master* 데이터베이스에 연결되어 있는지 확인합니다.

### <a name="create-a-new-database"></a>새 데이터베이스 만들기

1. SQL Server on Linux에서 SSMS 시작 및 서버에 연결

2. 개체 탐색기에서 ‘데이터베이스’ 폴더를 마우스 오른쪽 단추로 클릭한 다음, *새 데이터베이스...”를 클릭합니다. 

3. ‘새 데이터베이스’ 대화 상자에서 새 데이터베이스의 이름을 입력한 다음, ‘확인’을 클릭합니다.  

새 데이터베이스가 서버에서 생성되었습니다. T-SQL을 사용하여 새 데이터베이스를 만들려면 [CREATE DATABASE(SQL Server Transact-SQL)](../t-sql/statements/create-database-sql-server-transact-sql.md)를 참조하세요.

### <a name="drop-a-database"></a>데이터베이스 삭제

1. SQL Server on Linux에서 SSMS 시작 및 서버에 연결

2. 개체 탐색기에서 ‘데이터베이스’ 폴더를 확장하여 서버에 있는 모든 데이터베이스 목록을 표시합니다. 

3. 개체 탐색기에서 삭제하려는 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음, ‘삭제’를 클릭합니다. 

4. ‘개체 삭제’ 대화 상자에서 ‘기존 연결 닫기’를 선택한 후 ‘다음’을 클릭합니다.   

데이터베이스가 서버에서 삭제되었습니다. T-SQL을 사용하여 데이터베이스를 삭제하려면 [DROP DATABASE(SQL Server Transact-SQL)](../t-sql/statements/drop-database-transact-sql.md)를 참조하세요.

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>작업 모니터를 사용하여 SQL Server 작업에 대한 정보 보기

[작업 모니터](../relational-databases/performance-monitor/activity-monitor.md) 도구는 SSMS(SQL Server Management Studio)에 기본 제공되며 SQL Server 프로세스 및 해당 프로세스가 SQL Server의 현재 인스턴스에 미치는 영향에 대한 정보를 표시합니다.

1. SQL Server on Linux에서 SSMS 시작 및 서버에 연결

1. 개체 탐색기에서 ‘서버’ 노드를 마우스 오른쪽 단추로 클릭한 후 ‘작업 모니터’를 클릭합니다.  

작업 모니터는 다음 정보가 포함된 확장 및 축소 가능한 창을 표시합니다.

- 개요
- 프로세스
- 리소스 대기
- 데이터 파일 I/O
- 비용이 높은 최근 쿼리
- 비용이 높은 활성 쿼리

창을 확장하면 작업 모니터는 인스턴스에서 정보를 쿼리합니다. 창을 축소하면 해당 창에 대한 모든 쿼리 작업이 중지됩니다. 하나 이상의 창을 동시에 확장하여 인스턴스에 대한 여러 종류의 작업을 볼 수 있습니다.

## <a name="see-also"></a>관련 항목:
- [SSMS란 무엇인가요?](../ssms/sql-server-management-studio-ssms.md)
- [SSMS를 사용하여 데이터베이스 내보내기 및 가져오기](sql-server-linux-migrate-ssms.md)
- [자습서: SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)
- [자습서: Transact-SQL 문 작성](../t-sql/tutorial-writing-transact-sql-statements.md)
- [서버 성능 및 작업 모니터링](../relational-databases/performance/server-performance-and-activity-monitoring.md)

---
title: (SybaseToSQL) SQL Server에 SSMA 구성 요소 설치 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6121c75390e7493052a16b2e898eac69283e41ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63294566"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>SQL Server에 SSMA 구성 요소 설치(SybaseToSQL)
SSMA를 서버 쪽 데이터 마이그레이션에 사용할을 설치 하는 것 외에도 설치 해야 구성 요소가 실행 하는 컴퓨터의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이러한 구성 요소에는 데이터 마이그레이션 및 Sybase 공급자 서버-투-서버 연결을 사용 하도록 지 원하는 SSMA 확장 팩을 포함 합니다.  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA for Sybase 확장 팩  
SSMA 확장 팩은 데이터베이스를 추가 **sysdb** 하 고 **ssmatesterdb_syb**, 지정 된 인스턴스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 합니다 **sysdb** 데이터베이스 테이블 및 데이터를 마이그레이션하는 데 필요한 저장된 프로시저를 포함 합니다. **ssmatester_syb** 스키마를 포함 하는 데이터베이스 **ssma_sybase_utilities**, 테스터 SSMA 구성 요소에 사용 되는 개체 (테이블, 트리거, 뷰)를 생성 됩니다.  
  
또한 데이터를 마이그레이션할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA 만듭니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이그레이션에 대 한 서버 쪽 데이터 마이그레이션 엔진을 사용 하는 경우 에이전트 작업입니다.  
  
### <a name="installing-the-extension-pack"></a>확장 팩 설치  
데이터를 마이그레이션하기 전에 든 지 확장 팩을 설치 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
> [!IMPORTANT]  
> 확장 팩을 설치 하려면 인스턴스에서 sysadmin 서버 역할의 멤버 여야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
**확장 팩을 설치 하려면**  
  
1.  SSMA for Sybase 확장 팩 복사 합니다. *n*합니다. Install.exe, 여기서 *n* 는 실행 중인 컴퓨터에 빌드 번호 이며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
2.  Sybase 확장 팩 SSMA 두 번 클릭 합니다. *n*합니다. Install.exe 합니다.  
  
3.  시작 페이지에서 클릭 **다음**합니다.  
  
4.  최종 사용자 사용권 계약 페이지에서 사용권 계약을 읽습니다. 동의 하는 경우 선택 합니다 **사용권 계약에 동의** 확인란을 선택한 다음 클릭 **다음**합니다.  
  
5.  설치 유형 선택 페이지에서 클릭 **표준**합니다.  
  
6.  준비 설치 페이지를 클릭 **설치**합니다.  
  
7.  완료 된 설치의 첫 번째 단계 페이지에서 클릭 **다음**합니다.  
  
    인스턴스를 선택 하면 새 대화 상자가 표시 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확장 팩 설치에 대 한 합니다.  
  
8.  인스턴스 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ASE 데이터베이스 마이그레이션 선택한 클릭 위치 **다음**합니다.  
  
    기본 인스턴스는 컴퓨터와 동일한 이름입니다. 명명 된 인스턴스 뒤에 백슬래시 및 인스턴스 이름입니다.  
  
9. 연결 매개 변수 페이지에서 인증 방법을 선택한 다음 클릭 **다음**합니다.  
  
    Windows 인증 Windows 자격 증명을 사용 하 여 인스턴스의 로그온 하려고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 입력 해야 인증을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 이름 및 암호입니다.  
  
10. 서버 관리 페이지에서 선택 **유틸리티 데이터베이스 설치** *n*여기서 *n* 버전 번호 이며 클릭 **다음**합니다.  
  
    합니다 **sysdb** 데이터베이스가 만들어지고 저장된 프로시저는 해당 데이터베이스에 만들어집니다.  
  
    하는 경우 **테스터 데이터베이스 설치** 옵션이 선택 되어 테스터 **ssmatesterdb_syb** 데이터베이스가 만들어집니다.  
  
11. 다른 인스턴스에 유틸리티를 설치 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 선택 **인스턴스로 반환**를 클릭 하 고 **다음**합니다. 또는 마법사를 종료 하려면 클릭 **종료**합니다.  
  
### <a name="sql-server-database-objects"></a>SQL Server 데이터베이스 개체  
참조는 확장 팩을 설치한 후는 **ssma_syb.bcp_migration_packages** 테이블에 **sysdb** 데이터베이스입니다. 다음 저장된 프로시저도 표시 됩니다.  
  
-   **bcp_clean_migration_data**  
  
-   **bcp_ensure_message_table**  
  
-   **bcp_insert_new_message**  
  
-   **bcp_post_process**  
  
-   **bcp_read_new_migration_messages**  
  
-   **bcp_save_migration_package**  
  
-   **bcp_smart_truncate**  
  
-   **bcp_start_migration_process**  
  
-   **get_jobstep_info**  
  
-   **stop_agent_process**  
  
데이터를 마이그레이션할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA 만듭니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업입니다. 이러한 작업 이름은 **ssma_syb 데이터 마이그레이션 패키지 {GUID}** 에 표시 됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 노드의 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 작업 폴더에 있습니다.  
  
## <a name="sybase-providers"></a>Sybase 공급자  
ASE에서 데이터를 마이그레이션하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ASE 사이 직접 SQL Azure 데이터 마이그레이션 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure입니다. 이 데이터 마이그레이션 속도가 느려질 것 때문에 SSMA 통해는 이동 하지 않습니다.  
  
### <a name="installing-the-sybase-providers"></a>Sybase 공급자를 설치합니다.  
다음 지침을 Sybase 공급자를 설치 하기 위한 기본 설치 단계를 제공 합니다. 정확한 지시 Sybase 설치 프로그램의 버전에 따라 달라 집니다.  
  
> [!IMPORTANT]  
> 설치 프로그램을 실행 하기 전에 사용권 계약을 위반 하지 않는 확인 합니다.  
  
1.  Sybase ASE 설치 프로그램을 실행 합니다.  
  
2.  사용자 지정 설치를 선택 합니다.  
  
3.  기능 선택 페이지에서 ODBC, OLE DB 및 ADO.NET 데이터 공급자를 선택 합니다.  
  
4.  선택한 기능을 확인 한 다음 클릭 **완료** 데이터 공급자를 설치 합니다.  
  
## <a name="see-also"></a>관련 항목  
[클라이언트 Sybase 용 SSMA 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Sybase ASE 데이터베이스를 SQL Server-Azure SQL DB로 마이그레이션 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

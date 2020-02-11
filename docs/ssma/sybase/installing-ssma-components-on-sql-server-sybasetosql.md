---
title: SQL Server에 SSMA 구성 요소 설치 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1fbc3a8f74b21bd5a53bdd874b5c41ef522e29f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029014"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>SQL Server에 SSMA 구성 요소 설치(SybaseToSQL)
SSMA를 설치 하는 것 외에도 서버 쪽 데이터 마이그레이션을 사용 하기 위해를 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하는 컴퓨터에 구성 요소를 설치 해야 합니다. 이러한 구성 요소에는 데이터 마이그레이션을 지 원하는 SSMA 확장 팩과 서버 간 연결을 설정 하는 Sybase 공급자가 포함 됩니다.  
  
## <a name="ssma-for-sybase-extension-pack"></a>Sybase 확장 팩용 SSMA  
SSMA 확장 팩은 지정 된 인스턴스에 **sysdb** 및 **ssmatesterdb_syb**데이터베이스를 추가 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **Sysdb** 데이터베이스에는 데이터를 마이그레이션하는 데 필요한 테이블과 저장 프로시저가 포함 되어 있습니다. **Ssmatester_syb** 데이터베이스에는 ssma 테스터 구성 요소에서 사용 하는 개체 (테이블, 트리거, 뷰)가 생성 되는 스키마 **ssma_sybase_utilities**포함 되어 있습니다.  
  
또한 데이터를로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션하는 경우 ssma는 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션에 서버 쪽 데이터 마이그레이션 엔진을 사용 하는 경우 에이전트 작업을 만듭니다.  
  
### <a name="installing-the-extension-pack"></a>확장 팩 설치  
에 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션하기 전에 언제 든 지 확장 팩을 설치할 수 있습니다.  
  
> [!IMPORTANT]  
> 확장 팩을 설치 하려면 인스턴스에서 sysadmin 서버 역할의 멤버 여야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**확장 팩을 설치 하려면**  
  
1.  Sybase 확장 팩용 SSMA를 복사 합니다. *n*. 을 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하는 컴퓨터에 .exe를 설치 합니다. 여기서 *n* 은 빌드 번호입니다.  
  
2.  Sybase 확장 팩 용 SSMA를 두 번 클릭 합니다. *n*. Setup.exe를 설치 합니다.  
  
3.  Welcome 페이지에서 **다음**을 클릭합니다.  
  
4.  최종 사용자 사용권 계약 페이지에서 사용권 계약을 읽습니다. 동의 **하면 동의 함 확인란을** 선택 하 고 **다음**을 클릭 합니다.  
  
5.  설치 유형 선택 페이지에서 **일반**을 클릭 합니다.  
  
6.  설치 준비 완료 페이지에서 **설치**를 클릭 합니다.  
  
7.  설치의 첫 번째 단계를 완료 했습니다. 페이지에서 **다음**을 클릭 합니다.  
  
    새 대화 상자가 표시 되 고 확장 팩을 설치할 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 선택 합니다.  
  
8.  ASE 데이터베이스를 마이그레이션하려 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 인스턴스를 선택 하 고 **다음**을 클릭 합니다.  
  
    기본 인스턴스의 이름은 컴퓨터와 동일 합니다. 명명 된 인스턴스에는 백슬래시와 인스턴스 이름이 나옵니다.  
  
9. 연결 매개 변수 페이지에서 인증 방법을 선택 하 고 **다음**을 클릭 합니다.  
  
    Windows 인증에서는 Windows 자격 증명을 사용 하 여 인스턴스에 로그온을 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 인증을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 로그인 이름 및 암호를 입력 해야 합니다.  
  
10. 서버 관리 페이지에서 **유틸리티 데이터베이스 설치** *를 선택*합니다. 여기서 *n* 은 버전 번호이 고 **다음**을 클릭 합니다.  
  
    **Sysdb** 데이터베이스가 생성 되 고 해당 데이터베이스에 저장 프로시저가 생성 됩니다.  
  
    **테스터 데이터베이스 설치** 옵션을 선택 하면 테스터 **ssmatesterdb_syb** 데이터베이스가 생성 됩니다.  
  
11. 다른 인스턴스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]유틸리티를 설치 하려면 **인스턴스로 돌아가기**를 선택 하 고 **다음**을 클릭 합니다. 또는 마법사를 종료 하려면 **끝내기**를 클릭 합니다.  
  
### <a name="sql-server-database-objects"></a>데이터베이스 개체 SQL Server  
확장 팩을 설치한 후에는 **sysdb** 데이터베이스의 **ssma_syb bcp_migration_packages** 테이블이 표시 됩니다. 다음 저장 프로시저도 표시 됩니다.  
  
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
  
데이터를로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션할 때마다 ssma는 에이전트 작업을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 만듭니다. 이러한 작업에는 **데이터 마이그레이션 패키지 {GUID} ssma_syb**이름이 지정 되 고 작업 폴더 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 에이전트 노드에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 표시 됩니다.  
  
## <a name="sybase-providers"></a>Sybase 공급자  
ASE에서/Sql Azure로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터를 마이그레이션하는 경우 데이터는 ase와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/sql azure 간에 직접 마이그레이션됩니다. 이는 데이터 마이그레이션의 속도가 느려지므로 SSMA를 통해 이동 하지 않습니다.  
  
### <a name="installing-the-sybase-providers"></a>Sybase 공급자 설치  
다음 지침은 Sybase 공급자를 설치 하는 기본 설치 단계를 제공 합니다. 정확한 지침은 Sybase 설치 프로그램의 버전에 따라 달라 집니다.  
  
> [!IMPORTANT]  
> 설치 프로그램을 실행 하기 전에 사용권 계약을 위반 하지 않는지 확인 합니다.  
  
1.  Sybase ASE 설치 프로그램을 실행 합니다.  
  
2.  사용자 지정 설치를 선택 합니다.  
  
3.  기능 선택 페이지에서 ODBC, OLE DB 및 ADO.NET 데이터 공급자를 선택 합니다.  
  
4.  선택한 기능을 확인 한 다음 **마침** 을 클릭 하 여 데이터 공급자를 설치 합니다.  
  
## <a name="see-also"></a>참고 항목  
[Sybase 용 SSMA 클라이언트 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Sybase ASE 데이터베이스를 SQL Server로 마이그레이션-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

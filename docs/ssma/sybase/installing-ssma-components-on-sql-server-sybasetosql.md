---
title: "SQL Server (SybaseToSQL)에 SSMA 구성 요소 설치 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
caps.latest.revision: "10"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4c32a766183491f9ef398e1d1f96c3bb1e05aca4
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>SQL Server (SybaseToSQL)에 SSMA 구성 요소 설치
서버 쪽 데이터 마이그레이션을 사용 하 여에 대 한 SSMA를 설치 하는 것 외에도 설치 해야 구성 요소를 실행 하는 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 이러한 구성 요소를 지 원하는 데이터 마이그레이션 및 서버 간 연결을 허용 하도록 Sybase 공급자 SSMA 확장 팩을 포함 합니다.  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA for Sybase 확장 팩  
데이터베이스를 추가 하는 SSMA 확장 팩 **sysdb** 및 **ssmatesterdb_syb**을의 지정 된 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. **sysdb** 데이터베이스 테이블 및 데이터를 마이그레이션하는 데 필요한 저장된 프로시저를 포함 합니다. **ssmatester_syb** 데이터베이스 스키마가 포함 **ssma_sybase_utilities**, SSMA 테스터 구성 요소에서 사용 되는 개체 (테이블, 트리거, 뷰) 생성 됩니다.  
  
또한 데이터를 마이그레이션할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA 만듭니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 서버 쪽 데이터 마이그레이션 엔진으로 데이터를 마이그레이션하는 데 사용 되는 경우 에이전트 작업입니다.  
  
### <a name="installing-the-extension-pack"></a>확장 팩 설치  
데이터를 마이그레이션하기 전에 든 지 확장 팩을 설치 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
> [!IMPORTANT]  
> 확장 팩을 설치 하려면 인스턴스에서 sysadmin 서버 역할의 구성원 이어야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
**확장 팩을 설치 하려면**  
  
1.  SSMA for Sybase 확장 팩 복사 합니다. *n*. Install.exe 여기서  *n*  실행 중인 컴퓨터에 있는 빌드 번호 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
2.  Sybase 확장 팩 SSMA를 두 번 클릭 합니다. *n*. Install.exe 합니다.  
  
3.  시작 페이지에서 클릭 **다음**합니다.  
  
4.  최종 사용자 사용권 계약 페이지에서 사용권 계약을 읽습니다. 동의 하면 선택 된 **사용권 계약에 동의** 확인란을 선택한 다음 클릭 **다음**합니다.  
  
5.  설치 유형 선택 페이지에서 클릭 **일반**합니다.  
  
6.  설치 준비 완료 페이지를 클릭 **설치**합니다.  
  
7.  완료 된 첫 번째 단계 설치 페이지에서 클릭 **다음**합니다.  
  
    인스턴스를 선택 하면 새 대화 상자가 표시 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 확장 팩 설치에 대 한 합니다.  
  
8.  인스턴스를 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ASE 마이그레이션하기 선택한 다음 클릭 위치 **다음**합니다.  
  
    기본 인스턴스는 컴퓨터와 동일한 이름이 있습니다. 명명 된 인스턴스 수 뒤에 백슬래시 및 인스턴스 이름입니다.  
  
9. 연결 매개 변수 페이지에서 인증 방법을 선택한 다음 클릭 **다음**합니다.  
  
    Windows 인증 Windows 자격 증명을 사용 하 여 인스턴스의에 로그온 하려고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 입력 해야 인증을 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 로그인 이름 및 암호.  
  
10. 서버 관리 페이지에서 선택 **설치 유틸리티 데이터베이스**  *n* 여기서  *n*  버전 번호 이며 클릭 **다음**합니다.  
  
    **sysdb** 데이터베이스가 만들어지고 저장된 프로시저는 해당 데이터베이스에 만들어집니다.  
  
    경우 **테스터 데이터베이스 설치** 옵션을 선택은 테스터 **ssmatesterdb_syb** 데이터베이스가 생성 됩니다.  
  
11. 다른 인스턴스에 유틸리티를 설치 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]선택, **인스턴스를 반환**, 클릭 하 고 **다음**합니다. 마법사를 종료 하려면 또는 **종료**합니다.  
  
### <a name="sql-server-database-objects"></a>SQL Server 데이터베이스 개체  
참조 확장 팩을 설치한 후 됩니다는 **ssma_syb.bcp_migration_packages** 테이블에 **sysdb** 데이터베이스입니다. 다음 저장된 프로시저도 나타납니다.  
  
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
  
데이터를 마이그레이션하기 될 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA 만듭니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업입니다. 이러한 작업 이름은 **ssma_syb 데이터 마이그레이션 패키지 {GUID}**에 표시 됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 의 에이전트 노드 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 작업 폴더에 있습니다.  
  
## <a name="sybase-providers"></a>Sybase 공급자  
ASE에에서 데이터를 마이그레이션할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure 데이터 ASE 간에 직접 마이그레이션합니다 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure입니다. 따르지 않는 SSMA를 통해이 데이터 마이그레이션 속도가 느려질 것 때문에 있습니다.  
  
### <a name="installing-the-sybase-providers"></a>Sybase 공급자 설치  
다음 명령은 Sybase 공급자를 설치 하기 위한 기본 설치 단계를 제공 합니다. 정확한 지침은 Sybase 설치 프로그램의 버전에 따라 달라 집니다.  
  
> [!IMPORTANT]  
> 설치 프로그램을 실행 하기 전에 사용권 계약을 위반 하지 않는 확인 합니다.  
  
1.  Sybase ASE 설치 프로그램을 실행 합니다.  
  
2.  사용자 지정 설치를 선택 합니다.  
  
3.  기능 선택 페이지에서 ODBC, OLE DB 및 ADO.NET 데이터 공급자를 선택 합니다.  
  
4.  선택한 기능을 확인 한 다음 클릭 **마침** 데이터 공급자를 설치 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SSMA for Sybase 클라이언트 &#40; 설치 SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Azure SQL DB &#40; SQL Server-Sybase ASE 데이터베이스 마이그레이션 SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

---
title: SQL Server (SybaseToSQL)에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server
ms.assetid: dd368a1a-45b0-40e9-b4d3-5cdb48c26606
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2d7370b9b219c43bab4bfdc45377795edf148fc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63207859"
---
# <a name="connecting-to-sql-server-sybasetosql"></a>SQL Server에 연결(SybaseToSQL)
Sybase 적응형 Server Enterprise (ASE) 데이터베이스를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 대상 인스턴스 중 하나에 연결 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. SSMA 가져옵니다 인스턴스의 모든 데이터베이스에 대 한 메타 데이터에 연결 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터베이스 메타 데이터를 표시 하 고는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기입니다. SSMA의는 인스턴스에 대 한 정보를 저장 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 해도 암호를 저장 하지 않습니다.  
  
에 대 한 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로젝트를 닫을 때까지 활성 상태로 유지 합니다. 에 다시 연결 해야 프로젝트를 열면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 활성 서버에 연결 하려는 경우. 데이터베이스 개체를 로드할 때까지 오프 라인으로 작업할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 마이그레이션합니다.  
  
인스턴스에 대 한 메타 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자동으로 동기화 되지 않습니다. 대신 메타 데이터를 업데이트 하려는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기를 수동으로 업데이트 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 설명 된 대로 메타 데이터를 "Synchronizing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터"이이 항목의 뒷부분에 나오는 섹션입니다.  
  
## <a name="required-sql-server-permissions"></a>필요한 SQL Server 사용 권한  
에 연결 하는 데 사용 되는 계정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 해당 계정에서 수행 되는 작업에 따라 다른 권한이 필요 합니다.  
  
-   ASE 개체를 변환할 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문에서 메타 데이터를 업데이트할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 변환 된 구문에 스크립트를 저장 하려면 계정에는 인스턴스에 로그인 할 권한을 있어야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
-   데이터베이스 개체를 로드 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 최소 권한 요구 사항인 자격이 합니다 **db_owner** 대상 데이터베이스의 데이터베이스 역할.  
  
-   데이터를 마이그레이션하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 계정은의 구성원 이어야 합니다.는 **sysadmin** 서버 역할입니다. 실행 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 데이터 마이그레이션 패키지 있습니다.  
  
-   SSMA에서 생성 되는 코드를 실행 하려면 계정이 있어야 **Execute** 의 모든 사용자 정의 함수에 대 한 권한을 합니다 **ssma_syb** 의 스키마를 **sysdb** 데이터베이스입니다. 이러한 함수는 ASE 시스템 함수의 해당 하는 기능을 제공 하 고 변환 된 개체에 의해 사용 됩니다.  
  
경우에 연결 하는 데 사용 되는 계정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모든 마이그레이션을 수행 하려면 작업, 계정은의 구성원 이어야 합니다는 **sysadmin** 서버 역할입니다.  
  
## <a name="establishing-a-sql-server-connection"></a>SQL Server에 연결  
ASE 데이터베이스 개체를 변환 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구문을 인스턴스의 연결을 설정 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ASE 데이터베이스 또는 데이터베이스를 마이그레이션할 하려는 합니다.  
  
연결 속성을 정의할 때에 데이터베이스 개체 및 데이터 마이그레이션할 수 지정 합니다. 에 연결한 후 ASE 스키마 수준에서이 매핑을 사용자 지정할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [Sybase ASE 스키마를 SQL Server 스키마 매핑 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)합니다.  
  
> [!IMPORTANT]  
> 에 연결 하려고 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 했는지 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 되 고 연결을 허용할 수 있습니다.  
  
**SQL Server에 연결 하려면**  
  
1.  에 **파일** 메뉴에서 **SQL Server에 연결**합니다.  
  
    이전에 연결한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 명령 이름은 **SQL Server에 다시 연결**합니다.  
  
2.  연결 대화 상자에서 이름을 입력 하거나 선택 된 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
    -   로컬 컴퓨터의 기본 인스턴스에 연결 하는 경우 입력할 수 있습니다 **localhost** 또는 점 ( **.** ).  
  
    -   다른 컴퓨터의 기본 인스턴스에 연결 하는 경우에 컴퓨터의 이름을 입력 합니다.  
  
    -   다른 컴퓨터에 명명 된 인스턴스에 연결 하는 경우 뒤에 백슬래시 및 인스턴스 이름을 MyServer\MyInstance 같은 컴퓨터 이름을 입력 합니다.  
  
3.  경우 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 사용 되는 포트 번호를 입력, 기본이 아닌 포트에서 연결을 허용 하도록 구성 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결 합니다 **서버 포트** 상자입니다. 기본 인스턴스에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 기본 포트 번호는 1433입니다. 명명 된 인스턴스의 경우 SSMA에서 포트 번호 가져오기를 시도 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스입니다.  
  
4.  에 **데이터베이스** 상자에 대상 데이터베이스의 이름을 입력 합니다.  
  
    다시 연결할 때이 옵션을 사용할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
5.  에 **인증** 상자에서 연결에 사용할 인증 유형을 선택 합니다. 현재 Windows 계정을 사용 하려면 선택 **Windows 인증**합니다. 사용 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 선택 **SQL Server 인증** 로그인 이름 및 암호를 제공 합니다.  
  
6.  보안 연결에 대 한 두 개의 추가 되는 **연결 암호화** 하 고 **TrustServerCertificate** 확인란 합니다. 경우에만 **연결 암호화** 을 선택 합니다 **TrustServerCertificate** 확인란이 표시 됩니다. 때 **연결 암호화** 확인란이 선택 되어 (true) 및 **TrustServerCertificate** 선택 하지 않으면 (false) 검사지 것입니다 SQL Server SSL 인증서입니다. 서버 인증서의 유효성 검사는 SSL 핸드셰이크의 일부로 서버가 연결할 올바른 서버인지 확인합니다. 이 위해 클라이언트 쪽 및 서버 쪽에서 인증서를 설치 합니다.  
  
7.  **연결**을 클릭합니다.  
  
**더 높은 버전 호환성**  
  
-   에 연결할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 생성 되는 마이그레이션 프로젝트의 경우 2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005입니다.  
  
-   에 연결할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 생성 되는 마이그레이션 프로젝트의 경우 2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 있지만 즉, 더 낮은 버전에 연결할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   에 연결할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 만든 프로젝트의 SQL Server 2012 인 경우.  
  
-   더 높은 버전 호환성 SQL Azure 대해 올바르지 않습니다.  
  
||||||||
|-|-|-|-|-|-|-|
|**프로젝트 형식 및 대상 서버 버전**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (버전: 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (버전: 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Version:13.x)|SQL Azure|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||사용자 계정 컨트롤|예|예|사용자 계정 컨트롤||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||사용자 계정 컨트롤|예|사용자 계정 컨트롤||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||||사용자 계정 컨트롤|사용자 계정 컨트롤|| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||사용자 계정 컨트롤||  
|SQL Azure||||||사용자 계정 컨트롤|  
  
> [!IMPORTANT]
> 버전에 따라 하지 않지만 프로젝트 형식에 따라 데이터베이스 개체의 변환 수행 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결 되어 있습니다. 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 프로젝트 변환이 수행 됩니다 당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005의 더 높은 버전에 연결 되어 있더라도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016)  
  
## <a name="reconnecting-to-sql-server"></a>SQL Server에 다시 연결  
에 대 한 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로젝트를 닫을 때까지 활성 상태로 유지 합니다. 에 다시 연결 해야 프로젝트를 열면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 활성 서버에 연결 하려는 경우. 메타 데이터를 로드 데이터베이스 개체를 업데이트할 때까지 오프 라인으로 작업할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 데이터를 마이그레이션합니다.  
  
에 다시 연결 하는 절차 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결을 설정 하는 절차와 같습니다.  
  
## <a name="synchronizing-sql-server-metadata"></a>SQL Server 메타 데이터를 동기화합니다.  
에 대 한 메타 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 자동 업데이트 되지 않습니다. 메타 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 처음 연결할 때 메타 데이터 탐색기는 메타 데이터의 스냅숏으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 또는 수동으로 업데이트 메타 데이터는 마지막 시간입니다. 수동으로 모든 데이터베이스에 대해 또는 단일 데이터베이스 또는 데이터베이스 개체에 대 한 메타 데이터를 업데이트할 수 있습니다.  
  
**메타 데이터를 동기화 하려면**  
  
1.  에 연결 되어 있는지 확인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기 데이터베이스 옆의 확인란을 선택 또는 데이터베이스 스키마를 업데이트 합니다.  
  
    예를 들어, 모든 데이터베이스에 대 한 메타 데이터를 업데이트 하려면 선택 상자 옆 **데이터베이스**합니다.  
  
3.  데이터베이스 또는 개별 데이터베이스 또는 데이터베이스 스키마를 마우스 오른쪽 단추로 클릭 하 고 선택한 **데이터베이스와 동기화**합니다.  
  
## <a name="next-step"></a>다음 단계  
다음 단계는 마이그레이션 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   ASE 데이터베이스 및 스키마 간의 매핑을 사용자 지정 하려는 경우 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 및 스키마를 참조 하세요 [매핑 Sybase ASE 스키마를 SQL Server 스키마에 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)합니다.  
  
-   프로젝트에 대 한 구성 옵션을 사용자 지정 하려는 경우 참조 [프로젝트 옵션 설정 &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)합니다.  
  
-   참조를 하려는 경우에 사용자 지정 원본 및 대상 데이터 형식 매핑 [매핑 Sybase ASE 및 SQL Server 데이터 형식 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)합니다.  
  
-   이러한 템플릿 중 하나를 수행 해야 하는 경우에 Sybase ASE 데이터베이스 개체 정의 변환할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 정의 합니다. 자세한 내용은 [Sybase ASE 데이터베이스 개체 변환 &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
[Sybase ASE 데이터베이스를 SQL Server-Azure SQL DB로 마이그레이션 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

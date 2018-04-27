---
title: SQL Server (MySQLToSQL)에 연결 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- connecting to SQL Server 2008, SQL Server permission
- connecting to SQL Server 2008, synchronization
ms.assetid: 08233267-693e-46e6-9ca3-3a3dfd3d2be7
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9edacaa537f2df61dcdf131a5930bf5bfb92c1a8
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="connecting-to-sql-server-mysqltosql"></a>SQL Server (MySQLToSQL)에 연결
SQL Server에 MySQL 데이터베이스를 마이그레이션하려면 대상 SQL Server 인스턴스에 연결 해야 합니다. 에 연결할 때 SSMA의 SQL Server 인스턴스의 모든 데이터베이스에 대 한 메타 데이터를 가져오고 SQL Server 메타 데이터 탐색기에서 데이터베이스 메타 데이터를 표시 합니다. SSMA에 연결 되어 있지만 암호를 저장 하지 않는 SQL Server의 인스턴스 정보를 저장 합니다.  
  
SQL Server에 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 다시 연결 해야 SQL Server로 활성 서버에 연결 하려는 경우. SQL Server에 데이터베이스 개체를 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업 합니다.  
  
SQL Server의 인스턴스에 대 한 메타 데이터를 자동으로 동기화 되지 않습니다. 대신, SQL Server 메타 데이터 탐색기에서 메타 데이터를 업데이트 하려면 SQL Server 메타 데이터 수동으로 업데이트 해야 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "SQL Server 메타 데이터 동기화 중" 섹션을 참조 하십시오.  
  
## <a name="required-sql-server-permissions"></a>필요한 SQL Server 사용 권한  
SQL Server에 연결 하는 데 사용 되는 계정에는 계정 수행 하는 작업에 따라 다른 권한이 필요 합니다.  
  
-   MySQL 개체를 변환 하려면 [!INCLUDE[tsql](../../includes/tsql_md.md)] 를 SQL Server에서 메타 데이터를 업데이트 하거나 저장 하는 변환 된 구문을 구문, 스크립트, 계정에는 SQL Server 인스턴스에 로그온 할 수 있는 권한이 있어야 합니다.  
  
-   SQL Server에 데이터베이스 개체를 로드 하려면의 최소 권한 요구 사항은의 멤버 자격이 **db_owner** 대상 데이터베이스의 데이터베이스 역할입니다.  
  
## <a name="establishing-a-sql-server-connection"></a>SQL Server 연결 설정  
MySQL 데이터베이스 개체를 SQL Server 구문으로 변환 하기 전에 MySQL 데이터베이스 또는 데이터베이스를 마이그레이션할 하려는 SQL Server의 인스턴스에 대 한 연결을 설정 해야 합니다.  
  
연결 속성을 정의할 때도 데이터베이스 개체와 데이터 마이그레이션할 수를 지정 합니다. SQL Server에 연결 하면 MySQL 스키마 수준에서이 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 참조 [MySQL 데이터베이스를 SQL Server 스키마로 매핑 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> SQL Server에 연결 하려고 하기 전에 SQL Server의 인스턴스가 실행 되 고 연결을 허용할 수 있는지 확인 합니다.  
  
**SQL Server에 연결 하려면**  
  
1.  에 **파일** 메뉴 선택 **SQL Server에 연결** (이 옵션은 프로젝트를 만든 후).  
  
    SQL Server에 이전에 연결한 경우 명령 이름 됩니다 **SQL Server에 다시 연결**합니다.  
  
2.  연결 대화 상자에서 입력 하거나 SQL Server 인스턴스의 이름을 선택 합니다.  
  
    -   로컬 컴퓨터의 기본 인스턴스에 연결 하는 경우 입력할 수 있는 **localhost** 또는 점 (**.**).  
  
    -   다른 컴퓨터의 기본 인스턴스에 연결 하는 경우에 컴퓨터의 이름을 입력 합니다.  
  
    -   다른 컴퓨터에 명명 된 인스턴스에 연결 하는 경우 그 다음에 백슬래시 및 인스턴스 이름을 MyServer\MyInstance 같은 컴퓨터 이름을 입력 합니다.  
  
3.  SQL Server 인스턴스의 기본이 아닌 포트에서 연결을 허용 하도록 구성 된, 경우에 SQL Server 연결에 사용 되는 포트 번호를 입력의 **서버 포트** 상자입니다. SQL Server의 기본 인스턴스에 대 한 기본 포트 번호는 1433입니다. 명명 된 인스턴스에 대 한 SSMA는 SQL Server Browser 서비스에서 포트 번호 가져오기를 시도 합니다.  
  
4.  에 **인증** 상자에서 연결에 사용할 인증 유형을 선택 합니다. 현재 Windows 계정을 사용 하려면 선택 **Windows 인증**합니다. SQL Server 로그인을 사용 하려면 SQL Server 인증을 선택 하 고 로그인 이름 및 암호를 입력 하십시오.  
  
5.  보안 연결에 대 한 두 개의 컨트롤이 추가 되는 **연결 암호화** 및 **TrustServerCertificate** 확인란 합니다. 경우에만 **연결 암호화** 확인란이 **TrustServerCertificate** 확인란이 표시 됩니다. 때 **연결 암호화** (true)을 선택 하 고 **TrustServerCertificate** 선택 하지 않으면 (false) 인 검사지 것입니다 SQL Server SSL 인증서입니다. 서버 인증서의 유효성 검사는 SSL 핸드셰이크의 일부로 서버가 연결할 올바른 서버인지 확인합니다. 이 위해 서버 쪽 뿐만 아니라 클라이언트측에서 인증서를 설치 합니다.  
  
6.  연결을 클릭 합니다.  
  
**더 높은 버전 호환성**  
  
더 높은 버전의 SQL Server에 연결/다시 연결할 허용 됩니다.  
  
1.  에 연결할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 때 생성 되는 프로젝트는 2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005입니다.  
  
2.  에 연결할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 때 생성 되는 프로젝트는 2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 되지만 즉, 더 낮은 버전에 연결 하는 허용 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
3.  에 연결할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 때 생성 되는 프로젝트는 2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012입니다.  
  
4.  에 연결할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 때 생성 되는 프로젝트는 2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 합니다.  
  
5.  더 높은 버전 호환성에 대 한 "SQL Azure" 올바르지 않습니다.  
  
||||||||  
|-|-|-|-|-|-|-|  
|**프로젝트 형식 및 대상 서버 버전**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005<br /> (버전: 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008<br /> (버전: 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012<br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014<br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016<br />(Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005|예|사용자 계정 컨트롤|사용자 계정 컨트롤|사용자 계정 컨트롤|예||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008||예|사용자 계정 컨트롤|사용자 계정 컨트롤|예||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|||예|사용자 계정 컨트롤|예||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014||||예|예||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2016|||||예||  
|SQL Azure||||||예|  
  
> [!IMPORTANT]  
> 데이터베이스 개체의 변환을 수행 하는 프로젝트 형식에 따라 하지만의 버전에 따라 하지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에 연결 합니다. 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 프로젝트 변환이 수행 하는 기준으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 더 높은 버전의 연결 된 경우에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>SQL Server 메타 데이터를 동기화합니다.  
SQL Server 데이터베이스에 대 한 메타 데이터를 자동으로 업데이트 되지 않습니다. SQL Server 메타 데이터 탐색기에서 메타 데이터는 마지막 시간을 수동으로 또는 SQL Server에 처음 연결 하는 경우 메타 데이터의 스냅숏을 메타 데이터를 업데이트 합니다. 모든 데이터베이스에 대해 또는 모든 단일 데이터베이스 또는 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 동기화 하려면**  
  
1.  SQL Server에 연결 되어 있는지 확인 합니다.  
  
2.  SQL Server 메타 데이터 탐색기에서 데이터베이스 또는 데이터베이스 스키마를 업데이트 하려면 옆에 있는 확인란을 선택 합니다.  
  
    예를 들어 모든 데이터베이스에 대 한 메타 데이터를 업데이트 하려면 데이터베이스 옆의 상자를 선택 합니다.  
  
3.  데이터베이스 또는 개별 데이터베이스 또는 데이터베이스 스키마를 마우스 오른쪽 단추로 클릭 한 다음 선택 **데이터베이스와 동기화**합니다.  
  
## <a name="next-step"></a>다음 단계  
다음 단계는 마이그레이션에서 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   MySQL 스키마 및 SQL Server 데이터베이스 및 스키마 간의 매핑을 사용자 지정, 하려면 참조 [매핑 MySQL 데이터베이스를 SQL Server 스키마로 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   참조 프로젝트에 대 한 구성 옵션을 사용자 지정 하려면 [프로젝트 옵션 설정 &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   원본 및 대상 데이터 형식 매핑, 사용자 지정 하려면 참조 [매핑 MySQL 및 SQL Server 데이터 형식 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   이러한 작업을 수행 해야 하는 경우에 SQL Server 개체 정의에 MySQL 데이터베이스 개체 정의 변환할 수 있습니다. 자세한 내용은 참조 [MySQL 데이터베이스 변환 &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server-SQL Azure DB로 데이터베이스 마이그레이션 MySQL &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

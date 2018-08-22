---
title: SSMA 프로젝트 (MySQLToSQL) 작업 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Working with SSMA projects, create new project
- Working with SSMA projects, customize settings
- Working with SSMA projects, Open project
- Working with SSMA projects, Save project
ms.assetid: 9e4394e9-f177-41d9-839e-5d53a9c9b840
caps.latest.revision: 20
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7a67cd1b6678fec80397e8ac31358ae2c6b32e0a
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40393037"
---
# <a name="working-with-ssma-projects-mysqltosql"></a>SSMA 프로젝트 작업(MySQLToSQL)
SQL Server 또는 SQL Azure MySQL 데이터베이스를 마이그레이션하려면 먼저 SSMA 프로젝트를 만들어야 합니다. 프로젝트는 다음 정보를 포함 하는 파일:  
  
-   SQL Server 또는 SQL Azure 마이그레이션하려는 MySQL 데이터베이스에 대 한 메타 데이터입니다.  
  
-   SQL Server 또는 SQL Azure 마이그레이션된 개체 및 데이터를 받을 대상 인스턴스에 대 한 메타 데이터입니다.  
  
-   SQL Server 또는 SQL Azure 연결 정보입니다.  
  
-   프로젝트 설정입니다.  
  
프로젝트를 열면에 MySQL 및 SQL Server 또는 SQL Azure 연결이 끊어지도록 합니다. 기능을 사용 하면 오프 라인으로 작업할 수 있습니다. SQL Server에 다시 연결 하는 방법에 대 한 자세한 내용은 참조 하세요. [SQL Server에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="reviewing-default-project-settings"></a>기본 프로젝트 설정을 검토합니다.  
SSMA 변환 하 고 데이터베이스를 로드, 데이터 마이그레이션 및 SSMA MySQL 및 SQL Server 또는 SQL Azure 사용 하 여 동기화에 대 한 몇 가지 설정을 포함 합니다. 기본 설정은 많은 사용자에 게 적합 합니다. 그러나 새 SSMA 프로젝트를 만들기 전에 설정을 검토 해야 합니다. 필요한 경우 모든 새 프로젝트에 사용할 기본 설정을 변경할 수 있습니다.  
  
##### <a name="to-review-default-project-settings"></a>기본 프로젝트 설정을 검토 하려면  
  
1.  선택 **기본 프로젝트 설정** 에서 합니다 **도구** 메뉴.  
  
2.  라는 프로젝트 형식을 선택 **마이그레이션 대상 버전** 설정을 볼 / 변경 하려는 및 클릭에 대 한 드롭다운 **일반** 탭 합니다.  
  
3.  왼쪽된 창에서 클릭 **변환**합니다.  
  
4.  오른쪽 창에서 검토 하 고 필요에 따라 설정을 변경 합니다. 이러한 설정에 대 한 자세한 내용은 참조 하세요. [프로젝트 설정 &#40;변환&#41; &#40;MySQLToSQL&#41; ](../../ssma/mysql/project-settings-conversion-mysqltosql.md) 합니다.  
  
5.  마이그레이션, 동기화, SQL Azure, GUI 및 형식 매핑 페이지에 대해 1-3 단계를 반복 합니다.  
  
-   마이그레이션 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;마이그레이션&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)합니다.  
  
-   SQL Server에 대 한 동기화 설정에 대 한 자세한 내용은 참조 하세요. [프로젝트 설정 &#40;동기화&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)합니다.  
  
-   GUI 설정에 대 한 자세한 내용은 [프로젝트 설정 (GUI) (SSMA 공통)](http://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)합니다.  
  
-   데이터 형식 매핑 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;형식 매핑&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)합니다.  
  
-   SQL Azure 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;Azure SQL DB&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)합니다.  
  
> [!NOTE]  
> SQL Azure 설정을 선택한 경우에 표시 됩니다 **SQL Azure의 마이그레이션을** 프로젝트를 만드는 동안.  
  
## <a name="creating-new-projects"></a>새 프로젝트 만들기  
SQL Server 또는 SQL Azure MySQL 데이터베이스에서 데이터를 마이그레이션하려면, 프로젝트를 만들어야 합니다.  
  
##### <a name="to-create-a-new-project"></a>새 프로젝트를 만들려면  
  
1.  선택 **새 프로젝트** 에서 합니다 **파일** 메뉴. **새 프로젝트** 대화 상자가 나타납니다. **파일** 메뉴에서 **새 프로젝트**를 선택합니다. **새 프로젝트** 대화 상자가 나타납니다.  
  
2.  **이름** 입력란에 프로젝트 이름을  
  
3.  에 **위치** 상자에 입력 하거나 프로젝트에 대 한 폴더를 선택 합니다.  
  
4.  에 **마이그레이션에** 드롭다운, 대상의 버전을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션에 사용 합니다. 사용 가능한 옵션은 다음과 같습니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   Azure SQL DB  
  
클릭 하 고 **확인**  
  
SSMA는 프로젝트 파일을 만듭니다.  
  
## <a name="customizing-project-settings"></a>사용자 지정 프로젝트 설정  
기본값을 정의 하는 것 외에도 프로젝트 설정을 새 SSMA 프로젝트는 모두에 적용 되는 각 프로젝트에 대 한 설정을 사용자 지정할 수도 있습니다. 자세한 내용은 [프로젝트 옵션 설정 &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)합니다.  
  
원본 및 대상 데이터베이스 간의 데이터 형식 매핑 사용자 지정 하는 경우 프로젝트, 데이터베이스 또는 개체 수준에서 매핑을 정의할 수 있습니다. 자세한 내용은 [매핑 MySQL 및 SQL Server 데이터 형식 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)합니다.  
  
## <a name="saving-projects"></a>프로젝트를 저장합니다.  
프로젝트 저장 기능을 사용자를 게 기본적으로 SSMA 프로젝트 파일을 프로젝트 설정 및 선택적으로 데이터베이스 메타 데이터를 저장할 수 있습니다.  
  
##### <a name="to-save-a-project"></a>프로젝트를 저장 하려면  
  
-   에 **파일** 메뉴에서 **저장** 프로젝트입니다.  
  
프로젝트 내에서 데이터베이스 변경, 변환 되지 않은 경우 로드 하 고 메타 데이터를 저장 하면 SSMA 메시지가 나타납니다. 로드 및 메타 데이터를 저장 하면 오프 라인으로 작업 합니다. 또한 기술 지원 담당자와 같은 다른 사용자에 게 전체 프로젝트 파일을 보낼 수 있습니다. 메타 데이터를 저장 하 라는 메시지가 나타나면 다음을 수행 합니다.  
  
1.  각 데이터베이스의 상태를 보여 주는 **메타 데이터 누락**, 데이터베이스 이름 옆의 확인란을 선택 합니다. 메타 데이터를 저장 하면 몇 분 정도 걸릴 수 있습니다. 이 시점에서 메타 데이터를 저장 하지 않을 경우 모든 확인란을 선택 하지 마십시오.  
  
2.  **저장**을 클릭합니다.  
  
SSMA는 MySQL 스키마를 구문 분석 하 고 프로젝트 파일에 메타 데이터를 저장 합니다.  
  
## <a name="opening-projects"></a>열린 프로젝트  
프로젝트를 열면 MySQL에서 SQL Server 또는 SQL Azure 연결이 끊어집니다. 이 기능을 사용 하면 오프 라인으로 작업할 수 있습니다. 메타 데이터를 업데이트 하려면 SQL Server 또는 SQL Azure 데이터베이스 개체를 로드 합니다. 데이터를 마이그레이션하려면 SQL Server 또는 SQL Azure 다시 연결 해야 합니다.  
  
##### <a name="to-open-a-project"></a>프로젝트를 열려면  
  
1.  다음 절차 중 하나를 사용 합니다.  
  
    1.  에 **파일** 메뉴에서 **최근에 사용한 프로젝트**합니다.  
  
    2.  열려는 프로젝트를 선택 합니다.  
  
    3.  에 **파일** 메뉴에서 **프로젝트 열기**.m2ssproj 프로젝트 파일 찾기, 파일을 선택 및 클릭 **열기**.  
  
2.  MySQL에 다시 연결 합니다 **파일** 메뉴에서 **MySQL에 다시 연결**합니다.  
  
3.  SQL Server에 다시 연결 합니다 **파일** 메뉴에서 **SQL Server에 다시 연결**.  
  
4.  SQL Azure 다시 연결 합니다 **파일** 메뉴에서 **SQL Azure 다시 연결 합니다.**  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계 [MySQL에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
## <a name="see-also"></a>관련 항목  
[MySQL에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[SQL Server-Azure SQL DB로 마이그레이션 MySQL 데이터베이스 &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[SQL Server에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[Azure SQL DB에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  

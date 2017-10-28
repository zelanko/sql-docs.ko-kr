---
title: "SSMA 프로젝트 (MySQLToSQL) 사용 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 44d7c381e4cc0599e24f5df1024b31b75b1598f7
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="working-with-ssma-projects-mysqltosql"></a>SSMA 프로젝트 (MySQLToSQL) 작업
MySQL 데이터베이스를 SQL Server 또는 SQL Azure에 마이그레이션하려면 SSMA 프로젝트를 먼저 만들어야 할 합니다. 프로젝트는 다음 정보를 포함 하는 파일입니다.  
  
-   SQL Server 또는 SQL Azure로 마이그레이션하려는 MySQL 데이터베이스에 대 한 메타 데이터입니다.  
  
-   마이그레이션된 개체 및 데이터를 받을 SQL Azure 또는 SQL Server의 대상 인스턴스에 대 한 메타 데이터입니다.  
  
-   SQL Server 또는 SQL Azure 연결 정보입니다.  
  
-   프로젝트 설정 합니다.  
  
프로젝트를 열 때 MySQL 및 SQL Server 또는 SQL Azure에서 연결이 끊어지도록 합니다. 기능을 사용 하면 오프 라인으로 작업할 수 있습니다. SQL Server에 다시 연결 하는 방법에 대 한 자세한 내용은 참조 [SQL Server &#40;에 연결 MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="reviewing-default-project-settings"></a>기본 프로젝트 설정 검토  
SSMA 변환 하 고 데이터베이스를 로드, 데이터를 마이그레이션 및 MySQL 및 SQL Server 또는 SQL Azure와 SSMA 동기화에 대 한 몇 가지 설정을 포함 합니다. 기본 설정은 많은 사용자에 대 한 적절 한입니다. 그러나 새 SSMA 프로젝트를 만들기 전에 설정을 검토 해야 합니다. 필요한 경우에 모든 새 프로젝트에 사용할 기본 설정을 변경할 수 있습니다.  
  
##### <a name="to-review-default-project-settings"></a>기본 프로젝트 설정을 검토 하려면  
  
1.  선택 **기본 프로젝트 설정** 에서 **도구** 메뉴.  
  
2.  프로젝트 형식을 선택 **마이그레이션 대상 버전** 볼 / 변경할 수 있는 설정이 하 고 클릭 한 다음에 대 한 드롭다운 **일반** 탭 합니다.  
  
3.  왼쪽된 창에서 클릭 **변환**합니다.  
  
4.  오른쪽 창에서 검토 하 고 필요에 따라 설정을 변경 합니다. 이러한 설정에 대 한 자세한 내용은 참조 [프로젝트 설정 &#40; 변환 &#41; &#40; MySQLToSQL &#41; ](../../ssma/mysql/project-settings-conversion-mysqltosql.md) .  
  
5.  마이그레이션, 동기화, SQL Azure, GUI 및 유형 매핑 페이지에 대 한 1-3 단계를 반복 합니다.  
  
-   마이그레이션 설정에 대 한 정보를 참조 하십시오. [프로젝트 설정 &#40; 마이그레이션 &#41; &#40; MySQLToSQL &#41; ](../../ssma/mysql/project-settings-migration-mysqltosql.md).  
  
-   SQL Server에 대 한 동기화 설정에 대 한 정보를 참조 하십시오. [프로젝트 설정 &#40; 동기화 &#41; &#40; MySQLToSQL &#41; ](../../ssma/mysql/project-settings-synchronization-mysqltosql.md).  
  
-   GUI 설정에 대 한 정보를 참조 하십시오. [프로젝트 설정 (GUI) (SSMA 공통)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)합니다.  
  
-   데이터 형식 매핑 설정에 대 한 정보를 참조 하십시오. [프로젝트 설정 &#40; 형식 매핑 &#41; &#40; MySQLToSQL &#41; ](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
-   SQL Azure 설정에 대 한 정보를 참조 하십시오. [프로젝트 설정 &#40; Azure SQL DB &#41; &#40; MySQLToSQL &#41; ](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md).  
  
> [!NOTE]  
> SQL Azure 설정을 선택한 경우에 표시 됩니다 **SQL Azure로의 마이그레이션을** 프로젝트를 만드는 동안 합니다.  
  
## <a name="creating-new-projects"></a>새 프로젝트 만들기  
데이터를 마이그레이션하려면 MySQL 데이터베이스에서 SQL Server 또는 SQL Azure에 프로젝트를 만들어야 합니다.  
  
##### <a name="to-create-a-new-project"></a>새 프로젝트를 만들려면  
  
1.  선택 **새 프로젝트** 에서 **파일** 메뉴. **새 프로젝트** 대화 상자가 나타납니다. **파일** 메뉴에서 **새 프로젝트**를 선택합니다. **새 프로젝트** 대화 상자가 나타납니다.  
  
2.  **이름** 입력란에 프로젝트 이름을  
  
3.  에 **위치** 입력란에 입력 하거나 프로젝트에 대 한 폴더를 선택 합니다.  
  
4.  에 **마이그레이션에** 대상 버전을 선택한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 마이그레이션에 사용 합니다. 사용할 수 있는 옵션이 있습니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   Azure SQL DB  
  
클릭 하 고 **확인**  
  
SSMA는 프로젝트 파일을 만듭니다.  
  
## <a name="customizing-project-settings"></a>프로젝트 설정 사용자 지정  
기본값 정의 외에도 모든 새 SSMA 프로젝트에 적용 되는 프로젝트 설정 각 프로젝트에 대 한 설정을 사용자 지정할 수도 있습니다. 자세한 내용은 참조 [프로젝트 옵션 설정 &#40; MySQLToSQL &#41; ](../../ssma/mysql/setting-project-options-mysqltosql.md).  
  
원본 및 대상 데이터베이스 간에 데이터 형식 매핑을 사용자 지정 프로젝트, 데이터베이스 또는 개체 수준에서 매핑 정의할 수 있습니다. 자세한 내용은 참조 [매핑 MySQL 및 SQL Server 데이터 형식 &#40; MySQLToSQL &#41; ](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md).  
  
## <a name="saving-projects"></a>프로젝트 저장  
프로젝트 저장 기능에 사용자를를 기본적으로 SSMA 프로젝트 파일을 프로젝트 설정 및 필요에 따라 데이터베이스 메타 데이터를 저장할 수 있습니다.  
  
##### <a name="to-save-a-project"></a>프로젝트를 저장 하려면  
  
-   에 **파일** 메뉴 선택 **저장** 프로젝트.  
  
데이터베이스 프로젝트 내에서 변경 된 변환 하지 않은 경우 SSMA 하 라는 메시지가 나타납니다 로드 하 고 메타 데이터를 저장 합니다. 로드 및 메타 데이터를 저장 합니다. 오프 라인으로 작업할 수 있습니다. 또한 기술 지원 담당자와 같은 다른 사람에 게 전체 프로젝트 파일을 보낼 수 있습니다. 메타 데이터를 저장 하는 메시지가 다음을 수행 합니다.  
  
1.  상태를 보여 주는 각 데이터베이스에 대해 **메타 데이터 누락**, 데이터베이스 이름 옆에 있는 확인란을 선택 합니다. 메타 데이터를 저장 하면 몇 분 정도 걸릴 수 있습니다. 이 시점에서 메타 데이터를 저장 하지 않을 경우 모든 확인란을 선택 하지 마십시오.  
  
2.  **저장**을 클릭합니다.  
  
SSMA는 MySQL 스키마를 구문 분석 하 고 프로젝트 파일에 메타 데이터를 저장 합니다.  
  
## <a name="opening-projects"></a>프로젝트 열기  
프로젝트를 열 때 MySQL 및 SQL Server 또는 SQL Azure에서 연결이 끊어집니다. 이렇게 하면 오프 라인으로 작업할 수 있습니다. 메타 데이터를 업데이트 하려면 SQL Server 또는 SQL Azure에 데이터베이스 개체를 로드 합니다. 데이터를 마이그레이션하려면 SQL Server 또는 SQL Azure에 다시 연결 해야 합니다.  
  
##### <a name="to-open-a-project"></a>프로젝트를 열려면  
  
1.  다음 절차 중 하나를 사용 합니다.  
  
    1.  에 **파일** 메뉴에서 **최근에 사용한 프로젝트**합니다.  
  
    2.  열려는 프로젝트를 선택 합니다.  
  
    3.  에 **파일** 메뉴 선택 **프로젝트 열기**,.m2ssproj 프로젝트 파일, 파일을 찾은 다음 클릭 **열려**합니다.  
  
2.  MySQL에 다시 연결 하는 **파일** 메뉴 선택 **MySQL에 다시 연결**합니다.  
  
3.  SQL server에 다시 연결 하는 **파일** 메뉴 선택 **SQL Server에 다시 연결**합니다.  
  
4.  SQL Azure에 다시 연결 하는 **파일** 메뉴 선택 **SQL Azure에 다시 연결 합니다.**  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [MySQL &#40;에 연결 MySQLToSQL &#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
## <a name="see-also"></a>참고 항목  
[MySQL &#40;에 연결 MySQLToSQL &#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[Azure SQL DB &#40; SQL Server-MySQL 데이터베이스 마이그레이션 MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[SQL Server &#40;에 연결 MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[Azure SQL DB &#40;에 연결 MySQLToSQL &#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  


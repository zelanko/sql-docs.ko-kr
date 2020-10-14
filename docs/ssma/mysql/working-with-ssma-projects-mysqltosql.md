---
description: SSMA 프로젝트 작업(MySQLToSQL)
title: SSMA 프로젝트 작업 (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Working with SSMA projects, create new project
- Working with SSMA projects, customize settings
- Working with SSMA projects, Open project
- Working with SSMA projects, Save project
ms.assetid: 9e4394e9-f177-41d9-839e-5d53a9c9b840
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3da213467ad6513d4c25e6888bd095e80746cba7
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038276"
---
# <a name="working-with-ssma-projects-mysqltosql"></a>SSMA 프로젝트 작업(MySQLToSQL)
MySQL 데이터베이스를 SQL Server 또는 SQL Azure로 마이그레이션하려면 먼저 SSMA 프로젝트를 만들어야 합니다. 프로젝트는 다음 정보를 포함 하는 파일입니다.  
  
-   SQL Server 또는 SQL Azure로 마이그레이션하려는 MySQL 데이터베이스에 대 한 메타 데이터입니다.  
  
-   마이그레이션된 개체와 데이터를 받을 SQL Server 또는 SQL Azure의 대상 인스턴스에 대 한 메타 데이터입니다.  
  
-   연결 정보를 SQL Server 하거나 SQL Azure 합니다.  
  
-   프로젝트 설정.  
  
프로젝트를 열면 MySQL과 SQL Server 또는 SQL Azure에서 연결이 끊어집니다. 이를 통해 오프 라인으로 작업할 수 있습니다. SQL Server에 다시 연결 하는 방법에 대 한 자세한 내용은 [SQL Server &#40;MySQLToSQL에 연결](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md) 을 참조 하세요&#41;  
  
## <a name="reviewing-default-project-settings"></a>기본 프로젝트 설정 검토  
SSMA에는 데이터베이스를 변환 및 로드 하 고, 데이터를 마이그레이션하고, MySQL 및 SQL Server 또는 SQL Azure를 사용 하 여 SSMA를 동기화 하기 위한 여러 설정이 포함 됩니다. 기본 설정은 대부분의 사용자에 게 적합 합니다. 그러나 새 SSMA 프로젝트를 만들기 전에 설정을 검토 해야 합니다. 필요한 경우 모든 새 프로젝트에 사용 되는 기본 설정을 변경할 수 있습니다.  
  
##### <a name="to-review-default-project-settings"></a>기본 프로젝트 설정을 검토 하려면  
  
1.  **도구** 메뉴에서 **기본 프로젝트 설정** 을 선택 합니다.  
  
2.  설정을 보거나 변경할 **마이그레이션 대상 버전** 드롭다운에서 프로젝트 유형을 선택 하 고 **일반** 탭을 클릭 합니다.  
  
3.  왼쪽 창에서 **변환**을 클릭 합니다.  
  
4.  오른쪽 창에서 필요에 따라 설정을 검토 하 고 변경 합니다. 이러한 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;변환&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md) 을 참조 하세요.  
  
5.  마이그레이션, 동기화, SQL Azure, GUI 및 유형 매핑 페이지에 대해 1-3 단계를 반복 합니다.  
  
-   마이그레이션 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;migration&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)을 참조 하세요.  
  
-   SQL Server에 대 한 동기화 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;동기화&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)를 참조 하세요.  
  
-   GUI 설정에 대 한 자세한 내용은 [프로젝트 설정 (gui) (SSMA Common)](../sybase/project-settings-gui-sybasetosql.md)을 참조 하세요.  
  
-   데이터 형식 매핑 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;형식 매핑&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)을 참조 하세요.  
  
-   SQL Azure 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;Azure SQL Database&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)을 참조 하세요.  
  
> [!NOTE]  
> SQL Azure 설정은 프로젝트를 만드는 동안 **SQL Azure로 마이그레이션을** 선택한 경우에만 표시 됩니다.  
  
## <a name="creating-new-projects"></a>새 프로젝트 만들기  
MySQL 데이터베이스에서 SQL Server 또는 SQL Azure로 데이터를 마이그레이션하려면 프로젝트를 만들어야 합니다.  
  
##### <a name="to-create-a-new-project"></a>새 프로젝트를 만들려면  
  
1.  **파일** 메뉴에서 **새 프로젝트** 를 선택 합니다. **새 프로젝트** 대화 상자가 나타납니다. **파일** 메뉴에서 **새 프로젝트**를 선택합니다. **새 프로젝트** 대화 상자가 나타납니다.  
  
2.  **이름** 입력란에 프로젝트 이름을  
  
3.  **위치** 상자에서 프로젝트에 대 한 폴더를 입력 하거나 선택 합니다.  
  
4.  **마이그레이션** 드롭다운에서 마이그레이션에 사용 되는 대상 버전을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 제공되는 옵션은 다음과 같습니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   Azure SQL Database  
  
그런 다음 **확인** 을 클릭 합니다.  
  
SSMA에서 프로젝트 파일을 만듭니다.  
  
## <a name="customizing-project-settings"></a>프로젝트 설정 사용자 지정  
모든 새 SSMA 프로젝트에 적용 되는 기본 프로젝트 설정을 정의 하는 것 외에도 각 프로젝트에 대 한 설정을 사용자 지정할 수 있습니다. 자세한 내용은 [프로젝트 옵션 설정 &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)을 참조 하세요.  
  
원본 데이터베이스와 대상 데이터베이스 간에 데이터 형식 매핑을 사용자 지정 하는 경우 프로젝트, 데이터베이스 또는 개체 수준에서 매핑을 정의할 수 있습니다. 자세한 내용은 [MySQL 및 SQL Server 데이터 형식 &#40;MySQLToSQL&#41;매핑 ](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)을 참조 하세요.  
  
## <a name="saving-projects"></a>프로젝트 저장  
프로젝트 저장 기능을 사용 하면 사용자는 기본적으로 프로젝트 설정과 데이터베이스 메타 데이터를 SSMA 프로젝트 파일에 저장할 수 있습니다.  
  
##### <a name="to-save-a-project"></a>프로젝트를 저장하려면  
  
-   **파일** 메뉴에서 프로젝트 **저장** 을 선택 합니다.  
  
프로젝트 내의 데이터베이스가 변경 되었거나 변환 되지 않은 경우 SSMA에서 메타 데이터를 로드 하 고 저장 하 라는 메시지를 표시 합니다. 메타 데이터를 로드 하 고 저장 하면 오프 라인으로 작업할 수 있습니다. 또한 기술 지원 담당자와 같은 다른 사람에 게 전체 프로젝트 파일을 보낼 수 있습니다. 메타 데이터를 저장 하 라는 메시지가 표시 되 면 다음을 수행 합니다.  
  
1.  **누락 된 메타 데이터**의 상태를 표시 하는 각 데이터베이스에 대해 데이터베이스 이름 옆의 확인란을 선택 합니다. 메타 데이터를 저장 하는 데 몇 분 정도 걸릴 수 있습니다. 이때 메타 데이터를 저장 하지 않으려면 확인란을 선택 하지 마십시오.  
  
2.  **저장**을 클릭합니다.  
  
SSMA는 MySQL 스키마를 구문 분석 하 고 메타 데이터를 프로젝트 파일에 저장 합니다.  
  
## <a name="opening-projects"></a>프로젝트 열기  
프로젝트를 열면 MySQL과 SQL Server 또는 SQL Azure에서 연결이 끊어집니다. 이렇게 하면 오프 라인으로 작업할 수 있습니다. 메타 데이터를 업데이트 하려면 SQL Server 또는 SQL Azure 데이터베이스 개체를 로드 합니다. 데이터를 마이그레이션하려면 SQL Server 또는 SQL Azure에 다시 연결 해야 합니다.  
  
##### <a name="to-open-a-project"></a>프로젝트를 열려면  
  
1.  다음 절차 중 하나를 사용 합니다.  
  
    1.  **파일** 메뉴에서 **최근 프로젝트**를 가리킵니다.  
  
    2.  열려는 프로젝트를 선택 합니다.  
  
    3.  **파일** 메뉴에서 **프로젝트 열기**를 선택 하 고 m2ssproj 프로젝트 파일을 찾은 다음 파일을 선택 하 고 **열기**를 클릭 합니다.  
  
2.  MySQL에 다시 연결 하려면 **파일** 메뉴에서 **Mysql에 다시 연결**을 선택 합니다.  
  
3.  SQL Server에 다시 연결 하려면 **파일** 메뉴에서 **SQL Server에 다시 연결**을 선택 합니다.  
  
4.  SQL Azure에 다시 연결 하려면 **파일** 메뉴에서 **SQL Azure에 다시 연결을 선택 합니다.**  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [MySQL &#40;MySQLToSQL&#41;에 연결 하](../../ssma/mysql/connecting-to-mysql-mysqltosql.md) 는 것입니다.  
  
## <a name="see-also"></a>참고 항목  
[MySQL &#40;MySQLToSQL&#41;에 연결 ](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[MySQL 데이터베이스를 SQL Server-Azure SQL Database &#40;MySQLToSql&#41;로 마이그레이션 ](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[MySQLToSQL&#41;&#40;SQL Server에 연결 ](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[MySQLToSQL&#41;&#40;Azure SQL Database에 연결 ](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  

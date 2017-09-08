---
title: "Azure SQL DB (MySQLToSQL)에 연결 | Microsoft Docs"
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
- Connecting to SQL Azure, SQL Azure permissions
- Connecting to SQL Azure, synchronization
ms.assetid: d0b6f16a-1880-459d-a0c7-28b7ef15c56a
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b7cb16b0b6ca0f98aaaa68d566092ef5327cd012
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="connecting-to-azure-sql-db-mysqltosql"></a>Azure SQL DB (MySQLToSQL)에 연결
MySQL 데이터베이스를 SQL Azure로 마이그레이션하려면 SQL Azure의 대상 인스턴스에 연결 해야 합니다. 에 연결할 때 SSMA는 SQL Azure의 인스턴스에서 모든 데이터베이스에 대 한 메타 데이터를 가져오고 SQL Azure 메타 데이터 탐색기에서 데이터베이스 메타 데이터를 표시 합니다. SSMA는 SQL Azure에 연결 되어 있지만 암호를 저장 하지 않는 인스턴스 정보를 저장 합니다.  
  
SQL Azure에 대 한 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 다시 연결 해야 SQL azure 서버에 연결 되어 하려는 경우. SQL Azure에 데이터베이스 개체를 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업 합니다.  
  
SQL Azure의 인스턴스에 대 한 메타 데이터를 자동으로 동기화 되지 않습니다. 대신, SQL Azure 메타 데이터 탐색기의 메타 데이터를 업데이트 하려면 SQL Azure 메타 데이터 수동으로 업데이트 해야 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "SQL Azure 메타 데이터 동기화 중" 섹션을 참조 하십시오.  
  
## <a name="required-sql-azure-permissions"></a>필요한 SQL Azure 사용 권한  
SQL Azure에 연결 하는 데 사용 되는 계정에는 계정 수행 하는 작업에 따라 다른 권한이 필요 합니다.  
  
-   MySQL 개체를 변환 하려면 [!INCLUDE[tsql](../../includes/tsql_md.md)] 를 SQL Azure에서 메타 데이터를 업데이트 하거나 저장 하는 변환 된 구문을 구문, 스크립트, 계정에는 SQL Azure 인스턴스에 로그온 할 수 있는 권한이 있어야 합니다.  
  
-   SQL Azure 데이터베이스 개체를 로드,의 최소 권한 요구 사항은의 멤버 자격이 **db_owner** 대상 데이터베이스의 데이터베이스 역할입니다.  
  
## <a name="establishing-a-sql-azure-connection"></a>설정 SQL Azure 연결  
MySQL 데이터베이스 개체를 SQL Azure 구문으로 변환 하기 전에 SQL Azure에서 MySQL 데이터베이스 또는 데이터베이스를 마이그레이션할 하려는 인스턴스에 대 한 연결을 설정 해야 합니다.  
  
연결 속성을 정의할 때도 데이터베이스 개체와 데이터 마이그레이션할 수를 지정 합니다. SQL Azure에 연결 하면 MySQL 스키마 수준에서이 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 참조 [MySQL 데이터베이스를 SQL Server 스키마 &#40;에 매핑 MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> SQL Azure에 연결 하려고 하기 전에 SQL Azure의 인스턴스가 실행 되 고 연결을 허용할 수 있는지 확인 합니다.  
  
**SQL Azure에 연결 하려면**  
  
1.  에 **파일** 메뉴 선택 **SQL Azure에 연결** (이 옵션은 프로젝트를 만든 후).  
  
    SQL Azure에 이전에 연결한 경우 명령 이름 됩니다 **SQL Azure에 다시 연결**합니다.  
  
2.  연결 대화 상자에서 입력 하거나 SQL Azure의 서버 이름을 선택 합니다.  
  
3.  선택, 입력 또는 **찾아보기** 데이터베이스 이름입니다.  
  
4.  입력 하거나 선택 **UserName**합니다.  
  
5.  입력은 **암호**합니다.  
  
6.  SSMA는 SQL Azure에 암호화 된 연결을 권장합니다.  
  
7.  **연결**을 클릭합니다.  
  
> [!IMPORTANT]  
> MySQL 용 SSMA 연결을 지원 하지 않습니다 **마스터** SQL Azure 데이터베이스입니다.  
  
## <a name="synchronizing-sql-azure-metadata"></a>동기화 SQL Azure 메타 데이터  
SQL Azure 데이터베이스에 대 한 메타 데이터를 자동으로 업데이트 되지 않습니다. SQL Azure 메타 데이터 탐색기에서 메타 데이터는 마지막 시간을 수동으로 또는 SQL Azure에 처음 연결 하는 경우 메타 데이터의 스냅숏을 메타 데이터를 업데이트 합니다. 모든 데이터베이스에 대해 또는 모든 단일 데이터베이스 또는 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 동기화 하려면**  
  
1.  SQL Azure에 연결 되어 있는지 확인 합니다.  
  
2.  SQL Azure 메타 데이터 탐색기에서 데이터베이스 또는 데이터베이스 스키마를 업데이트 하려면 옆에 있는 확인란을 선택 합니다.  
  
    예를 들어 모든 데이터베이스에 대 한 메타 데이터를 업데이트 하려면 데이터베이스 옆의 상자를 선택 합니다.  
  
3.  데이터베이스 또는 개별 데이터베이스 또는 데이터베이스 스키마를 마우스 오른쪽 단추로 클릭 한 다음 선택 **데이터베이스와 동기화**합니다.  
  
## <a name="next-step"></a>다음 단계  
다음 단계는 마이그레이션에서 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   MySQL 스키마 및 SQL Azure 데이터베이스 및 스키마 간의 매핑을 사용자 지정, 하려면 참조 [SQL Server 스키마 &#40; 매핑 MySQL 데이터베이스 MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   참조 프로젝트에 대 한 구성 옵션을 사용자 지정 하려면 [프로젝트 옵션 설정 &#40; MySQLToSQL &#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   원본 및 대상 데이터 형식 매핑, 사용자 지정 하려면 참조 [매핑 MySQL 및 SQL Server 데이터 형식 &#40; MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   이러한 작업을 수행 해야 하는 경우에 SQL Azure 개체 정의에 MySQL 데이터베이스 개체 정의 변환할 수 있습니다. 자세한 내용은 참조 [MySQL 데이터베이스 변환 &#40; MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>참고 항목  
[Azure SQL DB &#40; SQL Server-MySQL 데이터베이스 마이그레이션 MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  


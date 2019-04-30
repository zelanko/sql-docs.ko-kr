---
title: Azure SQL DB (MySQLToSQL)에 연결 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Azure, SQL Azure permissions
- Connecting to SQL Azure, synchronization
ms.assetid: d0b6f16a-1880-459d-a0c7-28b7ef15c56a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 23d018a8d551a5c3a7f2978339b6cf7612f378fd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63253274"
---
# <a name="connecting-to-azure-sql-db-mysqltosql"></a>Azure SQL DB에 연결(MySQLToSQL)
SQL Azure MySQL 데이터베이스를 마이그레이션하려면 SQL Azure 대상 인스턴스에 연결 해야 합니다. 에 연결 하면 SSMA는 SQL Azure 인스턴스에서 모든 데이터베이스에 대 한 메타 데이터를 가져오고 SQL Azure 메타 데이터 탐색기에서 데이터베이스 메타 데이터를 표시 합니다. SSMA는 SQL Azure 연결 되어 있지만 암호를 저장 하지 않으므로의 인스턴스는 정보를 저장 합니다.  
  
SQL Azure 대 한 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 열면 다시 연결 해야 SQL Azure 서버에 활성 연결 하려는 경우. SQL Azure 데이터베이스 개체를 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업 합니다.  
  
SQL Azure 인스턴스에 대 한 메타 데이터를 자동으로 동기화 되지 않습니다. 대신, SQL Azure 메타 데이터 탐색기에서 메타 데이터를 업데이트 하려면 SQL Azure 메타 데이터를 수동으로 업데이트 해야 합니다. 자세한 내용은이 항목 뒷부분의 "SQL Azure 메타 데이터 동기화" 섹션을 참조 하세요.  
  
## <a name="required-sql-azure-permissions"></a>SQL Azure는 데 필요한 사용 권한  
SQL Azure 연결 하는 데 사용 되는 계정에는 작업을 수행 하는 계정에 따라 다른 권한이 필요 합니다.  
  
-   MySQL 개체를 변환할 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문, SQL Azure 메타 데이터를 업데이트 하거나 저장 하는 변환 된 구문을 스크립트, SQL Azure 인스턴스에 로그온 할 수 있는 권한이 있어야 합니다.  
  
-   SQL Azure 데이터베이스 개체를 로드 하려면 최소 권한 요구 사항인 자격이 합니다 **db_owner** 대상 데이터베이스의 데이터베이스 역할.  
  
## <a name="establishing-a-sql-azure-connection"></a>설정 된 SQL Azure 연결  
SQL Azure 구문에 MySQL 데이터베이스 개체를 변환 하기 전에 SQL Azure MySQL 데이터베이스 또는 데이터베이스를 마이그레이션할 하려는 인스턴스의 연결을 설정 해야 합니다.  
  
연결 속성을 정의할 때에 데이터베이스 개체 및 데이터 마이그레이션할 수 지정 합니다. SQL Azure 연결 하면 MySQL 스키마 수준에서이 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 [MySQL 데이터베이스를 SQL Server 스키마에 매핑 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> SQL Azure 연결 하려고 하기 전에 SQL Azure 인스턴스에 실행 되 고 연결을 허용할 수 있는지 확인 합니다.  
  
**SQL Azure 연결 하려면**  
  
1.  에 **파일** 메뉴에서 **SQL Azure 연결** (이 옵션은 프로젝트를 만든 후).  
  
    SQL Azure 이전에 연결한 경우 명령 이름 됩니다 **SQL Azure 다시 연결**합니다.  
  
2.  연결 대화 상자에서 입력 하거나 SQL Azure 서버 이름을 선택 합니다.  
  
3.  입력을 선택 하거나 **찾아보기** 데이터베이스 이름입니다.  
  
4.  입력 또는 선택 **UserName**합니다.  
  
5.  입력 된 **암호**합니다.  
  
6.  SSMA는 SQL Azure 암호화 된 연결을 권장합니다.  
  
7.  **연결**을 클릭합니다.  
  
> [!IMPORTANT]  
> MySQL 용 SSMA 연결을 지원 하지 않습니다 **마스터** SQL Azure 데이터베이스입니다.  
  
## <a name="synchronizing-sql-azure-metadata"></a>SQL Azure 동기화 메타 데이터  
SQL Azure 데이터베이스에 대 한 메타 데이터를 자동으로 업데이트 되지 않습니다. SQL Azure 메타 데이터 탐색기에서 메타 데이터는 마지막는 수동으로 또는 SQL Azure 처음 연결할 때 메타 데이터의 스냅숏으로 메타 데이터를 업데이트 합니다. 수동으로 모든 데이터베이스에 대해 또는 단일 데이터베이스 또는 데이터베이스 개체에 대 한 메타 데이터를 업데이트할 수 있습니다.  
  
**메타 데이터를 동기화 하려면**  
  
1.  SQL Azure 연결 되어 있는지 확인 합니다.  
  
2.  SQL Azure 메타 데이터 탐색기에서 데이터베이스 또는 데이터베이스 스키마를 업데이트 하려는 옆의 확인란을 선택 합니다.  
  
    예를 들어, 모든 데이터베이스에 대 한 메타 데이터를 업데이트 하려면 데이터베이스 옆의 확인란을 선택 합니다.  
  
3.  데이터베이스 또는 개별 데이터베이스 또는 데이터베이스 스키마를 마우스 오른쪽 단추로 클릭 하 고 선택한 **데이터베이스와 동기화**합니다.  
  
## <a name="next-step"></a>다음 단계  
다음 단계는 마이그레이션 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   MySQL 스키마 및 SQL Azure 데이터베이스 및 스키마 간의 매핑을 사용자 지정을 참조 하세요 [매핑 MySQL 데이터베이스를 SQL Server 스키마에 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   프로젝트에 대 한 구성 옵션을 사용자 지정을 참조 하세요 [프로젝트 옵션 설정 &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   원본 및 대상 데이터 형식 매핑 사용자 지정을 참조 하세요 [매핑 MySQL 및 SQL Server 데이터 형식 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   이러한 작업을 수행 해야 하는 경우에 SQL Azure 개체 정의에 MySQL 데이터베이스 개체 정의 변환할 수 있습니다. 자세한 내용은 [MySQL 데이터베이스 변환 &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>관련 항목  
[SQL Server-Azure SQL DB로 마이그레이션 MySQL 데이터베이스 &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

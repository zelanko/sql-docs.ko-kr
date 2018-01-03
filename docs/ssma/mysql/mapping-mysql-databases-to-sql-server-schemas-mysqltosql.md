---
title: "MySQL 데이터베이스를 SQL Server 스키마 (MySQLToSQL)로 매핑 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping, Modifying target database and schema
- Mapping, reverting to default database and schema
ms.assetid: 5c6fb445-92ae-4933-b77d-80230931c024
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4dd351ebbb052515d953f02ae74282dd1e1d62f1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="mapping-mysql-databases-to-sql-server-schemas-mysqltosql"></a>MySQL 데이터베이스를 SQL Server 스키마 (MySQLToSQL)로 매핑
기본적으로 MySQL 용 SSMA는 MySQL 스키마의 모든 개체를 마이그레이션합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 데이터베이스의 스키마 이름으로 지정 합니다. 그러나 MySQL 스키마 간의 매핑을 사용자 지정할 수는 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 데이터베이스입니다.  
  
## <a name="mysql-and-sql-server-or-sql-azure-schemas"></a>SQL Azure 및 SQL Server 또는 MySQL 스키마  
MySQL 개념 스키마의 데이터베이스와 해당 스키마 중 하나는 SQL Server 개념에 매핑됩니다. SSMA는 SQL Server 데이터베이스와 조합 스키마에 스키마로 가리킵니다.  
  
MySQL 개념 스키마의 데이터베이스와 해당 스키마 중 하나는 SQL Server 개념에 매핑됩니다. 예를 들어 MySQL 라는 스키마 해야할 **HR**합니다. SQL Server의 인스턴스 라는 데이터베이스가 있을 수 **HR**, 해당 데이터베이스 내에서 스키마는 및입니다. 하나의 스키마가는 **dbo** (또는 데이터베이스 소유자) 스키마. 기본적으로 MySQL 스키마 **HR** 에 매핑할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 및 스키마 **HR.dbo**합니다. SSMA 참조 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마로 데이터베이스와 스키마의 조합입니다.  
  
MySQL 간의 매핑을 수정할 수 있습니다 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure 스키마입니다.  
  
## <a name="modifying-the-target-database-and-schema"></a>대상 데이터베이스 및 스키마를 수정합니다.  
SSMA를 매핑할 수 MySQL 스키마를 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 스키마입니다.  
  
**데이터베이스 및 스키마를 수정 하려면**  
  
1.  MySQL 메타 데이터 탐색기에서 선택 **스키마**합니다.  
  
    **스키마 매핑** 개별 스키마를 선택 하면 탭은 또한 사용할 수 있습니다. 목록에는 **스키마 매핑** 탭은 선택한 개체에 대 한 사용자 지정 합니다.  
  
2.  오른쪽 창에서 클릭 하 고 **스키마 매핑** 탭 합니다.  
  
    다음 대상 값의 모든 MySQL 스키마의 목록이 표시 됩니다. 이 대상은 두 부분으로 구성 표기법으로 표시 됩니다 (*database.schema*)에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 개체와 데이터 마이그레이션할 수 있습니다.  
  
3.  클릭 하 고, 변경 하려는 매핑을 포함 하는 행 선택 **수정**합니다.  
  
    에 **대상 스키마 선택** 대화 상자에서 검색할 수 있습니다. 사용 가능한 대상 데이터베이스 및 스키마 또는 두 부분으로 구성 표기법 (database.schema)의 텍스트 상자에 이름을 지정 하 고 클릭 한 다음 데이터베이스 및 스키마 형식에 대 한 **확인**합니다.  
  
4.  대상 변경 되는 **스키마 매핑** 탭 합니다.  
  
**매핑 모드**  
  
-   SQL Server에 매핑  
  
원본 데이터베이스는 대상 데이터베이스에 매핑할 수 있습니다. 기본적으로 원본 데이터베이스 매핑된 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSMA를 사용 하 여 연결가 있는 데이터베이스입니다. 매핑되는 대상 데이터베이스에 존재 하지 않는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]를 묻는 메시지를 사용 하는 다음 **"데이터베이스 및/또는 스키마 대상에 존재 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터입니다. 해당 하는 동기화 하는 동안 만들어졌습니다. 마십시오 계속 하 시겠습니까 "?** 예를 클릭 합니다. 마찬가지로, 대상에서 존재 하지 않는 스키마를 스키마를 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 동기화 중에 생성 되는 데이터베이스입니다.  
  
-   SQL Azure에 매핑  
  
연결 된 대상에 원본 데이터베이스를 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 또는 연결 된 대상에 어떤 스키마 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다. 연결 된 대상 데이터베이스에서 어떤 존재 하지 않는 스키마 소스 스키마를 매핑할 경우 다음 메시지와 함께 나타납니다 **"스키마 대상 메타 데이터에는 존재 하지 않습니다. 해당 하는 동기화 하는 동안 만들어졌습니다. 계속 하 시겠습니까? "** 예를 클릭 합니다.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>기본 데이터베이스 및 스키마에 되돌리기  
MySQL 스키마와 SQL Server 스키마 간의 매핑을 사용자 지정 하는 경우 기본 값으로 다시 매핑이 되돌릴 수 있습니다.  
  
**기본 데이터베이스 및 스키마로 되돌리려면**  
  
1.  스키마 매핑 탭에서 모든 행을 선택 하 고 클릭 **기본값으로 재설정** 기본 데이터베이스 및 스키마에 되돌릴 수 있습니다.  
  
## <a name="next-steps"></a>Next Steps  
SQL Server 또는 SQL Azure 개체 MySQL 개체의 변환 분석 하려는 경우 다음을 할 수 있습니다 [변환 보고서를 만들](http://msdn.microsoft.com/en-us/2a56a003-3b0f-453a-963c-00c9e40933ec) 수 그렇지 않으면 [MySQL 데이터베이스 개체 정의 변환](http://msdn.microsoft.com/en-us/ac21850b-fb32-4704-9985-5759b7c688c7) 스키마를 SQL Server 또는 SQL Azure로  
  
## <a name="see-also"></a>관련 항목:  
[프로젝트 설정 &#40; 변환 &#41; &#40; MySQLToSQL &#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
[Azure SQL DB &#40;에 연결 MySQLToSQL &#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
[Azure SQL DB &#40; SQL Server-MySQL 데이터베이스 마이그레이션 MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[SQL Server &#40;에 연결 MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  

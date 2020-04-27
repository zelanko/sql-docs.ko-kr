---
title: MySQL 데이터베이스를 SQL Server 스키마에 매핑 (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping, Modifying target database and schema
- Mapping, reverting to default database and schema
ms.assetid: 5c6fb445-92ae-4933-b77d-80230931c024
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 215833c96fae02ae7877e00173fb5a920a47ee0c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67908983"
---
# <a name="mapping-mysql-databases-to-sql-server-schemas-mysqltosql"></a>MySQL 데이터베이스를 SQL Server 스키마에 매핑(MySQLToSQL)
기본적으로, MySQL 용 SSMA는 MySQL 스키마의 모든 개체를 스키마에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대해 명명 된 또는 SQL Azure 데이터베이스로 마이그레이션합니다. 그러나 MySQL 스키마와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터베이스 간의 매핑을 사용자 지정할 수 있습니다.  
  
## <a name="mysql-and-sql-server-or-sql-azure-schemas"></a>MySQL 및 SQL Server 또는 SQL Azure 스키마  
스키마의 MySQL 개념은 데이터베이스의 SQL Server 개념과 스키마 중 하나에 매핑됩니다. SSMA는 데이터베이스와 스키마의 SQL Server 조합을 스키마로 나타냅니다.  
  
스키마의 MySQL 개념은 데이터베이스의 SQL Server 개념과 스키마 중 하나에 매핑됩니다. 예를 들어 MySQL은 **HR**이라는 스키마를 포함할 수 있습니다. SQL Server 인스턴스에 **HR**이라는 데이터베이스가 있을 수 있으며, 해당 데이터베이스 내에는 스키마가 있습니다. 한 스키마는 **dbo** (또는 데이터베이스 소유자) 스키마입니다. 기본적으로 MySQL 스키마 **hr** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 및 스키마에 매핑됩니다. **dbo**. SSMA는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 스키마의 조합을 스키마로 나타냅니다.  
  
MySQL과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure 스키마 간의 매핑을 수정할 수 있습니다.  
  
## <a name="modifying-the-target-database-and-schema"></a>대상 데이터베이스 및 스키마 수정  
SSMA에서 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스키마 또는 SQL Azure 스키마에 MySQL 스키마를 매핑할 수 있습니다.  
  
**데이터베이스 및 스키마를 수정 하려면**  
  
1.  MySQL 메타 데이터 탐색기에서 **스키마**를 선택 합니다.  
  
    **스키마 매핑** 탭은 개별 스키마를 선택 하는 경우에도 사용할 수 있습니다. **스키마 매핑** 탭의 목록은 선택한 개체에 대해 사용자 지정 됩니다.  
  
2.  오른쪽 창에서 **스키마 매핑** 탭을 클릭 합니다.  
  
    모든 MySQL 스키마 목록에 대상 값이 표시 됩니다. 이 대상은에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 두 부분으로 구성 된 표기법 (*데이터베이스 스키마*) 또는 개체와 데이터가 마이그레이션되는 SQL Azure 표시 됩니다.  
  
3.  변경 하려는 매핑이 포함 된 행을 선택 하 고 **수정**을 클릭 합니다.  
  
    **대상 스키마 선택** 대화 상자에서 사용 가능한 대상 데이터베이스와 스키마를 찾아보거나 두 부분으로 구성 된 표기법 (데이터베이스 스키마)의 텍스트 상자에 데이터베이스 및 스키마 이름을 입력 한 다음 **확인을**클릭 합니다.  
  
4.  대상은 **스키마 매핑** 탭에서 변경 됩니다.  
  
**매핑 모드**  
  
-   SQL Server 매핑  
  
원본 데이터베이스를 대상 데이터베이스에 매핑할 수 있습니다. 기본적으로 원본 데이터베이스는 SSMA를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하 여 연결 된 대상 데이터베이스에 매핑됩니다. 매핑되는 대상 데이터베이스가 존재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하지 않는 경우 **"데이터베이스 및/또는 스키마가 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터에 없습니다." 라는 메시지가 표시 됩니다. 동기화 중에 생성 됩니다. 계속 하 시겠습니까? "** 예를 클릭합니다. 마찬가지로, 동기화 중에 생성 되는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 기존이 아닌 스키마에 스키마를 매핑할 수 있습니다.  
  
-   SQL Azure 매핑  
  
원본 데이터베이스를 연결 된 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 또는 연결 된 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 모든 스키마에 매핑할 수 있습니다. 원본 스키마를 연결 된 대상 데이터베이스의 존재 하지 않는 스키마에 매핑하면 **"스키마가 대상 메타 데이터에 없습니다." 라는 메시지가 표시 됩니다. 동기화 중에 생성 됩니다. 계속 하 시겠습니까? "** 예를 클릭 합니다.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>기본 데이터베이스 및 스키마로 되돌리기  
MySQL 스키마와 SQL Server 스키마 간의 매핑을 사용자 지정 하는 경우 매핑을 다시 기본값으로 되돌릴 수 있습니다.  
  
**기본 데이터베이스 및 스키마로 되돌리려면**  
  
1.  스키마 매핑 탭에서 행을 선택 하 고 기본값으로 **다시 설정** 을 클릭 하 여 기본 데이터베이스 및 스키마로 되돌립니다.  
  
## <a name="next-steps"></a>다음 단계  
MySQL 개체를 SQL Server 또는 SQL Azure 개체로 변환 하는 것을 분석 하려면 [변환 보고서를 만들](assessing-mysql-databases-for-conversion-mysqltosql.md) 수 있습니다. 그렇지 않으면 [mysql 데이터베이스 개체 정의를](converting-mysql-databases-mysqltosql.md) SQL Server 또는 SQL Azure 스키마로 변환할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[프로젝트 설정 &#40;MySQLToSQL&#41;&#41; &#40;변환](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
[Azure SQL DB &#40;MySQLToSQL&#41;에 연결](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
[MySQL 데이터베이스를 SQL Server로 마이그레이션-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[MySQLToSQL&#41;&#40;SQL Server에 연결](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  

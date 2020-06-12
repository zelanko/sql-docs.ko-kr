---
title: MySQL 데이터베이스를 SQL Server로 마이그레이션-Azure SQL DB | Microsoft Docs
description: 이 권장 프로세스를 사용 하 여 MySQL 데이터베이스를 SQL Server으로 마이그레이션하거나 SSMA (SQL Server Migration Assistant)를 사용 하 여 Azure SQL Database 합니다.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8006f9a0-394d-4238-8dc5-44255134628b
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0daee899775b5a8bb3a0e4b6ee0eef4a93eca00b
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293592"
---
# <a name="migrating-mysql-databases-to-sql-server---azure-sql-db-mysqltosql"></a>MySQL 데이터베이스를 SQL Server로 마이그레이션-Azure SQL DB (MySQLToSql)
MySQL 용 SSMA (SQL Server Migration Assistant)는 MySQL 데이터베이스를 SQL Server 또는 SQL Azure으로 신속 하 게 마이그레이션하는 데 도움이 되는 포괄적인 환경입니다. MySQL 용 SSMA를 사용 하 여 데이터베이스 개체 및 데이터를 검토 하 고, 마이그레이션을 위해 데이터베이스를 평가 하 고, 데이터베이스 개체를 SQL Server 또는 SQL Azure로 마이그레이션하고, 데이터를 SQL Server 또는 SQL Azure로 마이그레이션할 수 있습니다.  
  
## <a name="recommended-migration-process"></a>권장 마이그레이션 프로세스  
MySQL 데이터베이스에서 SQL Server 또는 SQL Azure로 개체 및 데이터를 성공적으로 마이그레이션하려면 다음 프로세스를 사용 합니다.  
  
1.  [SSMA 프로젝트를 사용 하 여 &#40;MySQLToSQL&#41;를 사용 ](../../ssma/mysql/working-with-ssma-projects-mysqltosql.md)합니다.  
  
    프로젝트를 만든 후 프로젝트 변환, 마이그레이션 및 형식 매핑 옵션을 설정할 수 있습니다. 프로젝트 설정에 대 한 자세한 내용은 [프로젝트 옵션 설정 &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)을 참조 하세요. 데이터 형식 매핑을 사용자 지정 하는 방법에 대 한 자세한 내용은 [MySQL 및 SQL Server 데이터 형식 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md) 를 참조 하세요.  
  
2.  [MySQL &#40;MySQLToSQL&#41;에 연결](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
3.  [MySQLToSQL&#41;&#40;SQL Server에 연결](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
4.  [MySQL 데이터베이스를 SQL Server 스키마 &#40;MySQLToSQL&#41;에 매핑](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
5.  [Azure SQL DB &#40;MySQLToSQL&#41;에 연결](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
6.  필요에 따라 [MySQLToSQL&#41;&#40;변환에 대해 MySQL 데이터베이스를 평가](../../ssma/mysql/assessing-mysql-databases-for-conversion-mysqltosql.md) 하 여 변환에 대 한 데이터베이스 개체를 평가 하 고 변환 시간을 예측할 수 있습니다.  
  
7.  [MySQL 데이터베이스 &#40;MySQLToSQL&#41;변환](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
8.  [동기화](loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
9. 다음 방법 중 하나를 수행 하 여이 작업을 수행할 수 있습니다.  
  
    -   스크립트를 저장 하 고 SQL Server 또는 SQL Azure에 대해 실행 합니다.  
  
    -   데이터베이스 개체를 동기화 합니다.  
  
10. [MySQL 데이터를 SQL Server로 마이그레이션-Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
11. 필요한 경우 데이터베이스 응용 프로그램을 업데이트 합니다.  
  
> [!NOTE]  
> Information_schema 및 MySQL 스키마는 마이그레이션할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
[&#40;MySqlToSql&#41;에 대 한 MySQL 용 SSMA 설치](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
[MySQL 용 SSMA를 시작 &#40;MySQLToSQL&#41;](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)  
  

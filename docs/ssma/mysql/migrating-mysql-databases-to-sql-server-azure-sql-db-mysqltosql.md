---
title: MySQL 데이터베이스를 SQL Server-SQL Azure DB로 마이그레이션 | Microsoft Docs
ms.prod: sql-non-specified
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
ms.assetid: 8006f9a0-394d-4238-8dc5-44255134628b
caps.latest.revision: 12
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: afd5e6aee5fb59c6e3eebb11c47d04b09e37bd40
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="migrating-mysql-databases-to-sql-server---azure-sql-db-mysqltosql"></a>SQL Server-Azure SQL DB (MySQLToSql) MySQL 데이터베이스 마이그레이션
SQL Server Migration Assistant (SSMA) MySQL 용 SQL Server 또는 SQL Azure에 MySQL 데이터베이스를 신속 하 게 마이그레이션할 수 있는 통합 환경을입니다. MySQL 용 SSMA를 사용해 있습니다 수 데이터베이스 개체와 데이터를 검토 평가 마이그레이션할 데이터베이스, SQL Server 또는 SQL Azure에 데이터베이스 개체를 마이그레이션할 하 고, 다음 SQL Server 또는 SQL Azure에 데이터를 마이그레이션합니다.  
  
## <a name="recommended-migration-process"></a>권장 되는 마이그레이션 프로세스  
을 성공적으로 마이그레이션하려면 개체 및 데이터에서 MySQL 데이터베이스를 SQL Server 또는 SQL Azure는 다음 프로세스를 사용 합니다.  
  
1.  [SSMA 프로젝트 작업 &#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-ssma-projects-mysqltosql.md)합니다.  
  
    프로젝트를 만든 후에 프로젝트 변환, 마이그레이션 및 유형 매핑 옵션을 설정할 수 있습니다. 프로젝트 설정에 대 한 자세한 내용은 참조 [프로젝트 옵션 설정 &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)합니다. 데이터 형식 매핑을 사용자 지정 하는 방법에 대 한 정보를 참조 하십시오. [매핑 MySQL 및 SQL Server 데이터 형식 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
2.  [MySQL에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
3.  [SQL Server에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
4.  [MySQL 데이터베이스를 SQL Server 스키마로 매핑 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
5.  [Azure SQL DB에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
6.  필요에 따라 [변환에 대 한 MySQL 데이터베이스 평가 &#40;MySQLToSQL&#41; ](../../ssma/mysql/assessing-mysql-databases-for-conversion-mysqltosql.md) 변환에 대 한 데이터베이스 개체를 평가 하는 변환 시간 예측 합니다.  
  
7.  [MySQL 데이터베이스 변환 &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
8.  [동기화](http://msdn.microsoft.com/en-us/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
9. 다음 방법 중 하나에서이 수행할 수 있습니다.  
  
    -   스크립트를 저장 하 고 SQL Server 또는 SQL Azure에서 실행 합니다.  
  
    -   데이터베이스 개체를 동기화 합니다.  
  
10. [SQL Server-Azure SQL DB에 MySQL 데이터 마이그레이션 &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
11. 필요한 경우 데이터베이스 응용 프로그램을 업데이트 합니다.  
  
> [!NOTE]  
> Information_schema 및 MySQL 스키마를 마이그레이션할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목:  
[MySQL 용 SSMA를 설치 &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
[MySQL 용 SSMA 시작 &#40;MySQLToSQL&#41;](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)  
  

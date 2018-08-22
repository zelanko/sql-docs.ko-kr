---
title: SQL Server (OracleToSQL)로 데이터베이스 마이그레이션 Oracle | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 05cdf94aaac3c3b5401681edb996ed740fbc94a6
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40396010"
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>Oracle 데이터베이스를 SQL Server로 마이그레이션(OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) for Oracle은 Oracle 데이터베이스를 신속 하 게 마이그레이션할 수 있도록 포괄적인 환경을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Azure SQL DB 또는 Azure SQL Data Warehouse. SSMA for Oracle을 사용 하 여 있습니다 수 데이터베이스 개체 및 데이터를 검토, 평가 마이그레이션에 대 한 데이터베이스, 데이터베이스 개체를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Azure SQL DB 또는 Azure SQL Data Warehouse 및 데이터를 마이그레이션하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Azure SQL DB 또는 Azure SQL 데이터 웨어하우스입니다. 참고 SYS 및 시스템 Oracle 스키마를 마이그레이션할 수 없습니다.
  
## <a name="recommended-migration-process"></a>권장 되는 마이그레이션 프로세스  
Oracle 데이터베이스에서 개체 및 데이터를 성공적으로 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Azure SQL DB 또는 Azure SQL Data Warehouse는 다음 프로세스를 사용 합니다.
  
1.  [새 SSMA 프로젝트를 만들](working-with-ssma-projects-oracletosql.md)합니다.  
  
    프로젝트를 만든 후에 프로젝트 변환, 마이그레이션 및 유형 매핑 옵션을 설정할 수 있습니다. 프로젝트 설정에 대 한 자세한 내용은 [프로젝트 옵션 설정 &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)합니다. 데이터 형식 매핑 사용자 지정 하는 방법에 대 한 정보를 참조 하세요 [매핑 Oracle 및 SQL Server 데이터 형식 &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)합니다.  
  
2.  [Oracle 데이터베이스 서버에 연결할](connecting-to-oracle-database-oracletosql.md)합니다.  
  
3.  [SQL Server의 인스턴스에 연결할](connecting-to-sql-server-oracletosql.md)합니다.  
  
4.  [Oracle 데이터베이스 스키마를 SQL Server 데이터베이스 스키마에 매핑](mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md)합니다.  
  
5.  필요에 따라 [평가 보고서를 만들](assessing-oracle-schemas-for-conversion-oracletosql.md) 변환에 대 한 데이터베이스 개체를 평가 하는 변환 시간 예측 합니다.  
  
6.  [Oracle 데이터베이스 스키마를 SQL Server 스키마 변환](converting-oracle-schemas-oracletosql.md)합니다.  
  
7.  [SQL Server로 변환 된 데이터베이스 개체를 로드](loading-converted-database-objects-into-sql-server-oracletosql.md)합니다.  
  
    다음 방법 중 하나에서이 수행할 수 있습니다.  
  
    -   스크립트를 저장 하 고 실행할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
    -   데이터베이스 개체를 동기화 합니다.  
  
8.  [SQL Server로 데이터 마이그레이션](migrating-oracle-data-into-sql-server-oracletosql.md)합니다.  
  
9. 필요한 경우 데이터베이스 응용 프로그램을 업데이트 합니다.  
  
## <a name="see-also"></a>관련 항목  
[Oracle 용 SSMA 설치 &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[Oracle 용 SSMA 시작 &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  

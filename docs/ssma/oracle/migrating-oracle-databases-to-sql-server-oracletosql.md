---
title: Oracle 데이터베이스를 SQL Server로 마이그레이션 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: e1021643d503e1ca77f120b81046b3773f8ff458
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68259106"
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>Oracle 데이터베이스를 SQL Server로 마이그레이션(OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Oracle 용 SSMA (Migration Assistant)는 Oracle 데이터베이스를, Azure SQL DB 또는 Azure SQL Data Warehouse로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]신속 하 게 마이그레이션하는 데 도움이 되는 포괄적인 환경입니다. Oracle 용 SSMA를 사용 하 여 데이터베이스 개체 및 데이터를 검토 하 고, 마이그레이션을 위해 데이터베이스를 평가 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 데이터베이스 개체를, AZURE sql db 또는 Azure SQL Data Warehouse로 마이그레이션한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], azure sql db 또는 Azure SQL Data Warehouse로 데이터를 마이그레이션할 수 있습니다. SYS 및 시스템 Oracle 스키마는 마이그레이션할 수 없습니다.
  
## <a name="recommended-migration-process"></a>권장 마이그레이션 프로세스  
Oracle 데이터베이스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], AZURE SQL DB 또는 Azure SQL Data Warehouse의 개체와 데이터를 성공적으로 마이그레이션하려면 다음 프로세스를 사용 합니다.
  
1.  [새 SSMA 프로젝트를 만듭니다](working-with-ssma-projects-oracletosql.md).  
  
    프로젝트를 만든 후 프로젝트 변환, 마이그레이션 및 형식 매핑 옵션을 설정할 수 있습니다. 프로젝트 설정에 대 한 자세한 내용은 [프로젝트 옵션 설정 &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)을 참조 하세요. 데이터 형식 매핑을 사용자 지정 하는 방법에 대 한 자세한 내용은 [OracleToSQL&#41;&#40;Oracle 및 SQL Server 데이터 형식 매핑 ](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)을 참조 하세요.  
  
2.  [Oracle 데이터베이스 서버에 연결](connecting-to-oracle-database-oracletosql.md)합니다.  
  
3.  [SQL Server 인스턴스에 연결](connecting-to-sql-server-oracletosql.md)합니다.  
  
4.  [Oracle 데이터베이스 스키마를 SQL Server 데이터베이스 스키마에 매핑합니다](mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
5.  필요에 따라 [평가 보고서를 만들어](assessing-oracle-schemas-for-conversion-oracletosql.md) 변환에 대 한 데이터베이스 개체를 평가 하 고 변환 시간을 예측할 수 있습니다.  
  
6.  [Oracle 데이터베이스 스키마를 SQL Server 스키마로 변환](converting-oracle-schemas-oracletosql.md)합니다.  
  
7.  [변환 된 데이터베이스 개체를 SQL Server으로 로드](loading-converted-database-objects-into-sql-server-oracletosql.md)합니다.  
  
    다음 방법 중 하나를 수행 하 여이 작업을 수행할 수 있습니다.  
  
    -   스크립트를 저장 하 고에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]실행 합니다.  
  
    -   데이터베이스 개체를 동기화 합니다.  
  
8.  [SQL Server로 데이터를 마이그레이션합니다](migrating-oracle-data-into-sql-server-oracletosql.md).  
  
9. 필요한 경우 데이터베이스 응용 프로그램을 업데이트 합니다.  
  
## <a name="see-also"></a>참고 항목  
[OracleToSQL&#41;&#40;Oracle 용 SSMA 설치](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[Oracle &#40;OracleToSQL&#41;에 대 한 SSMA 시작](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  

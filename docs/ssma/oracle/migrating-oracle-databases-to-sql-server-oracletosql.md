---
title: SQL Server (OracleToSQL)로 데이터베이스 마이그레이션 Oracle | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Active
ms.openlocfilehash: 09fe8820413108e4df6479b0a7c2bd95f1f84741
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>SQL Server (OracleToSQL) Oracle 데이터베이스 마이그레이션
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) for Oracle은 Oracle 데이터베이스를 신속 하 게 마이그레이션할 수 있는 포괄적인 환경 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Azure SQL 데이터 웨어하우스 또는 Azure SQL DB 합니다. SSMA for Oracle을 사용 하 여 있습니다 수 데이터베이스 개체와 데이터를 검토, 평가 마이그레이션할 데이터베이스, 데이터베이스 개체를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Azure SQL DB 또는 Azure SQL 데이터 웨어하우스 및 데이터를 마이그레이션하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Azure SQL DB 또는 Azure SQL 데이터 웨어하우스입니다. 참고 SYS 및 시스템 Oracle 스키마를 마이그레이션할 수 없습니다.
  
## <a name="recommended-migration-process"></a>권장 되는 마이그레이션 프로세스  
에 Oracle 데이터베이스에서 개체 및 데이터를 성공적으로 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Azure SQL 데이터 웨어하우스 또는 Azure SQL DB 다음 프로세스를 사용 합니다.
  
1.  [새 SSMA 프로젝트 만들기](http://msdn.microsoft.com/en-us/ee5d94c0-c7a6-4779-bd32-729bdaf61e1b)합니다.  
  
    프로젝트를 만든 후에 프로젝트 변환, 마이그레이션 및 유형 매핑 옵션을 설정할 수 있습니다. 프로젝트 설정에 대 한 정보를 참조 하십시오. [프로젝트 옵션 설정 &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)합니다. 데이터 형식 매핑을 사용자 지정 하는 방법에 대 한 정보를 참조 하십시오. [매핑 Oracle 및 SQL Server 데이터 형식 &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)합니다.  
  
2.  [Oracle 데이터베이스 서버에 연결](http://msdn.microsoft.com/en-us/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6)합니다.  
  
3.  [SQL Server의 인스턴스에 연결할](http://msdn.microsoft.com/en-us/1b2a8059-1829-4904-a82f-9c06de1e245f)합니다.  
  
4.  [Oracle 데이터베이스 스키마를 SQL Server 데이터베이스 스키마로 매핑](http://msdn.microsoft.com/en-us/0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc)합니다.  
  
5.  필요에 따라 [평가 보고서를 만들](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357) 변환에 대 한 데이터베이스 개체를 평가 하는 변환 시간 예측 합니다.  
  
6.  [Oracle 데이터베이스 스키마를 SQL Server 스키마로 변환](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272)합니다.  
  
7.  [SQL Server로 변환 된 데이터베이스 개체를 로드](http://msdn.microsoft.com/en-us/a8ae33b2-1883-4785-922b-ea0e31c0b37a)합니다.  
  
    다음 방법 중 하나에서이 수행할 수 있습니다.  
  
    -   스크립트를 저장 하 고 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
    -   데이터베이스 개체를 동기화 합니다.  
  
8.  [SQL Server로 데이터 마이그레이션](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13)합니다.  
  
9. 필요한 경우 데이터베이스 응용 프로그램을 업데이트 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[Oracle 용 SSMA를 설치 &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[Oracle 용 SSMA 시작 &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  

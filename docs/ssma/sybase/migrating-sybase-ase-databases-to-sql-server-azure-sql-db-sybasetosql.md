---
title: Sybase ASE 데이터베이스를 SQL Server-Azure SQL Database로 마이그레이션 | Microsoft Docs
description: 이 권장 프로세스를 사용 하 여 SAP 적응 서버 엔터프라이즈 데이터베이스를 SQL Server로 마이그레이션하거나 SSMA (SQL Server Migration Assistant)를 사용 하 여 Azure SQL Database 합니다.
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f37f80cda41279b7c773d7a2c89216c5f24e9000
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034985"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>SAP ASE 데이터베이스를 SQL Server-Azure SQL Database로 마이그레이션 (SybaseToSQL)
SAP 적응 서버 엔터프라이즈 (ASE) 용 SSMA (SQL Server Migration Assistant)는 SAP ASE 데이터베이스를 또는 Azure SQL Database으로 신속 하 게 마이그레이션하는 데 도움이 되는 포괄적인 환경입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . SAP ASE 용 SSMA를 사용 하 여 데이터베이스 개체 및 데이터를 검토 하 고, 마이그레이션을 위해 데이터베이스를 평가 하 고, 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL Database 마이그레이션하고, 데이터를 또는 Azure SQL Database로 마이그레이션할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="recommended-migration-process"></a>권장 마이그레이션 프로세스  
SAP ASE 데이터베이스에서 또는 Azure SQL Database 개체 및 데이터를 성공적으로 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음 프로세스를 사용 합니다.  
  
1.  [새 SSMA 프로젝트를 만듭니다](working-with-ssma-projects-sybasetosql.md).  
  
    프로젝트를 만든 후 프로젝트 변환, 마이그레이션 및 형식 매핑 옵션을 설정할 수 있습니다. 프로젝트 설정에 대 한 자세한 내용은 [프로젝트 옵션 설정 &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)을 참조 하세요. 데이터 형식 매핑을 사용자 지정 하는 방법에 대 한 자세한 내용은 [SYBASE ASE 및 SQL Server 데이터 형식 매핑 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)을 참조 하세요.  
  
2.  [SAP ASE 데이터베이스 서버에 연결](connecting-to-sybase-ase-sybasetosql.md)합니다.  
  
3.  [SQL Server 인스턴스에 연결](connecting-to-sql-server-sybasetosql.md) 하거나 [Azure SQL Database 인스턴스에](connecting-to-azure-sql-db-sybasetosql.md)연결 합니다.  
  
4.  [SAP ASE 데이터베이스 스키마를 SQL Server/Azure SQL Database 데이터베이스 스키마에 매핑합니다](./mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
5.  필요에 따라 [평가 보고서를 만들어](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) 변환에 대 한 데이터베이스 개체를 평가 하 고 변환 시간을 예측할 수 있습니다.  
  
6.  [SAP ASE 데이터베이스 스키마를 SQL Server/Azure SQL Database 스키마로 변환](./converting-sybase-ase-database-objects-sybasetosql.md)합니다.  
  
7.  [변환 된 데이터베이스 개체를 SQL Server/Azure SQL Database 로드](./loading-converted-database-objects-into-sql-server-sybasetosql.md)합니다.  
  
    스크립트를 저장 하 고 또는 Azure SQL Database에서 실행 하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체를 동기화 합니다.  
  
8.  [SQL Server/Azure SQL Database으로 데이터를 마이그레이션합니다](./migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md).  
  
9. 필요한 경우 데이터베이스 응용 프로그램을 업데이트 합니다.  
  
## <a name="see-also"></a>참조  
[SAP ASE 용 SSMA 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[SAP ASE 용 SSMA를 시작 하는 방법 &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  

---
title: Access 데이터베이스를 SQL Server-Azure SQL DB로 마이그레이션 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- instructions, migration
- migrating databases, overview
- overview, migration process
- procedure, migration
- recommended migration process
ms.assetid: 76a3abcf-2998-4712-9490-fe8d872c89ca
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 959af9bcb1879dc19d2bfb99253b4c40d637fd1e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68260239"
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>SQL Server-Azure SQL DB (AccessToSQL) 액세스 데이터베이스 마이그레이션
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA)는 Access 데이터베이스를 신속 하 게 마이그레이션할 수 있도록 하는 통합 환경을 제공 하는 도구 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. SSMA를 사용 하 여 액세스를 검토할 수 있습니다 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터베이스 개체, 마이그레이션에 대 한 Access 데이터베이스 평가, Access 데이터베이스 개체를 변환 및 로드에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터를 마이그레이션해야 합니다.  
  
## <a name="recommended-migration-process"></a>권장 되는 마이그레이션 프로세스  
개체 및 데이터에 대 한 액세스에서 마이그레이션하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure, 다음 프로세스를 사용 합니다.  
  
1.  [새 SSMA 프로젝트를 만들](creating-and-managing-projects-accesstosql.md)합니다. 프로젝트를 만들 수 있습니다 [프로젝트 옵션 설정](setting-conversion-and-migration-options-accesstosql.md)변환 옵션, 마이그레이션 옵션 및 데이터 형식 매핑을 포함 합니다.  
  
2.  [Access 데이터베이스 파일 추가](adding-and-removing-access-database-files-accesstosql.md) 프로젝트입니다.  
  
    컴퓨터나 네트워크에서 검색 된 파일을 포함 하 여 개별 파일을 추가할 수 있습니다.  
  
3.  [대상 인스턴스의 SQL Server에 연결](connecting-to-sql-server-accesstosql.md) 나 [SQL Azure 대상 인스턴스에 연결할](connecting-to-azure-sql-db-accesstosql.md)합니다.  
  
    SQL Server 또는 SQL Azure 연결할 수 있습니다.  
  
4.  하나 이상의 Access 데이터베이스 간의 매핑을 사용자 지정 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 스키마 [매핑할 원본 및 대상 데이터베이스를](mapping-source-and-target-databases-accesstosql.md)입니다.  
  
5.  필요에 따라 수 있습니다 [평가 보고서를 만드는](assessing-access-database-objects-for-conversion-accesstosql.md) 에 Access 데이터베이스 개체를 성공적으로 변환할 수 있는지 여부를 확인 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다.  
  
6.  [Access 데이터베이스 개체를 변환할](converting-access-database-objects-accesstosql.md) 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체를 정의 합니다.  
  
7.  [SQL Server로 변환 된 데이터베이스 개체를 로드](loading-converted-database-objects-into-sql-server-accesstosql.md)합니다.  
  
    에 데이터베이스 개체를 로드할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA를 또는 사용 하 여 SQL Azure 저장할 수 있습니다 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트입니다.  
  
8.  [SQL Server에 대 한 액세스 데이터를 마이그레이션할](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)합니다.  
  
    > [!NOTE]  
    > 변환 하 고, 로드 하 고, 스키마 및 데이터를 한 번에에서 마이그레이션할 수 있습니다. 한 번의 클릭 마이그레이션을 수행 하려면 클릭 합니다 **변환, 로드 및 마이그레이션** 단추입니다.  
  
9. 액세스 응용 프로그램에서 데이터를 사용 하려는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 사용 하 여 [SQL Server 테이블에 테이블 액세스 링크](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)합니다.  
  
또한이 과정을 안내 하는 마이그레이션 마법사를 사용할 수 있습니다. 자세한 내용은 [마이그레이션 마법사](migration-wizard-accesstosql.md)합니다.  
  
## <a name="see-also"></a>참조  
[액세스에 대 한 SQL Server Migration Assistant 시작](getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Access 데이터베이스 마이그레이션 준비](preparing-access-databases-for-migration-accesstosql.md)

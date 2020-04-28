---
title: SQL Server로 Access 데이터베이스 마이그레이션-Azure SQL DB | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68260239"
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>SQL Server로 Access 데이터베이스 마이그레이션-Azure SQL DB (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SSMA (Migration Assistant)는 Access 데이터베이스를 또는 SQL Azure로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 신속 하 게 마이그레이션하는 데 도움이 되는 종합적인 환경을 제공 하는 도구입니다. SSMA를 사용 하 여 데이터베이스 개체에 대 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 한 액세스 및 SQL Azure 데이터베이스 개체를 검토 하 고, access 데이터베이스 개체를 변환 하 고, access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체를 변환 하 고, 데이터를 SQL Azure 하 고, 데이터를 마이그레이션할 수 있습니다.  
  
## <a name="recommended-migration-process"></a>권장 마이그레이션 프로세스  
개체 및 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스에서 또는 SQL Azure 성공적으로 마이그레이션하려면 다음 프로세스를 사용 합니다.  
  
1.  [새 SSMA 프로젝트를 만듭니다](creating-and-managing-projects-accesstosql.md). 프로젝트를 만든 후에는 변환 옵션, 마이그레이션 옵션 및 데이터 형식 매핑을 포함 하 여 [프로젝트 옵션을 설정할](setting-conversion-and-migration-options-accesstosql.md)수 있습니다.  
  
2.  프로젝트에 [Access 데이터베이스 파일을 추가](adding-and-removing-access-database-files-accesstosql.md) 합니다.  
  
    컴퓨터 또는 네트워크에서 찾은 파일을 포함 하 여 개별 파일을 추가할 수 있습니다.  
  
3.  [SQL Server의 대상 인스턴스에 연결](connecting-to-sql-server-accesstosql.md) 하거나 [SQL Azure의 대상 인스턴스에 연결](connecting-to-azure-sql-db-accesstosql.md)합니다.  
  
    SQL Server 또는 SQL Azure에 연결할 수 있습니다.  
  
4.  하나 이상의 Access 데이터베이스와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 스키마 간의 매핑을 사용자 지정 하려면 [원본 데이터베이스와 대상 데이터베이스를 매핑합니다](mapping-source-and-target-databases-accesstosql.md).  
  
5.  필요에 따라 [평가 보고서를 만들어](assessing-access-database-objects-for-conversion-accesstosql.md) Access 데이터베이스 개체를 성공적으로 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 SQL Azure 수 있는지 여부를 확인할 수 있습니다.  
  
6.  [Access 데이터베이스 개체](converting-access-database-objects-accesstosql.md) 를 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure 개체 정의로 변환 합니다.  
  
7.  [변환 된 데이터베이스 개체를 SQL Server으로 로드](loading-converted-database-objects-into-sql-server-accesstosql.md)합니다.  
  
    SSMA를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터베이스 개체를 로드 하거나 스크립트를 저장할 [!INCLUDE[tsql](../../includes/tsql-md.md)] 수 있습니다.  
  
8.  [Access 데이터를 SQL Server으로 마이그레이션합니다](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md).  
  
    > [!NOTE]  
    > 한 번에 스키마 및 데이터를 변환, 로드 및 마이그레이션할 수 있습니다. 한 번 클릭으로 마이그레이션을 수행 하려면 **변환, 로드 및 마이그레이션** 단추를 클릭 합니다.  
  
9. Access 응용 프로그램에서 또는 SQL Azure의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 사용 하려면 [SQL Server 테이블에 액세스 테이블 연결](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)을 사용 합니다.  
  
마이그레이션 마법사를 사용 하 여이 프로세스를 안내할 수도 있습니다. 자세한 내용은 [마이그레이션 마법사](migration-wizard-accesstosql.md)를 참조 하십시오.  
  
## <a name="see-also"></a>참고 항목  
[액세스를 위한 SQL Server Migration Assistant 시작](getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[마이그레이션을 위해 Access 데이터베이스 준비](preparing-access-databases-for-migration-accesstosql.md)

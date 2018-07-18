---
title: Sybase ASE 데이터베이스를 SQL Server-Azure SQL DB로 마이그레이션 | Microsoft Docs
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a021ac1cfc442943b15ade737c54d0b9e227ef03
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982215"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>SQL Server-Azure SQL Database (SybaseToSQL)로 SAP ASE 데이터베이스 마이그레이션
SQL Server Migration Assistant (SSMA)에 대 한 SAP 적응형 Server Enterprise (ASE)는 SAP ASE 데이터베이스를 신속 하 게 마이그레이션할 수 있도록 포괄적인 환경 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL Database. SSMA SAP ase를 사용 하 여 있습니다 수 데이터베이스 개체 및 데이터를 검토, 평가 마이그레이션에 대 한 데이터베이스, 데이터베이스 개체를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL Database 및 데이터를 마이그레이션하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL Database.  
  
## <a name="recommended-migration-process"></a>권장 되는 마이그레이션 프로세스  
SAP ASE 데이터베이스에서 개체 및 데이터를 성공적으로 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL Database와 같은 프로세스를 사용 합니다.  
  
1.  [새 SSMA 프로젝트를 만들](http://msdn.microsoft.com/11091d95-c488-48c3-891a-743cac94ac93)합니다.  
  
    프로젝트를 만든 후에 프로젝트 변환, 마이그레이션 및 유형 매핑 옵션을 설정할 수 있습니다. 프로젝트 설정에 대 한 자세한 내용은 [프로젝트 옵션 설정 &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)합니다. 데이터 형식 매핑 사용자 지정에 대 한 자세한 내용은 [매핑 Sybase ASE 및 SQL Server 데이터 형식 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)합니다.  
  
2.  [SAP ASE 데이터베이스 서버에 연결할](http://msdn.microsoft.com/a45a2330-9175-4c9e-af38-ef920e350614)합니다.  
  
3.  [SQL Server 인스턴스에 연결](http://msdn.microsoft.com/dd368a1a-45b0-40e9-b4d3-5cdb48c26606) 나 [Azure SQL Database의 인스턴스에 연결](http://msdn.microsoft.com/9e77e4b0-40c0-455c-8431-ca5d43849aa7)합니다.  
  
4.  [SQL Server에 SAP ASE 데이터베이스 스키마 매핑 Azure SQL Database 데이터베이스 스키마 /](http://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268)합니다.  
  
5.  필요에 따라 [평가 보고서를 만들](http://msdn.microsoft.com/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c) 변환에 대 한 데이터베이스 개체를 평가 하는 변환 시간 예측 합니다.  
  
6.  [SQL Server로 SAP ASE 데이터베이스 스키마를 변환 / Azure SQL Database 스키마](http://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3)합니다.  
  
7.  [SQL Server로 변환 된 데이터베이스 개체를 로드 / Azure SQL Database](http://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06)합니다.  
  
    스크립트를 저장 하 고 실행 하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL Database 또는 데이터베이스 개체를 동기화 합니다.  
  
8.  [SQL Server로 데이터를 마이그레이션 / Azure SQL Database](http://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)합니다.  
  
9. 필요한 경우 데이터베이스 응용 프로그램을 업데이트 합니다.  
  
## <a name="see-also"></a>참고자료  
[SAP ASE 용 SSMA 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[SAP ASE 용 SSMA 시작 &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  

---
title: "SQL Server-Azure SQL DB에 Sybase ASE 데이터베이스 마이그레이션 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 63dc9188d93def41a5116386f93bf29e3b744e8e
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-sybase-ase-databases-to-sql-server---azure-sql-db-sybasetosql"></a>SQL Server-Azure SQL DB (SybaseToSQL) Sybase ASE 데이터베이스 마이그레이션
SQL Server Migration Assistant (SSMA) Sybase 용는 Sybase 적응형 Server Enterprise (ASE) 데이터베이스를 신속 하 게 마이그레이션할 수 있는 포괄적인 환경 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다. SSMA for Sybase를 사용 하 여 있습니다 수 데이터베이스 개체와 데이터를 검토, 평가 마이그레이션할 데이터베이스, 데이터베이스 개체를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB, 다음 데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다.  
  
## <a name="recommended-migration-process"></a>권장 되는 마이그레이션 프로세스  
ASE 데이터베이스에서 개체 및 데이터를 성공적으로 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB, 다음 프로세스를 사용 합니다.  
  
1.  [새 SSMA 프로젝트 만들기](http://msdn.microsoft.com/en-us/11091d95-c488-48c3-891a-743cac94ac93)합니다.  
  
    프로젝트를 만든 후에 프로젝트 변환, 마이그레이션 및 유형 매핑 옵션을 설정할 수 있습니다. 프로젝트 설정에 대 한 정보를 참조 하십시오. [프로젝트 옵션 설정 &#40; SybaseToSQL &#41; ](../../ssma/sybase/setting-project-options-sybasetosql.md). 데이터 형식 매핑 사용자 지정 하는 방법에 대 한 정보를 참조 하세요. [Sybase ASE 매핑 및 SQL Server 데이터 형식 &#40; SybaseToSQL &#41; ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [Sybase ASE 데이터베이스 서버에 연결](http://msdn.microsoft.com/en-us/a45a2330-9175-4c9e-af38-ef920e350614)합니다.  
  
3.  [SQL Server 인스턴스에 연결](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606) 또는 [Azure SQL DB의 인스턴스에 연결](http://msdn.microsoft.com/en-us/9e77e4b0-40c0-455c-8431-ca5d43849aa7)합니다.  
  
4.  [SQL Server에 ASE 데이터베이스 스키마 매핑 / Azure SQL DB 데이터베이스 스키마](http://msdn.microsoft.com/en-us/2c927003-c49d-4fe1-8e3e-5b2899166268)합니다.  
  
5.  필요에 따라 [평가 보고서를 만들](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c) 변환에 대 한 데이터베이스 개체를 평가 하는 변환 시간 예측 합니다.  
  
6.  [Sybase ASE 데이터베이스 스키마를 SQL Server로 변환 / Azure SQL DB 스키마](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3)합니다.  
  
7.  [SQL Server로 변환 된 데이터베이스 개체를 로드 / Azure SQL DB](http://msdn.microsoft.com/en-us/4c59256f-99a8-4351-9559-a455813dbd06)합니다.  
  
    하 여 스크립트를 저장 하 고 실행할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 하거나 Azure SQL DB가 데이터베이스 개체를 동기화 할 수 있습니다.  
  
8.  [SQL Server로 데이터 마이그레이션 / Azure SQL DB](http://msdn.microsoft.com/en-us/54a39f5e-9250-4387-a3ae-eae47c799811)합니다.  
  
9. 필요한 경우 데이터베이스 응용 프로그램을 업데이트 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SSMA for Sybase &#40; 설치 SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[SSMA for Sybase &#40; 시작 SybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  


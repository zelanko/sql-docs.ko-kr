---
title: "Access 데이터베이스를 SQL Server-SQL Azure DB로 마이그레이션 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- instructions, migration
- migrating databases, overview
- overview, migration process
- procedure, migration
- recommended migration process
ms.assetid: 76a3abcf-2998-4712-9490-fe8d872c89ca
caps.latest.revision: 23
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6d3c44ed3c73edae1b2b8d9cd244a2530c5748cf
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>SQL Server-Azure SQL DB (AccessToSQL)로 액세스 데이터베이스 마이그레이션
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA)는 Access 데이터베이스를 신속 하 게 마이그레이션할 수 있는 포괄적인 환경 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다. SSMA를 사용 하 여 액세스를 검토할 수 있습니다 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 데이터베이스 개체, Access 데이터베이스 마이그레이션에 대 한 평가, Access 데이터베이스 개체를 변환, 로드로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 데이터를 마이그레이션해야 합니다.  
  
## <a name="recommended-migration-process"></a>권장 되는 마이그레이션 프로세스  
개체 및 데이터에 대 한 액세스를 마이그레이션하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure로 다음 프로세스를 사용 합니다.  
  
1.  [새 SSMA 프로젝트 만들기](http://msdn.microsoft.com/en-us/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7)합니다. 프로젝트를 만든 후 다음을 할 수 있습니다 [프로젝트 옵션을 설정](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167)합니다. 여기에 변환 옵션, 마이그레이션 옵션 및 데이터 형식 매핑을 포함 합니다.  
  
2.  [Access 데이터베이스 파일을 추가](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced) 프로젝트에 있습니다.  
  
    개별 파일을 추가할 수 있습니다 또는 컴퓨터나 네트워크에서 검색 된 파일을 추가할 수 있습니다.  
  
3.  [SQL Server의 대상 인스턴스에 연결](http://msdn.microsoft.com/en-us/f84cf007-ddf1-4396-a07c-3e0729abc769) 또는 [SQL Azure의 대상 인스턴스에 연결](http://msdn.microsoft.com/en-us/1ba0d113-dc05-4431-8689-e14a8821bafd)합니다.  
  
    하거나 SQL Server 또는 SQL Azure에 연결할 수 있습니다.  
  
4.  하나 이상의 Access 데이터베이스 간의 매핑을 사용자 지정 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 스키마 [맵 소스 및 대상 데이터베이스가](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)합니다.  
  
5.  수 필요에 따라 [평가 보고서를 만들](http://msdn.microsoft.com/en-us/8b9e23d6-da62-437a-8c05-8ad2628b9441)를 Access 데이터베이스 개체를 성공적으로 변환할 수 있는지 여부를 확인 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다.  
  
6.  [Access 데이터베이스 개체를 변환](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c) 를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 개체를 정의 합니다.  
  
7.  [SQL Server로 변환 된 데이터베이스 개체를 로드](http://msdn.microsoft.com/en-us/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba)합니다.  
  
    데이터베이스 개체에 부 하나를 수행할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 저장할 수 있습니다 또는 SSMA를 사용 하 여 SQL Azure 또는 [!INCLUDE[tsql](../../includes/tsql_md.md)] 스크립트입니다.  
  
8.  [데이터 액세스를 SQL Server로 마이그레이션](http://msdn.microsoft.com/en-us/f3b18af7-1af0-499d-a00d-a0af94895625)합니다.  
  
    > [!NOTE]  
    > 변환, 로드 및 스키마와 데이터를 한 번에 마이그레이션할 수 있습니다. 한 번의 클릭 마이그레이션을 수행 하려면 클릭는 **변환, 로드 및 마이그레이션** 단추입니다.  
  
9. 액세스 응용 프로그램의 데이터를 사용 하는 경우 원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure를 사용 하 여 [SQL Server 테이블에 대 한 액세스 테이블을 연결](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4)합니다.  
  
또한이 과정을 안내 하는 마이그레이션 마법사를 사용할 수 있습니다. 자세한 내용은 참조 [마이그레이션 마법사](http://msdn.microsoft.com/en-us/5bab5914-b2ae-4795-8cf5-83e42d64bef2)합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server Migration Assistant for Access 시작](http://msdn.microsoft.com/en-us/462a731f-08f1-44e1-9eeb-4deac6d2f6c5)  
[Access 데이터베이스 마이그레이션을 준비](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  


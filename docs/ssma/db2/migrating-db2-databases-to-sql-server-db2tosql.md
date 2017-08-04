---
title: "SQL Server (DB2ToSQL)로 데이터베이스 마이그레이션 DB2 | Microsoft Docs"
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
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
caps.latest.revision: 4
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: fd66a7b19e359d9b30001e620bca53acd6f6d0ff
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>DB2 데이터베이스 (DB2ToSQL) SQL Server로 마이그레이션
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) for d b 2는 DB2 데이터베이스를 신속 하 게 마이그레이션할 수 있는 포괄적인 환경 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다. SSMA for d b 2를 사용 하 여 있습니다 수 데이터베이스 개체와 데이터를 검토, 평가 마이그레이션할 데이터베이스, 데이터베이스 개체를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB, 다음 데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다. 참고 SYS 및 시스템 DB2 스키마를 마이그레이션할 수 없습니다.  
  
## <a name="recommended-migration-process"></a>권장 되는 마이그레이션 프로세스  
DB2 데이터베이스에서 개체 및 데이터를 성공적으로 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB, 다음 프로세스를 사용 합니다.  
  
1.  [새 SSMA 프로젝트](http://msdn.microsoft.com/en-us/66437b45-4686-4fc7-a91b-ebde45e0f1b0)합니다.  
  
    프로젝트를 만든 후에 프로젝트 변환, 마이그레이션 및 유형 매핑 옵션을 설정할 수 있습니다. 프로젝트 설정에 대 한 정보를 참조 하십시오. [프로젝트 설정 &#40; 변환 &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md) 및 관련 구역을 합니다. 데이터 형식 매핑을 사용자 지정 하는 방법에 대 한 정보를 참조 하십시오. [DB2 매핑 및 SQL Server 데이터 형식 &#40; DB2ToSQL &#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)합니다.  
  
2.  [DB2 데이터베이스에 연결](http://msdn.microsoft.com/en-us/5eb5801d-f0c3-4127-97c0-0b1ef49f4844)합니다.  
  
3.  [SQL Server에 연결](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e)합니다.  
  
4.  [DB2 스키마를 SQL Server 스키마로 매핑](http://msdn.microsoft.com/en-us/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a)합니다.  
  
5.  필요에 따라 [평가 보고서](http://msdn.microsoft.com/en-us/9e13eba0-e3cf-4205-974f-c00f982061de) 변환에 대 한 데이터베이스 개체를 평가 하는 변환 시간 예측 합니다.  
  
6.  [DB2 스키마 변환](http://msdn.microsoft.com/en-us/7947efc3-ca86-4ec5-87ce-7603059c75a0)합니다.  
  
7.  [SQL Server로 변환 된 데이터베이스 개체를 로드](http://msdn.microsoft.com/en-us/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3)합니다.  
  
    다음 방법 중 하나에서이 수행할 수 있습니다.  
  
    -   스크립트를 저장 하 고 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
    -   데이터베이스 개체를 동기화 합니다.  
  
8.  [DB2 데이터를 SQL Server로 마이그레이션](http://msdn.microsoft.com/en-us/86cbd39f-6dac-409a-9ce1-7dd54403f84b)합니다.  
  
9. 필요한 경우 데이터베이스 응용 프로그램을 업데이트 합니다.  
  
## <a name="see-also"></a>참고 항목  
[DB2 &#40; DB2ToSQL &#41; SSMA를 설치합니다.](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[SSMA DB2 &#40; DB2ToSQL &#41;에 대 한 시작](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  


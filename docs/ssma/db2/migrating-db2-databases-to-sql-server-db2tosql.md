---
title: SQL Server (DB2ToSQL)로 데이터베이스 마이그레이션 DB2 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3af1de2e98b4baf4800603a8eb177b80fdb1da6f
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38985505"
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>DB2 데이터베이스 (DB2ToSQL) SQL Server로 마이그레이션
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) for DB2는 DB2 데이터베이스를 신속 하 게 마이그레이션할 수 있도록 포괄적인 환경 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다. SSMA for DB2를 사용 하 여 있습니다 수 데이터베이스 개체 및 데이터를 검토, 평가 마이그레이션에 대 한 데이터베이스, 데이터베이스 개체를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 및 데이터를 마이그레이션하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다. 참고 SYS 및 시스템 DB2 스키마를 마이그레이션할 수 없습니다.  
  
## <a name="recommended-migration-process"></a>권장 되는 마이그레이션 프로세스  
DB2 데이터베이스에서 개체 및 데이터를 성공적으로 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB의 경우 다음 프로세스를 사용 합니다.  
  
1.  [새 SSMA 프로젝트](http://msdn.microsoft.com/66437b45-4686-4fc7-a91b-ebde45e0f1b0)합니다.  
  
    프로젝트를 만든 후에 프로젝트 변환, 마이그레이션 및 유형 매핑 옵션을 설정할 수 있습니다. 프로젝트 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;변환&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md) 및 관련 섹션입니다. 데이터 형식 매핑 사용자 지정 하는 방법에 대 한 정보를 참조 하세요 [매핑 DB2 및 SQL Server 데이터 형식 &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)합니다.  
  
2.  [DB2 데이터베이스에 연결할](http://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844)합니다.  
  
3.  [SQL Server에 연결](http://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e)합니다.  
  
4.  [DB2 스키마를 SQL Server 스키마에 매핑](http://msdn.microsoft.com/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a)합니다.  
  
5.  필요에 따라 [평가 보고서](http://msdn.microsoft.com/9e13eba0-e3cf-4205-974f-c00f982061de) 변환에 대 한 데이터베이스 개체를 평가 하는 변환 시간 예측 합니다.  
  
6.  [DB2 스키마 변환](http://msdn.microsoft.com/7947efc3-ca86-4ec5-87ce-7603059c75a0)합니다.  
  
7.  [SQL Server로 변환 된 데이터베이스 개체를 로드](http://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3)합니다.  
  
    다음 방법 중 하나에서이 수행할 수 있습니다.  
  
    -   스크립트를 저장 하 고 실행할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
    -   데이터베이스 개체를 동기화 합니다.  
  
8.  [DB2 데이터를 SQL Server로 마이그레이션](http://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b)합니다.  
  
9. 필요한 경우 데이터베이스 응용 프로그램을 업데이트 합니다.  
  
## <a name="see-also"></a>관련 항목  
[DB2 용 SSMA 설치 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[DB2 용 SSMA 시작 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  

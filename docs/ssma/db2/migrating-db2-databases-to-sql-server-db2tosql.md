---
title: DB2 데이터베이스를 SQL Server로 마이그레이션 (DB2ToSQL) | Microsoft Docs
description: 이 권장 프로세스를 사용 하 여 DB2 데이터베이스를 SQL Server으로 마이그레이션하거나 SSMA (SQL Server Migration Assistant)를 사용 하 여 Azure SQL Database 합니다.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c66e88ff81cc8f7d06d3d946be8e476b175d1b47
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823684"
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>DB2 데이터베이스를 SQL Server로 마이그레이션 (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]D b 2 용 SSMA (Migration Assistant)는 DB2 데이터베이스를 또는 Azure SQL Database로 신속 하 게 마이그레이션하는 데 도움이 되는 포괄적인 환경입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . D b 2 용 SSMA를 사용 하 여 데이터베이스 개체 및 데이터를 검토 하 고, 마이그레이션을 위해 데이터베이스를 평가 하 고, 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL Database 마이그레이션하고, 데이터를 또는 Azure SQL Database로 마이그레이션할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . SYS 및 SYSTEM DB2 스키마는 마이그레이션할 수 없습니다.  
  
## <a name="recommended-migration-process"></a>권장 마이그레이션 프로세스  
DB2 데이터베이스에서 또는 Azure SQL Database 개체 및 데이터를 성공적으로 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음 프로세스를 사용 합니다.  
  
1.  [새 SSMA 프로젝트](https://msdn.microsoft.com/66437b45-4686-4fc7-a91b-ebde45e0f1b0)입니다.  
  
    프로젝트를 만든 후 프로젝트 변환, 마이그레이션 및 형식 매핑 옵션을 설정할 수 있습니다. 프로젝트 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;변환&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md) 및 관련 섹션을 참조 하세요. 데이터 형식 매핑을 사용자 지정 하는 방법에 대 한 자세한 내용은 [DB2 및 SQL Server 데이터 형식 &#40;DB2ToSQL&#41;매핑 ](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)을 참조 하세요.  
  
2.  [DB2 데이터베이스에 연결](https://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844)합니다.  
  
3.  [SQL Server에 연결 하는 중](https://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e)입니다.  
  
4.  [DB2 스키마를 SQL Server 스키마에 매핑합니다](https://msdn.microsoft.com/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a).  
  
5.  필요에 따라 [평가 보고서](https://msdn.microsoft.com/9e13eba0-e3cf-4205-974f-c00f982061de) 는 변환에 대 한 데이터베이스 개체를 평가 하 고 변환 시간을 추정 합니다.  
  
6.  [DB2 스키마를 변환](https://msdn.microsoft.com/7947efc3-ca86-4ec5-87ce-7603059c75a0)합니다.  
  
7.  [변환 된 데이터베이스 개체를 SQL Server으로 로드](https://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3)합니다.  
  
    다음 방법 중 하나를 수행 하 여이 작업을 수행할 수 있습니다.  
  
    -   스크립트를 저장 하 고에서 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
    -   데이터베이스 개체를 동기화 합니다.  
  
8.  [DB2 데이터를 SQL Server으로 마이그레이션합니다](https://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
9. 필요한 경우 데이터베이스 응용 프로그램을 업데이트 합니다.  
  
## <a name="see-also"></a>참고 항목  
[D b 2 용 SSMA &#40;DB2ToSQL&#41;설치](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[D b 2 용 SSMA &#40;DB2ToSQL&#41;시작](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  

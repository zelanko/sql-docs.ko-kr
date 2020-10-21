---
description: 데이터베이스 파일 이동
title: 데이터베이스 파일 이동 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- files [SQL Server], moving
- data files [SQL Server], moving
- file moving [SQL Server]
- moving full-text catalogs
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- scheduled disk maintenance [SQL Server]
- moving files
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
author: stevestein
ms.author: sstein
ms.openlocfilehash: fa8fe0e721bbe571cf1f47d95bfdd79029059846
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194313"
---
# <a name="move-database-files"></a>데이터베이스 파일 이동
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문의 FILENAME 절에 새 파일 위치를 지정하여 시스템 및 사용자 데이터베이스를 이동할 수 있습니다. 데이터, 로그 및 전체 텍스트 카탈로그 파일도 이런 식으로 이동할 수 있습니다. 이 방법은 다음과 같은 경우 유용합니다.  
  
-   오류 복구. 하드웨어 오류로 인해 데이터베이스가 주의 대상 모드에 있거나 종료된 경우를 예로 들 수 있습니다.  
  
-   계획된 재배치  
  
-   예약된 디스크 유지 관리를 위한 재배치  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[사용자 데이터베이스 이동](../../relational-databases/databases/move-user-databases.md)|사용자 데이터베이스 파일과 전체 텍스트 카탈로그 파일을 새 위치로 이동하는 절차에 대해 설명합니다.|  
|[시스템 데이터베이스 이동](../../relational-databases/databases/move-system-databases.md)|시스템 데이터베이스 파일을 새 위치로 이동하는 절차에 대해 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE &#40;Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)   
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  

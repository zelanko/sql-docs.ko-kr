---
title: 데이터베이스 파일 이동 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 9544d2d2b2c505e3557d9cd0ae348b41bec5e821
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871704"
---
# <a name="move-database-files"></a>데이터베이스 파일 이동
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) 문의 FILENAME 절에 새 파일 위치를 지정하여 시스템 및 사용자 데이터베이스를 이동할 수 있습니다. 데이터, 로그 및 전체 텍스트 카탈로그 파일도 이런 식으로 이동할 수 있습니다. 이 방법은 다음과 같은 경우 유용합니다.  
  
-   오류 복구. 하드웨어 오류로 인해 데이터베이스가 주의 대상 모드에 있거나 종료된 경우를 예로 들 수 있습니다.  
  
-   계획된 재배치  
  
-   예약된 디스크 유지 관리를 위한 재배치  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[사용자 데이터베이스 이동](move-user-databases.md)|사용자 데이터베이스 파일과 전체 텍스트 카탈로그 파일을 새 위치로 이동하는 절차에 대해 설명합니다.|  
|[시스템 데이터베이스 이동](system-databases.md)|시스템 데이터베이스 파일을 새 위치로 이동하는 절차에 대해 설명합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)  
  
  

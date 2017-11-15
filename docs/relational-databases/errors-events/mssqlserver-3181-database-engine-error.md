---
title: "MSSQLSERVER_3181 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 3181 (Database Engine error)
ms.assetid: e6d2e716-5263-477c-ad0e-7bcbfef4c1f3
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 0ca79a39e0a2e8d581fcf1b91157e650df14b7dc
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver3181"></a>MSSQLSERVER_3181
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|3181|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LDDB_STORAGE_VERIFY|  
|메시지 텍스트|이 백업을 복원하려고 하면 저장 공간 문제가 발생할 수 있습니다. 이어서 나타나는 메시지에서 자세한 정보를 제공합니다.|  
  
## <a name="explanation"></a>설명  
RESTORE VERIFYONLY 문은 데이터베이스가 복원될 디스크의 사용 가능한 저장 공간을 검사합니다.  
  
### <a name="possible-causes"></a>가능한 원인  
사용 가능한 디스크 공간이 확인하려는 백업을 복원하기에 부족할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
충분한 디스크 공간이 있는 위치로 백업을 복원하거나 디스크에 더 많은 공간을 제공합니다.  
  
## <a name="see-also"></a>관련 항목:  
[데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[새 위치로 파일 복원&#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE&#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
[RESTORE VERIFYONLY&#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  

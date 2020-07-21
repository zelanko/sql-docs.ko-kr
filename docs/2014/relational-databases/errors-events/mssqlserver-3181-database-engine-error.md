---
title: MSSQLSERVER_3181 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3181 (Database Engine error)
ms.assetid: e6d2e716-5263-477c-ad0e-7bcbfef4c1f3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3aca70f5f13ba81ae240abcc1e63fdf60b31e72d
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551768"
---
# <a name="mssqlserver_3181"></a>MSSQLSERVER_3181
    
## <a name="details"></a>세부 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|3181|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LDDB_STORAGE_VERIFY|  
|메시지 텍스트|이 백업을 복원하려고 하면 스토리지 공간 문제가 발생할 수 있습니다. 이어서 나타나는 메시지에서 자세한 정보를 제공합니다.|  
  
## <a name="explanation"></a>설명  
 RESTORE VERIFYONLY 문은 데이터베이스가 복원될 디스크의 사용 가능한 스토리지 공간을 검사합니다.  
  
### <a name="possible-causes"></a>가능한 원인  
 사용 가능한 디스크 공간이 확인하려는 백업을 복원하기에 부족할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 충분한 디스크 공간이 있는 위치로 백업을 복원하거나 디스크에 더 많은 공간을 제공합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](../backup-restore/restore-a-database-to-a-new-location-sql-server.md)   
 [SQL Server&#41;&#40;새 위치로 파일을 복원 합니다.](../backup-restore/restore-files-to-a-new-location-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)  
  
  

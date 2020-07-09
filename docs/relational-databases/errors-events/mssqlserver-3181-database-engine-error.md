---
title: MSSQLSERVER_3181 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3181 (Database Engine error)
ms.assetid: e6d2e716-5263-477c-ad0e-7bcbfef4c1f3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2201c81cfc4d4f5f31fb3ab107262d0825274858
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723678"
---
# <a name="mssqlserver_3181"></a>MSSQLSERVER_3181
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
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
[데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[새 위치로 파일 복원&#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE&#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
[RESTORE VERIFYONLY&#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  

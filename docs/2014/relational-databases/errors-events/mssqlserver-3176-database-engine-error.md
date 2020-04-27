---
title: MSSQLSERVER_3176 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3176 (Database Engine error)
ms.assetid: 4be24c64-2d52-4cb4-b4d7-36efbe4555b6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a4117013b671ee9c5d5acf1fcde94ab382468dc4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62914481"
---
# <a name="mssqlserver_3176"></a>MSSQLSERVER_3176
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|3176|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LDDB_FILE_CLAIM|  
|메시지 텍스트|'%ls'(%d) 및 '%ls'(%d)에서 파일 '%ls'을(를) 요구했습니다. WITH MOVE 절을 사용하여 하나 이상의 파일 위치를 다시 지정할 수 있습니다.|  
  
## <a name="explanation"></a>설명  
 파일을 두 가지 이상의 용도로 사용하려고 합니다.  
  
### <a name="possible-causes"></a>가능한 원인  
 다른 데이터베이스에서 이미 파일 이름을 사용하고 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 데이터베이스 파일을 다른 위치로 복원합니다. RESTORE 문에서 WITH MOVE 절을 사용하여 각 파일을 이동합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **데이터베이스 복원 옵션** 대화 상자의 **데이터베이스 파일을 다음으로 복원** 표에서 파일 위치를 변경합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server &#40;새 위치로 데이터베이스를 복원&#41;](../backup-restore/restore-a-database-to-a-new-location-sql-server.md)   
 [SQL Server&#41;&#40;새 위치로 파일을 복원 합니다.](../backup-restore/restore-files-to-a-new-location-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  

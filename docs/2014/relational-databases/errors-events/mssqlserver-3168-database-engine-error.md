---
title: MSSQLSERVER_3168 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3168 (Database Engine error)
ms.assetid: 991111d9-1eb3-43e9-9333-a75a775c3200
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5ea24081f4b3a41211f3bd8d6bba52aaec8b74fc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62868745"
---
# <a name="mssqlserver3168"></a>MSSQLSERVER_3168
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|3168|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LDDB_SYSTEMWRONGVER|  
|메시지 텍스트|디바이스 %ls에 있는 시스템 데이터베이스의 백업은 이 서버(%ls)와 다른 버전의 서버(%ls)에서 생성되었으므로 복원할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 백업을 원래 수행한 빌드가 아닌 다른 서버 빌드에서는 시스템 데이터베이스(**master**, **model** 또는 **msdb**)의 백업을 복원할 수 없습니다.  
  
> [!NOTE]  
>  서비스 팩 또는 핫픽스 빌드를 설치하면 서버 빌드 번호가 변경되며 서버 빌드는 항상 증분식입니다.  
  
### <a name="possible-causes"></a>가능한 원인  
 시스템 데이터베이스에 대한 데이터베이스 스키마가 서버 빌드 간에 변경되었을 수 있습니다. 스키마 변경으로 인해 불일치 문제가 발생하지 않도록 RESTORE 문은 백업 파일의 서버 빌드 번호를 백업을 복원하려는 서버의 빌드 번호와 비교합니다. 그 결과 빌드가 다르면 해당 문에서 3168 오류 메시지를 표시하고 복원 작업이 비정상적으로 종료됩니다.  
  
 이 문제가 발생할 수 있는 시나리오는 다음과 같습니다.  
  
-   사용자가 서버 B에서 수행한 백업에서 서버 A의 시스템 데이터베이스를 복원하려고 합니다. 서버 A와 서버 B는 서로 다른 서버 빌드에 있습니다. 예를 들어 서버 A는 원래 릴리스 버전 빌드에 있고 서버 B는 SP1(서비스 팩 1) 빌드에 있을 수 있습니다.  
  
-   사용자가 동일한 서버에서 수행한 백업에서 시스템 데이터베이스를 복원하려고 합니다. 그러나 백업을 수행할 당시에는 서버가 다른 빌드를 실행하고 있었습니다. 즉, 백업을 수행한 이후에 서버가 업그레이드되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
 이 시나리오에는 복원 프로세스가 마지막 수단으로 이미 시도되었습니다. 자세한 내용은 "[You cannot restore system database backups to a different build of SQL Server](https://support.microsoft.com/kb/264474)(시스템 데이터베이스 백업을 SQL Server의 다른 빌드로 복원할 수 없습니다.)"를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
  

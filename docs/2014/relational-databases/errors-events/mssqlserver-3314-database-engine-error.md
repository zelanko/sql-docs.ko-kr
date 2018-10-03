---
title: MSSQLSERVER_3314 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3314 (Database Engine error)
ms.assetid: f3a5ca6a-b502-4cab-b3b1-4bc753763fa9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b8d82911f013c9284a55bd55f00654a98633df0a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48086283"
---
# <a name="mssqlserver3314"></a>MSSQLSERVER_3314
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3314|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|ERR_LOG_RID2|  
|메시지 텍스트|데이터베이스 '%.*ls'에 로그된 작업을 실행 취소하는 중 로그 레코드 %S_LSN에서 오류가 발생했습니다. 일반적으로 특정 오류는 Windows 이벤트 로그 서비스에서 이미 오류로 로깅되어 있습니다. 백업에서 데이터베이스 또는 파일을 복원하거나 데이터베이스를 복구하십시오.|  
  
## <a name="explanation"></a>설명  
 실행 취소 복구에 대한 롤업 오류입니다. 이 오류가 발생하면 데이터베이스가 SUSPECT 상태가 됩니다. 주 파일 그룹(다른 파일 그룹도 해당될 수 있음)이 주의 대상이거나 손상되었을 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작하는 동안에는 데이터베이스를 복구할 수 없으므로 데이터베이스를 사용할 수 없습니다. 문제를 해결하려면 사용자 동작이 필요합니다.  
  
 **tempdb**에 대해 이 오류가 발생하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 종료됩니다.  
  
## <a name="user-action"></a>사용자 동작  
 이 오류는 서버 인스턴스를 시작하거나 데이터베이스를 복구하려는 지정된 시도 중에 시스템에 존재하는 일시적인 상태에 의해 발생할 수 있습니다. 또한 데이터베이스를 시작할 때마다 발생하는 영구적인 오류로 인해 발생할 수도 있습니다. 오류의 원인을 확인하려면 Windows 이벤트 로그에서 구체적인 오류를 나타내는 이전 오류를 조사하십시오.  
  
 3314 오류가 발생한 원인에 대한 자세한 내용을 보려면 Windows 이벤트 로그에서 해당 문제를 가리키는 이전 오류를 조사하십시오. 적절한 사용자 동작은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류가 일시적인 상태에 의해 발생했는지 영구적인 문제에 의해 발생했는지를 나타내는 Windows 이벤트 로그의 정보에 따라 달라집니다. 3314 오류 문제를 해결하기 위한 사용자 동작에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [DBCC CHECKDB&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](../backup-restore/complete-database-restores-simple-recovery-model.md)   
 [MSSQLSERVER_824](mssqlserver-824-database-engine-error.md)   
 [sys.databases&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  

---
title: MSSQLSERVER_3414 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3414 (Database Engine error)
ms.assetid: f25852f9-b91c-4356-b817-78bec9ec8db4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f02dafba3f6fbb8742c8b81ded8fccf39f0509f0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68098319"
---
# <a name="mssqlserver_3414"></a>MSSQLSERVER_3414
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3414|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|REC_GIVEUP|  
|메시지 텍스트|복구하는 동안 오류가 발생하여 데이터베이스 '%.*ls'(데이터베이스 ID %d)을(를) 다시 시작하지 못했습니다. 복구 오류를 진단하여 수정하거나 양호한 백업에서 복원하십시오. 오류를 수정할 수 없거나 예상할 수 없는 경우 기술 지원 서비스에 문의하십시오.|  
  
## <a name="explanation"></a>설명  
지정된 데이터베이스가 복구되었으나 복구 중 오류가 발생하여 시작에 실패했습니다. 이 오류가 발생하면 데이터베이스가 SUSPECT 상태가 됩니다. 주 파일 그룹(다른 파일 그룹도 해당될 수 있음)이 주의 대상이거나 손상되었을 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작하는 동안에는 데이터베이스를 복구할 수 없으므로 데이터베이스를 사용할 수 없습니다. 문제를 해결하려면 사용자 동작이 필요합니다.  
  
**tempdb**에 대해 이 오류가 발생하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 종료됩니다.  
  
## <a name="user-action"></a>사용자 동작  
이 오류는 서버 인스턴스를 시작하거나 데이터베이스를 복구하려는 지정된 시도 중에 시스템에 존재하는 일시적인 상태에 의해 발생할 수 있습니다. 또한 데이터베이스를 시작할 때마다 발생하는 영구적인 오류로 인해 발생할 수도 있습니다. 오류의 원인을 확인하려면 Windows 이벤트 로그에서 구체적인 오류를 나타내는 이전 오류를 조사하십시오.  
  
3414 오류가 발생한 원인에 대한 자세한 내용을 보려면 Windows 이벤트 로그에서 해당 문제를 가리키는 이전 오류를 조사하세요. 적절한 사용자 동작은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류가 일시적인 상태에 의해 발생했는지 영구적인 문제에 의해 발생했는지를 나타내는 Windows 이벤트 로그의 정보에 따라 달라집니다. 3414 오류 문제를 해결하기 위한 사용자 동작에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[ALTER DATABASE&#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[DBCC CHECKDB&#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[전체 데이터베이스 복원&#40;단순 복구 모델&#41;](~/relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
[MSSQLSERVER_824](~/relational-databases/errors-events/mssqlserver-824-database-engine-error.md)  
[sys.databases&#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  

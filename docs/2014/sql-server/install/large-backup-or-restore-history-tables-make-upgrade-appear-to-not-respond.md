---
title: 큰 백업 또는 복원 기록 테이블이 있으면 업그레이드가 응답 하지으로 나타납니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- backup history tables
- history tables
ms.assetid: f88d86ec-324b-4518-b6d7-1af7e7265812
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1b7d3f6c5734f743d83a712cea745c3816bcdbc0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082226"
---
# <a name="large-backup-or-restore-history-tables-make-upgrade-appear-to-not-respond"></a>큰 백업 또는 복원 기록 테이블이 있으면 업그레이드가 응답하지 않는 것으로 나타납니다.
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 경우 일부 백업 및 복원 기록 테이블에 새 열이 추가되었습니다. 이러한 테이블을 업그레이드하려면 새 열을 추가하도록 이러한 테이블을 변경해야 합니다. 이러한 테이블 중 하나 이상에 많은 수의 행이 포함되어 있으면 해당 테이블에 열을 추가하는 ALTER TABLE 문에서 업그레이드가 오랫동안 지체됩니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 다음 백업 또는 복원 기록 테이블에 많은 수의 행이 포함되어 있으면 업그레이드가 중지된 것처럼 보일 수 있습니다.  
  
-   **backupfile**  
  
-   **backupmediafamily**  
  
-   **backupmediaset**  
  
-   **backupset**  
  
-   **restorefile**  
  
-   **restorefilegroup**  
  
-   **restorehistory**  
  
 이러한 테이블 중 10,000개 이상의 행이 포함된 테이블이 있으면 업그레이드 관리자는 규칙 위반 오류를 보고합니다. 이때 업그레이드 관리자는 허용된 행 수를 초과한 테이블을 보고하지는 않습니다. 이러한 오류는 10,000개의 행을 초과하는 행이 처음 발견되는 대로 보고됩니다.  
  
## <a name="corrective-action"></a>수정 동작  
 10,000개의 행을 초과하는 행이 있으면 데이터베이스를 업그레이드하기 전에 행 수를 10,000개 미만으로 줄이는 것이 좋습니다. 이러한 모든 테이블의 행을 줄이기 위해 실행할 수 있습니다는 **sp_delete_backuphistory** 저장 프로시저입니다. 이 프로시저는 모든 백업 및 복원 기록 테이블에서 지정한 날짜보다 오래된 백업 세트의 항목을 삭제합니다. 자세한 내용은 [sp_delete_backuphistory&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql)를 참조하세요.  
  
> [!NOTE]  
>  백업 및 복원 기록 테이블에 10,000개 이상의 행이 있는 데이터베이스를 업그레이드할 수 있습니다. 그러나 큰 테이블이 변경되는 동안에는 업그레이드가 중지된 것처럼 보일 수 있습니다. 테이블이 클수록 업그레이드를 완료하는 데 걸리는 시간도 길어집니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  

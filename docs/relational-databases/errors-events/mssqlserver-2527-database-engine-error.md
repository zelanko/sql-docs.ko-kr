---
title: "MSSQLSERVER_2527 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2527 (Database Engine error)
ms.assetid: 1cef90ef-9c39-44e6-bc7f-316c8f53c10c
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 14f0f361ec4eefc2d1e232efaf7c899c0151d1f8
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver2527"></a>MSSQLSERVER_2527
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2527|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_INDEX_FILEGROUP_IS_OFFLINE|  
|메시지 텍스트|파일 그룹 F_NAME이(가) 오프라인 상태이므로 테이블 O_NAME의 인덱스 I_NAME을(를) 처리할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
이 정보 메시지는 인덱스에 대한 데이터를 저장하는 파일 그룹 중 하나가 오프라인 상태이므로 인덱스를 검사할 수 없음을 나타냅니다. 파일 그룹의 파일 상태에 따라 전체 파일 그룹의 사용 가능 여부가 결정됩니다. 파일 그룹을 사용하려면 파일 그룹 내의 모든 파일이 온라인 상태여야 합니다. 다른 문제가 없으면 같은 개체에 대한 다른 인덱스를 모두 검사합니다.  
  
## <a name="user-action"></a>사용자 동작  
지정된 파일 그룹의 파일 상태를 보려면 **sys.database_files** 또는 **sys.master_files** 카탈로그 뷰 중 하나를 쿼리하세요.  
  
백업에서 오프라인 파일을 복원하십시오.  
  
## <a name="see-also"></a>참고 항목  
[sys.database_files&#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[sys.master_files&#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
[RESTORE&#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  


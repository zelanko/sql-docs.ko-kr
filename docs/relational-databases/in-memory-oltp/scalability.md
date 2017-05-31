---
title: "확장성 | Microsoft 문서"
ms.custom: 
ms.date: 08/27/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a4891c57-56bb-49f4-9bb5-f11b745279e5
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5ab43ba6b6a27fa46b5214a60063c5df3f5496f4
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="scalability"></a>확장성
  SQL Server 2016에서는 메모리 액세스에 최적화된 테이블용 디스크의 저장소 확장성이 향상되었습니다.  
  
-   **여러 스레드에 메모리 액세스에 최적화된 테이블 유지**  
  
     이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]릴리스에서는 단일 오프라인 검사점 스레드가 트랜잭션 로그에서 메모리 액세스에 최적화된 테이블 변경 내용을 검사하여 데이터 및 델타 파일과 같은 검사점 파일에 이러한 변경 내용을 유지했습니다. 그러나 코어 수가 많으면 오프라인 검사점 스레드 하나로는 변경 내용을 검사하여 빠르게 유지할 수가 없었습니다.  
  
     [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서는 여러 동시 스레드가 메모리 액세스에 최적화된 테이블의 변경 내용을 유지합니다.  
  
-   **다중 스레드 복구**  
  
     이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]릴리스에서는 복구 작업의 일부분으로 수행되는 로그 적용이 단일 스레드에서 진행되었습니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서는 로그 적용이 다중 스레드로 수행됩니다.  
  
-   **병합 작업**  
  
     이제 병합 작업이 다중 스레드로 수행됩니다.  
  
-   **동적 관리 뷰**  
  
     [sys.dm_db_xtp_checkpoint_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-stats-transact-sql.md) 및 [sys.dm_db_xtp_checkpoint_files&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)가 크게 변경되었습니다.  
  
 다중 스레드 병합을 통해 로드를 처리할 수 있으므로 수동 병합은 사용하지 않도록 설정되었습니다.  
  
 메모리 내 OLTP 엔진은 계속해서 FILESTREAM을 기반으로 하여 메모리 액세스에 최적화된 파일 그룹을 사용하지만, 파일 그룹의 개별 파일은 FILESTREAM에서 분리됩니다. 메모리 내 OLTP 엔진을 통해 파일 만들기, 삭제, 가비지 수집 등 이러한 파일에 대한 작업을 완전하게 관리할 수 있습니다. [DBCC SHRINKFILE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)은 지원되지 않습니다.  
  
  


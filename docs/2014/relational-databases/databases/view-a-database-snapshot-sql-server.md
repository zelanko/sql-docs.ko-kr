---
title: 데이터베이스 스냅샷 보기(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], viewing
- displaying database snapshots
- viewing database snapshots
ms.assetid: 123f19b2-0850-4033-8507-59ebdfb368ee
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1b8648b9166ffa192ca21233ab6add38260a7dea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62871190"
---
# <a name="view-a-database-snapshot-sql-server"></a>데이터베이스 스냅샷 보기(SQL Server)
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]데이터베이스 스냅샷을 표시하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  데이터베이스 스냅샷을 만들거나, 되돌리거나, 삭제하려면 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용해야 합니다.  
  
 **항목 내용**  
  
-   **데이터베이스 스냅샷을 보려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **데이터베이스 스냅샷을 보려면**  
  
1.  개체 탐색기에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장합니다.  
  
3.  **데이터베이스 스냅샷**을 확장한 후 표시할 스냅샷을 선택합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **데이터베이스 스냅샷을 보려면**  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 데이터베이스 스냅샷을 나열하려면 NULL이 아닌 값에 대해 **sys.databases** 카탈로그 뷰의 [source_database_id](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 열을 쿼리합니다.  
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
-   [데이터베이스 스냅샷 만들기&#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md)  
  
-   [데이터베이스를 데이터베이스 스냅샷으로 되돌리기](revert-a-database-to-a-database-snapshot.md)  
  
-   [데이터베이스 스냅샷 삭제&#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 스냅샷&#40;SQL Server&#41;](database-snapshots-sql-server.md)  
  
  

---
title: SQL Server 인스턴스에서 데이터베이스의 목록 보기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- current databases
- databases currently on server [SQL Server]
- database list [SQL Server]
- viewing database list
- displaying database list
- databases [SQL Server], viewing
- servers [SQL Server], databases listed on
- listing databases
ms.assetid: 7ee7a789-db36-4be9-8a0e-0362a1e152dd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cdce1c0fc6f36bb0d58e93abba29ecab9d2dcd54
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526345"
---
# <a name="view-a-list-of-databases-on-an-instance-of-sql-server"></a>SQL Server 인스턴스에서 데이터베이스의 목록 보기
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]인스턴스에서 데이터베이스 목록을 보는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **SQL Server 인스턴스에서 데이터베이스의 목록을 보려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 **sys.databases** 의 호출자가 데이터베이스의 소유자가 아니고 데이터베이스가 **master** 또는 **tempdb**가 아닐 경우 해당 행을 보려면 최소한 서버 수준의 ALTER ANY DATABASE 또는 VIEW ANY DATABASE 권한이 있거나 **master** 데이터베이스에서 CREATE DATABASE 권한이 있어야 합니다. 호출자가 연결된 데이터베이스는 항상 **sys.databases**에서 볼 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-a-list-of-databases-on-an-instance-of-sql-server"></a>SQL Server 인스턴스에서 데이터베이스의 목록을 보려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  인스턴스에 있는 모든 데이터베이스 목록을 확인하려면 **데이터베이스**를 확장합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-a-list-of-databases-on-an-instance-of-sql-server"></a>SQL Server 인스턴스에서 데이터베이스의 목록을 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 데이터베이스 목록을 반환합니다. 목록에는 데이터베이스 이름, 데이터베이스 ID 및 데이터베이스를 만든 날짜가 포함됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT name, database_id, create_date  
FROM sys.databases ;  
GO  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 및 파일 카탈로그 뷰&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql)   
 [sys.databases&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  

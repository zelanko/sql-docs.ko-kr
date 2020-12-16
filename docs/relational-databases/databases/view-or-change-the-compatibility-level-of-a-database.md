---
title: 데이터베이스의 호환성 수준 보기 또는 변경 | Microsoft 문서
description: SQL Server Management Studio 또는 Transact-SQL을 사용하여 SQL Server에서 데이터베이스의 호환성 수준을 보거나 변경하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 11/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- compatibility levels [SQL Server], viewing
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], changing
ms.assetid: 579867ec-57cb-4cb8-af35-9688c1e9e15d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8b513694dacf477f0fde5d90ee9be6952158aa63
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481424"
---
# <a name="view-or-change-the-compatibility-level-of-a-database"></a>데이터베이스의 호환성 수준 보기 또는 변경
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]데이터베이스의 호환성 수준을 보거나 변경하는 방법에 대해 설명합니다. 데이터베이스의 호환성 수준을 변경하기 전에 변경 사항이 애플리케이션에 미치는 영향에 대해 이해하고 있어야 합니다. 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **데이터베이스의 호환성 수준을 보거나 변경하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-or-change-the-compatibility-level-of-a-database"></a>데이터베이스의 호환성 수준을 보거나 변경하려면  
  
1.  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭합니다.  
  
2.  **데이터베이스** 를 확장하고 해당 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성** 을 클릭합니다.  
  
     **데이터베이스 속성** 대화 상자가 열립니다.  
  
4.  **페이지 선택** 창에서 **옵션** 을 클릭합니다.  
  
     현재 호환성 수준이 **호환성 수준** 목록 상자에 표시됩니다.  
  
5.  호환성 수준을 변경하려면 목록에서 다른 옵션을 선택합니다. 다른 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 버전에 사용할 수 있는 옵션은 [ALTER DATABASE 호환성 수준(Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#supported-dbcompats) 페이지에 나열되어 있습니다.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-the-compatibility-level-of-a-database"></a>데이터베이스의 호환성 수준을 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 호환성 수준을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT compatibility_level  
FROM sys.databases WHERE name = 'AdventureWorks2012';  
GO  
```  
  
#### <a name="to-change-the-compatibility-level-of-a-database"></a>데이터베이스의 호환성 수준을 변경하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 호환성 수준을 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]의 호환성 수준인 `120`으로 변경합니다.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET COMPATIBILITY_LEVEL = 120;  
GO  
```  
  
## <a name="see-also"></a>참고 항목
 [ALTER DATABASE &#40;Transact-SQL&#41; 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)

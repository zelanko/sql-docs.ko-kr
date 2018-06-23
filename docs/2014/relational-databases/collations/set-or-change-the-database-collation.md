---
title: 데이터베이스 데이터 정렬 설정 또는 변경 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
caps.latest.revision: 34
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 769adcde56f3e77cee0a2458b1d32b9e763792f7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186093"
---
# <a name="set-or-change-the-database-collation"></a>데이터베이스 데이터 정렬 설정 또는 변경
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 데이터베이스 데이터 정렬을 설정하고 변경하는 방법에 대해 설명합니다. 데이터 정렬을 지정하지 않으면 서버 데이터 정렬이 사용됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **데이터베이스 데이터 정렬을 설정하거나 변경하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   Windows 유니코드 전용 데이터 정렬은 COLLATE 절에서 열 수준 및 식 수준 데이터의 `nchar`, `nvarchar` 및 `ntext` 데이터 형식에 데이터 정렬을 적용하기 위해서만 사용할 수 있고 COLLATE 절에서 데이터베이스 또는 서버 인스턴스의 데이터 정렬을 변경하기 위해 사용할 수는 없습니다.  
  
-   지정된 데이터 정렬 또는 참조된 개체가 사용하는 데이터 정렬에서 Windows가 지원하지 않는 코드 페이지를 사용하는 경우에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 오류가 나타납니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   지원되는 데이터 정렬 이름은 [Windows 데이터 정렬 이름&#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql) 및 [SQL Server 데이터 정렬 이름&#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)에서 확인할 수 있거나 [sys.fn_helpcollations&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql) 시스템 함수를 사용할 수 있습니다.  
  
-   데이터베이스 데이터 정렬을 변경하면 다음 사항이 변경됩니다.  
  
    -   시스템 테이블의 `char`, `varchar`, `text`, `nchar`, `nvarchar` 또는 `ntext` 열이 새 데이터 정렬로 변경됩니다.  
  
    -   저장 프로시저 및 사용자 정의 함수에 대한 모든 기존 `char`, `varchar`, `text`, `nchar`, `nvarchar` 또는 `ntext` 매개 변수와 스칼라 반환 값이 새 데이터 정렬로 변경됩니다.  
  
    -   `char`, `varchar`, `text`, `nchar`, `nvarchar`, 또는 `ntext` 시스템 데이터 형식 및 이러한 시스템 데이터 형식을 기반으로 하는 모든 사용자 정의 데이터 형식이 새 기본 데이터 정렬으로 변경 됩니다.  
  
-   사용자 데이터베이스에서 새로 만든 새 개체의 데이터 정렬은 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) 문의 COLLATE 절을 사용하여 변경할 수 있습니다. 이 문은 기존 사용자 정의 테이블에 있는 열의 데이터 정렬은 변경하지 않습니다. 이러한 열은 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql)문의 COLLATE 절을 사용하여 변경할 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 CREATE DATABASE  
 **master** 데이터베이스의 CREATE DATABASE 권한이 있거나 CREATE ANY DATABASE 또는 ALTER ANY DATABASE 권한이 있어야 합니다.  
  
 ALTER DATABASE  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-set-or-change-the-database-collation"></a>데이터베이스 데이터 정렬을 설정하거나 변경하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결하고 해당 인스턴스를 확장한 다음 **데이터베이스**를 확장합니다.  
  
2.  새 데이터베이스를 만들려는 경우 **데이터베이스** 를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터베이스**를 클릭합니다. 기본 데이터 정렬을 원하지 않는 경우 **옵션** 페이지를 클릭하고 **데이터 정렬** 드롭다운 목록에서 데이터 정렬을 선택합니다.  
  
     또는 데이터베이스가 이미 있는 경우 원하는 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. **옵션** 페이지를 클릭하고 **데이터 정렬** 드롭다운 목록에서 데이터 정렬을 선택합니다.  
  
3.  작업이 완료되면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-set-the-database-collation"></a>데이터베이스 데이터 정렬을 설정하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [COLLATE](/sql/t-sql/statements/collations) 절을 사용하여 데이터 정렬 이름을 지정하는 방법을 보여 줍니다. 이 예에서는 `MyOptionsTest` 데이터 정렬을 사용하는 `Latin1_General_100_CS_AS_SC` 데이터베이스를 만듭니다. 데이터베이스를 만든 후 `SELECT` 문을 실행하여 설정을 확인합니다.  
  
```tsql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE Latin1_General_100_CS_AS_SC;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
#### <a name="to-change-the-database-collation"></a>데이터베이스 데이터 정렬을 변경하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [ALTER DATABASE](/sql/t-sql/statements/collations) 문에 [COLLATE](/sql/t-sql/statements/alter-database-transact-sql) 절을 사용하여 데이터 정렬 이름을 변경하는 방법을 보여 줍니다. `SELECT` 문을 실행하여 변경 내용을 확인합니다.  
  
```tsql  
USE master;  
GO  
ALTER DATABASE MyOptionsTest  
COLLATE French_CI_AS ;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터 정렬 및 유니코드 지원](collation-and-unicode-support.md)   
 [sys.fn_helpcollations&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql)   
 [sys.databases&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [SQL Server 데이터 정렬 이름&#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)   
 [Windows 데이터 정렬 이름&#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql)   
 [COLLATE&#40;Transact-SQL&#41;](/sql/t-sql/statements/collations)   
 [데이터 정렬 선행 규칙&#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql)   
 [CREATE TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  

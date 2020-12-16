---
description: 데이터베이스 데이터 정렬 설정 또는 변경
title: 데이터베이스 데이터 정렬 설정 또는 변경 | Microsoft 문서
ms.custom: ''
ms.date: 10/27/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7fbaf22758dcf62d2159e63ee3af3c0507f3f607
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460576"
---
# <a name="set-or-change-the-database-collation"></a>데이터베이스 데이터 정렬 설정 또는 변경
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 데이터베이스 데이터 정렬을 설정하고 변경하는 방법에 대해 설명합니다. 데이터 정렬을 지정하지 않으면 서버 데이터 정렬이 사용됩니다.  
  
> [!IMPORTANT]
> `ALTER DATABASE COLLATE`Azure SQL Database의 문은 지원되지 않습니다.

 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **데이터베이스 데이터 정렬을 설정하거나 변경하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   Windows 유니코드 전용 데이터 정렬은 COLLATE 절에서 열 수준 및 식 수준 데이터의 **nchar**, **nvarchar** 및 **ntext** 데이터 형식에 데이터 정렬을 적용하기 위해서만 사용할 수 있고 COLLATE 절에서 데이터베이스 또는 서버 인스턴스의 데이터 정렬을 변경하기 위해 사용할 수는 없습니다.  
  
-   지정된 데이터 정렬 또는 참조된 개체가 사용하는 데이터 정렬에서 Windows가 지원하지 않는 코드 페이지를 사용하는 경우에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 오류가 나타납니다.  

###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
지원되는 데이터 정렬 이름은 [Windows 데이터 정렬 이름&#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) 및 [SQL Server 데이터 정렬 이름&#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)에서 확인할 수 있거나 [sys.fn_helpcollations&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) 시스템 함수를 사용할 수 있습니다.  
  
데이터베이스 데이터 정렬을 변경하면 다음 사항이 변경됩니다.  
  
-   시스템 테이블의 **char**, **varchar**, **text**, **nchar**, **nvarchar** 또는 **ntext** 열이 새 데이터 정렬로 변경됩니다.  
  
-   저장 프로시저 및 사용자 정의 함수에 대한 모든 기존 **char**, **varchar**, **text**, **nchar**, **nvarchar** 또는 **ntext** 매개 변수와 스칼라 반환 값이 새 데이터 정렬로 변경됩니다.  
  
-   **char**, **varchar**, **text**, **nchar**, **nvarchar** 또는 **ntext** 시스템 데이터 형식 및 이러한 시스템 데이터 형식을 기반으로 하는 모든 사용자 정의 데이터 형식이 새 기본 데이터 정렬로 변경됩니다.  
  
사용자 데이터베이스에서 새로 만든 새 개체의 데이터 정렬은 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문의 `COLLATE` 절을 사용하여 변경할 수 있습니다. 이 문은 기존 사용자 정의 테이블에 있는 열의 데이터 정렬은 **변경하지 않습니다**. 이러한 열은 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)의 `COLLATE` 절을 사용하여 변경할 수 있습니다.  

> [!IMPORTANT]
> 데이터베이스의 데이터 정렬 또는 개별 열을 변경해도 기존 테이블에 이미 저장된 기본 데이터는 **수정되지 않습니다**. 애플리케이션에서 서로 다른 데이터 정렬 간의 데이터 변환과 비교를 명시적으로 처리하지 않는 한, 데이터베이스의 기존 데이터를 새 데이터 정렬로 전환하는 것이 좋습니다. 이렇게 하면 애플리케이션이 데이터를 잘못 수정하여 잘못된 결과 또는 자동 데이터 손실이 발생할 수 있는 위험이 해소됩니다.   

데이터베이스 데이터 정렬이 변경되면 기본적으로 새 테이블만 새 데이터베이스 데이터 정렬을 상속합니다. 기존 데이터를 새 데이터 정렬로 변환하기 위한 몇 가지 대안이 있습니다.
-  현재 위치에서 데이터를 변환합니다. 기존 테이블에서 열에 대한 데이터 정렬을 변환하려면 [열 데이터 정렬 설정 또는 변경](../../relational-databases/collations/set-or-change-the-column-collation.md)을 참조하세요. 이 작업은 구현하기는 쉽지만, 큰 테이블 및 사용 중인 애플리케이션의 차단 문제로 이어질 수 있습니다. `MyString` 열을 새 데이터 정렬로 현재 위치에서 변환하려면 다음 예제를 참조하세요.

   ```sql
   ALTER TABLE dbo.MyTable
   ALTER COLUMN MyString VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8;
   ```

-  새 데이터 정렬을 사용하는 새 테이블에 데이터를 복사하고 동일한 데이터베이스에서 원래 테이블을 바꿉니다. 현재 데이터베이스에 데이터베이스 데이터 정렬을 상속하는 새 테이블을 만들고, 이전 테이블과 새 테이블 간에 데이터를 복사하고, 원래 테이블을 삭제하고, 새 테이블의 이름을 원래 테이블의 이름으로 바꿉니다. 이는 현재 위치에서 변환보다 더 빠른 작업이지만 외래 키 제약 조건, 기본 키 제약 조건 및 트리거와 같은 종속성이 있는 복잡한 스키마를 처리할 때 문제가 될 수 있습니다. 또한 애플리케이션에서 데이터를 계속 변경하는 경우 최종 컷오프 전에 원래 테이블과 새 테이블 간에 최종 데이터 동기화가 필요합니다. “복사하여 바꾸기” 변환으로 `MyString` 열을 새 데이터 정렬로 변환하는 방법은 다음 예를 참조하세요.

   ```sql
   CREATE TABLE dbo.MyTable2 (MyString VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8); 
   
   INSERT INTO dbo.MyTable2 
   SELECT * FROM dbo.MyTable; 
   
   DROP TABLE dbo.MyTable; 
   
   EXEC sp_rename 'dbo.MyTable2', 'dbo.MyTable’;
   ```

-  새 데이터 정렬을 사용하는 새 데이터베이스에 데이터를 복사하고 원래 데이터베이스를 바꿉니다. 새 데이터 정렬을 사용하여 새 데이터베이스를 만들고, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 가져오기/내보내기 마법사와 같은 도구를 통해 원래 데이터베이스에서 데이터를 전송합니다. 이는 복잡한 스키마에 대한 간단한 접근 방법입니다. 또한 애플리케이션에서 데이터를 계속 변경하는 경우 최종 컷오프 전에 원래 데이터베이스와 새 데이터베이스 간에 최종 데이터 동기화가 필요합니다.
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 새 데이터베이스를 만들려면 **마스터** 데이터베이스에서 `CREATE DATABASE` 권한이 필요하거나, `CREATE ANY DATABASE` 또는 `ALTER ANY DATABASE` 권한이 필요합니다.  
  
 기존 데이터베이스의 데이터 정렬을 변경하려면 데이터베이스에 대한 `ALTER` 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-set-or-change-the-database-collation"></a>데이터베이스 데이터 정렬을 설정하거나 변경하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결하고 해당 인스턴스를 확장한 다음 **데이터베이스** 를 확장합니다.  
  
2.  새 데이터베이스를 만들려는 경우 **데이터베이스** 를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터베이스** 를 클릭합니다. 기본 데이터 정렬을 원하지 않는 경우 **옵션** 페이지를 클릭하고 **데이터 정렬** 드롭다운 목록에서 데이터 정렬을 선택합니다.  
  
     또는 데이터베이스가 이미 있는 경우 원하는 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **속성** 을 클릭합니다. **옵션** 페이지를 클릭하고 **데이터 정렬** 드롭다운 목록에서 데이터 정렬을 선택합니다.  
  
3.  작업이 완료되면 **확인** 을 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-set-the-database-collation"></a>데이터베이스 데이터 정렬을 설정하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 이 예에서는 [COLLATE](~/t-sql/statements/collations.md) 절을 사용하여 데이터 정렬 이름을 지정하는 방법을 보여 줍니다. 이 예에서는 `MyOptionsTest` 데이터 정렬을 사용하는 `Latin1_General_100_CS_AS_SC` 데이터베이스를 만듭니다. 데이터베이스를 만든 후 `SELECT` 문을 실행하여 설정을 확인합니다.  
  
```sql  
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
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 이 예에서는 [ALTER DATABASE](~/t-sql/statements/collations.md) 문에 [COLLATE](../../t-sql/statements/alter-database-transact-sql.md) 절을 사용하여 데이터 정렬 이름을 변경하는 방법을 보여 줍니다. `SELECT` 문을 실행하여 변경 내용을 확인합니다.  
  
```sql  
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
  
## <a name="see-also"></a>참고 항목  
 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)   
 [sys.fn_helpcollations&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [SQL Server 데이터 정렬 이름&#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)   
 [Windows 데이터 정렬 이름&#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)   
 [COLLATE&#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [데이터 정렬 선행 규칙&#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  

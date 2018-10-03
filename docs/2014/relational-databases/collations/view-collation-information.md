---
title: 데이터 정렬 정보 보기 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], view
ms.assetid: 1338b4ea-7142-44bc-a3b9-44e54431405f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 692d64caad7d09f398d92a1cd41eb0b86111e115
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48138421"
---
# <a name="view-collation-information"></a>데이터 정렬 정보 보기
    
##  <a name="Top"></a> 개체 탐색기 메뉴 옵션을 사용하거나 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 서버, 데이터베이스 또는 열의 데이터 정렬을 볼 수 있습니다.  
  
##  <a name="Procedures"></a> 데이터 정렬 설정을 보는 방법  
 다음 중 하나를 사용할 수 있습니다.  
  
-   다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **개체 탐색기에서 서버(SQL Server의 인스턴스)에 대한 데이터 정렬 설정을 보려면**  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  인스턴스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
 **개체 탐색기에서 데이터베이스에 대한 데이터 정렬 설정을 보려면**  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
 **개체 탐색기에서 열에 대한 데이터 정렬 설정을 보려면**  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 데이터베이스를 확장한 다음 **테이블**을 확장합니다.  
  
3.  열이 포함된 테이블을 확장한 다음 **열**을 확장합니다.  
  
4.  열을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. 데이터 정렬 속성이 비어 있는 경우 열은 문자 데이터 유형이 아닙니다.  
  
###  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **서버의 데이터 정렬 설정을 보려면**  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결하고 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
2.  쿼리 창에서 SERVERPROPERTY 시스템 함수를 사용하는 다음 문을 입력합니다.  
  
    ```  
    SELECT CONVERT (varchar, SERVERPROPERTY('collation'));  
    ```  
  
3.  또는 sp_helpsort 시스템 저장 프로시저를 사용할 수 있습니다.  
  
    ```  
    EXECUTE sp_helpsort;  
    ```  
  
 **지원되는 모든 데이터 정렬을 보려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결하고 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
2.  쿼리 창에서 SERVERPROPERTY 시스템 함수를 사용하는 다음 문을 입력합니다.  
  
    ```  
    SELECT name, description FROM sys.fn_helpcollations();  
    ```  
  
 **데이터베이스의 데이터 정렬 설정을 보려면**  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결하고 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
2.  쿼리 창에서 sys.databases 시스템 카탈로그 뷰를 사용하는 다음 문을 입력합니다.  
  
    ```  
    SELECT name, collation_name FROM sys.databases;  
    ```  
  
3.  또는 DATABASEPROPERTYEX 시스템 함수를 사용할 수 있습니다.  
  
    ```  
    SELECT CONVERT (varchar, DATABASEPROPERTYEX('database_name','collation'));  
    ```  
  
 **열의 데이터 정렬 설정을 보려면**  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결하고 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
2.  쿼리 창에서 sys.columns 시스템 카탈로그 뷰를 사용하는 다음 문을 입력합니다.  
  
    ```  
    SELECT name, collation_name FROM sys.columns WHERE name = N'<insert character data type column name>';  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [SERVERPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)   
 [sys.fn_helpcollations&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql)   
 [sys.databases&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [sys.columns&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-columns-transact-sql)   
 [데이터 정렬 선행 규칙&#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql)   
 [sp_helpsort&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsort-transact-sql)  
  
  

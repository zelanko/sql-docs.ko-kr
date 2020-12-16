---
title: 저장 프로시저 삭제 | Microsoft 문서
description: SQL Server Management Studio 또는 Transact-SQL을 사용하여 SQL Server 2019(15.x)에서 저장 프로시저를 삭제하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- removing stored procedures
- stored procedures [SQL Server], deleting
- deleting stored procedures
ms.assetid: 232dbf4d-392a-406f-af3a-579518cd8e46
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 742b0e7f3631f5cf262ff6e20bdc64f1ba7bea7f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475314"
---
# <a name="delete-a-stored-procedure"></a>저장 프로시저 삭제
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
    
##  <a name="this-topic-describes-how-to-delete-a-stored-procedure-in-sscurrent-by-using-ssmanstudiofull-or-tsql"></a><a name="Top"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에 저장된 프로시저를 삭제하는 방법에 대해 설명합니다.  
  
-   **시작하기 전 주의 사항:**  [제한 사항](#Restrictions), [보안](#Security)  
  
-   **프로시저를 삭제하려면 다음을 사용합니다.**   [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
 프로시저를 삭제할 때 개체와 스크립트에 프로시저의 삭제가 적용되도록 업데이트하지 않으면 종속 개체와 스크립트가 실패할 수 있습니다. 그러나 동일한 이름 및 매개 변수의 프로시저가 삭제된 프로시저를 대체하기 위해 생성된 경우 참조하는 다른 개체는 올바르게 처리됩니다. 자세한 내용은 [저장 프로시저의 종속성 보기](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)를 참조하세요.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 프로시저가 속한 스키마에 대한 ALTER 권한 또는 프로시저에 대한 CONTROL 권한이 필요합니다.  
  
##  <a name="how-to-delete-a-stored-procedure"></a><a name="Procedures"></a> 저장 프로시저를 삭제하려면  
 다음 중 하나를 사용할 수 있습니다.  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **개체 탐색기에서 프로시저를 삭제하려면**  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스** 를 확장하고 해당 프로시저가 속한 데이터베이스를 확장한 다음 **프로그래밍 기능** 을 확장합니다.  
  
3.  **저장 프로시저** 를 확장하고 제거할 프로시저를 마우스 오른쪽 단추로 클릭한 다음 **삭제** 를 클릭합니다.  
  
4.  프로시저에 종속된 개체를 보려면 **종속성 표시** 를 클릭합니다.  
  
5.  올바른 프로시저가 선택되었는지 확인하고 **확인** 을 클릭합니다.  
  
6.  모든 종속 개체와 스크립트에서 참조 프로시저를 제거합니다.  

###  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 **쿼리 편집기에서 프로시저를 제거하려면**  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스** 를 확장하고 프로시저가 속한 데이터베이스를 확장하거나 도구 모음의 사용 가능한 데이터베이스 목록에서 데이터베이스를 선택합니다.  
  
3.  파일 메뉴에서 **새 쿼리** 를 클릭합니다.  
  
4.  현재 데이터베이스의 저장 프로시저 이름을 확인합니다. 개체 탐색기에서 **프로그래밍 기능** 을 확장한 다음 **저장 프로시저** 를 확장합니다. 또는 쿼리 편집기에서 다음 문을 실행합니다.  
  
    ```sql  
    SELECT name AS procedure_name   
        ,SCHEMA_NAME(schema_id) AS schema_name  
        ,type_desc  
        ,create_date  
        ,modify_date  
    FROM sys.procedures;  
    ```  
  
5.  다음 예제를 쿼리 편집기에 복사하여 붙여 넣고 저장 프로시저 이름을 입력하여 현재 데이터베이스에서 삭제합니다.  
  
    ```sql  
    DROP PROCEDURE <stored procedure name>;  
    GO  
    ```  
  
6.  모든 종속 개체와 스크립트에서 참조 프로시저를 제거합니다.  
  
## <a name="see-also"></a>참고 항목  
 [저장 프로시저 만들기](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [저장 프로시저 수정](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [저장 프로시저 이름 바꾸기](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [저장 프로시저의 정의 보기](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [저장 프로시저의 종속성 보기](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)   
 [DROP PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
  

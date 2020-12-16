---
description: 사용자 정의 함수 이름 바꾸기
title: 사용자 정의 함수 이름 바꾸기 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: c2695a5c-9cc5-4b18-8771-53027ca9a9af
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9031e0a1122ab1ee2158658ed9e9594381a44127
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466694"
---
# <a name="rename-user-defined-functions"></a>사용자 정의 함수 이름 바꾸기
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 사용자 정의 함수의 이름을 바꿀 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 사용자 정의 함수의 이름을 바꾸려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   함수 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 준수해야 합니다.  
  
-   사용자 정의 함수의 이름을 변경해도 **sys.sql_modules** 카탈로그 뷰의 정의 열에 있는 해당 개체 이름은 변경되지 않습니다. 따라서 이 개체 유형의 이름을 바꾸지 않는 것이 좋습니다. 대신 저장 프로시저를 삭제하고 새로운 이름으로 다시 만듭니다.  
  
-   사용자 정의 함수의 이름 또는 정의를 변경할 때 개체에 해당 함수의 변경 내용이 적용되도록 업데이트하지 않으면 종속 개체가 실패할 수 있습니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 함수를 삭제하려면 해당 함수가 속한 스키마에 대한 ALTER 권한이나 해당 함수에 대한 CONTROL 권한이 있어야 합니다. 함수를 다시 만들려면 데이터베이스에 대한 CREATE FUNCTION 권한과 함수가 생성되는 스키마에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-rename-user-defined-functions"></a>사용자 정의 함수의 이름을 바꾸려면  
  
1.  **개체 탐색기** 에서 이름을 바꿀 함수가 포함된 데이터베이스 옆의 더하기 기호를 클릭한 다음  
  
2.  **프로그래밍 기능** 폴더 옆의 더하기 기호를 클릭합니다.  
  
3.  이름을 바꿀 함수가 포함된 폴더 옆의 더하기 기호를 클릭합니다.  
  
    -   테이블 반환 함수  
  
    -   스칼라 반환 함수  
  
    -   Aggregate 함수  
  
4.  이름을 바꿀 함수를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기** 를 선택합니다.  
  
5.  함수의 새 이름을 입력합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 **사용자 정의 함수의 이름을 바꾸려면**  
  
 이 작업은 Transact-SQL 문을 사용하여 수행할 수 없습니다. Transact-SQL을 사용하여 사용자 정의 함수의 이름을 바꾸려면 먼저 기존 함수를 삭제하고 새로운 이름을 사용하여 다시 만들어야 합니다. 함수의 이전 이름을 사용하는 모든 코드 및 애플리케이션이 이제 새 이름을 사용하는지 확인합니다.  
  
 자세한 내용은 [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md) 및 [DROP FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [사용자 정의 함수 보기](../../relational-databases/user-defined-functions/view-user-defined-functions.md)  
  
  

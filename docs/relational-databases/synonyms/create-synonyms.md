---
description: 동의어 만들기
title: 동의어 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- sql13.swb.synonym.general.f1
helpviewer_keywords:
- creating synonyms
- synonyms [SQL Server], creating
ms.assetid: fedfa7a5-d0b6-4e2b-90f4-a08122958e33
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f5c4d25ed48715c9317ebe0df37ee4d2779abe10
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551602"
---
# <a name="create-synonyms"></a>동의어 만들기
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 동의어를 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 동의어 만들기**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
 지정된 스키마에서 동의어를 만들려면 사용자에게 CREATE SYNONYM 권한이 있어야 하며 스키마를 소유하거나 ALTER SCHEMA 권한이 있어야 합니다. CREATE SYNONYM 권한은 부여할 수 있는 권한입니다.  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-synonym"></a>동의어를 만들려면  
  
1.  **개체 탐색기**에서 새 뷰를 만들 데이터베이스를 확장합니다.  
  
2.  **동의어** 폴더를 마우스 오른쪽 단추로 클릭한 다음, **새 동의어...** 를 클릭합니다.  
  
3.  **새 동의어 추가** 대화 상자에 다음 정보를 입력합니다.  

     **동의어 이름**  
     이 개체에 사용할 새 이름을 입력합니다.  
  
     **동의어 스키마**  
     이 개체에 사용할 새 이름의 스키마를 입력합니다.  
  
     **서버 이름**  
     연결할 서버 인스턴스를 입력합니다.  
  
     **데이터베이스 이름**  
     개체가 포함된 데이터베이스를 입력하거나 선택합니다.  
  
     **스키마**  
     개체를 소유하는 스키마를 입력하거나 선택합니다.  
  
     **개체 유형**  
     개체 유형을 선택합니다.  
  
     **개체 이름**  
     동의어가 나타내는 개체의 이름을 입력합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-synonym"></a>동의어를 만들려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 있는 기존 테이블의 동의어를 만듭니다. 그런 다음 이후 예에서 이 동의어가 사용됩니다.  
  
```  
USE tempdb;  
GO  
CREATE SYNONYM MyAddressType  
FOR AdventureWorks2012.Person.AddressType;  
GO  
```  
  
 다음 예에서는 `MyAddressType` 동의어가 참조하는 기본 테이블에 행을 삽입합니다.  
  
```  
USE tempdb;  
GO  
INSERT INTO MyAddressType (Name)  
VALUES ('Test');  
GO  
```  
  
 다음 예에서는 동적 SQL에서 동의어를 참조하는 방법을 보여 줍니다.  
  
```  
USE tempdb;  
GO  
EXECUTE ('SELECT Name FROM MyAddressType');  
GO  
```  
  
  

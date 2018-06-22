---
title: 데이터베이스 마스터 키 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5d51012d037c04ea706feb0b7092f5eca6f09564
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090399"
---
# <a name="create-a-database-master-key"></a>데이터베이스 마스터 키 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 데이터베이스 마스터 키를 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   [Transact-SQL을 사용하여 데이터베이스 마스터 키를 만들려면](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 데이터베이스에 대한 CONTROL 권한이 필요합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-database-master-key"></a>데이터베이스 마스터 키를 만들려면  
  
1.  데이터베이스에 저장되는 마스터 키의 복사본을 암호화하기 위한 암호를 선택합니다.  
  
2.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
3.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
4.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- Creates a database master key for the "AdventureWorks2012" database.   
    -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."  
    USE AdventureWorks2012;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
    GO  
    ```  
  
 자세한 내용은 [CREATE MASTER KEY&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)를 참조하세요.  
  
  

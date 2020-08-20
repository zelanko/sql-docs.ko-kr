---
description: 'T-SQL 자습서: 데이터베이스 개체 삭제'
title: 'T-SQL 자습서: 데이터베이스 개체 삭제 | Microsoft Docs'
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.technology: t-sql
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting database objects
ms.assetid: ecf26dd5-4535-4ed6-86fc-c73f9d9dedec
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1a032737a39cf22e1b2d5516c615ced9d59dfc43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467534"
---
# <a name="lesson-3-delete-database-objects"></a>3단원: 데이터베이스 개체 삭제
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
이 단원에서는 1단원과 2단원에서 만든 개체를 제거한 다음 데이터베이스를 삭제합니다.  
  
개체를 삭제하기 전에 사용자가 올바른 데이터베이스에 있는지 확인합니다.
  
  ```sql  
  USE TestData;  
  GO  
  ```  

## <a name="revoke-stored-procedure-permissions"></a>저장 프로시저 사용 권한 취소
  
`REVOKE` 문을 사용하여 저장 프로시저에 대한 `Mary` 의 실행 권한을 제거합니다.
  
  ```sql  
  REVOKE EXECUTE ON pr_Names FROM Mary;  
  GO  
  ```  
  
## <a name="drop-permissions"></a>사용 권한 삭제

1. `DROP` 문을 사용하여 `Mary` 가 `TestData` 데이터베이스에 액세스할 수 있는 권한을 제거합니다.
  
   ```sql  
   DROP USER Mary;  
   GO  
   ```  


2. `DROP` 문을 사용하여 `Mary` 가 이 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]인스턴스에 액세스할 수 있는 권한을 제거합니다.
  
   ```sql  
   DROP LOGIN [<computer_name>\Mary];  
   GO   
   ```  
  
3. `DROP` 문을 사용하여 `pr_Names`저장 프로시저를 제거합니다.  
  
   ```sql  
   DROP PROC pr_Names;  
   GO   
   ```  
  
4. `DROP` 문을 사용하여 `vw_Names`뷰를 제거합니다.  
  
   ```sql  
   DROP VIEW vw_Names;  
   GO  
   ```  

## <a name="delete-table"></a>테이블 삭제
  
1. `DELETE` 문을 사용하여 `Products` 테이블에서 모든 행을 제거합니다.  
  
    ```sql  
    DELETE FROM Products;  
    GO  
    ```  
  
2.  `DROP` 문을 사용하여 `Products` 테이블을 제거합니다.  
  
    ```sql  
    DROP TABLE Products;  
    GO    
    ```  

## <a name="remove-database"></a>데이터베이스 제거
  
사용자가 `TestData` 데이터베이스에 있는 동안에는 이 데이터베이스를 제거할 수 없습니다. 따라서 먼저 컨텍스트를 다른 데이터베이스로 전환한 다음 `DROP` 문을 사용하여 `TestData` 데이터베이스를 제거합니다.  
  
  ```sql  
  USE MASTER;  
  GO  
  DROP DATABASE TestData;  
  GO   
  ```  
  
이것으로 [!INCLUDE[tsql](../includes/tsql-md.md)] 문 작성 자습서를 마칩니다. 이 자습서는 간략한 개요이므로 사용된 문에 대한 모든 옵션을 설명하지는 않습니다. 효율적인 데이터베이스 구조를 디자인 및 작성하고 데이터에 대한 보안 액세스를 구성하려면 이 자습서의 예제 데이터베이스보다 복잡한 데이터베이스가 필요합니다.  

  
  

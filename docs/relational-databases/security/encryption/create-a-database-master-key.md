---
title: 데이터베이스 마스터 키 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 01/02/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: aliceku
ms.author: aliceku
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ee5ecd798fd799c7c36f9a41c9fdfe44e9a967b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049991"
---
# <a name="create-a-database-master-key"></a>데이터베이스 마스터 키 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 데이터베이스 마스터 키를 만드는 방법에 대해 설명합니다.
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
데이터베이스에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="using-transact-sql"></a>Transact-SQL 사용  
  
### <a name="to-create-a-database-master-key"></a>데이터베이스 마스터 키를 만들려면  
  
1. 데이터베이스에 저장되는 마스터 키의 복사본을 암호화하기 위한 암호를 선택합니다.  
  
2. **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
3. 표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
4. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```sql
    -- Creates a database master key for the "AdventureWorks2012" database.   
    -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."  
    USE AdventureWorks2012;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
    GO  
    ```  
  
 자세한 내용은 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)를 참조하세요.  

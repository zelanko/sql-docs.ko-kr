---
title: 데이터베이스 마스터 키 만들기 | Microsoft 문서
description: Transact-SQL을 사용하여 SQL Server에서 데이터베이스 마스터 키를 만듭니다. 필요한 권한이 있어야 합니다.
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: jaszymas
ms.author: jaszymas
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5a5c3a93771a24a2cf3d1f5debb77b7026bef963
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463124"
---
# <a name="create-a-database-master-key"></a>데이터베이스 마스터 키 만들기

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 데이터베이스 마스터 키를 만드는 방법에 대해 설명합니다.

## <a name="security"></a>보안

### <a name="permissions"></a>사용 권한

데이터베이스에 대한 CONTROL 권한이 필요합니다.

## <a name="using-transact-sql"></a>Transact-SQL 사용

### <a name="to-create-a-database-master-key"></a>데이터베이스 마스터 키를 만들려면

1. 데이터베이스에 저장되는 마스터 키의 복사본을 암호화하기 위한 암호를 선택합니다.
2. **개체 탐색기** 에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.
3. **시스템 데이터베이스** 를 확장하고 `master`를 마우스 오른쪽 단추를 클릭한 다음, **새 쿼리** 를 클릭합니다.
4. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.

   ```sql
     -- Creates the master key.
     -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe".  
     CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  

   ```

자세한 내용은 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)를 참조하세요.

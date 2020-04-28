---
title: 데이터베이스 마스터 키 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql-server-2014
ms.reviewer: carlrab
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 86f74710e99079d0acd28db09bcf1e4ba7c57865
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74957247"
---
# <a name="create-a-database-master-key"></a>데이터베이스 마스터 키 만들기

이 항목에서는를 사용 `master` [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[tsql](../../../includes/tsql-md.md)]하 여에서 데이터베이스에 데이터베이스 마스터 키를 만드는 방법에 대해 설명 합니다.

**항목 내용**

- **시작하기 전 주의 사항:**

  [보안](#Security)

- [Transact-SQL을 사용하여 데이터베이스 마스터 키를 만들려면](#TsqlProcedure)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에

### <a name="security"></a><a name="Security"></a> 보안

#### <a name="permissions"></a><a name="Permissions"></a> 권한

데이터베이스에 대한 CONTROL 권한이 필요합니다.

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용

### <a name="to-create-a-database-master-key"></a>데이터베이스 마스터 키를 만들려면

1. 데이터베이스에 저장되는 마스터 키의 복사본을 암호화하기 위한 암호를 선택합니다.
2. **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.
3. **시스템 데이터베이스**를 확장하고 `master`를 마우스 오른쪽 단추를 클릭한 다음, **새 쿼리**를 클릭합니다.
4. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.

  ```sql
  -- Creates the master key.
  -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."
  CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';
```

자세한 내용은 [CREATE MASTER KEY&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)를 참조하세요.

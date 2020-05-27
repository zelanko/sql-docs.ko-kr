---
title: '@@DBTS(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@DBTS_TSQL'
- '@@DBTS'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@DBTS function'
- timestamp data type
ms.assetid: 91842ddd-91c0-4445-a03f-116f6bc991d0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 61743139f35ed3e8a5dd4bbac9bd1f4660cb2ec2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68136026"
---
# <a name="x40x40dbts-transact-sql"></a>&#x40;&#x40;DBTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 함수는 현재 데이터베이스의 현재 **timestamp** 데이터 형식 값을 반환합니다. 현재 데이터베이스는 보장된 고유한 타임스탬프 값을 갖습니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```
@@DBTS  
```  
  
## <a name="return-types"></a>반환 형식
**varbinary**
  
## <a name="remarks"></a>설명  
@@DBTS는 현재 데이터베이스에서 최근에 사용된 타임스탬프 값을 반환합니다. **timestamp** 열이 있는 행의 삽입 또는 업데이트는 새 타임스탬프 값을 생성합니다.
  
트랜잭션 격리 수준에 대한 변경 내용은 @@DBTS 함수에 영향을 주지 않습니다.
  
## <a name="examples"></a>예  
이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 현재 **timestamp**를 반환합니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@DBTS;  
```  
  
## <a name="see-also"></a>참고 항목
[구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)  
[커서 동시성&#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/properties/cursor-concurrency-odbc.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION&#40;Transact-SQL&#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)
  
  

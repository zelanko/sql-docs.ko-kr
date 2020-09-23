---
description: '&#x40;&#x40;MAX_PRECISION(Transact SQL)'
title: '@@MAX_PRECISION(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@MAX_PRECISION_TSQL'
- '@@MAX_PRECISION'
dev_langs:
- TSQL
helpviewer_keywords:
- precision [SQL Server], @@MAX_PRECISION
- numeric data type, precision level
- decimal data type, precision level
- '@@MAX_PRECISION function'
- data types [SQL Server], precision
ms.assetid: 9e7158a1-e503-422a-b326-3c9b06e181b2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 31b1c96a3cb6ab0a0a957ebcbff2d49776d658c8
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115138"
---
# <a name="x40x40max_precision-transact-sql"></a>&#x40;&#x40;MAX_PRECISION(Transact SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  현재 서버에 설정된 **decimal** 및 **numeric** 데이터 형식에서 사용하는 전체 자릿수를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
@@MAX_PRECISION  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 **tinyint**  
  
## <a name="remarks"></a>설명  
 기본적으로 최대 전체 자릿수는 38이 반환됩니다.  
  
## <a name="examples"></a>예제  
  
```sql  
SELECT @@MAX_PRECISION AS 'Max Precision'  
```  
  
## <a name="see-also"></a>참고 항목  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [decimal 및 numeric&#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [전체 자릿수, 소수 자릿수 및 길이&#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)  
  
  

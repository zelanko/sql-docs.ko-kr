---
description: 백슬래시(줄 연속 문자)(Transact SQL)
title: 백슬래시(줄 연속 문자)(Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '\_TSQL'
- '\'
dev_langs:
- TSQL
helpviewer_keywords:
- backwhack
- backslash
- escape character
- hack character
- '\ (backslash)'
- backslant
- bash
- reverse slant
- slosh
- reversed virgule
- line continuation character
- reverse solidus
ms.assetid: c97fbb20-3d12-4d0b-9b52-62a229bc83c0
author: rothja
ms.author: jroth
ms.openlocfilehash: 2437daed52cb8b4a79431465f8a27e5464185e23
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459285"
---
# <a name="backslash-line-continuation-transact-sql"></a>백슬래시(줄 연속 문자)(Transact SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

`\`는 가독성을 높이기 위해 긴 문자열 상수, 문자 또는 이진을 둘 이상의 줄로 나눕니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
<first section of string> \  
<continued section of string>  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 \<first section of string>  
 문자열의 시작 부분입니다.  
  
 \<continued section of string>  
 문자열의 계속되는 부분입니다.  
  
## <a name="remarks"></a>설명  
이 명령은 문자열의 첫째 섹션과 계속되는 섹션을 백슬래시 없이 한 문자열로 반환합니다. 백슬래시 뒤의 새 줄은 줄 바꿈 문자(U+000A) 또는 캐리지 리턴(U+000D)와 줄 바꿈(U+000A)의 조합(이 순서 유지)이어야 합니다. 

## <a name="examples"></a>예제  

### <a name="a-splitting-a-character-string"></a>A. 문자열 분할  

다음 예에서는 백슬래시 및 캐리지 리턴을 사용하여 문자열을 두 줄로 분할합니다.  
  
```  
SELECT 'abc\  
def' AS [ColumnResult];  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 abcdef
 ```    

### <a name="b-splitting-a-binary-string"></a>B. 이진 문자열 분할  

다음 예에서는 백슬래시 및 캐리지 리턴을 사용하여 이진 문자열을 두 줄로 분할합니다.  

```  
SELECT 0xabc\
def AS [ColumnResult];  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 0xABCDEF
 ```    

## <a name="see-also"></a>참고 항목  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [&#40;나누기&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/divide-transact-sql.md)   
 [&#40;나누기 대입&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [복합 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  

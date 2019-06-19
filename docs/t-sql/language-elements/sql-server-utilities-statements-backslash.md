---
title: 백슬래시(줄 연속 문자)(Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/09/2017
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
manager: craigg
ms.openlocfilehash: 4b03094aa0d75b2491e2635506c9a7b6563dacba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65981681"
---
# <a name="backslash-line-continuation-transact-sql"></a>백슬래시(줄 연속 문자)(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

`\`는 가독성을 높이기 위해 긴 문자열 상수, 문자 또는 이진을 둘 이상의 줄로 나눕니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
<first section of string> \  
<continued section of string>  
```  
  
## <a name="arguments"></a>인수  
 \<first section of string>  
 문자열의 시작 부분입니다.  
  
 \<continued section of string>  
 문자열의 계속되는 부분입니다.  
  
## <a name="remarks"></a>Remarks  
 이 명령은 문자열의 첫째 섹션과 계속되는 섹션을 백슬래시 없이 한 문자열로 반환합니다.  

## <a name="examples"></a>예  

### <a name="a-splitting-a-character-string"></a>1. 문자열 분할  

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

### <a name="b-splitting-a-binary-string"></a>2. 이진 문자열 분할  

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
  
  

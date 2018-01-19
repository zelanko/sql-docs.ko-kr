---
title: "백슬래시 (줄 연속 문자) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 11/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
f1_keywords:
- '\_TSQL'
- '\'
dev_langs: TSQL
helpviewer_keywords:
- backwhack
- backslash
- excape character
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
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 99586a80cce43c89aa7ce9a76c84e74652d343be
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="backslash-line-continuation-transact-sql"></a>백슬래시 (줄 연속 문자) (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

`\`가독성을 위해 두 개 이상의 줄으로 긴 문자열 상수, 문자 또는 이진을 중단합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
<first section of string> \  
<continued section of string>  
```  
  
## <a name="arguments"></a>인수  
 \<문자열의 첫 번째 섹션 >  
 문자열의 시작 부분입니다.  
  
 \<문자열의 부분을 계속 >  
 문자열의 계속되는 부분입니다.  
  
## <a name="remarks"></a>주의  
 이 명령은 문자열의 첫째 섹션과 계속되는 섹션을 백슬래시 없이 한 문자열로 반환합니다.  

## <a name="examples"></a>예  

### <a name="a-splitting-a-character-string"></a>1. 문자열 분  

다음 예제에서는를 사용 하 여 백슬래시 및 캐리지 리턴 문자 문자열 선을 두 선으로 분할 합니다.  
  
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

### <a name="b-splitting-a-binary-string"></a>2. 이진 문자열 분  

다음 예제에서는 백슬래시 및 캐리지 리턴을 사용 하 여 이진 문자열 선을 두 선으로 분할 합니다.  

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

## <a name="see-also"></a>관련 항목:  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [&#40; 나누기 &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/divide-transact-sql.md)   
 [&#40; 나누기 대입 &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [복합 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  

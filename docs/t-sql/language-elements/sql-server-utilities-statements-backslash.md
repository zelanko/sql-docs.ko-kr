---
title: "(백슬래시) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- '\_TSQL'
- '\'
dev_langs:
- TSQL
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
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 011025d20b6341b9fa43b25f6c14c91a135a6ffa
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-utilities-statements---backslash"></a>SQL Server 유틸리티 문 백슬래시
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]제공 되지 않은 명령 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 인식 되는 **sqlcmd** 및 **osql** 유틸리티 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 코드 편집기. 이러한 명령을 사용하면 일괄 처리 및 스크립트를 쉽게 읽고 실행할 수 있습니다.  
  
\ 가독성을 위해 두 개 이상의 줄으로 상수 긴 문자열을 중단 합니다.  
  
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
  
 백슬래시는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 아닙니다. 인식 되는 명령인는 **sqlcmd** 및 **osql** 유틸리티 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 코드 편집기.  
  
## <a name="examples"></a>예  
 다음 예에서는 백슬래시 및 캐리지 리턴을 사용하여 문자열을 두 줄로 분할합니다.  
  
```  
SELECT 'abc\  
def' AS ColumnResult;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 abcdef
 ```    
  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [&#40; 나누기 &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/divide-transact-sql.md)   
 [&#40; 나누기 EQUALS &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [복합 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


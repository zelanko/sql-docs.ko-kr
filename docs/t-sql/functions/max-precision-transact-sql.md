---
title: '@@MAX_PRECISION (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d52f6d347c274044d4902508920038e166efb65a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="maxprecision-transact-sql"></a>@@MAX_PRECISION (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  사용 하는 전체 자릿수 수준을 반환 **10 진수** 및 **숫자** 데이터 형식에서 현재 서버에 설정 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
@@MAX_PRECISION  
```  
  
## <a name="return-types"></a>반환 형식  
 **tinyint**  
  
## <a name="remarks"></a>주의  
 기본적으로 최대 전체 자릿수는 38이 반환됩니다.  
  
## <a name="examples"></a>예  
  
```  
SELECT @@MAX_PRECISION AS 'Max Precision'  
```  
  
## <a name="see-also"></a>관련 항목:  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [decimal 및 numeric&#40; Transact SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [전체 자릿수, 소수 자릿수 및 길이 &#40; Transact SQL &#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)  
  
  

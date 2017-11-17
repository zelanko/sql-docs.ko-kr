---
title: "!&gt; (보다 크지 않음) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- Not Greater
- Greater
- '!>_TSQL'
- '!>'
- Not Greater Than
dev_langs:
- TSQL
helpviewer_keywords:
- '!> (not greater than)'
- not greater than operator (!>)
ms.assetid: 71a413ed-64f1-4ab9-9c52-c5959a77d00f
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 61f574082f98aa61601035f44c73041275c386de
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="gt-not-greater-than-transact-sql"></a>!&gt; (보다 크지 않음) (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  두 식을 비교합니다(비교 연산자).   Null이 아닌 식을 비교하는 경우 왼쪽 피연산자의 값이 오른쪽 피연산자의 값보다 크지 않으면 결과는 TRUE이고 그렇지 않으면 결과는 FALSE입니다. =(등가) 비교 연산자와 달리 두 NULL 값에 대한 >= 비교의 결과는 ANSI_NULLS 설정에 따라 달라지지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
expression !> expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)합니다. 두 식은 모두 암시적으로 변환 가능한 데이터 형식이어야 합니다. 변환의 규칙에 따라 달라 집니다 [데이터 형식 우선 순위](../../t-sql/data-types/data-type-precedence-transact-sql.md)합니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  


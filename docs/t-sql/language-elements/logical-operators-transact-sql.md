---
title: 논리 연산자(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], logical
- testing truth
- truth testing
- "TRUE"
- "FALSE"
- logical operators [SQL Server], Transact-SQL
ms.assetid: edd92f08-76fb-4fd7-a4b6-8520d6a81df1
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4447b7f120bc393f9c8a587d3c9490b59bfa809a
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36254265"
---
# <a name="logical-operators-transact-sql"></a>논리 연산자(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  논리 연산자는 조건의 진위 여부를 테스트합니다. 논리 연산자도 비교 연산자처럼 TRUE, FALSE 또는 UNKNOWN 값의 **Boolean** 데이터 형식을 반환합니다.  
  
|연산자|의미|  
|--------------|-------------|  
|[ALL](../../t-sql/language-elements/all-transact-sql.md)|모든 비교 집합이 TRUE인 경우 TRUE입니다.|  
|[AND](../../t-sql/language-elements/and-transact-sql.md)|두 개의 부울 식이 모두 TRUE인 경우 TRUE입니다.|  
|[ANY](../../t-sql/language-elements/any-transact-sql.md)|비교 집합 중 하나가 TRUE인 경우 TRUE입니다.|  
|[BETWEEN](../../t-sql/language-elements/between-transact-sql.md)|피연산자가 범위 안에 있는 경우 TRUE입니다.|  
|[EXISTS](../../t-sql/language-elements/exists-transact-sql.md)|하위 쿼리에 행이 포함된 경우 TRUE입니다.|  
|[IN](../../t-sql/language-elements/in-transact-sql.md)|피연산자가 식 목록 중 하나와 같은 경우 TRUE입니다.|  
|[LIKE](../../t-sql/language-elements/like-transact-sql.md)|피연산자가 패턴과 일치하는 경우 TRUE입니다.|  
|[NOT](../../t-sql/language-elements/not-transact-sql.md)|다른 모든 부울 연산자의 값을 반대로 합니다.|  
|[OR](../../t-sql/language-elements/or-transact-sql.md)|하나의 부울 식이 TRUE인 경우 TRUE입니다.|  
|[SOME](../../t-sql/language-elements/some-any-transact-sql.md)|비교 집합 중 일부가 TRUE인 경우 TRUE입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [연산자 우선 순위&#40;Transact-SQL&#41;](../../t-sql/language-elements/operator-precedence-transact-sql.md)  
  
  

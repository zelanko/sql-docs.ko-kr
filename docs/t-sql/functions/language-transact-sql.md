---
title: '@@LANGUAGE (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@LANGUAGE_TSQL'
- '@@LANGUAGE'
dev_langs:
- TSQL
helpviewer_keywords:
- languages [SQL Server], current in use
- '@@LANGUAGE function'
- current language in use
- names [SQL Server], language in use
ms.assetid: 3e13b477-7dfa-4da6-9948-da2050d42527
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 33fcf5ceb2481b517844cb5334dd67c97b039b77
ms.contentlocale: ko-kr
ms.lasthandoff: 10/17/2017

---
# <a name="x40x40language-transact-sql"></a>&#x40;&#x40;언어 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 사용 중인 언어의 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@LANGUAGE  
```  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar**  
  
## <a name="remarks"></a>주의  
 유효한 공식 언어 이름을 포함 하 여 언어 설정에 대 한 정보를 보려면 실행 **sp_helplanguage** 매개 변수 지정 없이 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 세션의 언어를 반환합니다.  
  
```  
SELECT @@LANGUAGE AS 'Language Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Language Name                   
------------------------------  
us_english                      
```  
  
## <a name="see-also"></a>관련 항목:  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [언어 설정 &#40; Transact SQL &#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [sp_helplanguage &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)  
  
  



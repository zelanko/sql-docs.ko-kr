---
title: '@@LANGUAGE(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7171427ce54dcc8bcb8d3ec377a28cf51e9f80ef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="x40x40language-transact-sql"></a>&#x40;&#x40;LANGUAGE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 사용 중인 언어의 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@LANGUAGE  
```  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 유효한 공식 언어 이름을 포함하여 언어 설정에 대한 정보를 보려면 지정된 매개 변수 없이 **sp_helplanguage**를 실행하세요.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET LANGUAGE&#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [sp_helplanguage&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)  
  
  


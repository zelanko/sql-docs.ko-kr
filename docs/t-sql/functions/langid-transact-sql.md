---
title: '@@LANGID(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@LANGID'
- '@@LANGID_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- languages [SQL Server], current in use
- '@@LANGID function'
- current language in use
- ID for language in use
- local language IDs [SQL Server]
ms.assetid: 7a0fc089-2a48-4a81-9d78-2aaedb540d37
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 83aff89cf0651d338105788a4ca7ef7f751b8528
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109256"
---
# <a name="x40x40langid-transact-sql"></a>&#x40;&#x40;LANGID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 사용 중인 언어의 로컬 언어 식별자(ID)를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@LANGID  
```  
  
## <a name="return-types"></a>반환 형식  
 **smallint**  
  
## <a name="remarks"></a>Remarks  
 언어 ID를 포함한 언어 설정에 대한 정보를 보려면 매개 변수를 지정하지 않고 **sp_helplanguage**를 실행하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 세션의 언어를 `Italian`으로 설정한 다음 `@@LANGID`를 사용하여 이탈리아어의 ID를 반환합니다.  
  
```  
SET LANGUAGE 'Italian'  
SELECT @@LANGID AS 'Language ID'  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Changed language setting to Italiano.  
Language ID  
-----------  
6            
```  
  
## <a name="see-also"></a>참고 항목  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET LANGUAGE&#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [sp_helplanguage&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)  
  
  

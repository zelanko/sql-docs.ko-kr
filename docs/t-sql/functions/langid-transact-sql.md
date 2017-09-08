---
title: '@@LANGID (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4e27e2678cd5c54f44711ecd3d5d1d75a85f1a16
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="langid-transact-sql"></a>@@LANGID (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 사용 중인 언어의 로컬 언어 식별자(ID)를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
@@LANGID  
```  
  
## <a name="return-types"></a>반환 형식  
 **smallint**  
  
## <a name="remarks"></a>주의  
 언어 ID 번호를 포함 하 여 언어 설정에 대 한 정보를 보려면 실행 **sp_helplanguage** 매개 변수 지정 없이 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [언어 설정 &#40; Transact SQL &#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [sp_helplanguage &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)  
  
  

---
title: xp_sprintf (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_sprintf_TSQL
- xp_sprintf
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sprintf
ms.assetid: 1eedd65c-03cc-4eab-b76e-04684fdfec52
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3ba1648da108762b03155eb93e1ee11c53a75583
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75831762"
---
# <a name="xp_sprintf-transact-sql"></a>xp_sprintf(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  일련의 문자 및 값을 문자열 출력 매개 변수에 포맷하고 저장합니다. 각 포맷 인수는 해당되는 인수로 대체됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_sprintf { string OUTPUT , format }  
     [ , argument [ ,...n ] ]  
```  
  
## <a name="arguments"></a>인수  
 *문자열*  
 는 출력을 받는 **varchar** 변수입니다.  
  
 OUTPUT  
 지정한 경우 변수의 값을 출력 매개 변수에 넣습니다.  
  
 *형식과*  
 는 C 언어 **sprintf** 함수에서 지원 되는 것과 비슷한 *인수* 값에 대 한 자리 표시 자가 포함 된 서식 문자열입니다. 현재 % 포맷 인수만 지원됩니다.  
  
 *t*  
 해당되는 포맷 인수의 값을 표시하는 문자열입니다.  
  
 *n*  
 최대 50개의 인수를 지정할 수 있음을 나타내는 자리 표시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 **xp_sprintf** 에서 다음 메시지를 반환 합니다.  
  
 `The command(s) completed successfully.`  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;일반 확장 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;xp_sscanf &#40;](../../relational-databases/system-stored-procedures/xp-sscanf-transact-sql.md)  
  
  

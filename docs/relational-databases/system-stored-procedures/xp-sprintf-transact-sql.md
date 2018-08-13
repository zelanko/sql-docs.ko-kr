---
title: xp_sprintf (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: e8d0683523c12e4379b78e9fa92fb70d6d869051
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39556484"
---
# <a name="xpsprintf-transact-sql"></a>xp_sprintf(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  일련의 문자 및 값을 문자열 출력 매개 변수에 포맷하고 저장합니다. 각 포맷 인수는 해당되는 인수로 대체됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_sprintf { string OUTPUT , format }  
     [ , argument [ ,...n ] ]  
```  
  
## <a name="arguments"></a>인수  
 *string*  
 **varchar** 출력을 받는 변수입니다.  
  
 OUTPUT  
 지정한 경우 변수의 값을 출력 매개 변수에 넣습니다.  
  
 *format*  
 에 대 한 자리 표시자를 사용 하 여 형식 문자열 *인수* 값을 C 언어에서 지 원하는 것과 비슷합니다 **sprintf** 함수입니다. 현재 % 포맷 인수만 지원됩니다.  
  
 *argument*  
 해당되는 포맷 인수의 값을 표시하는 문자열입니다.  
  
 *n*  
 최대 50개의 인수를 지정할 수 있음을 나타내는 자리 표시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 **xp_sprintf** 다음 메시지를 반환 합니다.  
  
 `The command(s) completed successfully.`  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [일반 확장 저장된 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_sscanf &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-sscanf-transact-sql.md)  
  
  

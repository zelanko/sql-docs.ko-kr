---
title: sp_cursorunprepare (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorunprepare_TSQL
- sp_cursorunprepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorunprepare
ms.assetid: b46d4813-c4a9-4f9d-9979-2b5082ecf06a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e95828dcee6ea75c24df350379e6ac1e3c43d5ff
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733293"
---
# <a name="sp_cursorunprepare-transact-sql"></a>sp_cursorunprepare(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Sp_cursorprepare 저장 프로시저에서 개발 된 실행 계획을 삭제 합니다. sp_cursorunprepare은 TDS (tabular data stream) 패킷에서 ID = 6을 지정 하 여 호출 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursorunprepare handle  
```  
  
## <a name="arguments"></a>인수  
 *처리*  
 문을 준비할 때 sp_cursorprepare에서 반환 하는 *핸들* 값입니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_cursorprepare &#40;](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

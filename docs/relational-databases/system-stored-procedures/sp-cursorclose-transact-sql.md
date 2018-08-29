---
title: sp_cursorclose (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_close_TSQL
- sp_cursor_close
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorclose
ms.assetid: d9b7b44d-cdff-456e-97df-7031a3b9beb6
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1556ebbfd0f5e01cfccae734036122360e68944
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43022009"
---
# <a name="spcursorclose-transact-sql"></a>sp_cursorclose(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  닫습니다 커서를 할당 취소와 및 모든 관련된 리소스를 해제 합니다. 즉, KEYSET 또는 STATIC을 지원 하기 위해 사용 되는 임시 테이블을 삭제 **커서**합니다. sp_cursorclose가 ID를 지정 하 여 호출 = 9 tabular data TDS (stream) 패킷에서를 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursorclose cursor  
```  
  
## <a name="arguments"></a>인수  
 *cursor*  
 커서 *처리할* 에서 생성 된 값 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하며 sp_cursoropen 프로시저에서 반환 합니다. *커서* 필요로 하는 필수 매개 변수를 **int** 값을 입력 합니다.  
  
> [!NOTE]  
>  입력 값이 -1이면 현재 연결의 모든 커서에 대해 값이 적용됩니다.  
  
## <a name="remarks"></a>Remarks  
 *커서* 커서를 닫은 후 프로시저를 실행 하는 경우 또는 잘못 된 핸들을 지정 하는 경우 오류 메시지를 반환 합니다.  
  
 RPC 상태는 전체적인 성공 또는 실패를 나타냅니다.  
  
 DONE 행 개수는 항상 0입니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_cursoropen &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

---
title: sp_cursorclose (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_close_TSQL
- sp_cursor_close
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorclose
ms.assetid: d9b7b44d-cdff-456e-97df-7031a3b9beb6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 543e8c0b41000ec2afe9ab07aef08aa86967c2ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68108561"
---
# <a name="sp_cursorclose-transact-sql"></a>sp_cursorclose(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  커서를 닫고 할당 취소 하며 연결 된 모든 리소스를 해제 합니다. 즉, 키 집합 또는 정적 **커서**를 지 원하는 데 사용 되는 임시 테이블을 삭제 합니다. sp_cursorclose은 TDS (tabular data stream) 패킷에서 ID = 9를 지정 하 여 호출 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursorclose cursor  
```  
  
## <a name="arguments"></a>인수  
 *위치*  
 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 생성 하 고 sp_cursoropen 프로시저에서 반환 하는 커서 *핸들* 값입니다. *커서* 는 **int** 입력 값에 대해를 호출 하는 필수 매개 변수입니다.  
  
> [!NOTE]  
>  입력 값이 -1이면 현재 연결의 모든 커서에 대해 값이 적용됩니다.  
  
## <a name="remarks"></a>설명  
 커서를 닫은 후 또는 잘못 된 핸들이 지정 된 경우에는 *커서가* 오류 메시지를 반환 합니다.  
  
 RPC 상태는 전체적인 성공 또는 실패를 나타냅니다.  
  
 DONE 행 개수는 항상 0입니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_cursoropen &#40;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

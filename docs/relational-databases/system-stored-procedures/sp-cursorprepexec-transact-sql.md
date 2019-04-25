---
title: sp_cursorprepexec (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorprepexec_TSQL
- sp_cursorprepexec
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorprepexec
ms.assetid: 8094fa90-35b5-4cf4-8012-0570cb2ba1e6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f09f33f4f153f21cfe7a3c8c538c2f272b3df77b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62507343"
---
# <a name="spcursorprepexec-transact-sql"></a>sp_cursorprepexec(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  제출된 커서 문이나 일괄 처리에 대한 실행 계획을 컴파일한 다음 커서를 만들고 채웁니다. sp_cursorprepexec는 sp_cursorprepare와 sp_cursorexecute의 기능을 결합 합니다. 이 프로시저는 TDS(Tabular Data Stream) 패킷에서 ID = 5를 지정하여 호출합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursorprepexec prepared handle OUTPUT, cursor OUTPUT, params , statement , options  
    [ , scrollopt [ , ccopt [ , rowcount ] ] ]  
```  
  
## <a name="arguments"></a>인수  
 *준비 된 핸들*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 생성 된 준비 *처리* 식별자입니다. *준비 된 핸들* 필수 항목이 며 반환 **int**합니다.  
  
 *cursor*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 생성하는 커서 식별자입니다. *커서* sp_cursorfetch이이 커서에 대해 작동 하는 모든 후속 프로시저에 제공 해야 하는 필수 매개 변수입니다.  
  
 *params*  
 매개 변수가 있는 문을 식별합니다. 합니다 *params* 문에서 매개 변수 표식에 대 한 변수 정의 바뀝니다. *params* 필요로 하는 필수 매개 변수를 **ntext**를 **nchar**, 또는 **nvarchar** 값을 입력 합니다.  
  
> [!NOTE]  
>  사용 하 여는 **ntext** 입력 문자열 값 *stmt* 매개 변수가 및 *scrollopt* PARAMETERIZED_STMT 값이 ON입니다.  
  
 *statement*  
 커서 결과 집합을 정의합니다. *문* 호출에 대 한 필수 매개 변수 이며는 **ntext**를 **nchar** 또는 **nvarchar** 값을 입력 합니다.  
  
> [!NOTE]  
>  Stmt 값을 지정 하기 위한 규칙은 sp_cursoropen, 예외와 동일 하는 *stmt* 문자열 데이터 형식 이어야 합니다 **ntext**합니다.  
  
 *options*  
 커서 결과 집합 열의 설명을 반환하는 선택적 매개 변수입니다. *옵션* 다음이 필요 합니다 **int** 값을 입력 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 스크롤 옵션입니다. *scrollopt* 다음 중 하나를 필요로 하는 선택적 매개 변수 **int** 값을 입력 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 요청한 옵션이 적합 하지 않은에서 정의한 커서에 대 한 가능성으로 인해  *\<stmt >*,이 매개 변수 둘 다로 입력과 출력 사용 됩니다. 이러한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 적절한 형식을 할당하고 이 값을 수정합니다.  
  
 *ccopt*  
 동시성 제어 옵션입니다. *ccopt* 다음 중 하나를 필요로 하는 선택적 매개 변수 **int** 값을 입력 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS(이전의 LOCKCC)|  
|0x0004|**낙관적** (이전의 OPTCC)|  
|0x0008|OPTIMISTIC(이전의 OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 와 마찬가지로 *scrollpt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 요청 된 다른 값을 할당할 수 있습니다.  
  
 *rowcount*  
 AUTO_FETCH에 사용할 인출 버퍼 행 수를 나타내는 선택적 매개 변수입니다. 기본값은 20개 행입니다. *행 개수* 입력된 값과 반환 값으로 할당할 때 다르게 동작 합니다.  
  
|입력 값일 때|반환 값일 때|  
|--------------------|---------------------|  
|FAST_FORWARD 커서를 사용 하 여 AUTO_FETCH를 지정 하는 경우 *rowcount* 인출 버퍼에 배치할 행 수를 나타냅니다.|결과 집합의 행 수를 나타냅니다. 경우는 *scrollopt* AUTO_FETCH 값을 지정 하면 *rowcount* 는 인출 버퍼로 인출 된 행 수를 반환 합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 하는 경우 *params* 문을 매개 변수화 되지 다음 NULL 값을 반환 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_cursoropen &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorexecute &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursorprepare &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [sp_cursorfetch &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

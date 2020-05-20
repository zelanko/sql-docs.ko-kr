---
title: sp_cursorprepexec (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2019
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e82a82df5f532df05ad0f04a14c95b24850484bd
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831672"
---
# <a name="sp_cursorprepexec-transact-sql"></a>sp_cursorprepexec(Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  제출된 커서 문이나 일괄 처리에 대한 실행 계획을 컴파일한 다음 커서를 만들고 채웁니다. sp_cursorprepexec sp_cursorprepare 및 sp_cursorexecute의 기능을 결합 합니다. 이 프로시저는 TDS (tabular data stream) 패킷에서 ID = 5를 지정 하 여 호출 합니다.  
  
 ![링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursorprepexec prepared handle OUTPUT, cursor OUTPUT, params , statement , options  
    [ , scrollopt [ , ccopt [ , rowcount ] ] ]  
    [, '@parameter_name[,...n ]']
```  
  
## <a name="arguments"></a>인수  
 *준비 된 핸들*  
 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 생성 된 준비 *핸들* 식별자입니다. *준비 된 핸들* 은 필수 이며 **int**를 반환 합니다.  
  
 *cursor*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 생성하는 커서 식별자입니다. *커서* 는이 커서에 대해 작동 하는 모든 후속 프로시저에 제공 해야 하는 필수 매개 변수입니다 (예: sp_cursorfetch).  
  
 *params*  
 매개 변수가 있는 문을 식별합니다. 변수의 매개 변수 정의는 문에서 매개 변수 표식을 *대체 합니다.* *params* 는 **ntext**, **nchar**또는 **nvarchar** 입력 값을 호출 하는 필수 매개 변수입니다.  
  
> [!NOTE]  
>  *Stmt* 매개 변수화 되 고 *scrollopt* PARAMETERIZED_STMT 값이 ON 인 경우 **ntext** 문자열을 입력 값으로 사용 합니다.  
  
 *statement*  
 커서 결과 집합을 정의합니다. *Statement* 매개 변수는 필수 이며 **ntext**, **nchar**또는 **nvarchar** 입력 값에 대해를 호출 합니다.  
  
> [!NOTE]  
>  Stmt 값을 지정 하는 규칙은 sp_cursoropen의 경우와 동일 합니다. 단, *stmt* 문자열 데이터 형식은 **ntext**여야 합니다.  
  
 *options*  
 커서 결과 집합 열의 설명을 반환하는 선택적 매개 변수입니다. * 옵션에는 다음 **int** 입력 값이 필요 합니다.  
  
|값|설명|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 스크롤 옵션입니다. *scrollopt* 는 다음 **int** 입력 값 중 하나를 필요로 하는 선택적 매개 변수입니다.  
  
|값|설명|  
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
  
 요청 된 옵션이 * \< stmt>* 에서 정의 된 커서에 적합 하지 않을 수 있기 때문에이 매개 변수는 입력과 출력 둘 다로 사용 됩니다. 이러한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 적절한 형식을 할당하고 이 값을 수정합니다.  
  
 *ccopt*  
 동시성 제어 옵션입니다. *ccopt* 는 다음 **int** 입력 값 중 하나를 필요로 하는 선택적 매개 변수입니다.  
  
|값|설명|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS(이전의 LOCKCC)|  
|0x0004|**낙관적** (이전에는 OPTCC로 알려짐)|  
|0x0008|OPTIMISTIC(이전의 OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 *Scrollpt*와 마찬가지로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 요청한 것과 다른 값을 할당할 수 있습니다.  
  
 *개수*  
 AUTO_FETCH에 사용할 인출 버퍼 행 수를 나타내는 선택적 매개 변수입니다. 기본값은 20개 행입니다. *행 개수* 는 입력 값과 반환 값으로 할당 될 때 다르게 동작 합니다.  
  
|입력 값일 때|반환 값일 때|  
|--------------------|---------------------|  
|FAST_FORWARD와 함께 AUTO_FETCH 지정 하면 커서 *rowcount* 는 인출 버퍼에 넣을 행 수를 나타냅니다.|결과 집합의 행 수를 나타냅니다. *Scrollopt* AUTO_FETCH 값이 지정 된 경우 *rowcount* 는 인출 버퍼에 인출 된 행 수를 반환 합니다.|  

*parameter_name* Params 인수에 정의 된 하나 이상의 매개 변수 이름을 지정 합니다.  Params에 포함 된 모든 매개 변수에 대해 매개 변수를 제공 해야 합니다. Transact-sql 문이나 params의 일괄 처리에 매개 변수가 정의 되어 있지 않으면이 인수는 필요 하지 않습니다.
  
## <a name="return-code-values"></a>반환 코드 값  
 Params에서 NULL 값을 반환 하는 경우 문은 매개 변수화 되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_cursoropen &#40;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Transact-sql&#41;sp_cursorexecute &#40;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [Transact-sql&#41;sp_cursorprepare &#40;](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [Transact-sql&#41;sp_cursorfetch &#40;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  

---
title: sp_cursorprepare (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs: TSQL
helpviewer_keywords: sp_cursor_prepare
ms.assetid: 6207e110-f4bf-4139-b3ec-b799c9cb3ad7
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87d9a5eb64f10e07549a282dc77dc21d219b6584
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spcursorprepare-transact-sql"></a>sp_cursorprepare(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  커서 문이나 일괄 처리를 실행 계획으로 컴파일하되 커서를 만들지는 않습니다. 컴파일된 문은 나중에 sp_cursorexecute에서 사용할 수 있습니다. 이 절차에서는 sp_cursorexecute와 결합 되어 sp_cursoropen와 동일한 기능을 갖지만 두 단계로 분리 됩니다. sp_cursorprepare가 ID를 지정 하 여 호출 = 표 형식 데이터 TDS (stream) 패킷의 3입니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursorprepare prepared_handle OUTPUT, params , stmt , options  
    [ , scrollopt[ , ccopt]]  
```  
  
## <a name="arguments"></a>인수  
 *prepared_handle*  
 SQL Server에서 생성 된 준비 *처리* 정수 값을 반환 하는 식별자입니다.  
  
> [!NOTE]  
>  *prepared_handle* 이후에 커서를 열기 위해 sp_cursorexecute 프로시저에 제공 됩니다. 작성된 핸들은 로그오프하거나 sp_cursorunprepare 프로시저를 통해 명시적으로 핸들을 제거할 때까지 존재합니다.  
  
 *매개 변수*  
 매개 변수가 있는 문을 식별합니다. *params* 문에 매개 변수 표식에 대 한 변수 정의 바뀝니다. *params* 필요로 하는 필수 매개 변수는 **ntext**, **nchar**, 또는 **nvarchar** 값을 입력 합니다. 문에 매개 변수가 없으면 NULL 값을 입력합니다.  
  
> [!NOTE]  
>  사용 하 여는 **ntext** 입력으로 문자열 값으로 *stmt* 에 매개 변수가 및 *scrollopt* PARAMETERIZED_STMT 값이 ON입니다.  
  
 *stmt*  
 커서 결과 집합을 정의합니다. *stmt* 호출에 대 한 필수 매개 변수 이며 프로그램 **ntext**, **nchar** 또는 **nvarchar** 값을 입력 합니다.  
  
> [!NOTE]  
>  규칙을 지정 하는 *stmt* 값은 예외와 sp_cursoropen에 대해와 동일 하는 *stmt* 문자열 데이터 형식 이어야 합니다 **ntext**합니다.  
  
 *옵션*  
 커서 결과 집합 열의 설명을 반환하는 선택적 매개 변수입니다. *옵션* 하려면 다음이 필요 **int** 값을 입력 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 스크롤 옵션입니다. *scrollopt* 다음 중 하나 필요로 하는 선택적 매개 변수 **int** 값을 입력 합니다.  
  
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
  
 요청 된 값에서 정의한 커서에 대 한 적절 한 수 있으므로 *stmt*,이 매개 변수 둘 다로 사용 입력 및 출력 합니다. 이러한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 적절한 값을 할당합니다.  
  
 *ccopt*  
 동시성 제어 옵션입니다. *ccopt* 다음 중 하나 필요로 하는 선택적 매개 변수 **int** 값을 입력 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS(이전의 LOCKCC)|  
|0x0004|**낙관적** (이전의 optcc)|  
|0x0008|OPTIMISTIC(이전의 OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 와 마찬가지로 *scrollpt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 요청 된 것에서 다른 값을 할당할 수 있습니다.  
  
## <a name="remarks"></a>주의  
 RPC 상태 매개 변수는 다음 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|0|성공|  
|0x0001|실패|  
|1FF6|메타데이터를 반환할 수 없습니다.<br /><br /> 참고:이 대 한 이유는 문에 결과 집합을 생성 하지 않습니다. 예를 들어는 INSERT 또는 DDL 문입니다.|  
  
## <a name="examples"></a>예  
 때 *stmt* 매개 변수화 및 *scrollopt* PARAMETERIZED_STMT 값이 ON 일 문자열의 형식은 다음과 같습니다.  
  
 {  *\<지역 변수 이름 >**\<데이터 유형 >* } [,... *n* ]  
  
## <a name="see-also"></a>관련 항목:  
 [sp_cursorexecute &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursoropen &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorunprepare &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursorunprepare-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

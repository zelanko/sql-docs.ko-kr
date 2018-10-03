---
title: sp_cursorexecute (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorexecute
- sp_cursorexecute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_execute
ms.assetid: 6a204229-0a53-4617-a57e-93d4afbb71ac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fcc62c09d42adb10f8984a8f48d8b70e2f5c78de
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47854041"
---
# <a name="spcursorexecute-transact-sql"></a>sp_cursorexecute(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  sp_cursorprepare가 만든 실행 계획을 기반으로 하여 커서를 만들고 채웁니다. Sp_cursorprepare와 결합 하는이 절차에서는 sp_cursoropen과 동일한 기능 하지만 두 단계로 분리 됩니다. sp_cursorexecute ID를 지정 하 여 호출 되는 tabular data TDS (stream) 패킷에서 4 =.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursorexecute prepared_handle, cursor  
    [ , scrollopt[ OUTPUT ]  
    [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,bound param][,...n]]]]]  
```  
  
## <a name="arguments"></a>인수  
 *prepared_handle*  
 준비 된 문의 *처리할* sp_cursorprepare에서 반환 된 값입니다. *prepared_handle* 필요로 하는 필수 매개 변수를 **int** 값을 입력 합니다.  
  
 *cursor*  
 SQL Server에서 생성하는 커서 식별자입니다. *커서* sp_cursorfetch와 같이 커서에 대해 작동 하는 모든 후속 프로시저에 제공 해야 하는 필수 매개 변수  
  
 *scrollopt*  
 스크롤 옵션입니다. *scrollopt* 필요한 선택적 매개 변수를 **int** 값을 입력 합니다. Sp_cursorexecute*scrollopt* 매개 변수는 sp_cursoropen과 같은 값 옵션입니다.  
  
> [!NOTE]  
>  PARAMETERIZED_STMT 값은 지원되지 않습니다.  
  
> [!IMPORTANT]  
>  경우는 *scrollopt* 값을 지정 하지, 기본값은 KEYSET입니다 관계 없이 *scrollopt* sp_cursorprepare에서 지정한 값입니다.  
  
 *ccopt*  
 통화 제어 옵션입니다. *ccopt* 필요한 선택적 매개 변수를 **int** 값을 입력 합니다. Sp_cursorexecute*ccopt* 매개 변수는 sp_cursoropen과 같은 값 옵션입니다.  
  
> [!IMPORTANT]  
>  경우는 *ccopt* 값을 지정 하지, 기본값은 OPTIMISTIC입니다 관계 없이 *ccopt* sp_cursorprepare에서 지정한 값입니다.  
  
 *행 개수*  
 AUTO_FETCH에 사용할 인출 버퍼 행 수를 나타내는 선택적 매개 변수입니다. 기본값은 20개 행입니다. *행 개수* 입력된 값과 반환 값으로 할당할 때 다르게 동작 합니다.  
  
|입력 값일 때|반환 값일 때|  
|--------------------|---------------------|  
|FAST_FORWARD 커서를 사용 하 여 AUTO_FETCH를 지정 하는 경우 *rowcount* 인출 버퍼에 배치할 행 수를 나타냅니다.|결과 집합의 행 수를 나타냅니다. 경우는 *scrollopt* AUTO_FETCH 값을 지정 하면 *rowcount* 는 인출 버퍼로 인출 된 행 수를 반환 합니다.|  
  
 *bound_param*  
 추가 매개 변수의 선택적 사용을 나타냅니다.  
  
> [!NOTE]  
>  5번째 매개 변수 다음의 모든 매개 변수는 문 계획에 입력 매개 변수로 전달됩니다.  
  
## <a name="code-return-value"></a>코드 반환 값  
 *행 개수* 다음 값을 반환할 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|-1|행 수를 알 수 없습니다.|  
|-n|비동기 채우기가 적용됩니다.|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="scrollopt-and-ccopt-parameters"></a>scrollopt 및 ccopt 매개 변수  
 *scrollopt* 하 고 *ccopt* 즉 문을 식별 하는 준비 된 핸들을 컴파일해야 하는 서버 캐시에 대 한 캐시 된 계획 선점 될 경우에 유용 합니다. 합니다 *scrollopt* 하 고 *ccopt* 매개 변수 값에 포함 되어 sp_cursorprepare로 원래 요청에서 보낸 값과 일치 해야 합니다.  
  
> [!NOTE]  
>  PARAMETERIZED_STMT를 할당 하지 말아야 *scrollopt*합니다.  
  
 일치하는 값을 제공하지 않으면 계획이 다시 컴파일되어 준비 및 실행 작업을 부정하게 됩니다.  
  
## <a name="rpc-and-tds-considerations"></a>RPC 및 TDS 고려 사항  
 커서 선택 목록 메타데이터가 TDS 스트림에 반환되도록 요청하기 위해 RPC RETURN_METADATA 입력 플래그를 1로 설정할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_cursoropen &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

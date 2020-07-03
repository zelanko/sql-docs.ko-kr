---
title: sp_cursorexecute (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 800e70591e4ebb508bd5edd6426d43bdc3a16987
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85869736"
---
# <a name="sp_cursorexecute-transact-sql"></a>sp_cursorexecute(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  sp_cursorprepare가 만든 실행 계획을 기반으로 하여 커서를 만들고 채웁니다. Sp_cursorprepare와 결합 된이 프로시저는 sp_cursoropen와 동일한 기능을 수행 하지만 두 단계로 분할 됩니다. sp_cursorexecute은 TDS (tabular data stream) 패킷에서 ID = 4를 지정 하 여 호출 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursorexecute prepared_handle, cursor  
    [ , scrollopt[ OUTPUT ]  
    [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,bound param][,...n]]]]]  
```  
  
## <a name="arguments"></a>인수  
 *prepared_handle*  
 Sp_cursorprepare에서 반환 된 준비 된 문 *핸들* 값입니다. *prepared_handle* 은 **int** 입력 값에 대해를 호출 하는 필수 매개 변수입니다.  
  
 *cursor*  
 SQL Server에서 생성하는 커서 식별자입니다. *커서* 는 커서에 대해 작동 하는 모든 후속 프로시저에 제공 해야 하는 필수 매개 변수입니다 (예: sp_cursorfetch  
  
 *scrollopt*  
 스크롤 옵션입니다. *scrollopt* 는 **int** 입력 값을 필요로 하는 선택적 매개 변수입니다. Sp_cursorexecute*scrollopt* 매개 변수는 sp_cursoropen에 대 한 값 옵션과 동일 합니다.  
  
> [!NOTE]  
>  PARAMETERIZED_STMT 값은 지원되지 않습니다.  
  
> [!IMPORTANT]  
>  *Scrollopt* 값을 지정 하지 않으면 sp_cursorprepare에 지정 된 *scrollopt* 값에 관계 없이 기본값은 키 집합입니다.  
  
 *ccopt*  
 통화 제어 옵션입니다. *ccopt* 는 **int** 입력 값을 필요로 하는 선택적 매개 변수입니다. Sp_cursorexecute*ccopt* 매개 변수는 sp_cursoropen에 대 한 값 옵션과 동일 합니다.  
  
> [!IMPORTANT]  
>  *Ccopt* 값을 지정 하지 않으면 sp_cursorprepare에 지정 된 *ccopt* 값에 관계 없이 기본값은 낙관적입니다.  
  
 *개수*  
 AUTO_FETCH에 사용할 인출 버퍼 행 수를 나타내는 선택적 매개 변수입니다. 기본값은 20개 행입니다. *행 개수* 는 입력 값과 반환 값으로 할당 될 때 다르게 동작 합니다.  
  
|입력 값일 때|반환 값일 때|  
|--------------------|---------------------|  
|FAST_FORWARD와 함께 AUTO_FETCH 지정 하면 커서 *rowcount* 는 인출 버퍼에 넣을 행 수를 나타냅니다.|결과 집합의 행 수를 나타냅니다. *Scrollopt* AUTO_FETCH 값이 지정 된 경우 *rowcount* 는 인출 버퍼에 인출 된 행 수를 반환 합니다.|  
  
 *bound_param*  
 추가 매개 변수의 선택적 사용을 나타냅니다.  
  
> [!NOTE]  
>  5번째 매개 변수 다음의 모든 매개 변수는 문 계획에 입력 매개 변수로 전달됩니다.  
  
## <a name="code-return-value"></a>코드 반환 값  
 *rowcount* 는 다음 값을 반환할 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|-1|행 수를 알 수 없습니다.|  
|-n|비동기 채우기가 적용됩니다.|  
  
## <a name="remarks"></a>설명  
  
## <a name="scrollopt-and-ccopt-parameters"></a>scrollopt 및 ccopt 매개 변수  
 *scrollopt* 및 *ccopt* 는 캐시 된 계획이 서버 캐시에 대해 선점 되는 경우에 유용 합니다. 즉, 문을 식별 하는 준비 된 핸들을 다시 컴파일해야 합니다. *Scrollopt* 및 *ccopt* 매개 변수 값은 sp_cursorprepare 하기 위해 원래 요청에서 전송 된 값과 일치 해야 합니다.  
  
> [!NOTE]  
>  *Scrollopt*에 PARAMETERIZED_STMT를 할당 하면 안 됩니다.  
  
 일치하는 값을 제공하지 않으면 계획이 다시 컴파일되어 준비 및 실행 작업을 부정하게 됩니다.  
  
## <a name="rpc-and-tds-considerations"></a>RPC 및 TDS 고려 사항  
 커서 선택 목록 메타데이터가 TDS 스트림에 반환되도록 요청하기 위해 RPC RETURN_METADATA 입력 플래그를 1로 설정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_cursoropen &#40;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Transact-sql&#41;sp_cursorfetch &#40;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

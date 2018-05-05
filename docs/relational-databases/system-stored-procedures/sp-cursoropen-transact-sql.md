---
title: sp_cursoropen (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursoropen
- sp_cursoropen_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoropen
ms.assetid: 16462ede-4393-4293-a598-ca88c48ca70b
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 87bdad8532b4f7c744971d846a142bf74466cd2e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spcursoropen-transact-sql"></a>sp_cursoropen(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  커서를 엽니다. sp_cursoropen은 커서 및 커서 옵션과 연결 된 SQL 문을 한 다음 커서를 채웁니다. sp_cursoropen의 조합에 해당 되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 DECLARE_CURSOR 및 OPEN 합니다. 이 프로시저는 TDS(Tabular Data Stream) 패킷에서 ID =2를 지정하여 호출합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursoropen cursor OUTPUT, stmt  
    [, scrollopt[ OUTPUT ] [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,boundparam][,...n]]] ]]  
```  
  
## <a name="arguments"></a>인수  
 *cursor*  
 SQL Server에서 생성하는 커서 식별자입니다. *커서* 는 *처리* sp_cursorfetch와 같이 커서와 관련 된 모든 후속 프로시저에 제공 해야 하는 값입니다. *커서* 은 필수 매개 변수는 **int** 값을 반환 합니다.  
  
 *커서* 여러 커서를 단일 데이터베이스 연결에서 활성화 될 수 있습니다.  
  
 *stmt*  
 커서 결과 집합을 정의하는 필수 매개 변수입니다. 올바른 사용 될 수 있습니다 (유니코드, 크기, 등)와 상관 없이 모든 문자열 형식의 모든 유효한 쿼리 문자열 (구문 및 바인딩) *stmt* 값 형식입니다.  
  
 *scrollopt*  
 스크롤 옵션입니다. *scrollopt* 다음 중 하나 필요로 하는 선택적 매개 변수 **int** 값을 입력 합니다.  
  
|Value|Description|  
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
  
 요청 된 값에서 정의한 커서에 적합 하지 않습니다. 있으므로 *stmt*,이 매개 변수 둘 다로 사용 입력 및 출력 합니다. 이러한 경우 SQL Server에서 적절한 값을 할당합니다.  
  
 *ccopt*  
 동시성 제어 옵션입니다. *ccopt* 다음 중 하나 필요로 하는 선택적 매개 변수 **int** 값을 입력 합니다.  
  
|Value|Description|  
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
  
 와 마찬가지로 *scrollopt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 요청 된 문자인 *ccopt* 값입니다.  
  
 *행 개수*  
 AUTO_FETCH에 사용할 인출 버퍼 행 수입니다. 기본값은 20개 행입니다. *행 개수* 입력된 값과 반환 값으로 할당할 때 다르게 동작 합니다.  
  
|입력 값일 때|반환 값일 때|  
|--------------------|---------------------|  
|때 AUTO_FETCH *scrollopt* 값이 지정 *rowcount* 인출 버퍼에 배치할 행 수를 나타냅니다.<br /><br /> 참고: > 0은 AUTO_FETCH를 지정 하 고 되거나 무시 하는 경우 유효한 값입니다.|경우는 제외 나타냅니다 결과의 행 수가 설정 된 *scrollopt* AUTO_FETCH 값을 지정 합니다.|  
  
-  
  
 *boundparam*  
 추가 매개 변수의 사용을 나타냅니다. *boundparam* 경우 지정 해야 하는 선택적 매개 변수는 *scrollopt* PARAMETERIZED_STMT 값이 ON으로 설정 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 오류가 발생하지 않으면 sp_cursoropen은 다음 값 중 하나를 반환합니다.  
  
 0  
 프로시저가 실행되었습니다.  
  
 0x0001  
 실행 중에 오류가 발생했으나 작업에서 오류를 발생시킬 만큼 심각하지는 않은 사소한 오류입니다.  
  
 0x0002  
 비동기 작업이 진행 중입니다.  
  
 0x0002  
 FETCH 작업이 진행 중입니다.  
  
 변수를 잠그기 위한  
 이 커서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 의해 할당 취소되었으며 사용할 수 없습니다.  
  
 오류가 발생하면 반환 값이 불일치할 수 있으며 정확도를 보장할 수 없습니다.  
  
 경우는 *rowcount* 반환 값으로는 다음 결과 집합이 발생 하는 매개 변수를 지정 합니다.  
  
 -1  
 행 수가 알 수 없는 상태이거나 적합하지 않는 경우 반환됩니다.  
  
 -n  
 비동기 채우기가 적용되는 경우 반환됩니다. 페치에 배치 된 행 수를 나타냅니다 때 버퍼는 *scrollopt* AUTO_FETCH 값을 지정 합니다.  
  
 RPC를 사용 중이면 반환 값은 다음과 같습니다.  
  
 0  
 프로시저가 성공했습니다.  
  
 1.  
 프로시저가 실패했습니다.  
  
 2  
 키 집합 커서가 비동기적으로 생성되고 있습니다.  
  
 16  
 빠른 정방향 커서가 자동으로 닫혔습니다.  
  
> [!NOTE]  
>  sp_cursoropen 프로시저가 성공적으로 실행되면 TDS 열 형식 정보(0xa0 및 0xa1 메시지)가 포함된 결과 집합과 RPC 반환 매개 변수가 전송됩니다. 프로시저가 실패하면 하나 이상의 RPC 오류 메시지가 전송됩니다. 두 경우 모두 행 데이터가 반환 될 및 *수행* 메시지 수는 0이 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 이전 버전을 사용 중인 경우 0xa0, 0xa1(SELECT 문의 표준 항목)이 0xa5 및 0xa4 토큰 스트림과 함께 반환됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 버전을 사용 중인 경우에는 0x81(SELECT 문의 표준 항목)이 0xa5 및 0xa4 토큰 스트림과 함께 반환됩니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="stmt-parameter"></a>stmt 매개 변수  
 경우 *stmt* 실행을 지정, 저장된 프로시저의 입력된 매개 변수는 하거나 것으로 정의의 일부로 상수는 *stmt* 문자열을 읽거나로 지정 된 *boundparam* 인수입니다. 이 방법을 사용하면 선언된 변수를 바인딩된 매개 변수로 전달할 수 있습니다.  
  
 허용 되는 내용의 *stmt* 매개 변수가 여부에 종속 된 *ccopt* ALLOW_DIRECT 반환 값 또는의 나머지 부분에 연결 되어 있는 *ccopt* 값, 즉:  
  
-   ALLOW_DIRECT가 지정 하지 않으면 하거나는 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 또는 EXECUTE 문이 단일 SELECT 문을 포함 하는 저장된 프로시저를 사용 해야 호출 합니다. SELECT 문은 커서; 서 적합 해야 합니다는 또한 즉, SELECT INTO 또는 FOR BROWSE 키워드를 포함할 수 없습니다.  
  
-   ALLOW_DIRECT를 지정하면 여러 문이 들어 있는 다른 저장 프로시저를 실행하는 문을 비롯한 여러 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 생성될 수 있습니다. SELECT 외의 문이나 SELECT INTO 또는 FOR BROWSE 키워드를 포함하는 SELECT 문은 단순히 실행되기만 하며 커서는 작성되지 않습니다. 여러 문의 일괄 처리에 포함된 SELECT 문의 경우에도 마찬가지입니다. SELECT 문이 커서에만 관련된 절을 포함하는 경우 해당 절은 무시됩니다. 예를 들어, 값 *ccopt* 는 0x2002 이면 이것은 대 한 요청:  
  
    -   커서로 정규화되는 SELECT 문이 하나뿐인 경우 스크롤 잠금이 적용된 커서 또는  
  
    -   여러 문, SELECT가 아닌 단일 문 또는 커서로 적합하지 않은 SELECT 문이 있는 경우 직접 문 실행  
  
## <a name="scrollopt-parameter"></a>scrollopt 매개 변수  
 처음 5 개 *scrollopt* 값 (KEYSEY, DYNAMIC, FORWARD_ONLY, STATIC, FAST_FORWARD)은 상호 배타적입니다.  
  
 PARAMETERIZED_STMT 및 CHECK_ACCEPTED_TYPES는 OR을 사용하여 첫 5개 값에 연결할 수 있습니다.  
  
 AUTO_FETCH 및 AUTO_CLOSE는 OR을 통해 FAST_FORWARD에 연결할 수 있습니다.  
  
 CHECK_ACCEPTED_TYPES가 ON 이면 마지막 5 개 중 하나 이상을 *scrollopt* 값 (KEYSET_ACCEPTABLE`,` DYNAMIC_ACCEPTABLE, FORWARD_ONLY_ACCEPTABLE, STATIC_ACCEPTABLE, FAST_FORWARD_ACCEPTABLE)도 ON 이어야 합니다.  
  
 STATIC 커서는 항상 READ_ONLY로 열립니다. 즉, 이 커서를 통해 기본 테이블을 업데이트할 수 없습니다.  
  
## <a name="ccopt-parameter"></a>ccopt 매개 변수  
 처음 4 개 *ccopt* 값 (READ_ONLY, SCROLL_LOCKS 및 두 OPTIMISTIC 값)은 함께 사용할 수 없습니다.  
  
> [!NOTE]  
>  처음 4 개 중 하나를 선택 *ccopt* 값 지정 커서는 읽기 전용 또는 잠금이나 낙관적 방법을 업데이트 손실을된 방지 하는 데 사용 됩니다. 경우는 *ccopt* 값 지정 하지 않으면, 기본값은 OPTIMISTIC입니다.  
  
 ALLOW_DIRECT 및 CHECK_ACCEPTED_TYPES는 OR을 사용하여 첫 4개 값에 연결할 수 있습니다.  
  
 UPDT_IN_PLACE는 OR을 통해 READ_ONLY, SCROLL_LOCKS 또는 두 OPTIMISTIC 값 중 하나에 연결할 수 있습니다.  
  
 CHECK_ACCEPTED_TYPES가 ON 이면 마지막 4 개 중 하나 이상을 *ccopt* 값 (READ_ONLY_ACCEPTABLE, SCROLL_LOCKS_ACCEPTABLE 및 두 OPTIMISTIC_ACCEPTABLE 값 중 하나)도 ON 이어야 합니다.  
  
 위치 지정된 UPDATE 및 DELETE 함수는 인출 버퍼 및 경우에만 내 에서만 수행할 수 있습니다는 *ccopt* 값이 SCROLL_LOCKS 또는 OPTIMISTIC입니다. 지정된 값이 SCROLL_LOCKS이면 작업 성공이 보장됩니다. 지정된 값이 OPTIMISTIC인 경우 행이 마지막으로 인출된 이후 변경되었으면 작업이 실패합니다.  
  
 작업이 실패하는 이유는 지정된 값이 OPTIMISTIC이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 결정한 대로 타임스탬프나 체크섬 값을 비교하여 낙관적 동시성 제어 기능이 수행되기 때문입니다. 이러한 행이 하나라도 일치하지 않으면 작업이 실패합니다.  
  
 UPDT_IN_PLACE를 반환 값으로 지정하면 결과가 다음과 같이 제어됩니다.  
  
-   고유한 인덱스가 포함된 테이블에서 현재 위치 업데이트를 수행할 때 설정하지 않으면 커서가 행을 작업 테이블에서 삭제하고 커서에서 사용하는 키 열 중 하나의 끝에 삽입하여 해당 열을 변경합니다.  
  
-   ON으로 설정하면 커서가 작업 테이블의 원래 행에서 키 열을 단순히 업데이트합니다.  
  
## <a name="boundparam-parameter"></a>bound_param 매개 변수  
 매개 변수 이름은 *paramdef* 코드에서 오류 메시지에 따라 PARAMETERIZED_STMT 지정 하는 경우. PARAMETERIZED_STMT가 지정되지 않은 경우에는 오류 메시지에 이름이 지정되지 않습니다.  
  
## <a name="rpc-considerations"></a>RPC 고려 사항  
 커서 선택 목록 메타데이터가 TDS 스트림에 반환되도록 요청하기 위해 RPC RETURN_METADATA 입력 플래그를 0x0001로 설정할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="boundparam-parameter"></a>bound_param 매개 변수  
 5번째 매개 변수 다음의 모든 매개 변수는 문 계획에 입력 매개 변수로 전달됩니다. 이러한 첫 번째 매개 변수는 다음 형식의 문자열이어야 합니다.  
  
 *{지역 변수 이름과 데이터 형식이} [, … n].*  
  
 후속 매개 변수를 대체할 값을 전달를 *지역 변수 이름* 문의 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_cursorfetch &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

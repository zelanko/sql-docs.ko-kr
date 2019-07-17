---
title: sp_cursorfetch (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorfetch
- sp_cursorfetch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorfetch
ms.assetid: 14513c5e-5774-4e4c-92e1-75cd6985b6a3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4635bffa5b5b681d0ff202c4231c4d8b8d10ae26
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108507"
---
# <a name="spcursorfetch-transact-sql"></a>sp_cursorfetch(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스에서 하나 이상의 행 버퍼를 인출합니다. 이 버퍼의 행 그룹에는 커서의 이라고 *인출 버퍼*합니다. sp_cursorfetch가 ID를 지정 하 여 호출 = 7 tabular data TDS (stream) 패킷에서을 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursorfetch cursor  
    [ , fetchtype[ , rownum [ , nrows] ]]   
```  
  
## <a name="arguments"></a>인수  
 *cursor*  
 *처리할* 에서 생성 된 값 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_cursoropen에서 반환 합니다. *커서* 필요로 하는 필수 매개 변수를 **int** 값을 입력 합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 주의 섹션을 참조하십시오.  
  
 *fetchtype*  
 인출할 커서 버퍼를 지정합니다. *fetchtype* 다음 정수 입력된 값 중 하나 필요로 하는 선택적 매개 변수입니다.  
  
|값|이름|설명|  
|-----------|----------|-----------------|  
|0x0001|FIRST|첫 번째 버퍼를 인출 *nrows* 행. 하는 경우 *nrows* 0 커서는 결과 집합 앞에 배치 하 고 아무 행도 반환 합니다.|  
|0x0002|NEXT|다음 버퍼를 인출 *nrows* 행.|  
|0x0004|PREV|이전 버퍼를 인출 *nrows* 행.<br /><br /> 참고: FORWARD_ONLY는 한 방향 스크롤만 지원 하므로 오류 메시지가 반환 FORWARD_ONLY 커서에 대해 PREV를 사용 합니다.|  
|0x0008|LAST|마지막 버퍼를 인출 *nrows* 행. 하는 경우 *nrows* 0 이면 커서가 결과 집합 후 아무 행도 반환 합니다.<br /><br /> 참고: FORWARD_ONLY는 한 방향 스크롤만 지원 하므로 오류 메시지가 반환 FORWARD_ONLY 커서에 대해 LAST를 사용 합니다.|  
|0x10|ABSOLUTE|버퍼를 인출 *nrows* 사용 하 여 시작 하는 행의 *rownum* 행입니다.<br /><br /> 참고: FORWARD_ONLY는 한 방향 스크롤만 지원 하므로 오류 메시지가 반환 동적 커서 또는 FORWARD_ONLY 커서에 대해 ABSOLUTE를 사용 합니다.|  
|0x20|RELATIVE|버퍼를 인출 합니다 *nrows* 으로 지정 된 행부터 행을 *rownum* 현재 블록의 첫 번째 행의 행 값입니다. 이 예에서 *rownum* 음수가 될 수 있습니다.<br /><br /> 참고: FORWARD_ONLY는 한 방향 스크롤만 지원 하므로 오류 메시지가 반환 FORWARD_ONLY 커서에 대해 RELATIVE를 사용 합니다.|  
|0x80|REFRESH|기본 테이블의 버퍼를 다시 채웁니다.|  
|0x100|INFO|커서에 대한 정보를 검색합니다. 이 정보를 사용 하 여 반환 되는 *rownum* 하 고 *nrows* 매개 변수. 따라서 정보 지정 되 면 *rownum* 하 고 *nrows* 출력 매개 변수가 됩니다.|  
|0x200|PREV_NOADJUST|PREV와 같이 사용되지만 결과 집합 맨 위가 중간에 나오면 결과가 달라질 수 있습니다.|  
|0x400|SKIP_UPDT_CNCY|다른 하나를 사용 하 여 사용 해야 합니다 *fetchtype* INFO 제외 값입니다.|  
  
> [!NOTE]  
>  0x40 값은 지원되지 않습니다.  
  
 자세한 내용은 이 항목의 뒷부분에 나오는 주의 섹션을 참조하십시오.  
  
 *rownum*  
 ABSOLUTE 및 INFO의 행 위치를 지정 하는 데 사용 되는 선택적 매개 변수 *fetchtype* 입력 또는 출력 중 하나 또는 둘 다에 대 한 정수 값만을 사용 하 여 값입니다. *rownum* 의 행 오프셋 역할을 *fetchtype* 비트 값 RELATIVE입니다. *rownum* 다른 모든 값에 대해 무시 됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 주의 섹션을 참조하십시오.  
  
 *nrows*  
 인출할 행 수를 지정하는 데 사용되는 선택적 매개 변수입니다. 하는 경우 *nrows* 지정 하지 않으면 기본값은 20 개 행입니다. 데이터를 반환 하지 않고 위치를 설정 하려면 값 0 지정 합니다. 때 *nrows* 에 적용 되는 *fetchtype* 해당 쿼리에서 행의 총 수를 반환 정보 쿼리.  
  
> [!NOTE]  
>  *nrows* 새로 고침에서 무시 됩니다 *fetchtype* 비트 값입니다.  
>   
>  자세한 내용은 이 항목의 뒷부분에 나오는 주의 섹션을 참조하십시오.  
  
## <a name="return-code-values"></a>반환 코드 값  
 비트 값 INFO를 지정할 때 반환될 수 있는 값이 다음 표에 나와 있습니다.  
  
> [!NOTE]  
>  :   반환 되는 경우 버퍼의 내용이 그대로 유지 됩니다.  
  
|*\<rownum>*|설정 값|  
|------------------|------------|  
|열리지 않는 경우|0|  
|결과 집합 앞에 배치되는 경우|0|  
|결과 집합 뒤에 배치되는 경우|-1|  
|KEYSET 및 STATIC 커서의 경우|결과 집합에서 현재 위치에서 절대 행 수|  
|DYNAMIC 커서의 경우|1|  
|ABSOLUTE의 경우|-1은 집합의 마지막 행을 반환합니다.<br /><br /> -2는 집합의 마지막에서 두 번째 행 등을 반환합니다.<br /><br /> 참고: 둘 이상의 행이 경우 가져올 요청 된 경우 결과 집합의 마지막 두 행이 반환 됩니다.|  
  
|*\<nrows>*|설정 값|  
|-----------------|------------|  
|열리지 않는 경우|0|  
|KEYSET 및 STATIC 커서의 경우|일반적으로는 현재 키 집합 크기입니다.<br /><br /> **-m** 커서가 비동기 만들기 상태에 있는 경우 *m* 이 지점에 있는 행이 있습니다.|  
|DYNAMIC 커서의 경우|-1|  
  
## <a name="remarks"></a>설명  
  
## <a name="cursor-parameter"></a>cursor 매개 변수  
 인출 작업이 수행되기 전까지 커서의 기본 위치는 결과 집합의 첫 번째 행 앞입니다.  
  
## <a name="fetchtype-parameter"></a>fetchtype 매개 변수  
 Skip_upd_cncy를 합니다 *fetchtype* 값은 함께 사용할 수 없습니다.  
  
 SKIP_UPDT_CNCY를 지정하면 행을 인출하거나 새로 고칠 때 타임스탬프 열 값이 키 집합 테이블에 기록되지 않습니다. 키 집합 행을 업데이트하는 경우 타임스탬프 열의 값은 이전 값으로 유지됩니다. 키 집합 행을 삽입하는 경우에는 타임스탬프 열의 값이 정의되지 않습니다.  
  
 KEYSET 커서의 경우 이는 키 집합 테이블의 값이 건너뛰지 않는 마지막 FETCH(수행하는 경우) 중에 설정됨을 의미하며, 그 외의 경우에는 값이 채우기 중에 설정됩니다.  
  
 DYNAMIC 커서의 경우 이는 새로 고침과 함께 건너뛰기를 수행하는 경우 KEYSET과 같은 결과가 생성됨을 의미합니다. 다른 모든 인출 유형의 경우에는 키 집합 테이블이 잘립니다. 즉, 행이 삽입되는 중이며 타임스탬프 열의 값은 정의되지 않습니다. 따라서 DYNAMIC 커서에 대해 sp_cursorfetch를 실행할 때는 REFRESH 외의 작업에 대해 SKIP_UPDT_CNCY를 사용하지 않아야 합니다.  
  
 요청한 커서 위치가 결과 집합을 벗어나서 인출 작업이 실패하는 경우에는 커서 위치가 마지막 행 바로 다음으로 설정됩니다. 요청한 커서 위치가 결과 집합 앞에 배치되어 있어서 인출 작업이 실패하는 경우에는 커서 위치가 첫 번째 행 바로 앞으로 설정됩니다.  
  
## <a name="rownum-parameter"></a>rownum 매개 변수  
 사용 하는 경우 *rownum*, 지정된 된 행부터 버퍼가 채워집니다.  
  
 합니다 *fetchtype* 값의 위치를 절대 참조 *rownum* 전체 결과 내에서 설정 합니다. ABSOLUTE의 값이 음수이면 작업에서 결과 집합의 끝에서부터 행을 카운트하도록 지정됩니다.  
  
 합니다 *fetchtype* 상대 위치로 참조 값 *rownum* 현재 버퍼의 시작 부분에 커서의 위치를 기준으로 합니다. RELATIVE의 값이 음수이면 커서가 현재 커서 위치에서 뒤로 이동하도록 지정됩니다.  
  
## <a name="nrows-parameter"></a>nrows 매개 변수  
 합니다 *fetchtype* 값 REFRESH 및 INFO는이 매개 변수를 무시 합니다.  
  
 지정 하는 경우는 *fetchtype* 있는 첫 번째 값을 *nrow* 값을 0으로 커서는 인출 버퍼에 행이 없는 결과 집합 앞에 배치 됩니다.  
  
 지정 하는 경우는 *fetchtype* last 값을 *nrow* 값을 0으로 커서는 현재 인출 버퍼에 행이 없는 결과 집합 뒤에 배치 됩니다.  
  
 에 대 한 합니다 *fetchtype* 다음, PREV, ABSOLUTE, RELATIVE 및 PREV_NOADJUST의 값을 *nrow* 0 값이 올바르지 않습니다.  
  
## <a name="rpc-considerations"></a>RPC 고려 사항  
 RPC 반환 상태는 키 집합 크기 매개 변수가 최종인지 여부, 즉 비동기 방식으로 채워지고 있는 항목이 키 집합인지 임시 테이블인지를 나타냅니다.  
  
 RPC 상태 매개 변수는 다음 표에 나와 있는 값 중 하나로 설정됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|0|프로시저가 실행되었습니다.|  
|0x0001|프로시저가 실패했습니다.|  
|0x0002|논리적으로는 인출이 결과 앞에 와야 하지만 음의 방향 인출로 인해 커서 위치가 결과 집합 시작 부분으로 설정되었습니다.|  
|0x10|빠른 정방향 커서가 자동으로 닫혔습니다.|  
  
 행이 일반적인 결과 집합, 즉 열 형식(0x2a), 행(0xd1), 완료(0xfd) 순으로 반환됩니다. 메타 데이터 토큰 즉, sp_cursoropen에 대해 지정 된 대로 동일한 형식으로 전송 됩니다. 0x81, 0xa5 및 0xa4 SQL Server 7.0 사용자 등에 대 한 합니다. 행 상태 표시기는 BROWSE 모드와 비슷하게 각 행 끝에 숨겨진 열로 전송됩니다. 열 이름은 rowstat이고 데이터 형식은 INT4입니다. 이 rowstat 열은 다음 표에 있는 값 중 하나를 포함할 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|0x0001|FETCH_SUCCEEDED|  
|0x0002|FETCH_MISSING|  
  
 TDS 프로토콜은 이전 열을 보내지 않고 후행 상태 열을 보내는 방법을 제공하지 않으므로, 누락된 열에 대해서는 더미 데이터가 전송됩니다. 이 경우 Null 허용 필드는 Null로 설정되고 고정 길이 필드는 0, 빈 값, 해당 열의 기본값 중 적절한 값으로 설정됩니다.  
  
 DONE 행 개수는 항상 0이 됩니다. DONE 메시지는 실제 결과 집합 행 개수를 포함하며, 오류 또는 정보 메시지가 TDS 메시지 사이에 나타날 수 있습니다.  
  
 커서의 선택 목록에 대한 메타데이터가 TDS 스트림에 반환되도록 요청하려면 RPC RETURN_METADATA 입력 플래그를 1로 설정합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-prev-to-change-a-cursor-position"></a>A. PREV를 사용하여 커서 위치 변경  
 h2 커서가 다음과 같은 내용의 결과 집합을 생성하며 현재 위치는 아래와 같다고 가정해 봅니다.  
  
```  
row 1 contents      
row 2 contents  
row 3 contents  
row 4 contents  <-- current position  
row 5 contents   
row 6 contents  
```  
  
 다음으로, 인 sp_cursorfetch PREV 있는 *nrows* 값 5는 결과 집합의 첫 번째 행 앞 커서 두 행은 논리적으로 배치 합니다. 이 경우 커서가 첫 행에서 시작하도록 조정되며 요청한 행 수가 반환됩니다. 따라서 PRIOR 인출 버퍼에 있던 행이 반환되는 경우가 많습니다.  
  
> [!NOTE]  
>  RPC 상태 매개 변수가 2로 설정된 경우 위와 같은 현상이 발생합니다.  
  
### <a name="b-using-prevnoadjust-to-return-fewer-rows-than-prev"></a>2\. PREV_NOADJUST를 사용하여 PREV보다 적은 행 수 반환  
 PREV_NOADJUST는 반환하는 행 블록에서 현재 커서 위치나 그 뒤에 있는 행을 포함하지 않습니다. PREV_NOADJUST 경우 PREV가 현재 위치 뒤 행을 반환 하는 위치에서 요청 된 수보다 적은 수의 행을 반환 합니다 *nrows*합니다. 현재 지정 된 위치 예제의 경우 PREV를 적용 하면 이전에 sp_cursorfetch (h2, 4, 1, 5) 다음 행을 인출 합니다.  
  
```  
row1 contents   
row2 contents  
row3 contents  
row4 contents  
row5 contents  
```  
  
 그러나 경우 PREV_NOADJUST를 적용 하면 sp_cursorfetch (h2, 512, 6, 5)는 다음 행만 인출 합니다.  
  
```  
row1 contents   
row2 contents  
row3 contents   
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_cursoropen &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

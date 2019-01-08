---
title: sp_cursor (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_TSQL
- sp_cursor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor
ms.assetid: 41ade0ca-5f11-469d-bd4d-c8302ccd93b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e3277e64e4c4e04e270298d3532ebc0c2b1f93c5
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210522"
---
# <a name="spcursor-transact-sql"></a>sp_cursor(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 위치 업데이트를 요청합니다. 이 프로시저는 커서의 인출 버퍼 내에서 하나 이상의 행에 대해 작업을 수행합니다. sp_cursor가 ID를 지정 하 여 호출 = 테이블 형식 데이터 TDS (stream) 패킷의 1입니다.  
  
||  
|-|  
|**적용 대상**: SQL Server ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursor  cursor, optype, rownum, table  
    [ , value[...n]]]  
```  
  
## <a name="arguments"></a>인수  
 *cursor*  
 커서 핸들입니다. *커서* 필요로 하는 필수 매개 변수를 **int** 값을 입력 합니다. *커서* 되는 *처리* 값 SQL Server에서 생성 하 고 sp_cursoropen 프로시저에서 반환 됩니다.  
  
 *optype*  
 커서가 수행할 작업을 지정하는 필수 매개 변수입니다. *optype* 다음 중 하나 필요로 **int** 값을 입력 합니다.  
  
|값|이름|Description|  
|-----------|----------|-----------------|  
|0X0001|UPDATE|인출 버퍼에서 하나 이상의 행을 업데이트하는 데 사용됩니다.  에 지정 된 행 *rownum* 다시 액세스 하 고 업데이트 합니다.|  
|0x0002|Delete|인출 버퍼에서 하나 이상의 행을 삭제하는 데 사용됩니다. 에 지정 된 행 *rownum* 다시 액세스 및 삭제 합니다.|  
|0X0004|INSERT|SQL을 작성 하지 않고 데이터를 삽입 **삽입** 문입니다.|  
|0X0008|REFRESH|기본 테이블로 버퍼를 다시 채우는 데 사용되며, 낙관적 동시성 제어로 인해 업데이트나 삭제가 실패하는 경우 또는 UPDATE 후에 행을 새로 고치는 데 사용할 수 있습니다.|  
|0X10|LOCK|SQL Server U-잠금을 얻기 위해 지정된 된 행이 포함 된 페이지에 발생 합니다. 이 잠금은 S 잠금과는 호환되지만 X 잠금 또는 기타 U 잠금과는 호환되지 않습니다. 단기 잠금을 구현하는 데 사용할 수 있습니다.|  
|0X20|SETPOSITION|DELETE 또는 UPDATE 문을 배치 프로그램은 후속 SQL Server를 실행 하려는 경우에 사용 됩니다.|  
|0X40|ABSOLUTE|UPDATE 또는 DELETE와 함께 사용해야 합니다.  ABSOLUTE는 KEYSET 커서와 함께 사용해야 하며, DYNAMIC 커서의 경우에는 무시되고 STATIC 커서는 업데이트할 수 없습니다.<br /><br /> 참고: 인출되지 않은 키 집합의 행에 대해 ABSOLUTE를 지정하면 작업에서 동시성 검사가 실패할 수 있으며 반환 결과를 보장할 수 없습니다.|  
  
 *rownum*  
 커서가 작업을 수행하거나 업데이트 또는 삭제할 인출 버퍼의 행을 지정합니다.  
  
> [!NOTE]  
>  이 작업은 RELATIVE, NEXT 또는 PREVIOUS 인출 작업의 시작 지점이나 sp_cursor를 사용하여 수행하는 업데이트 또는 삭제에는 영향을 주지 않습니다.  
  
 *rownum* 필요로 하는 필수 매개 변수를 **int** 값을 입력 합니다.  
  
 1  
 인출 버퍼의 첫 번째 행을 나타냅니다.  
  
 2  
 인출 버퍼의 두 번째 행을 나타냅니다.  
  
 3, 4, 5  
 세 번째 행 등 번호 순서대로 해당 행을 나타냅니다.  
  
 n  
 인출 버퍼의 n번째 행을 나타냅니다.  
  
 0  
 인출 버퍼의 모든 행을 나타냅니다.  
  
> [!NOTE]  
>  업데이트, 삭제, 새로 고침 또는 잠금을 사용에만 유효 *optype* 값입니다.  
  
 *table*  
 테이블 이름 테이블을 식별 하는 *optype* 커서 정의 조인이 포함 되거나 모호한 열 이름을 반환 하는 경우에 적용 합니다 *값* 매개 변수. 특정 테이블을 지정하지 않으면 FROM 열의 첫 테이블이 기본적으로 사용됩니다. *테이블* 문자열 입력된 값을 필요로 하는 선택적 매개 변수입니다. 문자열은 원하는 문자나 UNICODE 데이터 형식으로 지정할 수 있습니다. *테이블* 다중 파트 테이블 이름일 수 있습니다.  
  
 *value*  
 값을 삽입하거나 업데이트하는 데 사용됩니다. 합니다 *값* 문자열 매개 변수는 UPDATE 및 INSERT에만 사용 됩니다 *optype* 값입니다. 문자열은 원하는 문자나 UNICODE 데이터 형식으로 지정할 수 있습니다.  
  
> [!NOTE]  
>  매개 변수 이름은 *값* 사용자가 지정할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 RPC를 사용할 때는 버퍼 번호가 0 사용 하 여 위치 지정된 DELETE 또는 UPDATE 작업 인 DONE 메시지를를 반환 합니다는 *rowcount* 인출 버퍼의 모든 행에 대해 1 (성공) 또는 0 (실패).  
  
## <a name="remarks"></a>Remarks  
  
## <a name="optype-parameter"></a>optype 매개 변수  
 SETPOSITION UPDATE, DELETE, 새로 고침 또는 LOCK과 조합을 제외 하 고 UPDATE 또는 DELETE를 사용 하 여 절대 또는 합니다 *optype* 값은 함께 사용할 수 없습니다.  
  
 UPDATE 값의 SET 절에서 생성 되는 *값* 매개 변수입니다.  
  
 INSERT를 사용 하는 이점은 *optype* 값은 방지할 수 있습니다 문자가 아닌 데이터 삽입을 위해 문자 형식으로 변환 합니다. 값은 UPDATE와 같은 방식으로 지정됩니다. 필수 열이 포함되어 있지 않으면 INSERT는 실패합니다.  
  
-   SETPOSITION 값은 RELATIVE, NEXT 또는 PREVIOUS 인출 작업의 시작 지점이나 sp_cursor 인터페이스를 사용하여 수행하는 업데이트 또는 삭제에는 영향을 주지 않습니다. 인출 버퍼에서 행을 지정하지 않는 모든 숫자의 위치는 1로 설정되고 오류는 반환되지 않습니다. 위치 다음 sp_cursorfetch 작업, T-SQL 일까 지 적용 됩니다 SETPOSITION을 실행 한 후 **인출** 작업 또는 sp_cursor SETPOSITION 작업을 같은 커서를 통해. 후속 sp_cursorfetch 작업은 커서 위치를 새 인출 버퍼의 첫 번째 행으로 설정하는 반면, 다른 커서 호출은 위치 값에 영향을 주지 않습니다. 위치 값을 마지막으로 수정된 행으로 설정하기 위해 REFRESH, UPDATE, DELETE 또는 LOCK을 사용하여 SETPOSITION을 OR 절에 연결할 수 있습니다.  
  
 인출 버퍼의 행을 통해 지정 되지 않은 경우는 *rownum* 매개 변수를 반환 하는 오류 없이 1로 위치 설정 됩니다. 위치가 설정되고 나면 같은 커서에서 다음 sp_cursorfetch 작업, T-SQL FETCH 작업 또는 sp_cursor SETPOSITION 작업을 수행할 때까지는 해당 위치가 적용된 상태로 유지됩니다.  
  
 커서 위치를 마지막으로 수정된 행으로 설정하기 위해 REFRESH, UPDATE, DELETE 또는 LOCK을 사용하여 SETPOSITION을 OR 절에 연결할 수 있습니다.  
  
## <a name="rownum-parameter"></a>rownum 매개 변수  
 지정 된 *rownum* 매개 변수는 인출 버퍼 내의 행 수가 아니라 키 집합 내의 행 수로 해석할 수 있습니다. 사용자는 동시성 제어가 유지되는지를 확인해야 합니다. 즉, SCROLL_LOCKS 커서에 대해 지정된 행에서 독립적으로 잠금을 유지해야 합니다. 이는 트랜잭션을 통해 수행할 수 있습니다. OPTIMISTIC 커서의 경우에는 이 작업을 수행하려면 이전에 행을 인출했어야 합니다.  
  
## <a name="table-parameter"></a>table 매개 변수  
 경우는 *optype* 값이 업데이트 또는 삽입 하 고 전체 업데이트 또는 삽입 문이으로 제출 되는 *값* 매개 변수, 지정 된 값 *테이블* 무시 됩니다.  
  
> [!NOTE]  
>  뷰와 관련해서는 뷰에 참가여하는 테이블 하나만 수정할 수 있습니다. 합니다 *값* 매개 변수 열 이름은 뷰의 열 이름을 반영 해야 하지만 테이블 이름 (이 경우 sp_cursor는 뷰 이름을 바꿉니다) 기본 테이블 이름일 수 있습니다.  
  
## <a name="value-parameter"></a>value 매개 변수  
 규칙을 사용 하 여 두 개의 대안이 *값* 인수 섹션에서 설명한 것 처럼:  
  
1.  이름을 사용할 수 '\@'에 대 한 명명 된 선택 목록의 열 이름에 붙일 *값* 매개 변수입니다. 이 이름을 사용하는 경우 데이터 변환이 필요하지 않을 수도 있다는 이점이 있습니다.  
  
2.  매개 변수를 사용 하 여 전체 UPDATE 또는 INSERT 문을 제출 하거나 여러 매개 변수를 사용 하 여 SQL Server에서 전체 문으로 작성 하는 UPDATE 또는 INSERT 문의 부분을 제출할 수 있습니다. 이 작업의 예는 이 항목 뒷부분의 예 섹션에 나와 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="alternative-value-parameter-uses"></a>다른 value 매개 변수 사용 방식  
 UPDATE의 경우:  
  
 단일 매개 변수를 사용하는 경우 다음 구문을 사용해 UPDATE 문을 제출할 수 있습니다.  
  
 `[ [ UPDATE <table name> ] SET ] {<column name> = expression} [,...n]`  
  
> [!NOTE]  
>  하는 경우 업데이트 \<테이블 이름 > 지정 된 값에 대 한 합니다 *테이블* 매개 변수는 무시 합니다.  
  
 여러 매개 변수를 사용하는 경우에는 첫 번째 매개 변수가 다음 형식의 문자열이어야 합니다.  
  
 `[ SET ] <column name> = expression  [,...n]`  
  
 그리고 후속 매개 변수는 다음 형식이어야 합니다.  
  
 `<column name> = expression  [,...n]`  
  
 이 경우에 \<테이블 이름 > 생성 된 update 문을 지정 했거나 기본값으로 합니다 *테이블* 매개 변수입니다.  
  
 INSERT의 경우:  
  
 단일 매개 변수를 사용하는 경우 다음 구문을 사용해 INSERT 문을 제출할 수 있습니다.  
  
 `[ [ INSERT [INTO] <table name> ] VALUES ] ( <expression> [,...n] )`  
  
> [!NOTE]  
>  경우 삽입  *\<테이블 이름 >* 지정 된 값에 대 한 합니다 *테이블* 매개 변수는 무시 합니다.  
  
 여러 매개 변수를 사용하는 경우에는 첫 번째 매개 변수가 다음 형식의 문자열이어야 합니다.  
  
 `[ VALUES ( ] <expression>  [,...n]`  
  
 그리고 후속 매개 변수는 다음 형식이어야 합니다.  
  
 `expression [,...n]`  
  
 단, VALUES를 지정한 경우는 예외입니다. 이 경우에는 마지막 식 다음에 후행 ")"가 있어야 합니다. 이 경우에  *\<테이블 이름 >* 생성 된 UPDATE 문을 지정 했거나 기본값으로 합니다 *테이블* 매개 변수입니다.  
  
> [!NOTE]  
>  매개 변수 하나를 명명된 매개 변수인 "`@VALUES`"로 제출할 수 있습니다. 이 경우 다른 명명된 매개 변수는 사용할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_cursoropen &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

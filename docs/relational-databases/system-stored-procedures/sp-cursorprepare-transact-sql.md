---
title: sp_cursorprepare (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_prepare
ms.assetid: 6207e110-f4bf-4139-b3ec-b799c9cb3ad7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2719e330ec2fde61b91ca11ef93784983c6c418c
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165905"
---
# <a name="sp_cursorprepare-transact-sql"></a>sp_cursorprepare(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  커서 문이나 일괄 처리를 실행 계획으로 컴파일하되 커서를 만들지는 않습니다. 컴파일된 문은 나중에 sp_cursorexecute에서 사용할 수 있습니다. Sp_cursorexecute와 결합 된이 프로시저는 sp_cursoropen와 동일한 기능을 수행 하지만 두 단계로 분할 됩니다. sp_cursorprepare은 TDS (tabular data stream) 패킷에서 ID = 3을 지정 하 여 호출 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursorprepare prepared_handle OUTPUT, params , stmt , options  
    [ , scrollopt[ , ccopt]]  
```  
  
## <a name="arguments"></a>인수  
 *prepared_handle*  
 정수 값을 반환 하는 SQL Server 생성 준비 *핸들* 식별자입니다.  
  
> [!NOTE]  
>  그런 다음 *prepared_handle* 는 커서를 열기 위해 sp_cursorexecute 프로시저에 제공 됩니다. 작성된 핸들은 로그오프하거나 sp_cursorunprepare 프로시저를 통해 명시적으로 핸들을 제거할 때까지 존재합니다.  
  
 *params*  
 매개 변수가 있는 문을 식별합니다. 변수의 매개 변수 정의는 문에서 매개 변수 표식을 *대체 합니다.* *params* 는 **ntext**, **nchar**또는 **nvarchar** 입력 값을 호출 하는 필수 매개 변수입니다. 문에 매개 변수가 없으면 NULL 값을 입력합니다.  
  
> [!NOTE]  
>  *Stmt* 매개 변수화 되 고 *scrollopt* PARAMETERIZED_STMT 값이 ON 인 경우 **ntext** 문자열을 입력 값으로 사용 합니다.  
  
 *stmt*  
 커서 결과 집합을 정의합니다. *Stmt* 매개 변수는 필수 이며 **ntext**, **nchar** 또는 **nvarchar** 입력 값에 대해를 호출 합니다.  
  
> [!NOTE]  
>  *Stmt* 값을 지정 하는 규칙은 sp_cursoropen의 경우와 동일 합니다. 단, *stmt* 문자열 데이터 형식은 **ntext**여야 합니다.  
  
 *options*  
 커서 결과 집합 열의 설명을 반환하는 선택적 매개 변수입니다. *옵션* 에는 다음 **int** 입력 값이 필요 합니다.  
  
|Value|설명|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 스크롤 옵션입니다. *scrollopt* 는 다음 **int** 입력 값 중 하나를 필요로 하는 선택적 매개 변수입니다.  
  
|Value|설명|  
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
  
 요청 된 값이 *stmt*에 의해 정의 된 커서에 적합 하지 않을 수 있기 때문에이 매개 변수는 입력 및 출력 모두로 사용 됩니다. 이러한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 적절한 값을 할당합니다.  
  
 *ccopt*  
 동시성 제어 옵션입니다. *ccopt* 는 다음 **int** 입력 값 중 하나를 필요로 하는 선택적 매개 변수입니다.  
  
|Value|설명|  
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
  
 *Scrollpt*와 마찬가지로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 요청한 것과 다른 값을 할당할 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 RPC 상태 매개 변수는 다음 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|0|성공|  
|0x0001|실패|  
|1FF6|메타데이터를 반환할 수 없습니다.<br /><br /> 참고:이 이유는 문이 결과 집합을 생성 하지 않기 때문입니다. 예를 들어 INSERT 또는 DDL 문입니다.|  
  
## <a name="examples"></a>예  
  다음은 sp_cursorprepare 및를 사용 하는 예제 sp_cursorexecute

```sql
declare @handle int , @p5 int, @p6 int
exec sp_cursorprepare @handle OUTPUT, 
    N'@dbid int', 
    N'select * from sys.databases where database_id < @dbid',
    1,
    @p5 output,
    @p6 output


declare @p1 int  
set @P1 = @handle 
declare @p2 int   
declare @p3 int  
declare @p4 int  
set @P6 = 4 
exec sp_cursorexecute @p1, @p2 OUTPUT, @p3 output , @p4 output, @p5 OUTPUT, @p6

exec sp_cursorfetch @P2

exec sp_cursorunprepare @handle
exec sp_cursorclose @p2
```
 
 *Stmt* 매개 변수화 되 고 *scrollopt* PARAMETERIZED_STMT 값이 ON 이면 문자열 형식은 다음과 같습니다.  
  
 { *\<지역 변수 이름 > * *\<데이터 형식 >* } [ ,... *n* ]  
  
## <a name="see-also"></a>관련 항목:  
 [ &#40;transact-sql&#41;  sp_cursorexecute](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)  
 [ &#40;transact-sql&#41;  sp_cursoropen](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
 [ &#40;transact-sql&#41;  sp_cursorunprepare](../../relational-databases/system-stored-procedures/sp-cursorunprepare-transact-sql.md)  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

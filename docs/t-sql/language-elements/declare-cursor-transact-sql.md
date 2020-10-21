---
description: DECLARE CURSOR(Transact-SQL)
title: DECLARE CURSOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECLARE_CURSOR_TSQL
- CURSOR_TSQL
- DECLARE CURSOR
- CURSOR
dev_langs:
- TSQL
helpviewer_keywords:
- DECLARE CURSOR statement
- cursors [SQL Server], attributes
- local cursors [SQL Server]
- nesting cursors
- Transact-SQL cursors, attributes
- global cursors [SQL Server]
ms.assetid: 5a3a27aa-03e8-4c98-a27e-809282379b21
author: rothja
ms.author: jroth
ms.openlocfilehash: 4a75da0d64957e87997e65fd135c332065a5fa31
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196638"
---
# <a name="declare-cursor-transact-sql"></a>DECLARE CURSOR(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  스크롤 동작, 커서가 작동하는 결과 집합을 구축하는 데 사용되는 쿼리 등 [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서의 특성을 정의합니다. `DECLARE CURSOR`는 ISO 표준 기반의 구문과 [!INCLUDE[tsql](../../includes/tsql-md.md)] 확장 세트를 사용하는 구문을 모두 허용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
ISO Syntax  
DECLARE cursor_name [ INSENSITIVE ] [ SCROLL ] CURSOR   
     FOR select_statement   
     [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]  
[;]  
Transact-SQL Extended Syntax  
DECLARE cursor_name CURSOR [ LOCAL | GLOBAL ]   
     [ FORWARD_ONLY | SCROLL ]   
     [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
     [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
     [ TYPE_WARNING ]   
     FOR select_statement   
     [ FOR UPDATE [ OF column_name [ ,...n ] ] ]  
[;]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *cursor_name*  
 정의된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서의 이름입니다. *cursor_name*은 식별자에 대한 규칙을 따라야 합니다.  
  
 INSENSITIVE  
 커서에서 사용할 데이터를 임시로 복사해 주는 커서를 정의합니다. 커서에 대한 모든 요청은 **tempdb**의 임시 테이블에서 응답하므로 기본 테이블에 대한 수정 내용은 해당 커서에 대한 인출에서 반환된 데이터에는 반영되지 않으며 이 커서는 수정을 허용하지 않습니다. ISO 구문을 사용할 때 `INSENSITIVE`를 생략하면 사용자가 기본 테이블에 커밋한 삭제 및 업데이트 내용이 후속 인출에 반영됩니다.  
  
 SCROLL  
 모든 인출 옵션(`FIRST`, `LAST`, `PRIOR`, `NEXT`, `RELATIVE`, `ABSOLUTE`)을 사용할 수 있도록 지정합니다. ISO `DECLARE CURSOR`에서 `SCROLL`을 지정하지 않으면 `NEXT` 인출 옵션만 지원됩니다. `FAST_FORWARD`까지 지정한 경우 `SCROLL`을 지정할 수 없습니다. `SCROLL`이 지정되지 않으면 페치 옵션 `NEXT`만 사용할 수 있고 커서는 `FORWARD_ONLY`가 됩니다.
  
 *select_statement*  
 커서의 결과 세트를 정의하는 표준 `SELECT` 문입니다. `FOR BROWSE` 및 `INTO` 키워드는 커서 선언의 *select_statement* 내에서 허용되지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 *select_statement*의 절이 요청된 커서 유형의 기능과 충돌할 경우 커서를 다른 유형으로 암시적으로 변환합니다.  
  
 READ ONLY  
 이 커서를 통한 업데이트를 방지합니다. `UPDATE` 또는 `DELETE` 문의 `WHERE CURRENT OF` 절에서 커서를 참조할 수 없습니다. 이 옵션은 업데이트할 커서의 기본 기능을 무시합니다.  
  
 UPDATE [OF *column_name* [**,**...*n*]]  
 커서 내에서 업데이트할 수 있는 열을 정의합니다. OF <column_name> [, <... n>]이 지정된 경우 나열된 열만 수정이 가능합니다. 열 목록 없이 `UPDATE`를 지정하면 모든 열을 업데이트할 수 있습니다.  
  
*cursor_name*  
정의된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서의 이름입니다. *cursor_name*은 식별자에 대한 규칙을 따라야 합니다.  
  
LOCAL  
커서 범위를 커서가 생성된 일괄 처리, 저장 프로시저, 트리거에 대해 로컬로 지정합니다. 커서 이름은 지정된 범위 내에서만 유효합니다. 일괄 처리, 저장 프로시저, 트리거의 로컬 커서 변수 또는 저장 프로시저의 `OUTPUT` 매개 변수에서 커서를 참조할 수 있습니다. `OUTPUT` 매개 변수는 호출한 일괄 처리, 저장 프로시저, 트리거로 로컬 커서를 다시 전달하는 데 사용되며 저장 프로시저가 종료된 후 커서 변수에 매개 변수를 할당하여 커서를 참조할 수 있습니다. 커서가 `OUTPUT` 매개 변수에서 다시 전달되지 않은 경우 일괄 처리나 저장 프로시저, 트리거가 종료되면 커서가 암시적으로 할당 취소됩니다. `OUTPUT` 매개 변수에서 커서가 다시 전달되면 커서를 참조하는 마지막 변수의 할당이 취소되거나 범위를 벗어날 때 커서의 할당이 취소됩니다.  
  
GLOBAL  
커서 범위를 연결에 대해 전역으로 지정합니다. 연결되어 실행하는 모든 저장 프로시저 또는 일괄 처리에서 커서 이름을 참조할 수 있습니다. 커서는 연결 해제 시에만 암시적으로 할당이 취소됩니다.  
  
> [!NOTE]  
>  `GLOBAL` 또는 `LOCAL` 중 하나도 지정하지 않으면 기본값은 **default to local cursor** 데이터베이스 옵션의 설정에 따라 결정됩니다.  
  
FORWARD_ONLY  
커서가 앞으로만 이동하고 첫 번째 행에서 마지막 행까지 스크롤할 수 있도록 지정합니다. 유일하게 지원되는 인출 옵션은 `FETCH NEXT`입니다. 현재 사용자가 만들거나 다른 사용자가 커밋하여 결과 집합의 행에 영향을 주는 모든 삽입, 업데이트 및 삭제 문은 행을 페치할 때 볼 수 있습니다. 그러나 커서는 뒤로 스크롤할 수 없기 때문에 행이 페치된 후 데이터베이스 행의 변경 내용은 대부분 커서를 통해 볼 수 없습니다. 정방향 전용 커서는 기본적으로 동적이며, 이는 현재 행이 처리될 때 모든 변경 내용이 감지됨을 의미합니다. 이렇게 하면 커서가 더 빨리 열리고 결과 집합이 기본 테이블에 대한 업데이트를 표시하도록 설정할 수 있습니다. 정방향 전용 커서는 역방향 스크롤을 지원하지 않지만 애플리케이션은 커서를 닫았다가 다시 열면 결과 집합의 시작 부분으로 돌아갈 수 있습니다. `STATIC`, `KEYSET` 또는 `DYNAMIC` 키워드를 사용하지 않고 `FORWARD_ONLY`를 지정하면 커서는 동적 커서로 작동합니다. `FORWARD_ONLY` 또는 `SCROLL` 중 하나도 지정하지 않으면 `STATIC`, `KEYSET` 또는 `DYNAMIC` 키워드를 지정하지 않는 이상 기본값은 `FORWARD_ONLY`입니다. `STATIC`, `KEYSET` 및 `DYNAMIC` 커서는 기본적으로 `SCROLL`입니다. ODBC, ADO 등의 데이터베이스 API와는 달리, `FORWARD_ONLY`는 `STATIC`, `KEYSET` 및 `DYNAMIC` [!INCLUDE[tsql](../../includes/tsql-md.md)] 커서에서 지원됩니다.  
   
 STATIC  
커서가 처음 열릴 때와 같은 결과 집합을 항상 표시하고 커서가 사용할 데이터의 임시 복사본을 만들도록 지정합니다. 커서에 대한 모든 요청은 **tempdb**의 이 임시 테이블에서 응답됩니다. 따라서 기본 테이블에 대한 삽입, 업데이트 및 삭제는 이 커서로 만들어진 페치에 의해 반환되는 데이터에 반영되지 않으며, 이 커서는 커서가 열린 후에 결과 집합의 멤버 자격, 순서 또는 값에 대한 변경 내용을 검색하지 못합니다. 정적 커서는 자체 업데이트, 삭제 및 삽입을 검색할 수 있지만 필수 사항은 아닙니다. 예를 들어 정적 커서가 행을 페치하고 다른 애플리케이션이 해당 행을 업데이트한다고 가정합니다. 애플리케이션이 정적 커서에서 행을 다시 페치하면 다른 애플리케이션에서 변경한 내용에도 불구하고 표시되는 값은 변경되지 않습니다. 모든 유형의 스크롤이 지원됩니다. 
  
KEYSET  
커서가 열릴 때 커서에 있는 행의 멤버 자격과 순서가 고정되도록 지정합니다. 행을 고유하게 식별하는 **keyset**이라는 키 집합이 **tempdb**의 테이블에 생성됩니다. 이 커서는 정적 커서와 동적 커서 간에 변경 내용을 검색하는 기능을 제공합니다. 정적 커서처럼 항상 결과 집합의 멤버 자격과 순서에 대한 변경 내용을 검색하지는 못합니다. 동적 커서처럼 결과 집합의 행 값에 대한 변경 내용을 검색합니다. 키 집합 커서는 키 집합이라는 고유 식별자(키) 집합으로 제어됩니다. 키는 결과 집합에서 행을 고유하게 식별하는 열 집합으로 작성됩니다. 키 집합은 쿼리 문에서 반환된 모든 행의 키 값 집합입니다. 키 집합 커서를 사용하여 커서의 각 행에 대해 키를 빌드 및 저장하고 클라이언트 워크스테이션 또는 서버에 저장합니다. 각 행에 액세스하면 저장된 키를 사용하여 데이터 원본에서 현재 데이터 값을 페치합니다. 키 집합 커서에서 키 집합이 완전히 채워지면 결과 집합 멤버 자격이 고정됩니다. 이후 멤버 자격에 영향을 주는 추가 또는 업데이트는 다시 열 때까지 결과 집합의 일부가 아닙니다. 사용자가 결과 집합을 스크롤할 때 데이터 값(키 집합 소유자 또는 다른 프로세스에 의해 생성됨)에 대한 변경 내용이 나타납니다.
-  행이 삭제되면 삭제된 행이 결과 집합의 간격으로 표시되므로 행을 페치하려고 하면 -2의 `@@FETCH_STATUS`가 반환됩니다. 행의 키는 키 집합에 있지만 행은 결과 집합에 더 이상 존재하지 않습니다. 
-  커서 외부에서 수행한 삽입은(다른 프로세스에 의해)은 커서를 닫았다가 다시 열 때만 볼 수 있습니다. 커서 내에서 수행한 삽입은 결과 집합의 끝에 표시됩니다.
-  커서 외부에서 키 값을 업데이트하는 것은 이전 행을 삭제하고 새 행을 삽입하는 것과 비슷합니다. 새 값을 가진 행을 볼 수 없으므로 이전 값을 가진 행을 인출하려고 하면 -2의 `@@FETCH_STATUS`로 반환됩니다. `WHERE CURRENT OF` 절을 지정하여 커서를 통해 업데이트를 수행한 경우에는 새 값을 볼 수 있습니다. 

> [!NOTE]  
> 쿼리가 고유 인덱스 없이 한 개 이상의 테이블을 참조하는 경우 키 집합 커서는 정적 커서로 변환됩니다.  
  
DYNAMIC  
커서 내부 또는 커서 외부의 다른 사용자가 변경했는지에 관계없이 커서를 스크롤하고 새 코드를 가져올 때 결과 집합의 행에 대해 수행된 모든 데이터 변경 내용을 반영하는 커서를 정의합니다. 따라서 모든 사용자가 실행한 모든 삽입, 업데이트 및 삭제 문은 커서를 통해 볼 수 있습니다. 따라서 인출할 때마다 행의 데이터 값, 순서 및 멤버 자격이 변경될 수 있습니다. 동적 커서에서는 `ABSOLUTE` 페치 옵션이 지원되지 않습니다. 커서 외부에서 수행된 업데이트는 커밋될 때까지 볼 수 없습니다(커서 트랜잭션 격리 수준이 `UNCOMMITTED`로 설정되어 있지 않은 경우). 예를 들어 동적 커서가 두 행을 페치하고 다른 애플리케이션이 해당 행 중 하나를 업데이트하고 다른 행을 삭제한다고 가정합니다. 그런 다음, 동적 커서가 해당 행을 페치하는 경우, 삭제된 행을 찾을 수 없지만 업데이트된 행에 대한 새 값을 표시합니다. 
  
FAST_FORWARD  
성능 최적화가 설정된 `FORWARD_ONLY`, `READ_ONLY` 커서를 지정합니다. `SCROLL` 또는 `FOR_UPDATE`까지 지정한 경우 `FAST_FORWARD`을 지정할 수 없습니다. 이 유형의 커서는 커서 내부에서 데이터 수정을 허용하지 않습니다.  
  
> [!NOTE]  
> `FAST_FORWARD` 및 `FORWARD_ONLY`를 같은 `DECLARE CURSOR` 문에 사용할 수 있습니다.  
  
READ_ONLY  
이 커서를 통한 업데이트를 방지합니다. `UPDATE` 또는 `DELETE` 문의 `WHERE CURRENT OF` 절에서 커서를 참조할 수 없습니다. 이 옵션은 업데이트할 커서의 기본 기능을 무시합니다.  
  
SCROLL_LOCKS  
커서를 통해 현재 위치 업데이트 또는 삭제가 반드시 실행되도록 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 커서에서 읽어 들이는 행을 잠가 나중에 수정할 때 사용할 수 있도록 합니다. `FAST_FORWARD` 또는 `STATIC`까지 지정한 경우 `SCROLL_LOCKS`을 지정할 수 없습니다.  
  
OPTIMISTIC  
커서에서 읽어 들인 행이 업데이트된 경우 커서를 통해 지정된 위치에서 업데이트 또는 삭제가 실행되지 않도록 지정합니다. 이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 커서로 행을 읽을 때 행을 잠그지 않습니다. 대신 **timestamp** 열 값을 비교하거나 테이블에 **timestamp** 열이 없을 경우 체크섬 값을 비교하여 커서로 읽은 행이 수정되었는지 여부를 확인합니다. 행이 수정된 경우 지정된 위치에서 업데이트나 삭제가 실행되지 않습니다. `FAST_FORWARD`까지 지정한 경우 `OPTIMISTIC`을 지정할 수 없습니다.  
  
 TYPE_WARNING  
 요청한 커서 형식이 다른 형식으로 암시적으로 변환된 경우 클라이언트에게 경고 메시지를 보내도록 지정합니다.  
  
 *select_statement*  
 커서의 결과 집합을 정의하는 표준 SELECT 문입니다. `COMPUTE`, `COMPUTE BY`, `FOR BROWSE` 및 `INTO` 키워드는 커서 선언의 *select_statement* 내에서 허용되지 않습니다.  
  
> [!NOTE]  
> 커서 선언 내에 쿼리 힌트를 사용할 수 있습니다. 그러나 `OPTION (<query_hint>)` 절도 함께 사용하는 경우 `FOR UPDATE OF` 뒤에 `FOR UPDATE OF`를 지정하세요.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 *select_statement*의 절이 요청된 커서 유형의 기능과 충돌할 경우 커서를 다른 유형으로 암시적으로 변환합니다. 자세한 내용은 암시적 커서 변환을 참조하세요.  
  
FOR UPDATE [OF *column_name* [**,**...*n*]]  
커서 내에서 업데이트할 수 있는 열을 정의합니다. `OF <column_name> [, <... n>]`이 제공된 경우 나열된 열만 수정이 가능합니다. `READ_ONLY` 동시성 옵션이 지정되지 않은 경우 열 목록 없이 `UPDATE`를 지정하면 모든 열을 업데이트할 수 있습니다.  
  
## <a name="remarks"></a>설명  
`DECLARE CURSOR`는 스크롤 동작, 커서가 작동하는 결과 세트를 구축하는 데 사용되는 쿼리 등 [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서의 특성을 정의합니다. `OPEN` 문은 결과 세트를 채우고 `FETCH`는 결과 세트에서 행을 반환합니다. `CLOSE` 문은 커서와 연결된 현재 결과 세트를 해제합니다. `DEALLOCATE` 문은 커서에서 사용된 리소스를 해제합니다.  
  
`DECLARE CURSOR` 문의 첫 번째 형식은 커서 동작을 선언하기 위해 ISO 구문을 사용합니다. `DECLARE CURSOR` 문의 두 번째 형식은 ODBC 또는 ADO의 데이터베이스 API 커서 함수에서 사용된 것과 동일한 커서 형식을 사용하여 커서를 정의할 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 확장을 사용합니다.  
  
위의 두 가지 형식을 함께 사용할 수는 없습니다. `CURSOR` 키워드 앞에 `SCROLL` 또는 `INSENSITIVE` 키워드를 지정하면 `CURSOR` 및 `FOR <select_statement>` 키워드 사이에 어떤 키워드도 사용할 수 없습니다. `CURSOR` 및 `FOR <select_statement>` 키워드 사이에 키워드를 지정하면 `CURSOR` 키워드 앞에 `SCROLL` 또는 `INSENSITIVE`를 지정할 수 없습니다.  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 구문을 사용하는 `DECLARE CURSOR`가 `READ_ONLY`, `OPTIMISTIC`,또는 `SCROLL_LOCKS`를 지정하지 않으면 기본값은 다음과 같습니다.  
  
-   권한 부족, 업데이트를 지원하지 않는 원격 테이블 액세스 등의 이유로 `SELECT` 문이 업데이트를 지원하지 않을 경우 커서는 `READ_ONLY`가 됩니다.  
  
-   `STATIC` 및 `FAST_FORWARD` 커서는 기본적으로 `READ_ONLY`입니다.  
  
-   `DYNAMIC` 및 `KEYSET` 커서는 기본적으로 `OPTIMISTIC`입니다.  
  
커서 이름은 다른 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서만 참조될 수 있으며 데이터베이스 API 함수에서는 참조될 수 없습니다. 예를 들어, 커서를 선언한 후 OLE DB, ODBC, ADO 함수나 메서드에서 커서 이름을 참조할 수 없습니다. 커서 행은 API의 인출 함수나 메서드를 사용하여 인출할 수 없고 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 FETCH 문을 사용해야만 인출할 수 있습니다.  
  
커서를 선언한 후 다음 시스템 저장 프로시저를 사용하여 커서의 특징을 확인할 수 있습니다.  
  
|시스템 저장 프로시저|Description|  
|------------------------------|-----------------|  
|**sp_cursor_list**|현재 연결에서 볼 수 있는 커서 목록과 그 특성을 반환합니다.|  
|**sp_describe_cursor**|정방향 전용 커서, 스크롤 커서 등의 커서 특성을 설명합니다.|  
|**sp_describe_cursor_columns**|커서 결과 집합에서 열의 특성을 설명합니다.|  
|**sp_describe_cursor_tables**|커서에 의해 액세스되는 기본 테이블을 설명합니다.|  
  
 변수는 커서를 선언하는 *select_statement*의 일부로 사용될 수 있습니다. 커서가 선언된 후에는 커서 변수 값이 변경되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 `DECLARE CURSOR` 권한은 커서에 사용된 보기, 테이블, 열에 대한 `SELECT` 권한이 있는 모든 사용자에게 기본적으로 부여됩니다.
 
## <a name="limitations-and-restrictions"></a>제한 사항

클러스터형 columnstore 인덱스가 있는 테이블에서는 커서 또는 트리거를 사용할 수 없습니다. 비클러스터형 columnstore 인덱스에는 이러한 제한이 적용되지 않습니다. 즉 비클러스터형 columnstore 인덱스가 있는 테이블에서는 커서 및 트리거를 사용할 수 있습니다. 
  
## <a name="examples"></a>예제  
  
### <a name="a-using-simple-cursor-and-syntax"></a>A. 단순 커서 및 구문 사용  

다음 커서를 열 때 생성된 결과 집합에는 테이블에 있는 모든 행과 모든 열이 포함됩니다. 이 커서는 업데이트가 가능하며 이 커서에 대해 수행한 인출에는 모든 업데이트와 삭제 내용이 나타납니다. `FETCH NEXT` 옵션을 지정하지 않았으므로 `SCROLL` 인출만 사용할 수 있습니다.  
 
```sql  
DECLARE vend_cursor CURSOR  
    FOR SELECT * FROM Purchasing.Vendor  
OPEN vend_cursor  
FETCH NEXT FROM vend_cursor;  
```  
  
### <a name="b-using-nested-cursors-to-produce-report-output"></a>B. 중첩된 커서를 사용하여 보고서 출력 생성  
 다음 예에서는 커서를 중첩시켜 복잡한 보고서를 생성하는 방법을 보여 줍니다. 각 공급업체에 대해 내부 커서가 선언됩니다.  
  
```sql  
SET NOCOUNT ON;  
  
DECLARE @vendor_id INT, @vendor_name NVARCHAR(50),  
    @message VARCHAR(80), @product NVARCHAR(50);  
  
PRINT '-------- Vendor Products Report --------';  
  
DECLARE vendor_cursor CURSOR FOR   
SELECT VendorID, Name  
FROM Purchasing.Vendor  
WHERE PreferredVendorStatus = 1  
ORDER BY VendorID;  
  
OPEN vendor_cursor  
  
FETCH NEXT FROM vendor_cursor   
INTO @vendor_id, @vendor_name  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    PRINT ' '  
    SELECT @message = '----- Products From Vendor: ' +   
        @vendor_name  
  
    PRINT @message  
  
    -- Declare an inner cursor based     
    -- on vendor_id from the outer cursor.  
  
    DECLARE product_cursor CURSOR FOR   
    SELECT v.Name  
    FROM Purchasing.ProductVendor pv, Production.Product v  
    WHERE pv.ProductID = v.ProductID AND  
    pv.VendorID = @vendor_id  -- Variable value from the outer cursor  
  
    OPEN product_cursor  
    FETCH NEXT FROM product_cursor INTO @product  
  
    IF @@FETCH_STATUS <> 0   
        PRINT '         <<None>>'       
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
  
        SELECT @message = '         ' + @product  
        PRINT @message  
        FETCH NEXT FROM product_cursor INTO @product  
        END  
  
    CLOSE product_cursor  
    DEALLOCATE product_cursor  
        -- Get the next vendor.  
    FETCH NEXT FROM vendor_cursor   
    INTO @vendor_id, @vendor_name  
END   
CLOSE vendor_cursor;  
DEALLOCATE vendor_cursor;  
```  
  
## <a name="see-also"></a>참고 항목  
 [@@FETCH_STATUS&#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md)   
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [커서&#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

---
title: DECLARE CURSOR (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECLARE_CURSOR_TSQL
- CURSOR_TSQL
- DECLARE CURSOR
- CURSOR
dev_langs: TSQL
helpviewer_keywords:
- DECLARE CURSOR statement
- cursors [SQL Server], attributes
- local cursors [SQL Server]
- nesting cursors
- Transact-SQL cursors, attributes
- global cursors [SQL Server]
ms.assetid: 5a3a27aa-03e8-4c98-a27e-809282379b21
caps.latest.revision: "51"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 0641f87c36d3dbed886dc7bb81aa1f179148a8cd
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="declare-cursor-transact-sql"></a>DECLARE CURSOR(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  스크롤 동작, 커서가 작동하는 결과 집합을 구축하는 데 사용되는 쿼리 등 [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서의 특성을 정의합니다. DECLARE CURSOR는 ISO 표준 기반의 구문과 [!INCLUDE[tsql](../../includes/tsql-md.md)] 확장 집합을 사용하는 구문을 모두 허용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
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
  
## <a name="arguments"></a>인수  
 *cursor_name*  
 이름인는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서를 정의 합니다. *cursor_name* 식별자에 대 한 규칙을 따라야 합니다.  
  
 INSENSITIVE  
 커서에서 사용할 데이터를 임시로 복사해 주는 커서를 정의합니다. 커서에 대 한 모든 요청은이 임시 테이블에 대 한 답변은 **tempdb**; 따라서 기본 테이블에 대 한 수정이이 커서에 대 한 인출에서 반환 된 데이터에 반영 되지 않으며이 커서를 허용 하지 않습니다 수정 합니다. ISO 구문을 사용할 때 INSENSITIVE를 생략하면 사용자가 기본 테이블에 커밋한 삭제 및 업데이트 내용이 후속 인출에 반영됩니다.  
  
 SCROLL  
 모든 인출 옵션(FIRST, LAST, PRIOR, NEXT, RELATIVE, ABSOLUTE)을 사용할 수 있도록 지정합니다. ISO DECLARE CURSOR에서 SCROLL을 지정하지 않으면 NEXT 인출 옵션만 지원됩니다. FAST_FORWARD가 지정된 경우에는 SCROLL을 지정할 수 없습니다.  
  
 *select_statement*  
 커서의 결과 집합을 정의하는 표준 SELECT 문입니다. 내에서 FOR BROWSE 및 INTO 키워드를 사용할 수 없습니다 *select_statement* 커서 선언 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]경우 커서 다른 형식으로 암시적으로 변환의 절 *select_statement* 요청한 커서 유형의 기능과 충돌할 합니다.  
  
 READ ONLY  
 이 커서를 통한 업데이트를 방지합니다. UPDATE 문 또는 DELETE 문의 WHERE CURRENT OF 절에서는 이 커서를 참조할 수 없습니다. 이 옵션은 업데이트할 커서의 기본 기능을 무시합니다.  
  
 업데이트 [OF *column_name* [**,**... *n*]]  
 커서 내에서 업데이트할 수 있는 열을 정의합니다. Of *column_name* [**,**... *.n*]가 지정 된 경우만 나열 된 열 수정이 가능 합니다. 열 목록 없이 UPDATE를 지정하면 모든 열을 업데이트할 수 있습니다.  
  
 *cursor_name*  
 이름인는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서를 정의 합니다. *cursor_name* 식별자에 대 한 규칙을 따라야 합니다.  
  
 LOCAL  
 커서 범위를 커서가 생성된 일괄 처리, 저장 프로시저, 트리거에 대해 로컬로 지정합니다. 커서 이름은 지정된 범위 내에서만 유효합니다. 일괄 처리, 저장 프로시저, 트리거의 로컬 커서 변수 또는 저장 프로시저의 OUTPUT 매개 변수에서 커서를 참조할 수 있습니다. OUTPUT 매개 변수는 호출한 일괄 처리, 저장 프로시저, 트리거로 로컬 커서를 다시 전달하는 데 사용되며 저장 프로시저가 종료된 후 커서 변수에 매개 변수를 할당하여 커서를 참조할 수 있습니다. 커서가 OUTPUT 매개 변수에서 다시 전달되지 않은 경우 일괄 처리나 저장 프로시저, 트리거가 종료되면 커서가 암시적으로 할당 취소됩니다. OUTPUT 매개 변수에서 커서가 다시 전달되면 커서를 참조하는 마지막 변수의 할당이 취소되거나 범위를 벗어날 때 커서의 할당이 취소됩니다.  
  
 GLOBAL  
 커서 범위를 연결에 대해 전역으로 지정합니다. 연결되어 실행하는 모든 저장 프로시저 또는 일괄 처리에서 커서 이름을 참조할 수 있습니다. 커서는 연결 해제 시에만 암시적으로 할당이 취소됩니다.  
  
> [!NOTE]  
>  기본값의 설정에 의해 제어 됩니다 GLOBAL 또는 LOCAL 모두를 지정 하는 경우는 **기본적으로 로컬 커서** 데이터베이스 옵션입니다.  
  
 FORWARD_ONLY  
 첫 번째 행에서 마지막 행 방향으로만 커서를 스크롤할 수 있도록 지정합니다. 유일하게 지원되는 인출 옵션은 FETCH NEXT입니다. STATIC, KEYSET, DYNAMIC 키워드를 사용하지 않고 FORWARD_ONLY를 지정하면 DYNAMIC 커서로 작동합니다. STATIC, KEYSET 또는 DYNAMIC 키워드가 지정된 경우를 제외하면 FORWARD_ONLY나 SCROLL을 모두 지정하지 않을 경우 FORWARD_ONLY가 기본값입니다. STATIC, KEYSET, DYNAMIC 커서는 기본적으로 SCROLL이 됩니다. ODBC, ADO 등의 데이터베이스 API와 달리 STATIC, KEYSET, DYNAMIC [!INCLUDE[tsql](../../includes/tsql-md.md)] 커서에서는 FORWARD_ONLY가 지원됩니다.  
  
 STATIC  
 커서에서 사용할 데이터를 임시로 복사해 주는 커서를 정의합니다. 커서에 대 한 모든 요청은이 임시 테이블에 대 한 답변은 **tempdb**; 따라서 기본 테이블에 대 한 수정이이 커서에 대 한 인출에서 반환 된 데이터에 반영 되지 않으며이 커서를 허용 하지 않습니다 수정 합니다.  
  
 KEYSET  
 커서가 열릴 때 커서에 있는 행의 멤버 자격과 순서가 고정되도록 지정합니다. 테이블에 행을 고유 하 게 식별 하는 키 집합이 빌드될 **tempdb** 라고는 **키 집합**합니다.  
  
> [!NOTE]  
>  쿼리가 고유 인덱스 없이 한 개 이상의 테이블을 참조하는 경우 키 집합 커서는 정적 커서로 변환됩니다.  
  
 커서 소유자가 만들거나 다른 사용자가 커밋한 기본 테이블의 키가 아닌 값을 변경하면 커서 소유자가 커서를 스크롤할 때 변경 사항이 표시됩니다. 하지만 다른 사용자가 삽입한 데이터는 볼 수 없습니다([!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서를 통해 삽입할 수 없음). 행을 인출 하려고 반환 하는 경우는 행이 삭제 되는 @@FETCH_STATUS -2입니다. 커서 외부에서 키 값을 업데이트하는 것은 이전 행을 삭제하고 새 행을 삽입하는 것과 비슷합니다. 새 값을 가진 행을 볼 수 있고 이전 값을 가진 행을 인출 하려고 하면 반환 된 @@FETCH_STATUS -2입니다. WHERE CURRENT OF 절을 지정하여 커서를 통해 업데이트를 수행한 경우에는 새 값을 볼 수 있습니다.  
  
 DYNAMIC  
 커서를 스크롤할 때 결과 집합에 행에 대한 모든 데이터 변경 사항이 반영되는 커서를 정의합니다. 따라서 인출할 때마다 행의 데이터 값, 순서 및 멤버 자격이 변경될 수 있습니다. 동적 커서에서는 ABSOLUTE 인출 옵션이 지원되지 않습니다.  
  
 FAST_FORWARD  
 성능 최적화가 설정된 FORWARD_ONLY, READ_ONLY 커서를 지정합니다. SCROLL 또는 FOR_UPDATE가 지정된 경우에는 FAST_FORWARD를 지정할 수 없습니다.  
  
> [!NOTE]  
>  FAST_FORWARD 및 FORWARD_ONLY를 모두 동일한 DECLARE CURSOR 문에 사용할 수 있습니다.  
  
 READ_ONLY  
 이 커서를 통한 업데이트를 방지합니다. UPDATE 문 또는 DELETE 문의 WHERE CURRENT OF 절에서는 이 커서를 참조할 수 없습니다. 이 옵션은 업데이트할 커서의 기본 기능을 무시합니다.  
  
 SCROLL_LOCKS  
 커서를 통해 현재 위치 업데이트 또는 삭제가 반드시 실행되도록 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 커서에서 읽어 들이는 행을 잠가 나중에 수정할 때 사용할 수 있도록 합니다. FAST_FORWARD 또는 STATIC을 지정한 경우에는 SCROLL_LOCKS를 지정할 수 없습니다.  
  
 OPTIMISTIC  
 커서에서 읽어 들인 행이 업데이트된 경우 커서를 통해 지정된 위치에서 업데이트 또는 삭제가 실행되지 않도록 지정합니다. 이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 커서로 행을 읽을 때 행을 잠그지 않습니다. 에 대 한 비교를 대신 사용 **타임 스탬프** 열 값 또는 테이블에 없는 경우 체크섬 값 **타임 스탬프** 커서로 읽은 후 행이 수정 되었는지 여부를 확인 하려면 열입니다. 행이 수정된 경우 지정된 위치에서 업데이트나 삭제가 실행되지 않습니다. FAST_FORWARD가 지정된 경우에는 OPTIMISTIC을 지정할 수 없습니다.  
  
 TYPE_WARNING  
 요청한 커서 형식이 다른 형식으로 암시적으로 변환된 경우 클라이언트에게 경고 메시지를 보내도록 지정합니다.  
  
 *select_statement*  
 커서의 결과 집합을 정의하는 표준 SELECT 문입니다. 내에서 COMPUTE, COMPUTE BY, FOR BROWSE 및 INTO 키워드를 사용할 수 없습니다 *select_statement* 커서 선언 합니다.  
  
> [!NOTE]  
>  커서 선언; 내에서 쿼리 힌트를 사용할 수 있습니다. 그러나 FOR UPDATE OF 절을 사용 하는 경우 옵션 지정 (*쿼리 힌트*) FOR UPDATE OF 뒤 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]경우 커서 다른 형식으로 암시적으로 변환의 절 *select_statement* 요청한 커서 유형의 기능과 충돌할 합니다. 자세한 내용은 암시적 커서 변환을 참조하세요.  
  
 업데이트에 대 한 [OF *column_name* [**,**... *n*]]  
 커서 내에서 업데이트할 수 있는 열을 정의합니다. Of *column_name* [**,**...  *n* ]를 제공 하면만 나열 된 열 수정이 가능 합니다. READ_ONLY 동시성 옵션이 지정되지 않은 경우 열 목록 없이 UPDATE를 지정하면 모든 열을 업데이트할 수 있습니다.  
  
## <a name="remarks"></a>주의  
 DECLARE CURSOR는 스크롤 동작, 커서가 작동하는 결과 집합을 만드는 데 사용되는 쿼리 등 [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서의 특성을 정의합니다. OPEN 문은 결과 집합을 채우고 FETCH는 결과 집합에서 행을 반환합니다. CLOSE 문은 커서와 연결된 현재 결과 집합을 해제하며 DEALLOCATE 문은 커서에서 사용된 리소스를 해제합니다.  
  
 DECLARE CURSOR 문의 첫 번째 형식은 커서 동작을 선언하기 위해 ISO 구문을 사용합니다. DECLARE CURSOR 문의 두 번째 형식은 ODBC 또는 ADO의 데이터베이스 API 커서 함수에서 사용된 것과 동일한 커서 형식을 사용하여 커서를 정의할 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 확장을 사용합니다.  
  
 위의 두 가지 형식을 함께 사용할 수는 없습니다. 에 대 한 커서 사이의 키워드를 사용할 수 없습니다에 SCROLL 또는 INSENSITIVE 키워드 CURSOR 키워드 앞을 지정 하면 *select_statement* 키워드입니다. 에 대 한 커서 사이의 키워드를 지정 하면 *select_statement* 키워드 CURSOR 키워드 앞에 SCROLL 또는 INSENSITIVE를 지정할 수 없습니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문을 사용하는 DECLARE CURSOR에서 READ_ONLY, OPTIMISTIC, SCROLL_LOCKS를 지정하지 않을 경우 기본값은 다음과 같습니다.  
  
-   권한 부족, 업데이트를 지원하지 않는 원격 테이블 액세스 등의 이유로 SELECT 문이 업데이트를 지원하지 않을 경우 커서는 READ_ONLY가 됩니다.  
  
-   STATIC 및 FAST_FORWARD 커서는 기본적으로 READ_ONLY가 됩니다.  
  
-   DYNAMIC 및 KEYSET 커서는 기본적으로 OPTIMISTIC이 됩니다.  
  
 커서 이름은 다른 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서만 참조될 수 있으며 데이터베이스 API 함수에서는 참조될 수 없습니다. 예를 들어, 커서를 선언한 후 OLE DB, ODBC, ADO 함수나 메서드에서 커서 이름을 참조할 수 없습니다. 커서 행은 API의 인출 함수나 메서드를 사용하여 인출할 수 없고 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 FETCH 문을 사용해야만 인출할 수 있습니다.  
  
 커서를 선언한 후 다음 시스템 저장 프로시저를 사용하여 커서의 특징을 확인할 수 있습니다.  
  
|시스템 저장 프로시저|Description|  
|------------------------------|-----------------|  
|**sp_cursor_list**|현재 연결에서 볼 수 있는 커서 목록과 그 특성을 반환합니다.|  
|**sp_describe_cursor**|정방향 전용 커서, 스크롤 커서 등의 커서 특성을 설명합니다.|  
|**sp_describe_cursor_columns**|커서 결과 집합에서 열의 특성을 설명합니다.|  
|**sp_describe_cursor_tables**|커서에 의해 액세스되는 기본 테이블을 설명합니다.|  
  
 일부분으로 변수를 사용할 수 있습니다는 *select_statement* 커서를 선언 하는 합니다. 커서가 선언된 후에는 커서 변수 값이 변경되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 DECLARE CURSOR 권한은 커서에 사용된 뷰, 테이블, 열에 대한 SELECT 권한이 있는 모든 사용자에게 기본적으로 부여됩니다.
 
## <a name="limitations-and-restrictions"></a>제한 사항

클러스터형된 columnstore 인덱스가 있는 테이블에서 커서 또는 트리거를 사용할 수 없습니다. 비클러스터형 columnstore 인덱스;에이 제한이 적용 되지 않습니다. 비클러스터형 columnstore 인덱스가 있는 테이블에서 커서 및 트리거를 사용할 수 있습니다. 
  
## <a name="examples"></a>예  
  
### <a name="a-using-simple-cursor-and-syntax"></a>1. 단순 커서 및 구문 사용  

다음 커서를 열 때 생성된 결과 집합에는 테이블에 있는 모든 행과 모든 열이 포함됩니다. 이 커서는 업데이트가 가능하며 이 커서에 대해 수행한 인출에는 모든 업데이트와 삭제 내용이 나타납니다. `FETCH NEXT` 옵션을 지정하지 않았으므로 `SCROLL` 인출만 사용할 수 있습니다.  

  
```  
DECLARE vend_cursor CURSOR  
    FOR SELECT * FROM Purchasing.Vendor  
OPEN vend_cursor  
FETCH NEXT FROM vend_cursor;  
```  
  
### <a name="b-using-nested-cursors-to-produce-report-output"></a>2. 중첩된 커서를 사용하여 보고서 출력 생성  
 다음 예에서는 커서를 중첩시켜 복잡한 보고서를 생성하는 방법을 보여 줍니다. 각 공급업체에 대해 내부 커서가 선언됩니다.  
  
```  
SET NOCOUNT ON;  
  
DECLARE @vendor_id int, @vendor_name nvarchar(50),  
    @message varchar(80), @product nvarchar(50);  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [@@FETCH_STATUS&#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md)   
 [닫기 &#40; Transact SQL &#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [커서&#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [할당 해제 &#40; Transact SQL &#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [FETCH &#40; Transact SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

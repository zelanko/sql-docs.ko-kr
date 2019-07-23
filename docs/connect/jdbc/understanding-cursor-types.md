---
title: 커서 유형 이해 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4f4d3db7-4f76-450d-ab63-141237a4f034
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dbd7e3622df44d6b696b56745495b684d6100eb1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004191"
---
# <a name="understanding-cursor-types"></a>커서 유형 이해
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  관계형 데이터베이스에서의 연산은 전체 행 집합에 적용됩니다. SELECT 문에 의해 반환된 행 집합은 문의 WHERE 절 조건을 만족하는 모든 행으로 구성됩니다. SELECT 문에 의해 반환된 전체 행 집합을 결과 집합이라고 합니다. 응용 프로그램에서는 전체 결과 집합을 한 단위로 사용하므로 항상 효과적으로 작업할 수는 없습니다. 이러한 애플리케이션에는 한 번에 한 행이나 적은 행 블록을 사용하여 작업하는 메커니즘이 필요합니다. 커서는 이러한 메커니즘을 제공하는 결과 집합에 대한 확장입니다.  
  
 커서는 다음을 수행하여 결과 집합 처리를 확장합니다.  
  
-   결과 집합의 특정 행에 위치를 정할 수 있습니다.  
  
-   결과 집합의 현재 위치에서 한 행 또는 행 블록을 검색합니다.  
  
-   결과 집합의 현재 위치에 있는 행 데이터를 수정할 수 있습니다.  
  
-   결과 집합에 나타난 데이터베이스 데이터에 대해 다른 사용자가 변경한 내용을 여러 가지 수준으로 볼 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서 유형에 대한 자세한 설명은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 “커서 유형(데이터베이스 엔진)” 항목을 참조하십시오.  
  
 JDBC 사양은 정방향 전용 커서 및 스크롤 가능 커서를 지원합니다. 이러한 커서는 다른 작업으로 인한 변경 사항을 감지하거나 감지하지 못하며 읽기 전용이거나 업데이트 가능합니다. 이 기능은 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)][SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스에서 제공됩니다.  
  
## <a name="remarks"></a>Remarks  
 JDBC 드라이버는 다음 커서 유형을 지원합니다.  
  
|결과 집합<br /><br /> (커서) 유형|SQL Server 커서 유형|특징|선택<br /><br /> 메서드|response<br /><br /> 버퍼링|설명|  
|------------------------------------|----------------------------|---------------------|-----------------------|----------------------------|-----------------|  
|TYPE_FORWARD_ONLY(CONCUR_READ_ONLY)|해당 사항 없음|정방향 전용, 읽기 전용|direct|전체|응용 프로그램은 결과 집합을 정방향으로 한 번 통과해야 합니다. 이것은 기본 동작이며 TYPE_SS_DIRECT_FORWARD_ONLY 커서와 동일하게 작동합니다. 드라이버는 문 실행 중 서버의 전체 결과 집합을 메모리로 읽습니다.|  
|TYPE_FORWARD_ONLY(CONCUR_READ_ONLY)|해당 사항 없음|정방향 전용, 읽기 전용|direct|adaptive|응용 프로그램은 결과 집합을 정방향으로 한 번 통과해야 합니다. 이것은 TYPE_SS_DIRECT_FORWARD_ONLY 커서와 동일하게 작동합니다. 드라이버는 응용 프로그램에서 요청할 경우 서버의 행을 읽어 클라이언트 쪽 메모리 사용량을 최소화합니다.|  
|TYPE_FORWARD_ONLY(CONCUR_READ_ONLY)|빠른 정방향|정방향 전용, 읽기 전용|cursor|해당 사항 없음|응용 프로그램은 서버 커서를 사용하여 결과 집합을 정방향으로 한 번 통과해야 합니다. 이 유형은 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY 커서와 동일하게 동작합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_FORWARD_ONLY(CONCUR_UPDATABLE)|동적(정방향 전용)|정방향 전용, 업데이트 가능|해당 사항 없음|해당 사항 없음|응용 프로그램은 한 개 이상의 행을 업데이트하기 위해 결과 집합을 정방향으로 한 번 통과해야 합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.<br /><br /> 기본적으로 인출 크기는 애플리케이션이 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) 메서드를 호출할 때 고정됩니다.<br /><br /> **참고:** JDBC 드라이버에서는 문 실행 결과를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 한 번에 모두 검색하는 것이 아니라 애플리케이션에 필요할 때 검색할 수 있는 선택 버퍼링 기능이 제공됩니다. 예를 들어 너무 커서 응용 프로그램 메모리에 한 번에 저장할 수 없는 큰 데이터를 검색해야 하는 경우 클라이언트 응용 프로그램에서는 이러한 값을 스트림으로 검색할 수 있습니다. 드라이버의 기본 동작은 “**adaptive**”입니다. 그러나 정방향 전용 업데이트 가능 결과 집합에 대해 선택 버퍼링을 사용하려면 애플리케이션은 **문자열** 값 “**adaptive”** 를 제공하여 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 메서드를 명시적으로 호출해야 합니다. 예제 코드는 [Large Data 샘플 업데이트](../../connect/jdbc/updating-large-data-sample.md)를 참조 하세요.|  
|TYPE_SCROLL_INSENSITIVE|정적|스크롤 가능, 업데이트 불가능<br /><br /> 외부 행 업데이트, 삽입 및 삭제는 표시되지 않음|해당 사항 없음|해당 사항 없음|응용 프로그램에 데이터베이스 스냅샷이 필요합니다. 결과 집합을 업데이트할 수 없습니다. CONCUR_READ_ONLY만 지원됩니다.  이외에 다른 모든 동시성 유형을 이 커서 유형과 함께 사용하는 경우 예외가 발생합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_READ_ONLY)|Keyset|스크롤 가능, 읽기 전용 외부 행 업데이트는 표시되며, 삭제는 데이터 누락으로 나타남<br /><br /> 외부 행 삽입은 표시되지 않음|해당 사항 없음|해당 사항 없음|응용 프로그램은 기존 행의 변경된 데이터만 볼 수 있어야 합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Keyset|스크롤 가능 및 업데이트 가능.<br /><br /> 외부 및 내부 행 업데이트는 표시되고 삭제는 데이터 누락으로 나타나며, 삽입은 표시되지 않음|해당 사항 없음|해당 사항 없음|애플리케이션은 ResultSet 개체를 사용하여 기존 행의 데이터를 변경할 수 있습니다. 또한 애플리케이션은 ResultSet 개체 외부에서 다른 사용자가 행에 대해 변경한 내용을 볼 수 있어야 합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_SS_DIRECT_FORWARD_ONLY|해당 사항 없음|정방향 전용, 읽기 전용|해당 사항 없음|전체 또는 선택|정수 값 = 2003. 완전히 버퍼링되는 읽기 전용 클라이언트 쪽 커서를 제공합니다. 서버 커서가 만들어지지 않습니다.<br /><br /> CONCUR_READ_ONLY 동시성 유형만 지원됩니다. 이외에 다른 모든 동시성 유형을 이 커서 유형과 함께 사용하는 경우 예외가 발생합니다.|  
|TYPE_SS_SERVER_CURSOR_FORWARD_ONLY|빠른 정방향|정방향 전용|해당 사항 없음|해당 사항 없음|정수 값 = 2004. 서버 커서를 사용하여 모든 데이터에 빠르게 액세스합니다. CONCUR_UPDATABLE 동시성 유형과 함께 사용하는 경우 업데이트할 수 있습니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.<br /><br /> 이 경우 선택 버퍼링을 사용하려면 애플리케이션에서 **String** 값 “**adaptive”** 를 제공하여 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 메서드를 명시적으로 호출해야 합니다. 예제 코드는 [Large Data 샘플 업데이트](../../connect/jdbc/updating-large-data-sample.md)를 참조 하세요.|  
|TYPE_SS_SCROLL_STATIC|정적|다른 사용자의 업데이트는 반영 안 됨|해당 사항 없음|해당 사항 없음|정수 값 = 1004. 응용 프로그램에 데이터베이스 스냅샷이 필요합니다. JDBC TYPE_SCROLL_INSENSITIVE에 해당하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 동의어로, 동시성 설정 동작이 동일합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_READ_ONLY)|Keyset|스크롤 가능, 읽기 전용. 외부 행 업데이트는 표시되며, 삭제는 데이터 누락으로 나타남<br /><br /> 외부 행 삽입은 표시되지 않음|해당 사항 없음|해당 사항 없음|정수 값 = 1005. 응용 프로그램은 기존 행의 변경된 데이터만 볼 수 있어야 합니다. JDBC TYPE_SCROLL_SENSITIVE에 해당하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 동의어로, 동시성 설정 동작이 동일합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Keyset|스크롤 가능 및 업데이트 가능.<br /><br /> 외부 및 내부 행 업데이트는 표시되고 삭제는 데이터 누락으로 나타나며, 삽입은 표시되지 않음|해당 사항 없음|해당 사항 없음|정수 값 = 1005. 응용 프로그램은 기존 행의 데이터를 변경하거나 기존 행의 변경된 데이터를 볼 수 있어야 합니다. JDBC TYPE_SCROLL_SENSITIVE에 해당하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 동의어로, 동시성 설정 동작이 동일합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_READ_ONLY)|Dynamic|스크롤 가능, 읽기 전용<br /><br /> 외부 행 업데이트와 삽입은 표시되고 삭제는 현재 인출 버퍼에서 일시적인 데이터 누락으로 나타남|해당 사항 없음|해당 사항 없음|정수 값 = 1006. 응용 프로그램은 기존 행의 변경된 데이터를 볼 수 있어야 하고, 커서의 수명 기간 동안 삽입되거나 삭제된 행을 볼 수 있어야 합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Dynamic|스크롤 가능 및 업데이트 가능.<br /><br /> 외부 및 내부 행 업데이트와 삽입은 표시되고 삭제는 현재 인출 버퍼에서 일시적인 데이터 누락으로 나타남|해당 사항 없음|해당 사항 없음|정수 값 = 1006. 애플리케이션은 ResultSet 개체를 사용하여 기존 행의 데이터를 변경하거나 행을 삽입 또는 삭제할 수 있습니다. 또한 애플리케이션은 ResultSet 개체 외부에서 다른 사용자가 변경, 삽입 또는 삭제한 내용을 볼 수 있어야 합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
  
## <a name="cursor-positioning"></a>커서 위치 지정  
 TYPE_FORWARD_ONLY, TYPE_SS_DIRECT_FORWARD_ONLY 및 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY 커서는 [next](../../connect/jdbc/reference/next-method-sqlserverresultset.md) 위치 지정 메서드만 지원합니다.  
  
 TYPE_SS_SCROLL_DYNAMIC 커서는 [absolute](../../connect/jdbc/reference/absolute-method-sqlserverresultset.md) 및 [getRow](../../connect/jdbc/reference/getrow-method-sqlserverresultset.md) 메서드를 지원하지 않습니다. absolute 메서드는 동적 커서에 대한 [first](../../connect/jdbc/reference/first-method-sqlserverresultset.md) 및 [relative](../../connect/jdbc/reference/relative-method-sqlserverresultset.md) 메서드 호출 조합으로 나타낼 수 있습니다.  
  
 getRow 메서드는 TYPE_FORWARD_ONLY, TYPE_SS_DIRECT_FORWARD_ONLY, TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, TYPE_SS_SCROLL_KEYSET 및 TYPE_SS_SCROLL_STATIC 커서로만 지원됩니다. 모든 정방향 전용 커서 유형의 getRow 메서드는 지금까지 커서를 통해 읽은 행 수를 반환합니다.  
  
> [!NOTE]  
>  애플리케이션이 지원되지 않는 커서 위치 지정을 호출하거나 지원되지 않는 getRow 메서드를 호출하면 “요청한 작업은 이 커서 유형에서는 지원되지 않습니다.”라는 메시지와 함께 예외가 발생합니다.  
  
 TYPE_SS_SCROLL_KEYSET 및 동일한 TYPE_SCROLL_SENSITIVE 커서는 삭제된 행을 표시합니다. 커서가 삭제된 행에 위치하게 되면 열 값을 사용할 수 없으며 [rowDeleted](../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) 메서드는 “true”가 됩니다. get\<Type> 메서드를 호출하면 “삭제된 행에서 값을 가져올 수 없습니다.”라는 메시지와 함께 예외가 발생합니다. 삭제된 행은 업데이트할 수 없습니다. 삭제된 행에서 update\<Type> 메서드를 호출하려고 하면 “삭제된 행은 업데이트할 수 없습니다.”라는 메시지와 함께 예외가 발생합니다. TYPE_SS_SCROLL_DYNAMIC 커서는 현재 인출 버퍼 외부로 이동할 때까지 동일한 동작을 수행합니다.  
  
 정방향 및 동적 커서는 인출 버퍼에서 액세스할 수 있는 경우에만 삭제된 행을 동일한 방식으로 표시합니다. 정방향 커서의 경우 이 작업은 비교적 간단합니다. 동적 커서의 경우 인출 크기가 1보다 크면 작업이 더 복잡해집니다. 응용 프로그램은 인출 버퍼로 정의된 창 내에서 커서를 앞뒤로 이동할 수 있지만, 업데이트되었던 원래 인출 버퍼를 벗어나는 경우 삭제된 행은 사라집니다. 응용 프로그램에서 동적 커서를 사용하여 일시적으로 삭제된 행을 표시하지 않으려면 인출 상대 값(0)을 사용해야 합니다.  
  
 TYPE_SS_SCROLL_KEYSET 또는 TYPE_SCROLL_SENSITIVE 커서 행의 키 값이 커서로 업데이트되면 행은 업데이트된 행이 커서의 선택 기준에 맞는지에 관계없이 결과 세트에서 원래 위치를 보존합니다. 행이 커서 외부에서 업데이트되었으면 삭제된 행은 행의 원래 위치에 나타나지만 새로운 키 값을 가진 다른 행이 커서에 존재하다가 삭제된 경우에만 커서에 나타납니다.  
  
 동적 커서의 경우 업데이트된 행은 인출 버퍼로 정의된 창이 남아 있을 때까지 인출 버퍼 내에서 위치를 보존합니다. 업데이트된 행은 이후에 결과 집합 내에서 다른 위치에 다시 나타나거나 완전히 사라집니다. 결과 집합에서 일시적인 불일치를 방지해야 하는 응용 프로그램은 인출 크기 1(기본값: CONCUR_SS_SCROLL_LOCKS 동시성을 가진 8개 행 및 다른 동시성을 가진 128개 행)을 사용해야 합니다.  
  
## <a name="cursor-conversion"></a>커서 변환  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 요청된 것과 다른 커서 유형을 구현하도록 선택할 수 있습니다. 이를 암시적 커서 변환(또는 커서 수준 내리기(cursor degradation))이라고 합니다. 암시적 커서 변환에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 “암시적 커서 변환 사용” 항목을 참조하십시오.  
  
 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에서는 TYPE_SCROLL_SENSITIVE 및 resultset CONCUR_UPDATABLE result 집합을 통해 데이터를 업데이트할 때 "커서가 읽기 전용입니다." 라는 메시지와 함께 예외가 throw 됩니다. 이 예외는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에서 해당 결과 집합에 대해 암시적 커서 변환을 수행하여 요청한 업데이트 가능 커서를 반환하지 못했기 때문에 발생합니다.  
  
 이 문제를 해결하기 위해 다음 두 가지 솔루션 중 하나를 수행할 수 있습니다.  
  
-   기본 테이블에 기본 키가 있는지 확인  
  
-   문을 만드는 동안 TYPE_SCROLL_SENSITIVE 대신 [SQLServerResultSet. TYPE_SS_SCROLL_DYNAMIC](../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md) 를 사용 합니다.  
  
## <a name="cursor-updating"></a>커서 업데이트  
 내부 업데이트는 커서 유형 및 동시성이 업데이트를 지원하는 커서에 대해서 지원됩니다. 커서가 결과 집합 내의 업데이트 가능 행에 위치하지 않을 경우(성공된 get\<Type> 메서드 호출 없음) update\<Type> 메서드를 호출하면 “결과 집합에 현재 행이 없습니다.”라는 메시지와 함께 예외가 발생합니다. JDBC 사양에 의하면 CONCUR_READ_ONLY인 커서의 열에 대해 업데이트 메서드를 호출할 경우 예외가 발생할 수 있습니다. 경쟁하는 업데이트 또는 삭제와 같은 낙관적 동시성 충돌 등으로 인해 행을 업데이트할 수 없을 경우 [insertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md), [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 또는 [deleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md)를 호출하면 예외가 발생합니다.  
  
 업데이트\<형식 >에 대 한 호출 후에는 updateRow 또는 [cancelrowupdates](../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md) 가\<호출 될 때까지 get 형식 >에서 영향을 받는 열에 액세스할 수 없습니다. 이를 통해 서버에서 반환하는 유형과 다른 유형을 사용하여 열을 업데이트하여 이후 getter 호출에서 정확하지 않은 결과를 제공하는 클라이언트 쪽 변환을 호출할 수 있는 문제를 방지할 수 있습니다. get\<Type>을 호출하면 “updateRow() 또는 cancelRowUpdates()를 호출하지 않으면 업데이트된 열에 액세스할 수 없습니다.”라는 메시지와 함께 예외가 발생합니다.  
  
> [!NOTE]  
>  업데이트된 열이 없을 때 updateRow 메서드가 호출되면 JDBC 드라이버에서 “업데이트된 열이 없을 때 updateRow()가 호출되었습니다.”라는 메시지와 함께 예외를 발생합니다.  
  
 [moveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md)가 호출된 후 결과 집합에서 get\<Type>, update\<Type>, insertRow 및 커서 위치 지정 메서드([moveToCurrentRow](../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md) 포함) 이외의 메서드를 호출하면 예외가 발생합니다. moveToInsertRow 메서드는 효율적으로 결과 집합을 삽입 모드로 배치하고, 커서 위치 지정 메서드는 삽입 모드를 종료합니다. 관련된 커서 위치 지정 호출은 moveToInsertRow가 호출되기 전의 위치를 기준으로 커서를 이동합니다. 커서 위치 지정 호출 후에 결과 대상 커서 위치는 새 커서 위치가 됩니다.  
  
 삽입 모드에서 커서 위치 지정 호출을 수행할 경우 호출 실패 후의 커서 위치는 moveToInsetRow가 호출되기 전의 원래 커서 위치입니다. insertRow가 실패하면 커서는 삽입 행에 남아 있고 커서는 삽입 모드를 유지합니다.  
  
 삽입 행의 열은 처음에는 초기화되지 않은 상태입니다. update\<Type> 메서드를 호출하면 열 상태를 초기화로 설정합니다. 초기화되지 않은 열에 대해 get\<Type> 메서드를 호출하면 예외가 발생합니다. insertRow 메서드를 호출하면 삽입 행의 모든 열을 초기화되지 않은 상태로 반환합니다.  
  
 insertRow 메서드가 호출될 때 초기화되지 않은 열이 있으면 열의 기본값이 삽입됩니다. 기본값이 없고 열이 Null 값을 허용하면 NULL이 삽입됩니다. 기본값이 없고 열이 Null 값을 허용하지 않으면 서버는 오류를 반환하고 예외가 발생합니다.  
  
> [!NOTE]  
>  getRow 메서드를 호출하면 삽입 모드에서 0을 반환합니다.  
>   
>  JDBC 드라이버는 위치 지정 업데이트 또는 삭제를 지원하지 않습니다. JDBC 사양에 따라 [setCursorName](../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md) 메서드는 영향을 주지 않으며 [getCursorName](../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md) 메서드는 호출 시 예외를 발행합니다.  
>   
>  읽기 전용 및 정적 커서는 업데이트할 수 없습니다.  
>   
>  SQL Server는 서버 커서를 단일 결과 집합으로 제한합니다. 일괄 처리 및 저장 프로시저에 여러 문이 있으면 정방향 읽기 전용 클라이언트 커서를 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버로 결과 집합 관리](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  

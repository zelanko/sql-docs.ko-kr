---
title: "커서 유형 이해 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4f4d3db7-4f76-450d-ab63-141237a4f034
caps.latest.revision: 51
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a65c11a0f6c623162049661a11cbc392a3d8b178
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-cursor-types"></a>커서 유형 이해
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  관계형 데이터베이스에서의 연산은 전체 행 집합에 적용됩니다. SELECT 문에 의해 반환된 행 집합은 문의 WHERE 절 조건을 만족하는 모든 행으로 구성됩니다. SELECT 문에 의해 반환된 전체 행 집합을 결과 집합이라고 합니다. 응용 프로그램에서는 전체 결과 집합을 한 단위로 사용하므로 항상 효과적으로 작업할 수는 없습니다. 이러한 응용 프로그램에는 한 번에 한 행이나 적은 행 블록을 사용하여 작업하는 메커니즘이 필요합니다. 커서는 이러한 메커니즘을 제공하는 결과 집합에 대한 확장입니다.  
  
 커서는 다음을 수행하여 결과 집합 처리를 확장합니다.  
  
-   결과 집합의 특정 행에 위치를 정할 수 있습니다.  
  
-   결과 집합의 현재 위치에서 한 행 또는 행 블록을 검색합니다.  
  
-   결과 집합의 현재 위치에 있는 행 데이터를 수정할 수 있습니다.  
  
-   결과 집합에 나타난 데이터베이스 데이터에 대해 다른 사용자가 변경한 내용을 여러 가지 수준으로 볼 수 있습니다.  
  
> [!NOTE]  
>  에 대 한 전체 설명은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 의 "커서 유형 (데이터베이스 엔진)" 항목을 참조 하는 커서 유형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
 JDBC 사양은 정방향 전용 커서 및 스크롤 가능 커서를 지원합니다. 이러한 커서는 다른 작업으로 인한 변경 사항을 감지하거나 감지하지 못하며 읽기 전용이거나 업데이트 가능합니다. 이 기능을 제공 된 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스입니다.  
  
## <a name="remarks"></a>주의  
 JDBC 드라이버는 다음 커서 유형을 지원합니다.  
  
|결과 집합<br /><br /> (커서) 유형|SQL Server 커서 유형|특징|선택<br /><br /> 메서드|response<br /><br /> 버퍼링|Description|  
|------------------------------------|----------------------------|---------------------|-----------------------|----------------------------|-----------------|  
|TYPE_FORWARD_ONLY(CONCUR_READ_ONLY)|해당 사항 없음|정방향 전용, 읽기 전용|direct|전체|응용 프로그램은 결과 집합을 정방향으로 한 번 통과해야 합니다. 이것은 기본 동작이며 TYPE_SS_DIRECT_FORWARD_ONLY 커서와 동일하게 작동합니다. 드라이버는 문 실행 중 서버의 전체 결과 집합을 메모리로 읽습니다.|  
|TYPE_FORWARD_ONLY(CONCUR_READ_ONLY)|해당 사항 없음|정방향 전용, 읽기 전용|direct|adaptive|응용 프로그램은 결과 집합을 정방향으로 한 번 통과해야 합니다. 이것은 TYPE_SS_DIRECT_FORWARD_ONLY 커서와 동일하게 작동합니다. 드라이버는 응용 프로그램에서 요청할 경우 서버의 행을 읽어 클라이언트 쪽 메모리 사용량을 최소화합니다.|  
|TYPE_FORWARD_ONLY(CONCUR_READ_ONLY)|빠른 정방향|정방향 전용, 읽기 전용|cursor|해당 사항 없음|응용 프로그램은 서버 커서를 사용하여 결과 집합을 정방향으로 한 번 통과해야 합니다. 이 유형은 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY 커서와 동일하게 동작합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_FORWARD_ONLY(CONCUR_UPDATABLE)|동적(정방향 전용)|정방향 전용, 업데이트 가능|해당 사항 없음|해당 사항 없음|응용 프로그램은 한 개 이상의 행을 업데이트하기 위해 결과 집합을 정방향으로 한 번 통과해야 합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.<br /><br /> 기본적으로 인출 크기는 응용 프로그램 호출 때 고정 됩니다는 [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) 의 메서드는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.<br /><br /> **참고:** JDBC 드라이버는에서 문 실행 결과 검색할 수 있는 선택 버퍼링 기능이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 응용 프로그램에서 필요할 때 보다는 한 번에 모두 있습니다. 예를 들어 너무 커서 응용 프로그램 메모리에 한 번에 저장할 수 없는 큰 데이터를 검색해야 하는 경우 클라이언트 응용 프로그램에서는 이러한 값을 스트림으로 검색할 수 있습니다. 드라이버의 기본 동작은 "**적응**"입니다. 그러나 정방향 전용 업데이트 가능 결과 집합에 대해 선택 버퍼링 가져오려면 응용 프로그램에 명시적으로 호출 하 여 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 의 메서드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 개체 제공 하 여 한 **문자열** 값 "**적응"**합니다. 예제 코드를 보려면 참조 [큰 데이터 업데이트 샘플](../../connect/jdbc/updating-large-data-sample.md)합니다.|  
|TYPE_SCROLL_INSENSITIVE|정적|스크롤 가능, 업데이트 불가능<br /><br /> 외부 행 업데이트, 삽입 및 삭제는 표시되지 않음|해당 사항 없음|해당 사항 없음|응용 프로그램에 데이터베이스 스냅숏이 필요합니다. 결과 집합을 업데이트할 수 없습니다. CONCUR_READ_ONLY만 지원됩니다.  이외에 다른 모든 동시성 유형을 이 커서 유형과 함께 사용하는 경우 예외가 발생합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_READ_ONLY)|Keyset|스크롤 가능, 읽기 전용 외부 행 업데이트는 표시되며, 삭제는 데이터 누락으로 나타남<br /><br /> 외부 행 삽입은 표시되지 않음|해당 사항 없음|해당 사항 없음|응용 프로그램은 기존 행의 변경된 데이터만 볼 수 있어야 합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Keyset|스크롤 가능 및 업데이트 가능.<br /><br /> 외부 및 내부 행 업데이트는 표시되고 삭제는 데이터 누락으로 나타나며, 삽입은 표시되지 않음|해당 사항 없음|해당 사항 없음|응용 프로그램에는 ResultSet 개체를 사용 하 여 기존 행의에서 데이터를 변경할 수 있습니다. 응용 프로그램은 결과 집합 개체 외부에서 다른 사용자가 변경한 행에 변경 내용을 확인할 수 있어야도 합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_SS_DIRECT_FORWARD_ONLY|해당 사항 없음|정방향 전용, 읽기 전용|해당 사항 없음|전체 또는 선택|정수 값 = 2003. 완전히 버퍼링되는 읽기 전용 클라이언트 쪽 커서를 제공합니다. 서버 커서가 만들어지지 않습니다.<br /><br /> CONCUR_READ_ONLY 동시성 유형만 지원됩니다. 이외에 다른 모든 동시성 유형을 이 커서 유형과 함께 사용하는 경우 예외가 발생합니다.|  
|TYPE_SS_SERVER_CURSOR_FORWARD_ONLY|빠른 정방향|정방향 전용|해당 사항 없음|해당 사항 없음|정수 값 = 2004. 서버 커서를 사용하여 모든 데이터에 빠르게 액세스합니다. CONCUR_UPDATABLE 동시성 유형과 함께 사용하는 경우 업데이트할 수 있습니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.<br /><br /> 이 경우에 대해 선택 버퍼링을 가져오려면 응용 프로그램에 명시적으로 호출 된 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 의 메서드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 개체를 제공 하는 **문자열 ** 값 "**적응"**합니다. 예제 코드를 보려면 참조 [큰 데이터 업데이트 샘플](../../connect/jdbc/updating-large-data-sample.md)합니다.|  
|TYPE_SS_SCROLL_STATIC|정적|다른 사용자의 업데이트는 반영 안 됨|해당 사항 없음|해당 사항 없음|정수 값 = 1004. 응용 프로그램에 데이터베이스 스냅숏이 필요합니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-JDBC TYPE_SCROLL_INSENSITIVE에 대 한 동의어 많고 동시성 설정 동작이 동일 합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_READ_ONLY)|Keyset|스크롤 가능, 읽기 전용. 외부 행 업데이트는 표시되며, 삭제는 데이터 누락으로 나타남<br /><br /> 외부 행 삽입은 표시되지 않음|해당 사항 없음|해당 사항 없음|정수 값 = 1005. 응용 프로그램은 기존 행의 변경된 데이터만 볼 수 있어야 합니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-JDBC TYPE_SCROLL_SENSITIVE에 대 한 동의어 있으며 동시성 설정 동작이 동일 합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Keyset|스크롤 가능 및 업데이트 가능.<br /><br /> 외부 및 내부 행 업데이트는 표시되고 삭제는 데이터 누락으로 나타나며, 삽입은 표시되지 않음|해당 사항 없음|해당 사항 없음|정수 값 = 1005. 응용 프로그램은 기존 행의 데이터를 변경하거나 기존 행의 변경된 데이터를 볼 수 있어야 합니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-JDBC TYPE_SCROLL_SENSITIVE에 대 한 동의어 있으며 동시성 설정 동작이 동일 합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_READ_ONLY)|Dynamic|스크롤 가능, 읽기 전용<br /><br /> 외부 행 업데이트와 삽입은 표시되고 삭제는 현재 인출 버퍼에서 일시적인 데이터 누락으로 나타남|해당 사항 없음|해당 사항 없음|정수 값 = 1006. 응용 프로그램은 기존 행의 변경된 데이터를 볼 수 있어야 하고, 커서의 수명 기간 동안 삽입되거나 삭제된 행을 볼 수 있어야 합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Dynamic|스크롤 가능 및 업데이트 가능.<br /><br /> 외부 및 내부 행 업데이트와 삽입은 표시되고 삭제는 현재 인출 버퍼에서 일시적인 데이터 누락으로 나타남|해당 사항 없음|해당 사항 없음|정수 값 = 1006. 응용 프로그램 기존 행에 대 한 데이터를 변경 또는 삽입 하거나 결과 집합 개체를 사용 하 여 행을 삭제할 수 있습니다. 응용 프로그램 변경, 삽입 및 ResultSet 개체 외부에서 다른 사람이 수행한 삭제를 볼 수도 해야 합니다.<br /><br /> 행이 인출 크기에 지정된 블록의 서버에서 검색됩니다.|  
  
## <a name="cursor-positioning"></a>커서 위치 지정  
 TYPE_FORWARD_ONLY, TYPE_SS_DIRECT_FORWARD_ONLY 및 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY 커서 지원만 [다음](../../connect/jdbc/reference/next-method-sqlserverresultset.md) 위치 지정 메서드만 있습니다.  
  
 TYPE_SS_SCROLL_DYNAMIC 커서는 지원 하지는 [절대](../../connect/jdbc/reference/absolute-method-sqlserverresultset.md) 및 [getRow](../../connect/jdbc/reference/getrow-method-sqlserverresultset.md) 메서드. Absolute 메서드 호출 조합으로 나타낼 수 있습니다는 [첫 번째](../../connect/jdbc/reference/first-method-sqlserverresultset.md) 및 [상대](../../connect/jdbc/reference/relative-method-sqlserverresultset.md) 동적 커서에 대 한 메서드.  
  
 GetRow 메서드는 TYPE_FORWARD_ONLY, TYPE_SS_DIRECT_FORWARD_ONLY, TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, TYPE_SS_SCROLL_KEYSET 및 TYPE_SS_SCROLL_STATIC 커서로 지원 됩니다. 모든 정방향 전용 커서 유형으로 getRow 메서드는 지금까지 커서를 통해 읽은 행 수를 반환 합니다.  
  
> [!NOTE]  
>  응용 프로그램 통화 또는 getRow 메서드는 지원 되지 않는 호출 위치를 지정 하는 지원 되지 않는 커서를 하면 메시지와 함께 예외가, "요청 된 작업이이 커서 유형과 함께 지원 되지 않습니다."  
  
 TYPE_SS_SCROLL_KEYSET 및 동일한 TYPE_SCROLL_SENSITIVE 커서는 삭제된 행을 표시합니다. 열 값을 사용할 수 없는 경우 삭제 된 행에 커서가 및 [rowDeleted](../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) 메서드는 "true"를 반환 합니다. 호출을\<유형 > 메서드는 메시지와 함께 예외를 throw, "삭제 된 행에서 값을 가져올 수 없습니다". 삭제된 행은 업데이트할 수 없습니다. 업데이트를 호출 하려고 하면\<유형 > 삭제 된 행에 대 한 메서드, 메시지와 함께 예외가, "삭제 된 행을 업데이트할 수 없습니다."입니다. TYPE_SS_SCROLL_DYNAMIC 커서는 현재 인출 버퍼 외부로 이동할 때까지 동일한 동작을 수행합니다.  
  
 정방향 및 동적 커서는 인출 버퍼에서 액세스할 수 있는 경우에만 삭제된 행을 동일한 방식으로 표시합니다. 정방향 커서의 경우 이 작업은 비교적 간단합니다. 동적 커서의 경우 인출 크기가 1보다 크면 작업이 더 복잡해집니다. 응용 프로그램은 인출 버퍼로 정의된 창 내에서 커서를 앞뒤로 이동할 수 있지만, 업데이트되었던 원래 인출 버퍼를 벗어나는 경우 삭제된 행은 사라집니다. 응용 프로그램에서 동적 커서를 사용하여 일시적으로 삭제된 행을 표시하지 않으려면 인출 상대 값(0)을 사용해야 합니다.  
  
 TYPE_SS_SCROLL_KEYSET 또는 TYPE_SCROLL_SENSITIVE 커서 행의 키 값이 커서로 업데이트되면 행은 업데이트된 행이 커서의 선택 기준에 맞는지에 관계없이 결과 집합에서 원래 위치를 보존합니다. 행이 커서 외부에서 업데이트되었으면 삭제된 행은 행의 원래 위치에 나타나지만 새로운 키 값을 가진 다른 행이 커서에 존재하다가 삭제된 경우에만 커서에 나타납니다.  
  
 동적 커서의 경우 업데이트된 행은 인출 버퍼로 정의된 창이 남아 있을 때까지 인출 버퍼 내에서 위치를 보존합니다. 업데이트된 행은 이후에 결과 집합 내에서 다른 위치에 다시 나타나거나 완전히 사라집니다. 결과 집합에서 일시적인 불일치를 방지해야 하는 응용 프로그램은 인출 크기 1(기본값: CONCUR_SS_SCROLL_LOCKS 동시성을 가진 8개 행 및 다른 동시성을 가진 128개 행)을 사용해야 합니다.  
  
## <a name="cursor-conversion"></a>커서 변환  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]요청 된 것과 다른 커서 유형을 구현 하도록 선택할 수 있습니다, 그리고 참조 되는 있는 암시적 커서 변환 (또는 커서 성능 저하). 암시적 커서 변환에 대 한 자세한 내용은의 "암시적 커서 변환 사용" 항목을 참조 하십시오. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
 와 [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)]ResultSet.TYPE_SCROLL_SENSITIVE 및 ResultSet.CONCUR_UPDATABLE 결과 통해 데이터를 업데이트 하는 경우, 설정는 메시지 "는 커서가 읽기 전용"와 함께 예외가 throw 됩니다. 이 예외가 발생 하기 때문에 [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)] 에서 해당 결과 집합 요청한 업데이트 가능 커서를 반환 하지 않았습니다에 대해 암시적 커서 변환을 수행 합니다.  
  
 이 문제를 해결하기 위해 다음 두 가지 솔루션 중 하나를 수행할 수 있습니다.  
  
-   기본 테이블에 기본 키가 있는지 확인  
  
-   사용 하 여 [SQLServerResultSet.TYPE_SS_SCROLL_DYNAMIC](../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md) ResultSet.TYPE_SCROLL_SENSITIVE 문을 만드는 동안 대신 합니다.  
  
## <a name="cursor-updating"></a>커서 업데이트  
 내부 업데이트는 커서 유형 및 동시성이 업데이트를 지원하는 커서에 대해서 지원됩니다. 커서는 결과 집합의 업데이트 가능 행에 위치 하지 않을 경우 (없음 get\<유형 > 메서드 호출에 성공), 업데이트에 대 한 호출\<유형 > 메서드는 메시지와 함께 예외를 throw 합니다, "결과 집합에는 현재 행이 없습니다." JDBC 사양에 의하면 CONCUR_READ_ONLY인 커서의 열에 대해 업데이트 메서드를 호출할 경우 예외가 발생할 수 있습니다. 경쟁 하는 업데이트 또는 삭제와 같은 낙관적 동시성 충돌 때문에 행이 업데이트할 수와 같은 있지 않은 경우는 예외가 하지 발생 될 때까지 [insertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md), [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md), 또는 [deleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md) 호출 됩니다.  
  
 업데이트를 호출한 후\<유형 >, get 영향을 받는 열에 액세스할 수 없습니다\<유형 > updateRow 될 때까지 또는 [cancelRowUpdates](../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md) 가 호출 합니다. 이를 통해 서버에서 반환하는 유형과 다른 유형을 사용하여 열을 업데이트하여 이후 getter 호출에서 정확하지 않은 결과를 제공하는 클라이언트 쪽 변환을 호출할 수 있는 문제를 방지할 수 있습니다. 호출을\<유형 > 메시지와 함께 예외를 throw 합니다, "updaterow () 업데이트 된 열에 액세스할 수 없거나 또는 cancelrowupdates."  
  
> [!NOTE]  
>  UpdateRow 메서드를 호출 하 경우 열이 없으면 업데이트 될 때 JDBC 드라이버는 메시지와 함께 예외를 throw 합니다, 그리고 "updaterow () 열이 없는 경우 호출 업데이트 되었습니다."  
  
 후 [moveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) 된 호출에서 예외가 throw 됩니다 발생 하지 않고 다른 방법\<유형 >, 업데이트\<유형 >, insertRow, 및 커서 위치 지정 메서드 (포함 하 여 [ moveToCurrentRow](../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md))은 결과 집합에서 호출 합니다. MoveToInsertRow 메서드는 효율적으로 결과 집합을 삽입 모드로 배치 하 고 커서 위치 지정 메서드는 삽입 모드를 종료 합니다. 관련 된 커서 위치 지정 호출은 moveToInsertRow가 호출 되기 전에 당시 위치를 기준으로 커서를 이동 합니다. 커서 위치 지정 호출 후에 결과 대상 커서 위치는 새 커서 위치가 됩니다.  
  
 커서 위치 지정 호출 되는 삽입에서 모드에 실패 하는 동안 수행 된 후 실패 한 호출 moveToInsetRow 전의 원래 커서 위치는 커서 위치를 호출 했습니다 하는 경우. InsertRow가 실패 하면 커서는 삽입 행에 남아 않으며 커서에 남아 모드를 삽입 합니다.  
  
 삽입 행의 열은 처음에는 초기화되지 않은 상태입니다. 업데이트에 대 한 호출\<유형 > 방법이 설정 하면 열 상태 초기화 합니다. 호출을 get\<유형 > 메서드에서 초기화 되지 않은 열에 대 한 예외를 throw 합니다. InsertRow 메서드를 호출 하면 삽입 행의 초기화 되지 않은 상태로 있는 모든 열의 반환합니다.  
  
 InsertRow 메서드를 호출할 때 모든 열을 초기화 되지 않은, 열에 대 한 기본 값이 삽입 됩니다. 기본값이 없고 열이 Null 값을 허용하면 NULL이 삽입됩니다. 기본값이 없고 열이 Null 값을 허용하지 않으면 서버는 오류를 반환하고 예외가 발생합니다.  
  
> [!NOTE]  
>  GetRow 메서드를 호출 하면 삽입 모드에서에서 0을 반환 합니다.  
>   
>  JDBC 드라이버는 위치 지정 업데이트 또는 삭제를 지원하지 않습니다. JDBC 사양에 따라는 [setCursorName](../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md) 메서드에서 아무 작업도 및 [getCursorName](../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md) 메서드 호출 하면 예외가 throw 됩니다.  
>   
>  읽기 전용 및 정적 커서는 업데이트할 수 없습니다.  
>   
>  SQL Server는 서버 커서를 단일 결과 집합으로 제한합니다. 일괄 처리 및 저장 프로시저에 여러 문이 있으면 정방향 읽기 전용 클라이언트 커서를 사용해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 결과 집합 관리](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  


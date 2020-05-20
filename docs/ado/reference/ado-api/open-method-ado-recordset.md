---
title: Open 메서드 (ADO 레코드 집합) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Open
- Recordset15::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 3236749c-4b71-4235-89e2-ccdfaaa9319d
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a091a606cf3049c055794bc16cc51db78a40978
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762181"
---
# <a name="open-method-ado-recordset"></a>Open 메서드(ADO 레코드 집합)
[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체에 대 한 커서를 엽니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>매개 변수  
 *소스*  
 (선택 사항) 유효한 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체, SQL 문, 테이블 이름, 저장 프로시저 호출, URL 또는 영구적으로 저장 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)을 포함 하는 파일 또는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체의 이름으로 계산 되는 **Variant** 입니다.  
  
 *ActiveConnection*  
 (선택 사항) 유효한 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 변수 이름으로 계산 되는 **변형** 이거나, [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 매개 변수를 포함 하는 **문자열** 입니다.  
  
 *CursorType*  
 (선택 사항) **레코드 집합**을 열 때 공급자가 사용 해야 하는 커서의 유형을 결정 하는 [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) 값입니다. 기본값은 **Adopenforwardonly**입니다.  
  
 *LockType*  
 (선택 사항) **레코드 집합**을 열 때 공급자가 사용 해야 하는 잠금 유형 (동시성)을 결정 하는 [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) 값입니다. 기본값은 **Adlockreadonly**입니다.  
  
 *Options*  
 (선택 사항) 공급자가 **명령** 개체 이외의 항목을 나타내거나 이전에 저장 된 파일에서 **레코드 집합** 을 복원 해야 하는 경우에 *소스* 인수를 평가 하는 방법을 나타내는 **Long** 값입니다. 비트 OR 연산자와 함께 사용할 수 있는 하나 이상의 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 또는 [executeto 열거형](../../../ado/reference/ado-api/executeoptionenum.md) 값이 될 수 있습니다.  
  
> [!NOTE]
>  지속형 **레코드 집합**을 포함 하는 **스트림에서** **레코드 집합** 을 여는 경우 **Adasyncfetchnonblocking** 의 [executeoptionenum](../../../ado/reference/ado-api/executeoptionenum.md) 값을 사용 하면 아무런 효과가 없습니다. fetch는 동기식 이며 차단 됩니다.  
  
> [!NOTE]
>  **AdExecuteNoRecords** 또는 **AdExecuteStream** 의 **Executeopenenum** 값은 **Open**과 함께 사용 하면 안 됩니다.  
  
## <a name="remarks"></a>설명  
 ADO **레코드 집합** 의 기본 커서는 서버에 있는 앞 으로만 이동 가능한 읽기 전용 커서입니다.  
  
 **레코드 집합** 개체에 대해 **Open** 메서드를 사용 하면 기본 테이블의 레코드, 쿼리 결과 또는 이전에 저장 된 **레코드 집합**을 나타내는 커서가 열립니다.  
  
 선택적 *source* 인수를 사용 하 여 **명령** 개체 변수, SQL 문, 저장 프로시저, 테이블 이름, URL 또는 전체 파일 경로 이름 중 하나를 사용 하 여 데이터 원본을 지정할 수 있습니다. *Source* 가 파일 경로 이름인 경우 전체 경로 ("c:\dir\file.rst"), 상대 경로 (".. \file.rst ") 또는 URL (" <https://files/file.rst> ")이 있습니다.  
  
 호출의 성공 여부를 쉽게 확인할 수 있는 방법이 없기 때문에 레코드를 반환 하지 않는 작업 쿼리를 수행 하는 데 **Open** 메서드의 *Source* 인수를 사용 하는 것은 좋지 않습니다. 이러한 쿼리에서 반환 되는 **레코드 집합** 은 닫힙니다. SQL INSERT 문과 같이 레코드를 반환 하지 않는 쿼리를 수행 하려면 대신 **Command** 개체의 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드 또는 [Connection](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 메서드를 호출 합니다.  
  
 *ActiveConnection* 인수는 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성에 해당 하며, **레코드 집합** 개체를 열 연결을 지정 합니다. 이 인수에 대 한 연결 정의를 전달 하면 ADO에서 지정 된 매개 변수를 사용 하 여 새 연결을 엽니다. [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**로 설정 하 여 클라이언트 쪽 커서를 사용 하 여 **레코드 집합** 을 연 후에는이 속성의 값을 변경 하 여 다른 공급자에 게 업데이트를 보낼 수 있습니다. 또는이 속성을 **Nothing** (Microsoft Visual Basic)으로 설정 하거나 NULL로 설정 하 여 모든 공급자에서 **레코드 집합** 의 연결을 끊을 수 있습니다. 그러나 서버 쪽 커서에 대 한 *ActiveConnection* 를 변경 하면 오류가 생성 됩니다.  
  
 **레코드 집합** 개체 (*Source*, *CursorType*및 *LockType*)의 속성에 직접 대응 하는 다른 인수에 대 한 인수는 다음과 같습니다.  
  
-   이 속성은 **레코드 집합** 개체가 열리기 전에 읽기/쓰기입니다.  
  
-   속성 설정은 **Open** 메서드를 실행할 때 해당 인수를 전달 하지 않는 한 사용 됩니다. 인수를 전달 하면 해당 속성 설정이 재정의 되 고 속성 설정이 인수 값으로 업데이트 됩니다.  
  
-   **레코드 집합** 개체를 열면 이러한 속성이 읽기 전용이 됩니다.  
  
> [!NOTE]
>  **ActiveConnection** 속성은 **레코드 집합** 개체가 열려 있지 않아도 [원본](../../../ado/reference/ado-api/source-property-ado-recordset.md) 속성이 유효한 **명령** 개체로 설정 된 **레코드 집합** 개체에 대해 읽기 전용입니다.  
  
 *Source* 인수에서 **Command** 개체를 전달 하 고 *ActiveConnection* 인수도 전달 하면 오류가 발생 합니다. **Command** 개체의 **ActiveConnection** 속성은 이미 올바른 **연결** 개체 또는 연결 문자열로 설정 되어 있어야 합니다.  
  
 *원본* 인수에서 **Command** 개체 이외의 다른 항목을 전달 하는 경우 *Options* 인수를 사용 하 여 *소스* 인수의 계산을 최적화할 수 있습니다. *옵션* 인수가 정의 되지 않은 경우 ADO에서 인수가 SQL 문, 저장 프로시저, URL 또는 테이블 이름 인지 확인 하기 위해 공급자를 호출 해야 하기 때문에 성능이 저하 될 수 있습니다. 사용 중인 *원본* 유형을 알고 있는 경우 *Options* 인수를 설정 하면 ADO가 관련 코드로 직접 이동 합니다. *Options* 인수가 *원본* 유형과 일치 하지 않으면 오류가 발생 합니다.  
  
 *원본* 인수에서 **Stream** 개체를 전달 하는 경우 다른 인수로 정보를 전달 하면 안 됩니다. 사용할 경우 오류가 발생합니다. **ActiveConnection** 정보는 **스트림에서** **레코드 집합** 을 열 때 유지 되지 않습니다.  
  
 *옵션* 인수의 기본값은 **레코드 집합과**연결 된 연결이 없는 경우 **adcmdfile** 입니다. 이는 일반적으로 영구적으로 저장 된 **레코드 집합** 개체의 경우에 해당 합니다.  
  
 데이터 원본에서 레코드를 반환 하지 않는 경우 공급자는 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 및 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성을 모두 **True**로 설정 하 고 현재 레코드 위치는 정의 되지 않습니다. 커서 유형에 서 허용 되는 경우이 빈 **레코드 집합** 개체에 새 데이터를 추가할 수 있습니다.  
  
 열려 있는 **레코드 집합** 개체에 대 한 작업을 완료 한 경우 [Close](../../../ado/reference/ado-api/close-method-ado.md) 메서드를 사용 하 여 연결 된 시스템 리소스를 해제 합니다. 개체를 닫으면 메모리가 제거 되지 않습니다. 속성 설정을 변경 하 고 **open** 메서드를 사용 하 여 나중에 다시 열 수 있습니다. 메모리에서 개체를 완전히 제거 하려면 개체 변수를 *Nothing*으로 설정 합니다.  
  
 **ActiveConnection** 속성을 설정 하기 전에 피연산자가 없는 **Open** 을 호출 하 여 **레코드 집합** [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에 필드를 추가 하 여 만든 **레코드 집합** 의 인스턴스를 만듭니다.  
  
 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**로 설정한 경우 다음 두 가지 방법 중 하나를 통해 비동기적으로 행을 검색할 수 있습니다. 권장 방법은 *옵션* 을 **adasyncfetch**로 설정 하는 것입니다. 또는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에서 "비동기 행 집합 처리" 동적 속성을 사용할 수 있지만 *Options* 매개 변수를 **adasyncfetch**로 설정 하지 않으면 관련 검색 된 이벤트가 손실 될 수 있습니다.  
  
> [!NOTE]
>  MS 원격 공급자에서의 배경 페치는 **Open** 메서드의 *Options* 매개 변수를 통해서만 지원 됩니다.  
  
> [!NOTE]
>  Http 체계를 사용 하는 Url은 자동으로 [Microsoft OLE DB 공급자에 게 Internet 게시용](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)으로 호출 됩니다. 자세한 내용은 [절대 및 상대 url](../../../ado/guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 및 [executeoptionenum](../../../ado/reference/ado-api/executeoptionenum.md) 값의 특정 조합이 잘못 되었습니다. 결합할 수 없는 옵션에 대 한 자세한 내용은 [execute옵션 열거형](../../../ado/reference/ado-api/executeoptionenum.md)및 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)에 대 한 항목을 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Open 및 Close 메서드 예제 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 및 Close 메서드 예제 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 및 Close 메서드 예제 (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Save 및 Open 메서드 예제 (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Open 메서드 (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 메서드 (ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 메서드 (ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 메서드](../../../ado/reference/ado-api/openschema-method.md)   
 [Save 메서드](../../../ado/reference/ado-api/save-method.md)

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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9aee9b4f6054b5cbfca41db35f34a27000a7ac01
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719222"
---
# <a name="open-method-ado-recordset"></a>Open 메서드(ADO 레코드 집합)
커서를 엽니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 (선택 사항) A **Variant** 유효한로 평가 되는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체, SQL 문, 테이블 이름, 저장된 프로시저 호출, URL 또는 파일의 이름 또는 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체를 포함 하는 영구적으로 저장 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
 *ActiveConnection*  
 (선택 사항) 중 하나를 **Variant** 유효한 계산 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 변수 이름 또는 **문자열** 포함 하는 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 매개 변수입니다.  
  
 *CursorType*  
 (선택 사항) A [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) 공급자를 열 때 사용 해야 하는 커서의 형식을 결정 하는 값을 **레코드 집합**합니다. 기본값은 **adOpenForwardOnly**합니다.  
  
 *LockType*  
 (선택 사항) A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) 사용할지 결정 하는 어떤 유형의 잠금 (동시성) 공급자를 열 때 값을 **Recordset**합니다. 기본값은 **adLockReadOnly**합니다.  
  
 *Options*  
 (선택 사항) **긴** 공급자를 평가 해야 하는 방법을 나타내는 값을 *원본* 것 이외의 다른 나타내는 경우 인수는 **명령** 개체 또는 합니다 **레코드 집합** 이전에 저장 된 파일에서 복원 해야 합니다. 하나 이상의 수 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 하거나 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 값을 비트 OR 연산자를 함께 사용할 수 있습니다.  
  
> [!NOTE]
>  열면를 **레코드 집합** 에서 **Stream** 포함 된 지속형 **레코드 집합**를 사용 하 여는 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 값**adAsyncFetchNonBlocking** 영향을 주지 것입니다; fetch는 동기 및 차단 됩니다.  
  
> [!NOTE]
>  합니다 **ExecuteOpenEnum** 의 값 **adExecuteNoRecords** 또는 **adExecuteStream** 사용 하 여 사용할 수 없습니다 **열기**합니다.  
  
## <a name="remarks"></a>Remarks  
 ADO에 대 한 기본 커서 **레코드 집합** 는 서버에 있는 읽기 전용, 정방향 전용 커서입니다.  
  
 사용 하 여는 **엽니다** 메서드를 **레코드 집합** 개체는 기본 테이블, 쿼리 또는 이전에 저장 된 결과에서 레코드를 나타내는 커서를 엽니다 **레코드 집합**.  
  
 옵션을 사용 하 여 *원본* 중 하나를 사용 하 여 데이터 원본을 지정 하려면 인수:를 **명령** 개체 변수, SQL 문, 저장된 프로시저, 테이블 이름, URL 또는 전체 파일 경로 이름입니다. 하는 경우 *원본* 는 파일 경로 이름에 전체 경로 ("c:\dir\file.rst"), 상대 경로 수 있습니다 ("... \file.rst"), 또는 URL ("<https://files/file.rst>").  
  
 사용 하는 좋은 방법이 아닙니다 합니다 *원본* 인수를 **열기** 메서드 호출에 성공 했는지 여부를 확인 하려면 쉬운 방법이 없기 때문에 레코드를 반환 하지 않는 작업 쿼리를 수행 하 합니다. 합니다 **레코드 집합** 등 반환한 쿼리 닫히게 됩니다. 호출 SQL INSERT 문과 같은 레코드를 반환 하지 않는 쿼리를 수행 하는 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드를 **명령** 개체 또는 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 메서드의 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체를 대신 합니다.  
  
 *ActiveConnection* 인수에 해당 합니다 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성 연결을 열고 지정를 **레코드 집합** 개체입니다. 이 인수에 대 한 연결 정의 전달 하는 경우 ADO는 지정된 된 매개 변수를 사용 하 여 새 연결을 엽니다. 연 후 합니다 **레코드 집합** 설정 하 여 클라이언트 쪽 커서를 사용 하 여 합니다 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**를 보내도록이 속성의 값을 변경할 수 있습니다 다른 공급자를 업데이트 합니다. 이 속성 설정할 수 있습니다 **아무** (Microsoft Visual Basic) 또는 연결을 끊을 NULL를 **레코드 집합** 모든 공급자에서. 하지만 변경 *ActiveConnection* 서버측 커서에서 오류를 생성 합니다.  
  
 속성에 해당 하는 다른 인수를 **레코드 집합** 개체 (*원본*를 *CursorType*, 및 *LockType*), 속성에 대 한 인수의 관계는 다음과 같습니다.  
  
-   속성은 읽기/쓰기 전에 합니다 **레코드 집합** 개체가 열려 있습니다.  
  
-   속성 설정을 실행 하는 경우 해당 인수를 전달 하지 않은 경우 사용 되는 **열기** 메서드. 인수를 전달 하는 경우 해당 하는 속성 설정을 재정의 하 고 속성 설정을 인수 값으로 업데이트 됩니다.  
  
-   연 후는 **레코드 집합** 개체를 이러한 속성 읽기 전용이 됩니다.  
  
> [!NOTE]
>  합니다 **ActiveConnection** 에 대 한 읽기 전용 속성은 **레코드 집합** 갖는 개체 [원본](../../../ado/reference/ado-api/source-property-ado-recordset.md) 속성은 유효한 **명령** 개체 경우에 합니다 **레코드 집합** 개체 열려 있지 않습니다.  
  
 전달 하는 경우는 **명령** 개체를 *원본* 인수 및 패스를 *ActiveConnection* 인수 오류가 발생 합니다. **ActiveConnection** 의 속성을 **명령** 유효한 개체 설정 되어 있어야 **연결** 개체 또는 연결 문자열입니다.  
  
 것 이외의 전달 하는 경우는 **명령** 개체를 *원본* 인수를 사용할 수는 *옵션* 평가 최적화 하는 인수는 *원본*  인수입니다. 경우는 *옵션* 인수 정의 하지 않으면, ADO 인수 SQL 문, 저장된 프로시저, URL 또는 테이블 이름 인지 확인 하는 공급자에 대 한 호출을 확인 해야 하기 때문에 성능이 저하 될 수 있습니다. 무엇을 알고 있는 경우 *소스* 설정, 사용 중인 형식을 합니다 *옵션* 인수 관련 코드를 직접 이동할 수는 ADO에 지시 합니다. 경우는 *옵션* 인수가 일치 하지 않습니다는 *원본* 입력에 오류가 발생 합니다.  
  
 전달 하는 경우는 **Stream** 개체를 *원본* 인수를 전달 해서는 안 정보 다른 인수에 있습니다. 이렇게 하면 오류가 생성 됩니다. **ActiveConnection** 정보 없는 경우 보존을 **레코드 집합** 에서 열리는 **Stream**합니다.  
  
 에 대 한 기본값을 *옵션* 인수가 **adCmdFile** 없는 연결 된 경우를 **레코드 집합**합니다. 이 일반적으로 사용 됩니다 영구적으로 저장 **레코드 집합** 개체입니다.  
  
 공급자를 모두 설정 하는 데이터 원본이 없는 레코드를 반환 하는 경우는 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 및 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성을 **True**, 고 현재 레코드 위치가 정의 되지 않습니다. 이 비어 있는 것으로 새 데이터를 계속 추가할 수 있습니다 **레코드 집합** 개체 커서 유형을 사용 하면 수 있습니다.  
  
 열려 있는 작업을 완료 있을 때 **레코드 집합** 개체를 사용 합니다 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 관련 시스템 리소스를 해제 하는 방법입니다. 개체 닫기지 않습니다 하지 메모리에서 제거 합니다. 해당 속성 설정을 변경 하 고 사용할 수 있습니다 합니다 **엽니다** 나중에 다시 열면 하는 방법입니다. 메모리에서 개체를 완전히 제거 하려면 개체 변수를 설정 합니다 *Nothing*합니다.  
  
 전에 **ActiveConnection** 속성이 설정 되 면 호출 **열려** 의 인스턴스를 만드는 없음 피연산자를 사용 하 여는 **레코드 집합** 필드를 추가 하 여 만든는  **레코드 집합** [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션입니다.  
  
 설정한 경우 합니다 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**, 두 가지 방법 중 하나에서 비동기적으로 행을 검색할 수 있습니다. 설정 하는 것이 좋습니다 *옵션* 하 **adAsyncFetch**합니다. 또는의 "비동기 행 집합 Processing" 동적 속성을 사용할 수는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 있고 관련된 검색된 이벤트 손실 될 수 있습니다 설정 하지 않은 경우 합니다 *옵션* 매개변수**adAsyncFetch**합니다.  
  
> [!NOTE]
>  통해서만 지원 되는 MS 원격 공급자에서 백그라운드 페치를 **엽니다** 메서드의 *옵션* 매개 변수입니다.  
  
> [!NOTE]
>  Http 체계를 사용 하 여 Url은 자동으로 호출 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 [절대 및 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
 특정 조합의 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 하 고 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 값이 잘못 되었습니다. 에 대 한 옵션을 함께 수 없습니다. 내용은 항목을 참조 하십시오.는 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md), 및 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Open 및 Close 메서드 예제 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 및 Close 메서드 예제 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 및 Close 메서드 예제 (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Save 및 Open 메서드 예제 (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Open 메서드 (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 메서드 (ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 메서드 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 메서드](../../../ado/reference/ado-api/openschema-method.md)   
 [Save 메서드](../../../ado/reference/ado-api/save-method.md)

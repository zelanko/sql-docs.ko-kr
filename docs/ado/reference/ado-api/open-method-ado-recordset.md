---
title: "Open 메서드 (ADO 레코드 집합) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::raw_Open
- Recordset15::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 3236749c-4b71-4235-89e2-ccdfaaa9319d
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1977d0381311ac2d7f43bd161099d1f0eb0f6665
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="open-method-ado-recordset"></a>Open 메서드 (ADO 레코드 집합)
커서를 열고는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 (선택 사항) A **Variant** 유효한으로 계산 되는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체, SQL 문, 테이블 이름, 저장된 프로시저 호출, URL 또는 파일의 이름 또는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 포함 된 개체는 영구적으로 저장 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
 *ActiveConnection*  
 (선택 사항) 어느 한 **Variant** 유효한으로 계산 되는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 변수 이름 또는 **문자열** 포함 된 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 매개 변수입니다.  
  
 *모두*  
 (선택 사항) A [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) 값 공급자를 열 때 사용 해야 하는 커서의 형식을 결정 하는 **레코드 집합**합니다. 기본값은 **adOpenForwardOnly**합니다.  
  
 *LockType*  
 (선택 사항) A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) 사용할지 결정 하는 어떤 유형의 잠금 (동시성) 공급자를 열 때 값은 **레코드 집합**합니다. 기본값은 **adLockReadOnly**합니다.  
  
 *옵션*  
 (선택 사항) A **긴** 공급자를 평가 하는 방식을 나타내는 값의 *소스* 인수를 나타냅니다 이외의 경우는 **명령** 개체 또는 하는 **레코드 집합** 이전에 저장 된 파일에서 복원 해야 합니다. 하나 이상의 수 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 또는 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 비트 OR 연산자를 함께 사용할 수 있는 값입니다.  
  
> [!NOTE]
>  여는 경우는 **레코드 집합** 에서 **스트림** 포함 하는 지속형 **레코드 집합**를 사용 하 여는 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 값**adAsyncFetchNonBlocking** 아무런 효과가 없습니다;는 페치는 동기 및 차단 됩니다.  
  
> [!NOTE]
>  **ExecuteOpenEnum** 값 **adExecuteNoRecords** 또는 **adExecuteStream** 으로 쓰일 수 없습니다 **열려**합니다.  
  
## <a name="remarks"></a>주의  
 ADO에 대 한 기본 커서 **레코드 집합** 는 서버에 있는 읽기 전용, 정방향 전용 커서입니다.  
  
 사용 하 여는 **열려** 메서드를 한 **레코드 집합** 개체는 기본 테이블, 쿼리 또는 이전에 저장 된 결과에서 레코드를 나타내는 커서를 열고 **레코드 집합**합니다.  
  
 사용 하 여 선택적 *소스* 인수는 다음 중 하나를 사용 하 여 데이터 원본을 지정 하려면:는 **명령** 개체 변수, SQL 문, 저장된 프로시저, 테이블 이름, URL 또는 전체 파일 경로 이름입니다. 경우 *소스* 는 파일 경로 이름 전체 경로 ("c:\dir\file.rst"), 상대 경로 수 있습니다 ("… \file.rst"), 또는 URL ("http://files/file.rst").  
  
 사용 하는 것이 좋지 않습니다는 *소스* 의 인수는 **열려** 메서드를 쉽게 호출에 성공 했는지 여부를 결정할 수 있기 때문에 레코드를 반환 하지 않는 작업 쿼리를 수행 합니다. **레코드 집합** 등에서 반환 되는 쿼리 종료 됩니다. SQL INSERT 문과 같은 레코드를 반환 하지 않는 쿼리를 수행 하려면는 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 의 메서드는 **명령** 개체 또는 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 는 방식의[연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체를 대신 합니다.  
  
 *ActiveConnection* 인수에 해당는 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성 어떤 연결을 열에 지정 된 **레코드 집합** 개체입니다. 이 인수에 대 한 연결 정의 전달 하는 경우 ADO는 지정된 된 매개 변수를 사용 하 여 새 연결을 엽니다. 연 후는 **레코드 집합** 설정 하 여 클라이언트 쪽 커서는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**을 보내려고이 속성의 값을 변경할 수 있습니다 다른 공급자를 업데이트 합니다. 이 속성 설정할 수 있습니다 **아무** (Microsoft Visual Basic) 또는 연결을 끊을 NULL는 **레코드 집합** 공급자에서 합니다. 하지만 변경 *ActiveConnection* 서버 쪽 커서에서 오류를 생성 합니다.  
  
 속성에 해당 하는 다른 인수는 **레코드 집합** 개체 (*소스*, *모두*, 및 *LockType*), 속성에 대 한 인수의 관계는 다음과 같습니다.  
  
-   속성은 읽기/쓰기 하기 전에 **레코드 집합** 개체가 열릴 합니다.  
  
-   실행할 때 해당 하는 인수를 전달 하지 않으면 속성 설정이 사용 됩니다는 **열려** 메서드. 인수를 전달 하면 해당 하는 속성 설정을 재정의 하 고 속성 설정이 고 인수 값으로 업데이트 됩니다.  
  
-   연 후는 **레코드 집합** 개체를 이러한 속성은 읽기 전용이 됩니다.  
  
> [!NOTE]
>  **ActiveConnection** 에 대 한 읽기 전용 속성은 **레코드 집합** 개체 [소스](../../../ado/reference/ado-api/source-property-ado-recordset.md) 속성이 유효한 **명령** 개체 경우에는 **레코드 집합** 개체가 열려 있습니다.  
  
 전달 하는 경우는 **명령** 개체는 *소스* 인수 및 패스는 *ActiveConnection* 인수, 오류가 발생 합니다. **ActiveConnection** 의 속성은 **명령** 을 유효한 개체 설정 되어 있어야 **연결** 개체 또는 연결 문자열입니다.  
  
 요소를 이외의 전달 하는 경우는 **명령** 개체는 *소스* 인수, 있습니다 사용할 수 있습니다는 *옵션* 의 평가 최적화 하는 인수는 *소스*  인수입니다. 경우는 *옵션* 인수가 정의 되지 않은, ADO 인수 SQL 문, 저장된 프로시저, URL 또는 테이블 이름 인지 확인 하는 공급자에 대 한 호출을 확인 해야 하기 때문에 성능이 저하 될 수 있습니다. 무엇을 알고 있는 경우 *소스* 설정, 사용 중인 형식을 *옵션* 인수 관련 코드로 바로 이동할 수는 ADO에 지시 합니다. 경우는 *옵션* 인수가 일치 하지 않습니다는 *소스* 입력 오류가 발생 합니다.  
  
 전달 하는 경우는 **스트림** 개체는 *소스* 인수를 전달 해서는 안 정보를 다른 인수에 있습니다. 이렇게 하면 오류가 발생 합니다. **ActiveConnection** 정보를 유지 하는 경우는 **레코드 집합** 에서 열린는 **스트림**합니다.  
  
 에 대 한 기본값은 *옵션* 인수가 **adCmdFile** 연결이 연결 된 경우는 **레코드 집합**합니다. 이 일반적으로 사용 됩니다 영구적으로 저장에 대 한 **레코드 집합** 개체입니다.  
  
 공급자 둘 다 설정 하는 데이터 원본이 없는 레코드를 반환 하는 경우는 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 및 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성을 **True**, 고 현재 레코드 위치 정의 되지 않습니다. 이 비어 있는 것으로 새 데이터에 추가할 수 있습니다 **레코드 집합** 커서 유형을 허용 하는 경우 개체입니다.  
  
 열려 있는 작업을 완료 한 경우 **레코드 집합** 개체를 가져오려면는 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 관련 시스템 리소스를 해제 하는 메서드. 개체를 닫아도 제거 되지 않고 메모리;에서 으로 설정 하 고 사용 하 여는 **열고** 나중에 다시 열 수 있습니다. 메모리에서 개체를 완전히 제거 하려면 개체 변수를 설정 *Nothing*합니다.  
  
 전에 **ActiveConnection** 속성이 설정 되어 있으면 호출 **열려** 의 인스턴스를 만드는 없음 피연산자와 함께 **레코드 집합** 필드를 추가 하 여 만든는  **레코드 집합** [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션입니다.  
  
 설정한 경우는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**, 두 가지 방법 중 하나에 비동기적으로 행을 검색할 수 있습니다. 설정 하는 것이 좋습니다 *옵션* 를 **adAsyncFetch**합니다. 또는의 "비동기 행 집합 처리" 동적 속성을 사용할 수는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션 하지만 검색 된 관련된 이벤트가 손실 될 수 있습니다 설정 하지 않은 경우는 *옵션* 매개변수**adAsyncFetch**합니다.  
  
> [!NOTE]
>  통해서만 지원 되는 배경 MS 원격 공급자에서 페치는 **열려** 메서드의 *옵션* 매개 변수입니다.  
  
> [!NOTE]
>  Url은 http 체계를 사용 하 여 자동으로 호출 됩니다는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 참조 [절대 경로 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
 특정 조합은 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 및 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 값이 올바르지 않습니다. 에 대 한 옵션을 함께 수 없습니다 내용은 항목을 참조 하십시오.는 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md), 및 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Open 및 Close 메서드 예제 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 및 Close 메서드 (VBScript) 예제](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 및 Close 메서드 예제 (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [저장 하 고 (VB) 메서드 예제 열기](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Open 메서드 (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 메서드 (ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 메서드 (ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 메서드](../../../ado/reference/ado-api/openschema-method.md)   
 [Save 메서드](../../../ado/reference/ado-api/save-method.md)


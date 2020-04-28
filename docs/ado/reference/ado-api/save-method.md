---
title: Save 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Recordset::Save
- _Recordset::raw_Save
helpviewer_keywords:
- Save method [ADO]
ms.assetid: ed3d9678-5c28-4e61-8bb3-7dfb66d99cf5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ec1601749b6537484cead17c50492de131932ea
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931171"
---
# <a name="save-method"></a>Save 메서드
파일 또는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체에 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 을 저장 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>매개 변수  
 *대상*  
 선택 사항입니다. **레코드 집합** 을 저장할 파일의 전체 경로 이름을 나타내는 **Variant** 이거나 **스트림** 개체에 대 한 참조입니다.  
  
 *PersistFormat*  
 선택 사항입니다. **레코드 집합** 을 저장할 형식을 지정 하는 [persistformatenum](../../../ado/reference/ado-api/persistformatenum.md) 값 (XML 또는 ADTG)입니다. 기본값은 **adPersistADTG**입니다.  
  
## <a name="remarks"></a>설명  
 [Save Method](../../../ado/reference/ado-api/save-method.md) 메서드는 열린 **레코드 집합**에 대해서만 호출할 수 있습니다. [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드를 사용 하 여 나중에 *대상*에서 **레코드 집합** 을 복원할 수 있습니다.  
  
 [필터 속성](../../../ado/reference/ado-api/filter-property.md) 속성이 **레코드 집합**에 적용 되는 경우 필터에서 액세스할 수 있는 행만 저장 됩니다. **레코드 집합이** 계층적 이면 부모 **레코드**집합을 포함 하 여 현재 자식 **레코드 집합과** 해당 자식 항목이 저장 됩니다. 자식 **레코드 집합** 의 Save 메서드를 호출 하면 자식 및 모든 자식 항목이 저장 되지만 부모는 저장 되지 않습니다.  
  
 처음으로 **레코드 집합**을 저장할 때 *대상을*지정 하는 것이 선택 사항입니다. *Destination*을 생략 하면 **레코드 집합**의 Source 속성 값으로 설정 된 이름으로 새 파일이 생성 됩니다.  
  
 첫 번째 저장 후에 **save** 를 호출할 때 *Destination* 을 생략 하면이 고, 그렇지 않으면 런타임 오류가 발생 합니다. 이후에 새 *대상*으로 **Save** 를 호출 하면 해당 **레코드 집합이** 새 대상에 저장 됩니다. 그러나 새 대상과 원래 대상이 둘 다 열립니다.  
  
 **저장** **은 레코드 집합 또는** *대상을*닫지 않으므로 **레코드 집합** 을 사용 하 여 계속 작업 하 고 최근 변경 내용을 저장할 수 있습니다. *대상은* **레코드 집합** 을 닫을 때까지 열린 상태로 유지 됩니다.  
  
 보안을 위해 **Save** 메서드는 Microsoft Internet Explorer에서 실행 되는 스크립트에서 낮은 및 사용자 지정 보안 설정을 사용 하도록 허용 합니다.  
  
 비동기 **레코드 집합** 페치, 실행 또는 업데이트 작업이 진행 되는 동안 **save** 메서드가 호출 되 면 **저장** 은 비동기 작업이 완료 될 때까지 대기 합니다.  
  
 레코드는 레코드 **집합**의 첫 번째 행부터 저장 됩니다. **Save** 메서드가 완료 되 면 현재 행 위치가 **레코드 집합**의 첫 번째 행으로 이동 합니다.  
  
 최상의 결과를 위해 [CursorLocation 속성 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient** 로 설정 하 고 **저장**을 사용 하 여 설정 합니다. 공급자가 **레코드 집합** 개체를 저장 하는 데 필요한 일부 기능을 지원 하지 않는 경우 Cursor Service가 해당 기능을 제공 합니다.  
  
 **CursorLocation** 속성이 **aduseserver**로 설정 된 상태에서 **레코드 집합** 을 유지 하면 **레코드 집합** 에 대 한 업데이트 기능이 제한 됩니다. 일반적으로는 단일 테이블 업데이트, 삽입 및 삭제만 허용 됩니다 (공급자 기능에 따라 달라 집니다). [Resync 메서드](../../../ado/reference/ado-api/resync-method.md) 메서드는이 구성 에서도 사용할 수 없습니다.  
  
> [!NOTE]
>  **Advariant**, **adIDispatch**또는 **AdIUnknown** 형식의 **필드가** 포함 된 **레코드 집합** 을 ADO에서 지원 하지 않으므로 예기치 않은 결과가 발생할 수 있습니다.  
  
 조건 문자열 (예: OrderDate > ' 12/31/1999 ') 형식의 필터만 지속형 **레코드 집합**의 내용에 영향을 줍니다. **책갈피** 배열을 사용 하거나 [filtergroupenum](../../../ado/reference/ado-api/filtergroupenum.md) 의 값을 사용 하 여 만든 필터는 지속형 **레코드 집합**의 내용에 영향을 주지 않습니다. 이러한 규칙은 클라이언트 쪽 또는 서버 쪽 커서를 사용 하 여 만든 **레코드 집합**에 적용 됩니다.  
  
 *Destination* 매개 변수는 OLE DB IStream 인터페이스를 지 원하는 개체를 받아들일 수 있으므로 **레코드 집합** 을 ASP Response 개체에 직접 저장할 수 있습니다. 자세한 내용은 **XML 레코드 집합 지 속성 시나리오**를 참조 하세요.  
  
 다음 Visual Basic 코드와 같이 XML 형식의 **레코드 집합** 을 MSXML DOM 개체의 인스턴스에 저장할 수도 있습니다.  
  
```  
Dim xDOM As New MSXML.DOMDocument  
Dim rsXML As New ADODB.Recordset  
Dim sSQL As String, sConn As String  
  
sSQL = "SELECT customerid, companyname, contactname FROM customers"  
sConn="Provider=Microsoft.Jet.OLEDB.4.0;Data Source=Northwind.mdb"  
rsXML.Open sSQL, sConn  
rsXML.Save xDOM, adPersistXML   'Save Recordset directly into a DOM tree.  
...  
```  
  
> [!NOTE]
>  계층적 레코드 집합 (데이터 셰이프)을 XML 형식으로 저장할 때 두 가지 제한 사항이 적용 됩니다. 계층 구조 **레코드 집합** 에 보류 중인 업데이트가 포함 되어 있고 매개 변수가 있는 계층적 **레코드 집합**을 저장할 수 없는 경우 XML로 저장할 수 없습니다.  
  
 XML 형식으로 저장 된 **레코드 집합** 은 utf-8 형식을 사용 하 여 저장 됩니다. 이러한 파일이 ADO 스트림에 로드 될 때 스트림의 Charset 속성이 UTF-8 형식에 적절 한 값으로 설정 되지 않은 경우 stream 개체는 스트림에서 **레코드 집합** 을 열려고 시도 하지 않습니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>참고 항목  
 [Save 및 Open 메서드 예제 (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Save 및 Open 메서드 예제 (VC + +)](../../../ado/reference/ado-api/save-and-open-methods-example-vc.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 메서드 (ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [SaveToFile 메서드](../../../ado/reference/ado-api/savetofile-method.md)

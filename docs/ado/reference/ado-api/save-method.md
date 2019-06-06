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
manager: jroth
ms.openlocfilehash: 0953b76ff642387679c907e6f0b3364cbac898df
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711389"
---
# <a name="save-method"></a>Save 메서드
저장 합니다 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) 파일에서 또는 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>매개 변수  
 *대상*  
 (선택 사항) A **Variant** 파일의 전체 경로 이름을 나타내는 위치를 **레코드 집합** 저장 하는 것에 대 한 참조 또는 **Stream** 개체.  
  
 *PersistFormat*  
 (선택 사항) [PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md) 되는 형식을 지정 하는 값을 **레코드 집합** (XML 또는 ADTG) 저장 하는 것입니다. 기본값은 **adPersistADTG**합니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 [Save 메서드](../../../ado/reference/ado-api/save-method.md) 메서드를 열 때만 호출할 수 있습니다 **레코드 집합**합니다. 사용 합니다 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md) 이상 복원 방법 합니다 **레코드 집합** 에서 *대상*합니다.  
  
 경우는 [필터 속성](../../../ado/reference/ado-api/filter-property.md) 속성에 적용 되는 **레코드 집합**, 다음 필터에서 액세스할 수 있는 행만 저장 됩니다. 경우는 **Recordset** 계층형 현재 자식 **레코드 집합** 및 자식의 부모를 포함 하 여 저장 됩니다 **레코드 집합**. 경우 자식의 Save 메서드 **레코드 집합** 는 자식 노드와 모든 자식이 저장 되지만 호출 됩니다.  
  
 처음 저장할 때 합니다 **레코드 집합**를 지정 하는 선택 사항이 *대상*합니다. 생략 하면 *대상*의 소스 속성의 값으로 설정 하는 이름의 새 파일이 만들어집니다 합니다 **레코드 집합**합니다.  
  
 생략 *대상* 이후에 호출 하는 경우 **저장** 후 첫 번째 저장 또는 런타임 오류가 발생 합니다. 이후에 호출 하는 경우 **저장할** 새 *대상*의 **레코드 집합** 새 대상에 저장 됩니다. 그러나 새로운 대상 이자 원래 대상은 둘 다 열어야 합니다.  
  
 **저장** 닫지 않습니다를 **레코드 집합** 또는 *대상*이므로 사용 하 여 작업을 계속할 수는 **레코드 집합** 가장 최근의 변경 내용을 저장 합니다. *대상* 될 때까지 열린 상태로 유지 됩니다 합니다 **레코드 집합** 닫혀 있습니다.  
  
 보안을 위해 합니다 **저장할** 메서드는 Microsoft Internet Explorer에서 실행 하는 스크립트에서 낮은 및 사용자 지정 보안 설정의 사용만을 허용 합니다.  
  
 경우는 **저장** 메서드는 비동기 하는 동안 **레코드 집합** 인출, 실행 또는 업데이트 작업이 진행에서 한 다음 **저장** 비동기 작업이 될 때까지 대기 완료 되었습니다.  
  
 첫 번째 행부터 레코드가 저장 되는 **레코드 집합**합니다. 경우는 **저장** 메서드가 완료 되 면 현재 행 위치가 첫 번째 행으로 이동 합니다 **레코드 집합**합니다.  
  
 최상의 결과 설정 합니다 [CursorLocation 속성 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient** 사용 하 여 **저장**합니다. 경우 공급자에 게 지원 하지 않습니다 모든 기능을 저장 하는 데 필요한 **레코드 집합** 개체 커서 서비스에서 해당 기능을 제공 합니다.  
  
 경우는 **레코드 집합** 함께 유지 되는 **CursorLocation** 속성이로 설정 **가 adUseServer**, 업데이트 기능을 **레코드집합**제한 됩니다. 일반적으로 단일 테이블 업데이트, 삽입 및 삭제 (공급자 기능에 따라)를 기준으로 수만 있습니다. 합니다 [Resync 메서드](../../../ado/reference/ado-api/resync-method.md) 메서드는 또한이 구성에서 사용할 수 있습니다.  
  
> [!NOTE]
>  저장 된 **레코드 집합** 사용 하 여 **필드** 형식의 **adVariant**, **adIDispatch**, 또는 **adIUnknown** 는 ADO에서 지원 되는 없고 예기치 않은 결과가 발생할 수 있습니다.  
  
 조건 문자열의 형태로 필터링 (예: OrderDate > ' 12/31/1999 ') 지속형된 내용의 영향을 줄 **레코드 집합**합니다. 배열을 사용 하 여 작성 된 필터 **책갈피** 의 값을 사용 하 여 또는 합니다 [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) 지속형된는 내용의 영향을 주지 것입니다 **레코드 집합**합니다. 이러한 규칙에 적용할 **레코드 집합**클라이언트 쪽 이나 서버 쪽 커서를 사용 하 여 만든 s입니다.  
  
 때문에 *대상* OLE DB IStream 인터페이스를 지 원하는 모든 개체를 허용할 수 있는, 저장할 수는 **레코드 집합** ASP 응답 개체에 직접. 자세한 내용은 참조 하십시오 합니다 **XML 레코드 집합 지 속성 시나리오**합니다.  
  
 저장할 수도 있습니다는 **레코드 집합** MSXML DOM 개체의 인스턴스를 XML 형식으로 다음 Visual Basic 코드에 표시 됩니다으로:  
  
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
>  두 개의 제한에는 XML 형식의 계층적 레코드 집합 (데이터 셰이프)를 저장할 때 적용 됩니다. 경우 XML로 저장할 수 없습니다는 계층적 **Recordset** 보류 중인 업데이트가 포함 매개 변수가 있는 저장할 수 없습니다 계층적 **레코드 집합**.  
  
 A **레코드 집합** 저장 된 xml에서 형식으로 u t F-8 형식을 사용 하 여 저장 됩니다. 이러한 파일을 ADO Stream에 로드 되 면 Stream 개체는 하려고 하지 않습니다 엽니다는 **레코드 집합** 스트림에서 스트림의 문자 집합 속성 utf-8 형식에 대 한 적절 한 값으로 설정 되어 있지 않으면입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목  
 [Save 및 Open 메서드 예제 (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Save 및 Open 메서드 예제 (VC + +)](../../../ado/reference/ado-api/save-and-open-methods-example-vc.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 메서드 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [SaveToFile 메서드](../../../ado/reference/ado-api/savetofile-method.md)

---
title: Save 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Recordset::Save
- _Recordset::raw_Save
helpviewer_keywords:
- Save method [ADO]
ms.assetid: ed3d9678-5c28-4e61-8bb3-7dfb66d99cf5
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a92e053443dbb32aae83756a98facdc53fa74725
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35281442"
---
# <a name="save-method"></a>Save 메서드
저장 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 파일에 또는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>매개 변수  
 *대상*  
 (선택 사항) A **Variant** 파일의 전체 경로 이름을 나타내는 위치는 **레코드 집합** , 저장 하는 것에 대 한 참조는 **스트림** 개체입니다.  
  
 *PersistFormat*  
 (선택 사항) A [PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md) 되는 형식을 지정 하는 값은 **레코드 집합** (XML 또는 ADTG) 저장 하는 것입니다. 기본값은 **adPersistADTG**합니다.  
  
## <a name="remarks"></a>Remarks  
 [Save 메서드](../../../ado/reference/ado-api/save-method.md) 열린에 에서만 메서드를 호출할 수 **레코드 집합**합니다. 사용 하 여는 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md) 이후 복원 하는 메서드는 **레코드 집합** 에서 *대상*합니다.  
  
 경우는 [Filter 속성](../../../ado/reference/ado-api/filter-property.md) 속성에 적용 되는 **레코드 집합**, 필터 액세스할 수 있는 행만 저장 됩니다. 경우는 **레코드 집합** 계층형 현재 자식 다음 **레코드 집합** 및 자식의 부모를 포함 하 여 저장 됩니다 **레코드 집합**합니다. 경우 자식의 Save 메서드 **레코드 집합** 가 자식 및 모든 자식 저장 되지만 부모를 호출 합니다.  
  
 처음으로 저장 하면는 **레코드 집합**를 지정 하는 선택 사항이 *대상*합니다. 생략 하면 *대상*의 Source 속성의 값으로 설정 하는 이름의 새 파일이 생성 됩니다는 **레코드 집합**합니다.  
  
 생략 *대상* 이후에 호출 **저장** 후 첫 번째 저장 또는 런타임 오류가 발생 합니다. 않으면 런타임 **저장** 를 새 *대상*, **레코드 집합** 새 대상에 저장 됩니다. 그러나 새 대상 및 원본 대상 둘 다 열려 있을 합니다.  
  
 **저장** 닫지 않습니다는 **레코드 집합** 또는 *대상*계속 작업할 수 있으므로 **레코드 집합** 가장 최근의 변경 내용을 저장 합니다. *대상* 될 때까지 열린 상태로 유지 됩니다는 **레코드 집합** 닫혀 있습니다.  
  
 보안상의 이유로 **저장** 메서드는 Microsoft Internet Explorer에서 실행 되는 스크립트에서 낮은 및 사용자 지정 보안 설정의 사용만을 허용 합니다.  
  
 경우는 **저장** 동안 비동기 메서드는 **레코드 집합** 인출, 실행 또는 업데이트 작업이 진행 중에 다음 중인 **저장** 비동기 작업이 될 때까지 대기 완료 되었습니다.  
  
 레코드의 첫 번째 행부터 저장 되는 **레코드 집합**합니다. 경우는 **저장** 메서드가 완료 되 면 현재 행의 위치가의 첫 번째 행으로 이동 되는 **레코드 집합**합니다.  
  
 최상의 결과 위해 설정 된 [앞 속성 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient** 와 **저장**합니다. 경우에 공급자가 지원 하지 저장 하는 데 필요한 기능을 모두 **레코드 집합** 개체 커서 서비스에서 해당 기능을 제공 합니다.  
  
 경우는 **레코드 집합** 함께 유지는 **앞** 속성이로 설정 **가 adUseServer**, 업데이트 기능에 대 한는 **레코드 집합**제한 됩니다. 일반적으로 단일 테이블 업데이트, 삽입 및 삭제 (공급자 기능에 따라)를 허용 됩니다. [메서드 Resync](../../../ado/reference/ado-api/resync-method.md) 메서드는 또한이 구성에서 사용할 수 없습니다.  
  
> [!NOTE]
>  저장 한 **레코드 집합** 와 **필드** 형식의 **adVariant**, **adIDispatch**, 또는 **adIUnknown** 은 ADO에서 지원 없고 예기치 않은 결과가 발생할 수 있습니다.  
  
 조건 문자열의 형태로 필터링 (예: OrderDate > ' 12/31/1999 ')의 지속형 내용이 영향을 **레코드 집합**합니다. 필터의 배열을 사용 하 여 만든 **책갈피** 의 값을 사용 하 여 또는 [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) 지속형된는 내용의 영향을 주지 것입니다 **레코드 집합**합니다. 이러한 규칙에 적용 **레코드 집합**클라이언트 쪽 이나 서버 쪽 커서를 사용 하 여 만든 s입니다.  
  
 때문에 *대상* OLE DB IStream 인터페이스를 지 원하는 모든 개체를 허용할 수 있는, 저장할 수는 **레코드 집합** ASP 응답 개체에 직접 합니다. 자세한 정보를 참조 하십시오는 **XML 레코드 집합 지 속성 시나리오**합니다.  
  
 저장할 수도 있습니다는 **레코드 집합** MSXML DOM 개체의 인스턴스를 XML 형식으로로 표시 되며 다음 Visual Basic 코드:  
  
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
>  XML 형식의 계층적 레코드 집합 (데이터 셰이프)를 저장할 때는 두 가지 제한 사항이 적용 합니다. 경우에 XML로 저장할 수 없습니다 계층적 **레코드 집합** 보류 중인 업데이트가 포함 되어 매개 변수가 있는 저장할 수 없습니다 계층적 **레코드 집합**합니다.  
  
 A **레코드 집합** 저장 된 XML의 형식이 u t F-8 형식을 사용 하 여 저장 됩니다. 이러한 파일이 ADO 스트림으로 로드 되 면 스트림 개체를 열려고 시도 하지 것입니다는 **레코드 집합** 스트림에서 스트림의 문자 집합 속성은 u t F-8 형식에 대 한 적절 한 값으로 설정 되어 있지 않으면입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목  
 [저장 하 고 (VB) 메서드 예제 열기](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [저장 및 열기 메서드 예제 (VC + +)](../../../ado/reference/ado-api/save-and-open-methods-example-vc.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 메서드 (ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [SaveToFile 메서드](../../../ado/reference/ado-api/savetofile-method.md)

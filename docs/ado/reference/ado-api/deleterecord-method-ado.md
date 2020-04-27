---
title: DeleteRecord 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_DeleteRecord
- _Record::DeleteRecord
helpviewer_keywords:
- DeleteRecord method [ADO]
ms.assetid: 2726498c-dbd8-4266-983b-ae7d62c39142
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 409c4e21395b7b903cf4ff03726fbd37a2a218d1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67919078"
---
# <a name="deleterecord-method-ado"></a>DeleteRecord 메서드(ADO)
[레코드로](../../../ado/reference/ado-api/record-object-ado.md)표시 되는 엔터티를 삭제 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 선택 사항입니다. 삭제할 엔터티 (예: 파일 또는 디렉터리)를 식별 하는 URL을 포함 하는 **문자열** 값입니다. *Source* 를 생략 하거나 빈 문자열을 지정 하면 현재 [레코드가](../../../ado/reference/ado-api/record-object-ado.md) 나타내는 엔터티가 삭제 됩니다. 레코드가 컬렉션 레코드 (디렉터리와 같은 **Adcollectionrecord**의[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md) ) 이면 모든 자식 (예: 하위 디렉터리)도 삭제 됩니다.  
  
 *Async*  
 선택 사항입니다. **True**인 경우 삭제 작업을 보조적 지정 하는 **부울** 값입니다.  
  
## <a name="remarks"></a>설명  
 이 메서드가 완료 되 면이 **레코드가** 나타내는 개체에 대 한 작업이 실패할 수 있습니다. **DeleteRecord**를 호출한 후에는 공급자가 데이터 원본을 사용 하 여 **레코드** 를 업데이트 하는 시기에 따라 레코드의 동작을 **예측할 수 없게** 되므로 **레코드** 를 닫아야 합니다.  
  
 레코드 [집합](../../../ado/reference/ado-api/recordset-object-ado.md)에서이 **레코드** 를 가져온 경우이 작업의 결과는 **레코드 집합**에 즉시 반영 되지 않습니다. 레코드 집합을 닫았다가 다시 열거나, **레코드 집합** [Requery](../../../ado/reference/ado-api/requery-method.md) 메서드, [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드 또는 다시 [동기화](../../../ado/reference/ado-api/resync-method.md) 메서드를 실행 하 여 **레코드 집합** 을 새로 고칩니다.  
  
> [!NOTE]
>  Http 체계를 사용 하는 Url은 자동으로 [Microsoft OLE DB 공급자에 게 Internet 게시용](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)으로 호출 됩니다. 자세한 내용은 [절대 및 상대 url](../../../ado/guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Delete 메서드 (ADO Fields Collection)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO Parameters Collection)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 메서드(ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)

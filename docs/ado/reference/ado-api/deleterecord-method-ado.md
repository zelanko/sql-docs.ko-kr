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
manager: craigg
ms.openlocfilehash: 23c66eb3ca786df27f856539e8bba026d2b1ea71
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140197"
---
# <a name="deleterecord-method-ado"></a>DeleteRecord 메서드(ADO)
가 나타내는 엔터티를 삭제 한 [레코드](../../../ado/reference/ado-api/record-object-ado.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 (선택 사항) A **문자열** 삭제할 엔터티 (예: 파일 또는 디렉터리)를 식별 하는 URL을 포함 하는 값입니다. 하는 경우 *소스* 생략 되거나 빈 문자열인 경우 현재 표시 된 엔터티를 지정 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 삭제 됩니다. 레코드 컬렉션 레코드인 경우 ([RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md) 의 **adCollectionRecord**, 디렉터리와 같은) 모든 자식 (예를 들어, 하위 디렉터리)도 삭제 됩니다.  
  
 *Async*  
 (선택 사항) A **부울** 값을 때 **True**, 비동기 삭제 작업 임을 지정 합니다.  
  
## <a name="remarks"></a>Remarks  
 이 나타내는 개체에 대 한 작업 **레코드** 이 메서드가 완료 된 후 실패할 수 있습니다. 호출한 후 **DeleteRecord**, **레코드** 때문에 닫아야의 동작을 **레코드** 공급자를 업데이트 하는 시점에 예기치 않은 따라 될 수 있습니다는 **레코드** 데이터 소스를 사용 하 여 합니다.  
  
 이 경우 **레코드** 에서 가져온를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 다음이 작업의 결과 즉시 반영 되지 것입니다는 **레코드 집합**합니다. 새로 고침 합니다 **레코드 집합** 를 닫았다가 다시 열어서, 또는 실행 하 여는 **레코드 집합** [Requery](../../../ado/reference/ado-api/requery-method.md) 메서드를 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드를 또는 [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드.  
  
> [!NOTE]
>  Http 체계를 사용 하 여 Url은 자동으로 호출 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 [절대 및 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Delete 메서드 (ADO 필드 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO 매개 변수 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 메서드(ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)

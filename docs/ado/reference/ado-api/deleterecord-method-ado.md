---
title: 참여할 수 있는 메서드 (ADO) | Microsoft Docs
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
- _Record::raw_DeleteRecord
- _Record::DeleteRecord
helpviewer_keywords:
- DeleteRecord method [ADO]
ms.assetid: 2726498c-dbd8-4266-983b-ae7d62c39142
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 168b53d0ad68f55656e005f7523a0c09ba599004
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277642"
---
# <a name="deleterecord-method-ado"></a>참여할 수 있는 메서드 (ADO)
가 나타내는 엔터티를 삭제 한 [레코드](../../../ado/reference/ado-api/record-object-ado.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 (선택 사항) A **문자열** 삭제할 엔터티 (예: 파일 또는 디렉터리)를 식별 하는 URL을 포함 하는 값입니다. 경우 *소스* 를 생략 하거나 빈 문자열인 경우 현재 표시 되는 엔터티에 지정 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 삭제 됩니다. 레코드 컬렉션 레코드인 경우 ([RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md) 의 **adCollectionRecord**, 디렉터리와 같은) 모든 자식 항목 (예를 들어 하위 디렉터리)도 삭제 됩니다.  
  
 *비동기*  
 (선택 사항) A **부울** 값 때 **True**, 삭제 작업이 비동기 임을 지정 합니다.  
  
## <a name="remarks"></a>Remarks  
 이 표시 되는 개체에 대 한 작업 **레코드** 이 메서드가 완료 된 후 실패할 수 있습니다. 호출한 후 **참여할 수 있는**, **레코드** 때문에 닫아야의 동작은 **레코드** 공급자 업데이트 한 경우에 예측할 수 없는 따라 될 수 있습니다는 **레코드** 데이터 원본과 합니다.  
  
 이 경우 **레코드** 에서 가져온는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 다음이 작업의 결과 즉시 반영 되지 것입니다는 **레코드 집합**합니다. 새로 고침는 **레코드 집합** 으로 닫고 다시 열면 또는 실행 하 여는 **레코드 집합** [Requery](../../../ado/reference/ado-api/requery-method.md) 메서드는 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드, 또는 [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드.  
  
> [!NOTE]
>  Url은 http 체계를 사용 하 여 자동으로 호출 됩니다는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 참조 [절대 경로 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Delete 메서드 (ADO 필드 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO Parameters 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 메서드(ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)

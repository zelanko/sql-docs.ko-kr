---
title: 범위란 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::MoveRecord
- _Record::raw_MoveRecord
helpviewer_keywords:
- MoveRecord method [ADO]
ms.assetid: 6d2807b0-b861-4583-bcaf-fb0b82e0f2d0
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: efd293a02bb3611a0f49a3234f081defb0aa8e8f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="moverecord-method-ado"></a>범위란 메서드 (ADO)
이동 하 여 표시 되는 엔터티에 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 다른 위치에 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 (선택 사항) A **문자열** 식별 하는 URL을 포함 하는 값은 **레코드** 를 이동 해야 합니다. 경우 *소스* 를 생략 하거나 빈 문자열이 면이 나타내는 개체를 지정 **레코드** 이동 됩니다. 예를 들어 경우는 **레코드** 파일을 파일의 내용 나타내는로 지정 된 위치로 이동 *대상*합니다.  
  
 *대상*  
 (선택 사항) A **문자열** 값 위치를 지정 하는 URL이 포함 된 여기서 *소스* 이동 됩니다.  
  
 *UserName*  
 (선택 사항) A **문자열** 필요한 경우에 대 한 액세스 권한을 부여 하는 사용자 ID를 포함 하는 값 *대상*합니다.  
  
 *암호*  
 (선택 사항) A **문자열** 필요한 경우 확인 하는 암호가 포함 된 *UserName*합니다.  
  
 *옵션*  
 (선택 사항) A [MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md) 해당 기본값은 값 **메서드의 동작**합니다. 이 메서드의 동작을 지정합니다.  
  
 *비동기*  
 (선택 사항) A **부울** 값 때 **True**,이 작업은 비동기 되지 않아야 합니다.  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 값입니다. 일반적으로 값 *대상* 반환 됩니다. 그러나 반환 된 정확한 값은 공급자에 따라 다릅니다.  
  
## <a name="remarks"></a>주의  
 값 *소스* 및 *대상* 않아야 고, 그렇지 않으면 동일 하면 런타임 오류가 발생 합니다. 최소한 서버, 경로 및 리소스 이름은 달라 야 합니다.  
  
 이 메서드를 인터넷 게시 공급자를 사용 하 여 파일에 대 한 모든 하이퍼텍스트 링크를 이동 하 여 다르게 지정 되지 않는 파일을 업데이트 *옵션*합니다. 이 메서드는 실패 하는 경우 *대상* 하지 않으면 (예를 들어 파일 또는 디렉터리), 기존 개체를 식별 **adMoveOverWrite** 지정 됩니다.  
  
> [!NOTE]
>  사용 하 여는 **adMoveOverWrite** 주의 해 서 옵션입니다. 예를 들어 디렉터리에 파일을 이동할 때이 옵션을 지정 하는 삭제 디렉터리 하 고 파일로 바꿉니다.  
  
 특정 한 특성은 **레코드** 와 같은 개체는 [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) 속성을이 작업이 완료 된 후 업데이트 되지 것입니다. 새로 고침는 **레코드** 닫아 개체의 속성은 **레코드**, 파일 또는 디렉터리 옮겨졌습니다 위치의 URL로 다시 열어 다음 합니다.  
  
 이 경우 **레코드** 에서 가져온는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 이동한 파일 또는 디렉터리의 새 위치에 즉시 반영 되지 것입니다는 **레코드 집합**합니다. 새로 고침의 **레코드 집합** 으로 닫고 다시 열면 됩니다.  
  
> [!NOTE]
>  Url은 http 체계를 사용 하 여 자동으로 호출 됩니다는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 참조 [절대 경로 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Move 메서드 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드(RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)

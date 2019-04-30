---
title: MoveRecord 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::MoveRecord
- _Record::raw_MoveRecord
helpviewer_keywords:
- MoveRecord method [ADO]
ms.assetid: 6d2807b0-b861-4583-bcaf-fb0b82e0f2d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2deba8c745b29b5bd69432060debad2c585e31b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242747"
---
# <a name="moverecord-method-ado"></a>MoveRecord 메서드(ADO)
이동 하 여 표시 되는 엔터티에 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 다른 위치에 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 (선택 사항) A **문자열** 식별 하는 URL을 포함 하는 값을 **레코드** 이동 해야 합니다. 하는 경우 *소스* 생략 되거나 빈 문자열인 경우이 나타내는 개체를 지정 **레코드** 이동 됩니다. 예를 들어 경우는 **레코드** 파일을 파일의 내용 나타내는 지정 된 위치로 이동 *대상*합니다.  
  
 *대상*  
 (선택 사항) A **문자열** 위치를 지정 하는 URL이 포함 된 값 위치 *원본* 이동 됩니다.  
  
 *UserName*  
 (선택 사항) A **문자열** 필요한 경우에 대 한 액세스 권한을 부여 하는 사용자 ID를 포함 하는 값 *대상*합니다.  
  
 *암호*  
 (선택 사항) A **문자열** 필요한 경우를 확인 하는 암호가 포함 된 *UserName*합니다.  
  
 *Options*  
 (선택 사항) A [MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md) 값을 지정 합니다 **메서드의 동작**합니다. 이 메서드의 동작을 지정 합니다.  
  
 *Async*  
 (선택 사항) A **부울** 값을 때 **True**, 지정이 작업은 비동기 여야 합니다.  
  
## <a name="return-value"></a>반환 값  
 **문자열** 값입니다. 일반적으로 값 *대상* 반환 됩니다. 그러나 공급자에 따라 다릅니다는 정확한 값을 반환 합니다.  
  
## <a name="remarks"></a>Remarks  
 값 *원본* 하 고 *대상* 아니어야 고, 그렇지 않으면 동일 하면 런타임 오류가 발생 합니다. 최소한 서버, 경로 및 리소스 이름이 달라 야 합니다.  
  
 이 메서드를 인터넷 게시 공급자를 사용 하 여 파일에 대 한 모든 하이퍼텍스트 링크를 여 달리 지정 하지 않으면 이동 되는 파일을 업데이트 *옵션*합니다. 이 메서드가 실패 하는 경우 *대상* 하지 않으면 (예를 들어, 파일 또는 디렉터리), 기존 개체를 식별 **adMoveOverWrite** 지정 됩니다.  
  
> [!NOTE]
>  사용 된 **adMoveOverWrite** 옵션을 신중 하 게 합니다. 예를 들어, 디렉터리에 파일을 이동 하는 경우이 옵션을 지정 디렉터리를 삭제 되며 파일을 바꿉니다.  
  
 특정 한 특성을 **레코드** 개체를 [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) 속성을이 작업이 완료 된 후 업데이트 되지 것입니다. 새로 고침 합니다 **레코드** 닫아 개체의 속성을 **레코드**, 파일 또는 디렉터리가 이동 된 위치의 URL을 사용 하 여 닫았다가 다시 열면 다음.  
  
 이 경우 **레코드** 에서 가져온를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 이동할된 파일 또는 디렉터리의 새 위치에 즉시 반영 되지 것입니다는 **레코드 집합**합니다. 새로 고침 합니다 **레코드 집합** 를 닫았다가 다시 열면 됩니다.  
  
> [!NOTE]
>  Http 체계를 사용 하 여 Url은 자동으로 호출 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 [절대 및 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Move 메서드 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드(RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)

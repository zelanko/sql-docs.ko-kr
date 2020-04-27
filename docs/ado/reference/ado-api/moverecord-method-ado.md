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
ms.openlocfilehash: 157e38c2c9c23ff8f7e92af40385b0962c6dcb70
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918070"
---
# <a name="moverecord-method-ado"></a>MoveRecord 메서드(ADO)
[레코드로](../../../ado/reference/ado-api/record-object-ado.md) 표시 되는 엔터티를 다른 위치로 이동 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 선택 사항입니다. 이동할 **레코드** 를 식별 하는 URL을 포함 하는 **문자열** 값입니다. *Source* 를 생략 하거나 빈 문자열을 지정 하면이 **레코드가** 나타내는 개체가 이동 합니다. 예를 들어 **레코드가** 파일을 나타내는 경우 파일의 내용이 *Destination*에서 지정한 위치로 이동 합니다.  
  
 *대상*  
 선택 사항입니다. *소스* 를 이동할 위치를 지정 하는 URL을 포함 하는 **문자열** 값입니다.  
  
 *이름*  
 선택 사항입니다. 필요한 경우 *대상*에 대 한 액세스 권한을 부여 하는 사용자 ID를 포함 하는 **문자열** 값입니다.  
  
 *암호*  
 선택 사항입니다. 필요한 경우 *사용자 이름을*확인 하는 암호를 포함 하는 **문자열** 입니다.  
  
 *옵션*  
 선택 사항입니다. 기본값이 **Admoveunspecified 되지 않은** [MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md) 값입니다. 이 메서드의 동작을 지정 합니다.  
  
 *Async*  
 선택 사항입니다. **True**인 경우이 작업이 비동기가 되도록 지정 하는 **부울** 값입니다.  
  
## <a name="return-value"></a>Return Value  
 **문자열** 값입니다. 일반적으로 *Destination* 값이 반환 됩니다. 그러나 반환 되는 정확한 값은 공급자에 따라 다릅니다.  
  
## <a name="remarks"></a>설명  
 *원본* 및 *대상* 의 값은 달라 야 합니다. 그렇지 않으면 런타임 오류가 발생 합니다. 적어도 서버, 경로 및 리소스 이름은 서로 달라 야 합니다.  
  
 인터넷 게시 공급자를 사용 하 여 이동한 파일의 경우이 메서드는 *옵션*으로 지정 하지 않는 한 이동 중인 파일의 모든 하이퍼텍스트 링크를 업데이트 합니다. **Admoveoverwrite** 가 지정 되지 않은 경우 *대상* 에서 기존 개체 (예: 파일 또는 디렉터리)를 식별 하는 경우이 메서드는 실패 합니다.  
  
> [!NOTE]
>  **Admoveoverwrite** 옵션을 신중 하 게 사용 합니다. 예를 들어 파일을 디렉터리로 이동할 때이 옵션을 지정 하면 디렉터리가 삭제 되 고 파일로 바뀝니다.  
  
 [Parenturl](../../../ado/reference/ado-api/parenturl-property-ado.md) 속성과 같은 **Record** 개체의 특정 특성은이 작업이 완료 된 후 업데이트 되지 않습니다. **레코드**를 닫은 다음 파일 또는 디렉터리가 이동 된 위치의 URL을 사용 하 여 **레코드** 개체의 속성을 다시 엽니다.  
  
 레코드 [집합](../../../ado/reference/ado-api/recordset-object-ado.md)에서이 **레코드** 를 가져온 경우 이동한 파일이 나 디렉터리의 새 위치가 **레코드 집합**에 즉시 반영 되지 않습니다. 레코드 집합을 닫았다가 다시 열어 **레코드 집합** 을 새로 고칩니다.  
  
> [!NOTE]
>  Http 체계를 사용 하는 Url은 자동으로 [Microsoft OLE DB 공급자에 게 Internet 게시용](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)으로 호출 됩니다. 자세한 내용은 [절대 및 상대 url](../../../ado/guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Move 메서드 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드(RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)

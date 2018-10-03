---
title: ConnectModeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectModeEnum
helpviewer_keywords:
- ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2a5ab00cc6e01b97639ae3f7d353fa2462ef3fd0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47637861"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
데이터 수정에 사용할 수 있는 권한을 지정는 [연결](../../../ado/reference/ado-api/connection-object-ado.md)연를 [레코드](../../../ado/reference/ado-api/record-object-ado.md)에 대 한 값을 지정 하거나를 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 의 속성을  **레코드** 하 고 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|읽기 전용 권한을 나타냅니다.|  
|**adModeReadWrite**|3|읽기/쓰기 권한을 나타냅니다.|  
|**adModeRecursive**|0x400000|다른와 함께 사용할 *\*ShareDeny\** 값 (**adModeShareDenyNone**하십시오 **adModeShareDenyWrite**, 또는 **adModeShareDenyRead**) 현재 모든 하위 레코드에 공유 제한이 전파 **레코드**합니다. 이 영향을 주지 않습니다 경우는 **레코드** 자식이 없습니다. 에 사용 되는 경우 런타임 오류가 생성 됩니다 **adModeShareDenyNone** 만 합니다. 그러나 사용 하 여 사용할 수 있습니다 **adModeShareDenyNone** 다른 값과 결합 하는 경우. 예를 들어 사용할 수 있습니다 "**adModeRead** 하거나 **adModeShareDenyNone** 하거나 **adModeRecursive**"입니다.|  
|**adModeShareDenyNone**|16|다른 모든 권한으로 연결을 열 수 있습니다. 다른 사용자의 읽기 또는 쓰기 액세스가 거부될 수 있습니다.|  
|**adModeShareDenyRead**|4|읽기 권한으로 연결을 열에서 다른 사용자를 방지 합니다.|  
|**adModeShareDenyWrite**|8|쓰기 권한으로 연결을 열에서 다른 사용자를 방지 합니다.|  
|**adModeShareExclusive**|12|연결을 열어 다른 사용자를 방지 합니다.|  
|**adModeUnknown**|0|기본. 사용 권한을 아직 설정 되지 않은 또는 확인할 수 없습니다 나타냅니다.|  
|**adModeWrite**|2|쓰기 전용 권한을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.ConnectMode.READ|  
|AdoEnums.ConnectMode.READWRITE|  
|(동일한 기능이 없습니다 AdoEnums.ConnectMode.RECURSIVE의)|  
|AdoEnums.ConnectMode.SHAREDENYNONE|  
|AdoEnums.ConnectMode.SHAREDENYREAD|  
|AdoEnums.ConnectMode.SHAREDENYWRITE|  
|AdoEnums.ConnectMode.SHAREEXCLUSIVE|  
|AdoEnums.ConnectMode.UNKNOWN|  
|AdoEnums.ConnectMode.WRITE|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Mode 속성(ADO)](../../../ado/reference/ado-api/mode-property-ado.md)|[Open 메서드(ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Open 메서드(ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)|[스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|

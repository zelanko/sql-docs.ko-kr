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
ms.openlocfilehash: debf6f9dc4ac1326caf9fbf32b65f15f34a19094
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67933452"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
[연결](../../../ado/reference/ado-api/connection-object-ado.md)의 데이터를 수정 하거나 [레코드](../../../ado/reference/ado-api/record-object-ado.md)를 열거나 **Record** 및 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체의 [Mode](../../../ado/reference/ado-api/mode-property-ado.md) 속성 값을 지정 하는 데 사용할 수 있는 권한을 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|읽기 전용 권한을 나타냅니다.|  
|**adModeReadWrite**|3|읽기/쓰기 권한을 나타냅니다.|  
|**adModeRecursive**|0x400000|다른 * \*sharedeny\* * 값 (**adModeShareDenyNone**, **adModeShareDenyWrite**또는 **adModeShareDenyRead**)과 함께 사용 되어 현재 **레코드**의 모든 하위 레코드에 공유 제한을 전파 합니다. **레코드** 에 자식이 없는 경우에는 영향을 주지 않습니다. **AdModeShareDenyNone** 에서만 사용 되는 경우 런타임 오류가 생성 됩니다. 그러나 다른 값과 결합 하는 경우 **adModeShareDenyNone** 와 함께 사용할 수 있습니다. 예를 들어 "**adModeRead** 또는 **adModeShareDenyNone** 또는 **adModeRecursive**"을 사용할 수 있습니다.|  
|**adModeShareDenyNone**|16|다른 사용자가 모든 권한으로 연결을 열 수 있도록 허용 합니다. 다른 사용자의 읽기 또는 쓰기 액세스가 거부될 수 있습니다.|  
|**adModeShareDenyRead**|4|다른 사용자가 읽기 권한을 가진 연결을 열 수 없도록 합니다.|  
|**adModeShareDenyWrite**|8|다른 사용자가 쓰기 권한으로 연결을 열 수 없도록 합니다.|  
|**adModeShareExclusive**|12|다른 사용자가 연결을 열 수 없도록 합니다.|  
|**adModeUnknown**|0|기본값 사용 권한이 아직 설정 되지 않았거나 확인할 수 없음을 나타냅니다.|  
|**adModeWrite**|2|쓰기 전용 권한을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums|  
|AdoEnums. READWRITE|  
|(AdoEnums에 해당 하는 항목이 없습니다.|  
|AdoEnums SHAREDENYNONE|  
|AdoEnums SHAREDENYREAD|  
|AdoEnums SHAREDENYWRITE|  
|AdoEnums. SHAREEXCLUSIVE|  
|AdoEnums 모드입니다. 알 수 없음|  
|AdoEnums|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Mode 속성(ADO)](../../../ado/reference/ado-api/mode-property-ado.md)|[Open 메서드(ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Open 메서드(ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)|[스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|

---
title: ConnectModeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ConnectModeEnum
helpviewer_keywords: ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 99befb958e09e6973059d9677fa51ca1d5f7fc1c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="connectmodeenum"></a>ConnectModeEnum
데이터 수정에 대 한 사용할 수 있는 사용 권한을 지정는 [연결](../../../ado/reference/ado-api/connection-object-ado.md)열고는 [레코드](../../../ado/reference/ado-api/record-object-ado.md), 또는 대 한 값을 지정 하는 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 의 속성은  **레코드** 및 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|읽기 전용 권한을 나타냅니다.|  
|**adModeReadWrite**|3|읽기/쓰기 권한을 나타냅니다.|  
|**adModeRecursive**|0x400000|다른와 함께 사용할  *\*ShareDeny\**  값 (**adModeShareDenyNone**, **adModeShareDenyWrite**, 또는 **adModeShareDenyRead**) 현재 공유 제한이 모든 하위 레코드를 전파 하는 데 **레코드**합니다. 경우에 없는 아무런 영향을 미치지는 **레코드** 자식을 포함 하지 않습니다. 함께 사용 하는 경우 런타임 오류가 발생 **adModeShareDenyNone** 만 합니다. 하지만,와 함께 사용할 수 **adModeShareDenyNone** 다른 값과 결합 하는 경우. 사용할 수는 예를 들어 "**adModeRead** 또는 **adModeShareDenyNone** 또는 **adModeRecursive**"입니다.|  
|**adModeShareDenyNone**|16|다른 사용자가 모든 권한으로 연결을 열 수 있습니다. 다른 사용자의 읽기 또는 쓰기 액세스가 거부될 수 있습니다.|  
|**adModeShareDenyRead**|4|다른 사용자를 한 읽기 권한이 있는 한 연결을 열 수 없도록 방지 합니다.|  
|**adModeShareDenyWrite**|8|다른에서 쓰기 권한으로 연결을 열 수 없습니다.|  
|**adModeShareExclusive**|12|다른 사용자를 한 연결을 열 수 없도록 방지 합니다.|  
|**adModeUnknown**|0|기본. 사용 권한이 설정 되지 않은 또는 확인할 수 없는 나타냅니다.|  
|**adModeWrite**|2|쓰기 전용 권한을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.ConnectMode.READ|  
|AdoEnums.ConnectMode.READWRITE|  
|(에 AdoEnums.ConnectMode.RECURSIVE의 해당 키 없음)|  
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

---
title: Mode 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Mode
- _Stream::Mode
- _Record::Mode
helpviewer_keywords:
- Mode property [ADO]
ms.assetid: 808661eb-0d7c-4e6d-8e40-9dc3bef3d77a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e821c98f5d390e0eb30dcada9a816c6e29d9d482
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707552"
---
# <a name="mode-property-ado"></a>Mode 속성(ADO)
데이터 수정에 사용할 수 있는 권한을 나타냅니다는 [연결](../../../ado/reference/ado-api/connection-object-ado.md)를 [레코드](../../../ado/reference/ado-api/record-object-ado.md), 또는 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) 값입니다. 에 대 한 기본값을 **연결** 됩니다 **adModeUnknown**합니다. 에 대 한 기본값을 **레코드** 개체가 **adModeRead**합니다. 기본값을 **Stream** 원본에 연결 (원본으로 또는 기본적으로 URL을 사용 하 여 열린 **Stream** 의 **레코드**)는  **adModeRead**합니다. 에 대 한 기본값을 **Stream** 내부 연관 되지 않은 (메모리에서 시작) 하는 원본이 **adModeUnknown**.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **모드** 속성을 설정 하거나 현재 연결에서 공급자가 사용에 대 한 액세스 권한을 반환 합니다. 설정할 수 있습니다 합니다 **모드** 속성 경우에만 합니다 **연결** 개체가 닫혀 있습니다.  
  
 에 대 한는 **Stream** 개체를 사용 하 여 원본에서 상속 된 액세스 모드를 지정 하지 않으면 합니다 **Stream** 개체입니다. 예를 들어 경우는 **Stream** 에서 열리는 **레코드** 개체와 동일한 모드에서 열리는 기본적으로는 **레코드**합니다.  
  
 이 속성이 읽기/쓰기 개체는 닫혀 있고 읽기 전용 개체 열려 있는 동안입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용 되 면 **연결** 개체를 **모드** 속성 설정할 수 있습니다 **adModeUnknown**합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목  
 [IsolationLevel 및 모드 속성 예제 (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 및 모드 속성 예제 (VC + +)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   

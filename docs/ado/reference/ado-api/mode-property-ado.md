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
ms.openlocfilehash: bc5b2e2bce410309656bad5591a3df90781cc8bc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932224"
---
# <a name="mode-property-ado"></a>Mode 속성(ADO)
[연결](../../../ado/reference/ado-api/connection-object-ado.md), [레코드](../../../ado/reference/ado-api/record-object-ado.md)또는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체의 데이터를 수정 하는 데 사용할 수 있는 권한을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 [Connectmodeenum](../../../ado/reference/ado-api/connectmodeenum.md) 값을 설정 하거나 반환 합니다. **연결** 의 기본값은 **admodeunknown**입니다. **Record** 개체의 기본값은 **adModeRead**입니다. 원본으로 URL을 사용 하 여 열거나 **레코드**의 기본 **스트림으로** 연 기본 소스와 연결 된 **스트림의** 기본값은 **adModeRead**입니다. 내부 소스와 연결 되지 않은 (메모리에서 인스턴스화된) **스트림의** 기본값은 **admodeunknown**입니다.  
  
## <a name="remarks"></a>설명  
 **Mode** 속성을 사용 하 여 현재 연결에서 공급자가 사용 하는 액세스 권한을 설정 하거나 반환 합니다. **연결** 개체가 닫혀 있을 때만 **Mode** 속성을 설정할 수 있습니다.  
  
 **Stream** 개체의 경우 액세스 모드가 지정 되지 않은 경우 **stream** 개체를 여는 데 사용 된 원본에서 상속 됩니다. 예를 들어 **record** 개체에서 **스트림을** 열 경우 기본적으로 **레코드**와 동일한 모드로 열립니다.  
  
 개체가 닫혀 있는 동안에는이 속성이 읽기/쓰기이 고, 개체가 열려 있는 동안에는 읽기 전용입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽 **연결** 개체에서 사용 하는 경우 **Mode** 속성은 **admodeunknown**으로만 설정할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>참고 항목  
 [IsolationLevel 및 Mode 속성 예제 (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 및 Mode 속성 예제 (VC + +)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   

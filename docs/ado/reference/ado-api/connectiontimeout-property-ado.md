---
title: ConnectionTimeout 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionTimeout
helpviewer_keywords:
- ConnectionTimeout property [ADO]
ms.assetid: 8904a403-1383-4b4b-b53d-5c01d6f5deac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5cb3e6e1cc4266551bfeabf09bde1a65fea032f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707251"
---
# <a name="connectiontimeout-property-ado"></a>ConnectionTimeout 속성(ADO)
종료 하 고 오류를 생성 하기 전에 연결을 설정 하는 동안 대기할 시간을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 **긴** 연결이 열릴 때까지 대기 하는 초 단위로 나타내는 값입니다. 기본값은 15입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 합니다 **ConnectionTimeout** 속성을 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 경우 네트워크 트래픽 또는 많은 서버 사용에서 지연이 발생 하 게 연결 시도 중단 하는 데 필요한 개체입니다. 경우에서 시간을 **ConnectionTimeout** 오류가 발생 하는 연결을 열기 전에 속성 설정은 경과 하 고 ADO 시도 취소 합니다. 속성을 0으로 설정 하면 ADO 연결이 열릴 때까지 무한정 기다릴 수 있습니다. 코드를 작성 하는 공급자를 지원 해야 합니다 **ConnectionTimeout** 기능입니다.  
  
 합니다 **ConnectionTimeout** 를 열었을 때 닫혀 있고 읽기 전용으로 연결 되 면 속성은 읽기/쓰기입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [ConnectionString, ConnectionTimeout, 및 State 속성 예제 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString, ConnectionTimeout, 및 State 속성 예제 (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [CommandTimeout 속성(ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)

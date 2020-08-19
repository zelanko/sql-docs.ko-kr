---
description: ConnectionTimeout 속성(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c117974f9335ef3aa939f742781f3f381ab6cbd2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444445"
---
# <a name="connectiontimeout-property-ado"></a>ConnectionTimeout 속성(ADO)
시도를 종료 하 고 오류를 생성 하기 전에 연결을 설정 하는 동안 대기 하는 시간을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 연결이 열릴 때까지 대기 하는 시간 (초)을 나타내는 **long** 값을 설정 하거나 반환 합니다. 기본값은 15입니다.  
  
## <a name="remarks"></a>설명  
 네트워크 트래픽 또는 과도 한 서버 사용의 지연으로 인해 연결 시도를 중단 해야 하는 경우 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체에서 **ConnectionTimeout** 속성을 사용 합니다. 연결을 열기 전에 **ConnectionTimeout** 속성 설정의 시간이 경과 하면 오류가 발생 하 고 ADO에서 시도를 취소 합니다. 속성을 0으로 설정 하면 ADO는 연결이 열릴 때까지 무기한 대기 합니다. 코드를 작성 하는 공급자가 **ConnectionTimeout** 기능을 지원 하는지 확인 합니다.  
  
 **ConnectionTimeout** 속성은 연결이 닫힌 경우 읽기/쓰기이 고, 열려 있으면 읽기 전용입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [ConnectionString, ConnectionTimeout 및 State 속성 예제 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString, ConnectionTimeout 및 State 속성 예제 (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [CommandTimeout 속성(ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)

---
title: "ConnectionTimeout 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::ConnectionTimeout
helpviewer_keywords:
- ConnectionTimeout property [ADO]
ms.assetid: 8904a403-1383-4b4b-b53d-5c01d6f5deac
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d00956df35fc6b3f5d6d864ea72d9efdea69fe56
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="connectiontimeout-property-ado"></a>ConnectionTimeout 속성 (ADO)
시도 종료 하 고 오류를 생성 하기 전에 연결을 설정 하는 동안 대기 시간을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **긴** 연결이 열리기 전까지 대기 하는 초 단위로 나타내는 값입니다. 기본값은 15입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **ConnectionTimeout** 속성에는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 경우 네트워크 트래픽 또는 중형 서버 사용에서 지연이 발생 하 게 연결 시도 중단 하는 데 필요한 개체입니다. 경우는에서 시간은 **ConnectionTimeout** 오류가 발생 속성 설정이 연결을 열기 전에 경과 하 고 ADO 시도 취소 합니다. 속성을 0으로 설정 하는 경우 ADO는 연결이 열릴 때까지 무기한 대기 합니다. 코드를 작성 하는 공급자를 지원 하는지 확인는 **ConnectionTimeout** 기능입니다.  
  
 **ConnectionTimeout** 속성은 읽기/쓰기 연결이 닫혀 있고 읽기 전용으로 열려 있으면입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ConnectionString, ConnectionTimeout, 및 상태 속성 예제 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString, ConnectionTimeout, 및 상태 속성 예제 (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [CommandTimeout 속성(ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)


---
title: "CommandTimeout 속성 (ADO) | Microsoft Docs"
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
f1_keywords: Command15::CommandTimeout
helpviewer_keywords: CommandTimeout property [ADO]
ms.assetid: c611f857-d6b0-4dca-8925-f4a02e769eb0
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 64a989729fa084210cc780d9fb88a0830ddfddb4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="commandtimeout-property-ado"></a>CommandTimeout 속성 (ADO)
시도 종료 하 고 오류를 생성 하기 전에 명령을 실행 하는 동안 대기 시간을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **긴** 명령이 실행 때까지 대기 하는 초 단위로 나타내는 값입니다. 기본값은 30입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **CommandTimeout** 속성에는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 또는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 의 취소를 허용 하는 개체는 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드 네트워크 트래픽 또는 중형 서버 사용의 지연으로 인해 호출 합니다. 간격 설정는 **CommandTimeout** 속성 명령 실행을 완료 하면 오류가 발생 하 고 ADO 명령을 취소 되기 전에 경과 합니다. 속성을 0으로 설정 하는 경우 ADO는 무기한 실행이 완료 될 때까지 대기 합니다. 확인을 작성 하는 코드 지원 공급자 및 데이터 소스는 **CommandTimeout** 기능입니다.  
  
 **CommandTimeout** 에 설정는 **연결** 에 영향을 주지 않습니다는 **CommandTimeout** 에 설정 된 **명령** 개체에 동일한 **연결**, 즉는 **명령** 개체의 **CommandTimeout** 속성의 값을 상속 하지 않습니다는 **연결** 개체의 **CommandTimeout** 값입니다.  
  
 에 **연결** 개체는 **CommandTimeout** 속성은 유지 읽기/쓰기 이후에 **연결** 열릴 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [ConnectionTimeout 속성(ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)

---
title: Close 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Close
- _Stream::Close
- _Record::Close
helpviewer_keywords:
- Close method [ADO]
ms.assetid: 3cdf27d1-a180-4cff-8e42-95dec5fb1b55
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e692e8853417abae386ac151eca4b49f11b12f02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698993"
---
# <a name="close-method-ado"></a>Close 메서드(ADO)
열려 있는 개체와 모든 종속 개체를 닫습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>Remarks  
 사용 된 **닫습니다** 닫는 메서드를를 [연결](../../../ado/reference/ado-api/connection-object-ado.md), [레코드](../../../ado/reference/ado-api/record-object-ado.md), [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 또는 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체 모든 연결 된 시스템 리소스를 해제 합니다. 개체 닫기지 않습니다 하지 메모리에서 제거 합니다. 해당 속성 설정을 변경 하 고 나중에 다시 열 수 있습니다. 메모리에서 개체를 완전히 제거 하려면 개체를 닫고 다음 개체 변수를 설정 합니다 *Nothing* (Visual Basic에서는).  
  
## <a name="connection"></a>연결  
 사용 하 여 합니다 **닫습니다** 닫는 메서드를를 **연결** 개체에도 활성 닫힙니다 **레코드 집합** 연결과 관련 된 개체입니다. A [명령](../../../ado/reference/ado-api/command-object-ado.md) 연관 된 개체를 **연결** 닫는 개체 유지 되지만 더 이상 사용 하 여 연결 될를 **연결** 개체, 즉 해당 [ ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성에 설정할 **Nothing**합니다. 또한 합니다 **명령** 개체의 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 공급자가 정의한 매개 변수의 컬렉션을 지워집니다.  
  
 나중에 호출 수를 [열려](../../../ado/reference/ado-api/open-method-ado-connection.md) 동일 또는 다른 데이터 원본에 대 한 연결을 다시 설정 하는 방법입니다. 동안 합니다 **연결** 개체가 닫혀, 데이터 원본에 대해 열린 연결을 필요로 하는 모든 메서드를 호출 하면 오류가 발생 합니다.  
  
 닫는 **연결** 열린 동안 개체 **레코드 집합** 연결에서 개체 롤백합니다 보류 중인 변경 내용을 모든 합니다 **레코드 집합** 개체입니다. 명시적으로 닫는 **연결** 개체 (호출를 **닫기** 메서드) 진행률 트랜잭션 되는 동안 오류를 생성 합니다. 경우는 **연결** 개체 트랜잭션이 진행에서 중일 때 범위를 벗어나는, ADO 자동으로 트랜잭션을 롤백합니다.  
  
## <a name="recordset-record-stream"></a>레코드 집합에서 레코드를 Stream  
 사용 하 여는 **닫습니다** 닫는 메서드를를 **레코드 집합**를 **레코드**, 또는 **Stream** 개체 관련된 데이터 및 단독 액세스를 해제 합니다. 이 특정 개체를 통해 데이터에 했습니다 있을 수 있습니다. 나중에 호출 수를 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 동일 하거나 수정 된 개체를 다시 여는 메서드 특성입니다.  
  
 하지만 **레코드 집합** 개체가 닫혀, 라이브 커서를 필요로 하는 모든 메서드를 호출 하면 오류가 발생 합니다.  
  
 편집을 진행 하는 동안 즉시 업데이트 모드에 있으면 호출을 **닫기** 방법으로 오류를 생성, 대신를 호출 합니다 [업데이트](../../../ado/reference/ado-api/update-method.md) 또는 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 메서드 첫 번째. 닫으면 합니다 **레코드 집합** 일괄 처리 업데이트 모드에서는 마지막 이후의 모든 변경 내용이 개체 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 호출 손실 됩니다.  
  
 사용 하는 경우는 [복제](../../../ado/reference/ado-api/clone-method-ado.md) 개방적이 고 복사본을 만들어야 하는 방법 **레코드 집합** 개체를 원본 또는 복제본을 닫는 영향을 주지 않습니다 다른 복사본입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목  
 [Open 및 Close 메서드 예제 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 및 Close 메서드 예제 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 및 Close 메서드 예제 (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 메서드 (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Save 메서드](../../../ado/reference/ado-api/save-method.md)

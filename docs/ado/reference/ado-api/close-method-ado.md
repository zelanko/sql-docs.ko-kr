---
title: Close 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Close
- _Stream::Close
- _Record::Close
helpviewer_keywords:
- Close method [ADO]
ms.assetid: 3cdf27d1-a180-4cff-8e42-95dec5fb1b55
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1cf9ee921355368dc9aaffb2905fb79eced5b7d
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35276488"
---
# <a name="close-method-ado"></a>Close 메서드 (ADO)
열려 있는 개체와 모든 종속 개체를 닫습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>Remarks  
 사용 하 여는 **닫습니다** 을 닫는 메서드는 [연결](../../../ado/reference/ado-api/connection-object-ado.md), [레코드](../../../ado/reference/ado-api/record-object-ado.md), [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 또는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체 모든 연결 된 시스템 리소스를 해제 합니다. 개체를 닫아도 제거 되지 않고 메모리;에서 으로 설정 하 고 나중에 다시 열 수 있습니다. 메모리에서 개체를 완전히 제거 하려면 개체를 닫고 다음 개체 변수를 설정 *Nothing* (Visual Basic)에서는 합니다.  
  
## <a name="connection"></a>연결  
 사용 하는 **닫습니다** 을 닫는 메서드는 **연결** 개체에는 활성도 닫힙니다 **레코드 집합** 연결과 관련 된 개체입니다. A [명령](../../../ado/reference/ado-api/command-object-ado.md) 연관 된 개체는 **연결** 닫으려는 개체 유지 되지만과 더 이상 연결 될 것을 **연결** 개체, 즉 해당 [ ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성으로 설정 됩니다 **Nothing**합니다. 또한는 **명령** 개체의 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션의 모든 공급자가 정의한 매개 변수 지워질 예정입니다.  
  
 나중에 호출 수는 [열려](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드는 동일한 데이터 원본이 나 다른 데이터 원본에 연결을 다시 설정 합니다. 반면는 **연결** 개체가 닫혀, 데이터 원본에 대해 열린 연결을 필요로 하는 메서드를 호출 하면 오류가 발생 합니다.  
  
 닫기는 **연결** 열려 있는 동안 개체 **레코드 집합** 연결에서 개체 롤백합니다 보류 중인 변경 내용이 모든는 **레코드 집합** 개체입니다. 명시적으로 닫을 **연결** 개체 (호출는 **닫기** 메서드)는 트랜잭션이 중인 동안 진행 하면 오류가 발생 합니다. 경우는 **연결** 개체는 트랜잭션이 진행 중인 동안 범위를 벗어납니다, ADO 자동으로 트랜잭션을 롤백합니다.  
  
## <a name="recordset-record-stream"></a>레코드 집합, 레코드, 스트림  
 사용 하는 **닫습니다** 을 닫는 메서드는 **레코드 집합**, **레코드**, 또는 **스트림** 개체는 연결 된 데이터 및 모든 단독 액세스를 해제 합니다. 이 특정 개체를 통해 데이터에 했을 수도 있습니다. 나중에 호출할 수 있습니다는 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 동일 하지만, 또는 수정 된 개체를 다시 열려면 메서드 특성입니다.  
  
 반면는 **레코드 집합** 개체가 닫혀, 라이브 커서를 필요로 하는 메서드를 호출 하면 오류가 발생 합니다.  
  
 편집 하는 즉시 업데이트 모드에 있는 동안 진행 중인 경우 호출 된 **닫기** 방법으로 오류를 생성, 대신, 호출는 [업데이트](../../../ado/reference/ado-api/update-method.md) 또는 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 메서드 첫 번째입니다. 닫으면는 **레코드 집합** 일괄 업데이트 모드에서는 마지막 이후의 모든 변경 내용은 개체 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 호출 손실 됩니다.  
  
 사용 하는 경우는 [복제](../../../ado/reference/ado-api/clone-method-ado.md) 열린의 복사본을 만들고 메서드 **레코드 집합** 개체를 원본 또는 복제본을 닫으면 영향을 주지 않습니다 다른 복사본입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목  
 [Open 및 Close 메서드 예제 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 및 Close 메서드 (VBScript) 예제](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 및 Close 메서드 예제 (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 메서드 (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Save 메서드](../../../ado/reference/ado-api/save-method.md)

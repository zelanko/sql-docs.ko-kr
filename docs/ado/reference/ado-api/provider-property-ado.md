---
title: "공급자 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::get_Provider
- Connection15::PutProvider
- Connection15::put_Provider
- Connection15::GetProvider
- Connection15::Provider
helpviewer_keywords: Provider property [ADO]
ms.assetid: 0ff70e72-0061-4ffc-90fb-e3ea23129bb2
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ead9a90e3788efd420251912612de520279b43e5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="provider-property-ado"></a>공급자 속성 (ADO)
에 대 한 공급자의 이름을 표시 한 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **문자열** 공급자 이름을 나타내는 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **공급자** 속성을 설정 하거나 연결에 대 한 공급자의 이름을 반환 합니다. 하지만이 속성의 내용으로 설정할 수도 있습니다는 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성 또는 *ConnectionString* 의 인수는 [열려](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드; 공급자를 지정 호출 하는 동안 둘 이상의 위치에는 **열려** 메서드 예기치 않은 결과 가질 수 있습니다. 지정 된 없는 공급자 속성은 기본적으로 MSDASQL ([Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)).  
  
 **공급자** 속성은 읽기/쓰기 연결이 닫혀 있고 읽기 전용으로 열려 있으면입니다. 설정이 적용 되지 않습니다 할 때까지 열거나는 **연결** 개체 또는 액세스는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 의 컬렉션은 **연결** 개체입니다. 설정이 유효 하지 않을 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [공급자 및 DefaultDatabase 속성 예제 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [공급자 및 DefaultDatabase 속성 예제 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)

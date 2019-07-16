---
title: 공급자 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::get_Provider
- Connection15::PutProvider
- Connection15::put_Provider
- Connection15::GetProvider
- Connection15::Provider
helpviewer_keywords:
- Provider property [ADO]
ms.assetid: 0ff70e72-0061-4ffc-90fb-e3ea23129bb2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fae46773befb13105ed9dcd81b1116be48cf0675
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931455"
---
# <a name="provider-property-ado"></a>Provider 속성(ADO)
에 대 한 공급자의 이름을 나타내는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 **문자열** 공급자 이름을 지정 하는 값입니다.  
  
## <a name="remarks"></a>설명  
 사용 된 **공급자** 속성을 설정 하거나 연결 공급자의 이름을 반환 합니다. 그러나이 속성의 내용으로 설정할 수도 있습니다는 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성 또는 *ConnectionString* 인수의 [열기](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드를 공급자를 지정 호출 하는 동안 하나 이상의 위치에는 **열고** 메서드 예기치 않은 결과가 있을 수 있습니다. 공급자가 없습니다 지정 된 경우 속성을 기본값으로 설정 됩니다 MSDASQL ([Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)).  
  
 합니다 **공급자** 를 열었을 때 닫혀 있고 읽기 전용으로 연결 되 면 속성은 읽기/쓰기입니다. 설정이 적용 되지 않습니다 때까지 열거나를 **연결** 개체 또는 액세스를 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 의 컬렉션을 **연결** 개체입니다. 설정이 올바르지 않으면 오류가 발생 했습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Provider 및 DefaultDatabase 속성 예제 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider 및 DefaultDatabase 속성 예제 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)

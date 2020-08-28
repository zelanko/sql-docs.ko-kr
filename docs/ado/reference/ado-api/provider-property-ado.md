---
description: Provider 속성(ADO)
title: Provider 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4c3f45e8652568bd0440121e27ee6ee0c116e676
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989914"
---
# <a name="provider-property-ado"></a>Provider 속성(ADO)
[연결](./connection-object-ado.md) 개체에 대 한 공급자의 이름을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 공급자 이름을 나타내는 **문자열** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **공급자** 속성을 사용 하 여 연결에 대 한 공급자의 이름을 설정 하거나 반환 합니다. 이 속성은 [connectionstring](./connectionstring-property-ado.md) 속성의 내용 또는 [Open](./open-method-ado-connection.md) 메서드의 *connectionstring* 인수에 의해 설정 될 수도 있습니다. 그러나 **Open** 메서드를 호출 하는 동안 둘 이상의 장소에 공급자를 지정 하면 예기치 않은 결과가 발생할 수 있습니다. 공급자를 지정 하지 않으면이 속성은 기본적으로 MSDASQL ([Microsoft OLE DB provider FOR ODBC](../../guide/appendixes/microsoft-ole-db-provider-for-odbc.md))로 지정 됩니다.  
  
 **공급자** 속성은 연결이 닫혀 있을 때 읽기/쓰기이 고, 열려 있으면 읽기 전용입니다. **연결 개체를 열거나** **Connection** 개체의 [Properties](./properties-collection-ado.md) 컬렉션에 액세스할 때 까지는 설정이 적용 되지 않습니다. 설정이 유효 하지 않으면 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Provider 및 DefaultDatabase 속성 예제 (VB)](./provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider 및 DefaultDatabase 속성 예제 (VB)](./provider-and-defaultdatabase-properties-example-vb.md)   
 [ODBC 용 Microsoft OLE DB 공급자](../../guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [부록 A: 공급자](../../guide/appendixes/appendix-a-providers.md)
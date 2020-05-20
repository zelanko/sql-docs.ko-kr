---
title: Error 개체 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error
helpviewer_keywords:
- error object [ADO]
ms.assetid: a175d453-fa55-4f49-9ede-a26d83177919
author: rothja
ms.author: jroth
ms.openlocfilehash: 717a3af4bec62725cc4cf5da8621163f24c2ab3f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764534"
---
# <a name="error-object"></a>Error 개체
공급자와 관련 된 단일 작업과 관련 된 데이터 액세스 오류에 대 한 세부 정보를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 ADO 개체와 관련 된 모든 작업은 하나 이상의 공급자 오류를 생성할 수 있습니다. 오류가 발생 하는 경우 하나 이상의 **오류** 개체가 [Connection](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [Errors](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션에 배치 됩니다. 다른 ADO 작업에서 오류가 생성 되 면 **errors** 컬렉션이 지워지고 새 **오류** 개체 집합이 **errors** 컬렉션에 배치 됩니다.  
  
> [!NOTE]
>  각 **Error** 개체는 ADO 오류가 아닌 특정 공급자 오류를 나타냅니다. ADO 오류는 런타임 예외 처리 메커니즘에 노출 됩니다. 예를 들어 Microsoft Visual Basic에서 ADO 관련 오류가 발생 하면 **오류 발생 시** 이벤트가 트리거되고 **오류** 개체에 표시 됩니다. ADO 오류의 전체 목록은 [Errorvalueenum](../../../ado/reference/ado-api/errorvalueenum.md) 항목을 참조 하세요.  
  
 **오류** 개체의 속성을 읽고 다음을 포함 하 여 각 오류에 대 한 구체적인 정보를 얻을 수 있습니다.  
  
-   [설명](../../../ado/reference/ado-api/description-property.md) 속성-오류 텍스트를 포함 합니다. 이 속성은 기본 속성입니다.  
  
-   [Number](../../../ado/reference/ado-api/number-property-ado.md) 속성은 오류 상수의 정수 ( **Long** ) 값을 포함 합니다.  
  
-   [소스](../../../ado/reference/ado-api/source-property-ado-error.md) 속성-오류를 발생 시킨 개체를 식별 합니다. 이는 데이터 원본에 대 한 요청에 따라 **Errors** 컬렉션에 몇 가지 **오류** 개체가 있는 경우에 특히 유용 합니다.  
  
-   SQL 데이터 원본의 정보를 제공 하는 [SQLState](../../../ado/reference/ado-api/sqlstate-property.md) 및 [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md) 속성  
  
 공급자 오류가 발생 하면 **연결** 개체의 **Errors** 컬렉션에 배치 됩니다. ADO는 단일 ADO 작업을 통해 여러 오류를 반환 하 여 공급자와 관련 된 오류 정보를 허용할 수 있도록 지원 합니다. 오류 처리기에서 이러한 풍부한 오류 정보를 얻으려면 작업 중인 언어나 환경의 적절 한 오류 트래핑 기능을 사용한 다음 중첩 된 루프를 사용 하 여 **Errors** 컬렉션에 있는 각 **오류** 개체의 속성을 열거 합니다.  
  
> [!NOTE]
>  **Microsoft Visual Basic 및 VBScript 사용자** 유효한 **연결** 개체가 없으면 **오류** 개체에서 오류 정보를 검색 해야 합니다.  
  
 공급자와 마찬가지로 ADO는 잠재적으로 새 공급자 오류를 생성할 수 있는 호출을 수행 하기 전에 **OLE 오류 정보** 개체를 지웁니다. 그러나 **연결** 개체의 **Errors** 컬렉션은 공급자가 새 오류를 생성 하거나 [Clear](../../../ado/reference/ado-api/clear-method-ado.md) 메서드를 호출 하는 경우에만 지워집니다.  
  
 일부 속성 및 **메서드는 오류 컬렉션에** **오류** 개체로 표시 되지만 프로그램의 실행을 중단 하지 않는 경고를 반환 합니다. [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드를 호출 하기 전에 **Connection** 개체의 [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드 또는 **레코드 집합** 개체에 대해 [Filter](../../../ado/reference/ado-api/filter-property.md) 속성을 설정 하 고 **Errors** 컬렉션에서 **Clear** 메서드를 호출 합니다. 이렇게 하면 **Errors** 컬렉션의 [Count](../../../ado/reference/ado-api/count-property-ado.md) 속성을 읽어 반환 된 경고를 테스트할 수 있습니다.  
  
 **Error** 개체는 스크립팅에 안전 하지 않습니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Error 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Description, HelpContext, HelpFile, NativeError, Number, Source 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description, HelpContext, HelpFile, NativeError, Number, Source 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Connection 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Errors 컬렉션 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)

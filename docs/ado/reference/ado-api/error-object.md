---
title: Error 개체 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error
helpviewer_keywords:
- error object [ADO]
ms.assetid: a175d453-fa55-4f49-9ede-a26d83177919
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6911493ab691b2c5e40ff4fa7331261070d981be
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="error-object"></a>Error 개체
공급자 관련 단일 작업에 관련 된 데이터 액세스 오류에 대 한 세부 정보를 포함 합니다.  
  
## <a name="remarks"></a>주의  
 ADO 개체를 관련 된 모든 작업 공급자 오류가 하나 이상 생성할 수 있습니다. 하나 이상의 오류가 발생할 때마다 **오류** 개체에 배치 되는 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 의 컬렉션은 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다. 다른 ADO 작업에서 오류를 생성 하는 경우는 **오류** 컬렉션의 선택을 취소 하 고 새로운 집합이 **오류** 개체에 배치 됩니다는 **오류** 컬렉션입니다.  
  
> [!NOTE]
>  각 **오류** 개체는 ADO 오류가 아니라 공급자 특정 오류를 나타냅니다. ADO 오류는 런타임 예외 처리 메커니즘에 노출 됩니다. 예를 들어 Microsoft Visual Basic에서 ADO 관련 오류 발생 트리거할는 **On Error** 이벤트에 표시는 **오류** 개체입니다. ADO 오류 목록은 전체 참조는 [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md) 항목입니다.  
  
 읽을 수는 **오류** 개체의 속성을 다음을 포함 한 각 오류에 대 한 세부 정보:  
  
-   [설명](../../../ado/reference/ado-api/description-property.md) 오류의 텍스트를 포함 하는 속성입니다. 기본 속성입니다.  
  
-   [번호](../../../ado/reference/ado-api/number-property-ado.md) 포함 된 속성을는 **긴** 의 오류 상수 정수 값입니다.  
  
-   [소스](../../../ado/reference/ado-api/source-property-ado-error.md) 속성을 오류를 발생 시킨 개체를 식별 합니다. 이 기능은 여러 있을 때 특히 유용 **오류** 개체에 **오류** 데이터 원본에 대 한 요청 후 컬렉션입니다.  
  
-   [SQLState](../../../ado/reference/ado-api/sqlstate-property.md) 및 [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md) SQL 데이터 원본에서 정보를 제공 하는 속성입니다.  
  
 에 위치한 공급자 오류가 발생 하는 경우는 **오류** 의 컬렉션은 **연결** 개체입니다. ADO 지원 단일 ADO 작업 수 있도록 오류 정보에 대 한 공급자와 관련 하 여 여러 개의 오류를 반환 합니다. 오류 처리기에서 이러한 풍부한 오류 정보를 사용 하려면 언어 또는 작업 중인 환경에 적절 한 오류 트래핑 기능을 사용 하 고 중첩 된 루프를 사용 하 여 각 속성을 열거 하 **오류** 개체에 **오류** 컬렉션입니다.  
  
> [!NOTE]
>  **Microsoft Visual Basic 및 VBScript 사용자** 더 유효한 경우 **연결** 개체에서 오류 정보를 검색 해야 합니다는 **오류** 개체입니다.  
  
 공급자와 마찬가지로 이때 ADO 지웁니다는 **OLE 오류 정보** 새 공급자 오류를 생성 될 수도 호출을 수행 하기 전에 개체입니다. 그러나는 **오류** 컬렉션에는 **연결** 개체를 선택이 취소 하 고 있거나 공급자 새 오류가 있을 때만 채운는 [지우기](../../../ado/reference/ado-api/clear-method-ado.md) 메서드를 호출 합니다.  
  
 일부 속성 및 메서드로 표시 되는 경고를 반환 **오류** 개체에 **오류** 컬렉션 하지만 프로그램 실행이 중단 되지는 않습니다. 호출 하기 전에 [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), 또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 에 대 한 메서드는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체는 [열](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드를 한 **연결** ; 개체 또는 설정는 [필터](../../../ado/reference/ado-api/filter-property.md) 속성에는 **레코드 집합** 개체를 호출 하는 **의선택을취소**에서 메서드는 **오류** 컬렉션입니다. 읽을 수 이런 방식으로 [개수](../../../ado/reference/ado-api/count-property-ado.md) 속성은 **오류** 테스트할 컬렉션을 경고를 반환 합니다.  
  
 **오류** 개체가 스크립팅 작업에 안전 합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [Error 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Errors 컬렉션 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)

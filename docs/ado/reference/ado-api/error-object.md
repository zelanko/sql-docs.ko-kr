---
title: 오류 개체 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5018dc921267663d64037024ef21c82ac6e3f7c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932969"
---
# <a name="error-object"></a>Error 개체
공급자와 관련 된 단일 작업에 관련 된 데이터 액세스 오류에 대 한 세부 정보를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 ADO 개체와 관련 된 모든 작업이 하나 이상의 공급자 오류를 생성할 수 있습니다. 하나 이상의 오류가 발생할 때마다 **오류** 개체에 배치 됩니다 합니다 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 의 컬렉션을 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다. 다른 ADO 작업에서 오류를 생성 하는 경우는 **오류** 컬렉션의 선택을 취소 하 고 새 집합입니다 **오류** 개체에 배치 됩니다는 **오류** 컬렉션.  
  
> [!NOTE]
>  각 **오류** 개체는 ADO 오류가 아니라 특정 공급자 오류를 나타냅니다. ADO 오류는 런타임 예외 처리 메커니즘에 노출 됩니다. 예를 들어, Microsoft Visual Basic의 ADO 관련 오류가 발생 트리거할를 **오류 발생 시** 이벤트에 표시 합니다 **오류** 개체입니다. ADO 오류 목록은 전체 참조는 [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md) 항목입니다.  
  
 읽을 수는 **오류** 개체의 속성을 다음을 비롯 한 각 오류에 대 한 세부 정보:  
  
-   합니다 [설명을](../../../ado/reference/ado-api/description-property.md) 오류의 텍스트를 포함 하는 속성입니다. 기본 속성입니다.  
  
-   [수](../../../ado/reference/ado-api/number-property-ado.md) 포함 하는 속성을 **긴** 오류 상수 정수 값입니다.  
  
-   합니다 [원본](../../../ado/reference/ado-api/source-property-ado-error.md) 오류를 발생 시킨 개체를 식별 하는 속성입니다. 있을 때 특히 유용 **오류** 개체를 **오류** 데이터 원본에 요청을 수행 하는 컬렉션입니다.  
  
-   합니다 [SQLState](../../../ado/reference/ado-api/sqlstate-property.md) 하 고 [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md) SQL 데이터 원본에서 정보를 제공 하는 속성입니다.  
  
 에 위치한 공급자 오류가 발생 하는 경우는 **오류** 의 컬렉션을 **연결** 개체입니다. ADO 지원 공급자 관련 오류 정보에 대 한 허용 하도록 단일 ADO 작업으로 여러 오류를 반환 합니다. 오류 처리기에서이 다양 한 오류 정보를 얻으려면 언어나, 사용 중인 환경에 적절 한 오류 트래핑 기능을 사용 하 여 다음 중첩 된 루프를 사용 하 여 각 속성을 열거할 **오류** 개체는 **오류** 컬렉션입니다.  
  
> [!NOTE]
>  **Microsoft Visual Basic 및 VBScript 사용자** 없으면 잘못 **연결** 개체에서 오류 정보를 검색 해야 합니다 **오류** 개체입니다.  
  
 공급자와 마찬가지로 이때 ADO 지웁니다 합니다 **OLE 오류 정보** 새 공급자 오류를 생성 될 수도 호출 전에 개체입니다. 그러나를 **오류** 컬렉션에는 **연결** 개체는 지워지고 때 또는 공급자는 새 오류를 생성 하는 경우에 채워집니다를 [지우기](../../../ado/reference/ado-api/clear-method-ado.md) 메서드가 호출 됩니다.  
  
 일부 속성 및 메서드 반환로 표시 되는 경고 **오류** 개체를 **오류** 컬렉션 하지만 프로그램의 실행을 중단 되지는 않습니다. 호출 하기 전에 [다시 동기화](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), 또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) ; 개체는 [엽니다](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드를를 **연결** 개체를 가져오거나 설정 합니다 [필터](../../../ado/reference/ado-api/filter-property.md) 속성을를 **레코드 집합** 개체를 호출는 **선택을취소**메서드는 **오류** 컬렉션입니다. 읽을 수 있습니다 따라서를 [수](../../../ado/reference/ado-api/count-property-ado.md) 의 속성을 **오류** 를 테스트할 컬렉션 경고를 반환 합니다.  
  
 합니다 **오류** 개체가 스크립팅 작업에 안전 합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [Error 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [설명, HelpContext, HelpFile, NativeError, 번호, 원본 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [설명, HelpContext, HelpFile, NativeError, 번호, 원본 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Errors 컬렉션 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)

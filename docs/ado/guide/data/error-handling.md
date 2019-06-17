---
title: 오류 처리 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reporting errors [ADO]
- errors [ADO]
- ADO, error handling
ms.assetid: 4909e413-f3b0-4183-8ad3-67b1434df742
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 56d41b8c8fddff4d49cdb213834f45eac7fd5462
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700765"
---
# <a name="error-handling"></a>오류 처리
ADO 오류 발생 하는 응용 프로그램에 알리기 위해 여러 가지 방법을 사용 합니다. 이 섹션에서는 ADO 응용 프로그램은 알림을 보내는 방법 및 사용할 때 발생할 수 있는 오류의 유형을 설명 합니다. 이러한 오류를 처리 하는 방법에 대 한 제안이 끝납니다.  
  
## <a name="how-does-ado-report-errors"></a>ADO 오류를 보고 하는 방법  
 ADO는 여러 가지 방법으로 오류에 대 한 수를 알립니다.  
  
-   ADO 오류 런타임 오류를 생성합니다. ADO 오류를 사용 하는 등의 기타 런타임 오류 하는 동일한 방식으로 처리를 **오류 발생 시** Visual Basic의 문입니다.  
  
-   프로그램은 OLE DB에서 오류를 받을 수 있습니다. OLE DB 오류가 런타임 오류를 생성합니다.  
  
-   경우 오류는 하나 이상의 데이터 공급자에 특정 **오류** 개체에 배치 됩니다는 **오류** 의 컬렉션을 **연결** 는 데이터에 액세스 하는 데 사용 된 개체 오류가 발생 한 저장 합니다.  
  
-   오류 정보에 위치한 이벤트를 발생 시킨 프로세스 오류가 생성 하는 경우는 **오류** 개체 및 이벤트에 매개 변수로 전달 합니다. 참조 [ADO 이벤트 처리](../../../ado/guide/data/handling-ado-events.md) 이벤트에 대 한 자세한 내용은 합니다.  
  
-   업데이트 또는 다른 대량 작업과 관련 된 문제를 처리할 때 발생 하는 일괄 처리를 **레코드 집합** 로 표시 되어야 합니다 **상태** 속성의를 **레코드 집합**합니다. 예를 들어, 스키마 제약 조건 위반 또는 권한이 여 지정할 수 있습니다 **RecordStatusEnum** 값입니다.  
  
-   특정 관련 발생 하는 문제 **필드** 현재 레코드에도으로 표시 됩니다는 **상태** 각각의 속성 **필드** 에 **필드**  의 컬렉션을 **레코드** 하거나 **레코드 집합**합니다. 업데이트를 완료할 수 없습니다 또는 호환 되지 않는 데이터 형식으로 지정할 수 있습니다 예를 들어 **FieldStatusEnum** 값입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ADO 오류](../../../ado/guide/data/ado-errors.md)  
  
-   [공급자 오류](../../../ado/guide/data/provider-errors.md)  
  
-   [필드 관련 오류 정보](../../../ado/guide/data/field-related-error-information.md)  
  
-   [레코드 집합 관련 오류 정보](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [다른 언어로 오류 처리](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [오류 예측](../../../ado/guide/data/anticipating-errors.md)

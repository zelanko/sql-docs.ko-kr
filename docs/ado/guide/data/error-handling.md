---
title: "오류 처리 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reporting errors [ADO]
- errors [ADO]
- ADO, error handling
ms.assetid: 4909e413-f3b0-4183-8ad3-67b1434df742
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8434e598deba57bf72dfdb8df1c31990113b304c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="error-handling"></a>오류 처리
ADO 오류 발생 하는 응용 프로그램에 알리기 위해 여러 가지 방법을 사용 합니다. 이 섹션에는 ADO 및 응용 프로그램 통지 하는 방법을 사용 하는 경우 발생할 수 있는 오류의 유형을 설명 합니다. 이러한 오류를 처리 하는 방법에 대 한 제안이 결론을 내립니다.  
  
## <a name="how-does-ado-report-errors"></a>ADO 오류를 보고 하는 방법  
 ADO 여러 가지 방법으로 오류에 대 한 알려줍니다.  
  
-   ADO 오류 런타임 오류를 생성합니다. ADO 오류를 사용 하는 등의 다른 런타임 오류는 동일한 방식으로 처리는 **On Error** Visual Basic의 문.  
  
-   프로그램은 OLE DB에서 오류를 받을 수 있습니다. OLE DB 오류는 런타임에 오류를 생성합니다.  
  
-   경우 오류는 데이터 공급자에 하나 이상의 특정 **오류** 개체에 배치 되는 **오류** 의 컬렉션은 **연결** 데이터에 액세스 하는 데 사용 된 개체 오류가 발생 한 경우 저장 합니다.  
  
-   이벤트를 발생 시킨 프로세스 오류가 생성 하는 경우 오류 정보에 저장 됩니다는 **오류** 개체 및 이벤트를 매개 변수로 전달 합니다. 참조 [ADO 이벤트 처리](../../../ado/guide/data/handling-ado-events.md) 이벤트에 대 한 자세한 내용은 합니다.  
  
-   업데이트 또는 다른 대량 작업과 관련 된 문제를 처리할 때 발생 하는 일괄 처리는 **레코드 집합** 로 표시 되도록는 **상태** 의 속성은 **레코드 집합**합니다. 예를 들어 스키마 제약 조건 위반 또는 사용 권한이 여 지정할 수 있습니다 **RecordStatusEnum** 값입니다.  
  
-   특정 관련 된 발생 하는 문제 **필드** 현재 레코드에서도로 표시 됩니다는 **상태** 각 속성 **필드** 에 **필드**  의 컬렉션은 **레코드** 또는 **레코드 집합**합니다. 업데이트를 완료할 수 없습니다 또는 호환 되지 않는 데이터 형식으로 지정할 수 있습니다 예를 들어 **FieldStatusEnum** 값입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ADO 오류](../../../ado/guide/data/ado-errors.md)  
  
-   [공급자 오류](../../../ado/guide/data/provider-errors.md)  
  
-   [필드 관련 오류 정보](../../../ado/guide/data/field-related-error-information.md)  
  
-   [레코드 집합 관련 오류 정보](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [다른 언어로 오류 처리](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [오류 예측](../../../ado/guide/data/anticipating-errors.md)

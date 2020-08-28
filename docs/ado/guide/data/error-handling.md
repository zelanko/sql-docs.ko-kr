---
description: ADO의 오류 처리
title: 오류 처리 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reporting errors [ADO]
- errors [ADO]
- ADO, error handling
ms.assetid: 4909e413-f3b0-4183-8ad3-67b1434df742
author: rothja
ms.author: jroth
ms.openlocfilehash: dd91a11798b292fffcb0cdc96ad7eec8504029fa
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991324"
---
# <a name="error-handling-in-ado"></a>ADO의 오류 처리
ADO는 여러 가지 방법을 사용 하 여 발생 하는 오류를 응용 프로그램에 알립니다. 이 섹션에서는 ADO를 사용할 때 발생할 수 있는 오류 유형과 응용 프로그램에 알리는 방법을 설명 합니다. 이러한 오류를 처리 하는 방법에 대 한 제안으로 마무리 합니다.  
  
## <a name="how-does-ado-report-errors"></a>ADO에서 오류를 보고 하는 방법  
 ADO는 다음과 같은 여러 가지 방법으로 오류에 대해 알려줍니다.  
  
-   ADO 오류는 런타임 오류를 생성 합니다. Visual Basic에서 **On error** 문을 사용 하는 것과 같은 다른 런타임 오류와 동일한 방식으로 ADO 오류를 처리 합니다.  
  
-   프로그램은 OLE DB에서 오류를 받을 수 있습니다. OLE DB 오류가 발생 하면 런타임 오류도 생성 됩니다.  
  
-   오류가 데이터 공급자와 관련 된 경우 오류가 발생 했을 때 데이터 저장소에 액세스 하는 데 사용 된 **연결** 개체의 **Errors** 컬렉션에 하나 이상의 **오류** 개체가 배치 됩니다.  
  
-   이벤트를 발생 시킨 프로세스에서 오류가 발생 한 **경우 오류 정보는 오류 개체에** 배치 되 고 이벤트에 매개 변수로 전달 됩니다. 이벤트에 대 한 자세한 내용은 [ADO 이벤트 처리](./handling-ado-events.md) 를 참조 하세요.  
  
-   일괄 처리 업데이트 또는 **레코드 집합** 을 포함 하는 다른 대량 작업을 처리할 때 발생 하는 문제는 **레코드 집합**의 **Status** 속성으로 표시 될 수 있습니다. 예를 들어 스키마 제약 조건 위반 또는 권한이 부족 한 경우 **Recordstatusenum** 값으로 지정할 수 있습니다.  
  
-   현재 레코드의 특정 **필드** 와 관련 하 여 발생 하는 문제는 **레코드** 또는 **레코드 집합**의 **Fields** 컬렉션에 있는 각 **필드** 의 **Status** 속성에도 표시 됩니다. 예를 들어 완료할 수 없는 업데이트 또는 호환 되지 않는 데이터 형식을 **Fieldstatusenum** 값으로 지정할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ADO 오류](./ado-errors.md)  
  
-   [공급자 오류](./provider-errors.md)  
  
-   [필드 관련 오류 정보](./field-related-error-information.md)  
  
-   [레코드 집합 관련 오류 정보](./recordset-related-error-information.md)  
  
-   [다른 언어로 오류 처리](./handling-errors-in-other-languages.md)  
  
-   [오류 예측](./anticipating-errors.md)
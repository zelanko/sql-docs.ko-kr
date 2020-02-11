---
title: Microsoft Visual Basic에서 ADO 사용 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, Visual Basic
- Visual Basic [ADO]
ms.assetid: 9dfb6784-037d-4f9d-bb7f-b506b4498573
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22286cbe571420475cf273ca377d16e79610fc3e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926564"
---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>Microsoft Visual Basic 및 Visual Basic for Applications에서 ADO 사용
ADO 프로젝트를 설정 하 고 ADO 코드를 작성 하는 것은 Visual Basic 또는 Visual Basic for Applications를 사용 하는 경우와 비슷합니다. 이 항목에서는 Visual Basic와 Visual Basic for Applications 모두 ADO를 사용 하는 방법을 설명 하 고 차이점을 설명 합니다.

## <a name="referencing-the-ado-library"></a>ADO 라이브러리 참조
 프로젝트에서 ADO 라이브러리를 참조 해야 합니다.

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>Microsoft Visual Basic에서 ADO를 참조 하려면

1.  Visual Basic의 **프로젝트** 메뉴에서 **참조 ...** 를 선택 합니다.

2.  목록에서 **Microsoft ADO(ActiveX Data Objects) x. x 라이브러리** 를 선택 합니다. 다음 라이브러리도 하나 이상 선택 되어 있는지 확인 합니다.

    -   Visual Basic for Applications

    -   Visual Basic 런타임 개체 및 프로시저

    -   개체 및 프로시저 Visual Basic

    -   OLE Automation

3.  **확인**을 클릭합니다.

 예를 들어 Microsoft Access를 사용 하 여 Visual Basic for Applications와 마찬가지로 ADO를 쉽게 사용할 수 있습니다.

#### <a name="to-reference-ado-from-microsoft-access"></a>Microsoft Access에서 ADO를 참조 하려면

1.  Microsoft Access의 **데이터베이스** 창에서 **모듈 탭을 사용 하 여 모듈** 을 선택 하거나 만듭니다.

2.  **도구** 메뉴에서 **참조 ...** 를 선택 합니다.

3.  목록에서 **Microsoft ADO(ActiveX Data Objects) x. x 라이브러리** 를 선택 합니다. 다음 라이브러리도 하나 이상 선택 되어 있는지 확인 합니다.

    -   Visual Basic for Applications

    -   Microsoft Access 8.0 개체 라이브러리 (또는 그 이상)

    -   Microsoft DAO 3.5 개체 라이브러리 (이상)

4.  **확인**을 클릭합니다.

## <a name="creating-ado-objects-in-visual-basic"></a>Visual Basic에서 ADO 개체 만들기
 해당 변수에 대 한 개체의 인스턴스 및 자동화 변수를 만들려면 **Dim** 또는 **CreateObject**의 두 가지 메서드를 사용할 수 있습니다.

### <a name="dim"></a>Dim
 **Dim** 과 함께 **New** 키워드를 사용 하 여 한 단계로 ADO 개체의 인스턴스를 선언 하 고 만들 수 있습니다.

```
Dim conn As New ADODB.Connection
```

 또는 **Dim** 문 선언 및 개체 인스턴스화를 두 단계로 수행할 수도 있습니다.

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  프로젝트에서 ADO 라이브러리를 올바르게 참조 하 `ADODB` 는 경우 **Dim** 문과 함께 progid를 명시적으로 사용할 필요는 없습니다. 그러나이를 사용 하면 다른 라이브러리와 이름 충돌이 발생 하지 않습니다.

> [!NOTE]
>  예를 들어 동일한 프로젝트에 ADO와 DAO 둘 다에 대 한 참조를 포함 하는 경우 다음 코드와 같이 **레코드 집합** 개체를 인스턴스화할 때 사용할 개체 모델을 지정 하는 한정자를 포함 해야 합니다.

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 **CreateObject** 메서드를 사용 하는 경우 선언 및 개체 인스턴스화는 두 개의 불연속 단계 여야 합니다.

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 **CreateObject** 로 인스턴스화된 개체는 런타임에 바인딩되어 있으며,이는 강력 하 게 형식화 되지 않고 명령줄 완성이 사용 되지 않음을 의미 합니다. 그러나 프로젝트에서 ADO 라이브러리 참조를 건너뛸 수 있으며 특정 버전의 개체를 인스턴스화할 수 있습니다. 다음은 그 예입니다.

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 특히 ADO 버전 2.0 형식 라이브러리에 대 한 참조를 만들고 개체를 만들어이를 수행할 수도 있습니다.

 **CreateObject** 메서드를 사용 하 여 개체를 인스턴스화하는 것은 일반적으로 **Dim** 문을 사용 하는 것 보다 느립니다.

## <a name="handling-events"></a>이벤트 처리
 Microsoft Visual Basic에서 ADO 이벤트를 처리 하려면 **WithEvents** 키워드를 사용 하 여 모듈 수준 변수를 선언 해야 합니다. 변수는 클래스 모듈의 일부로만 선언할 수 있으며 모듈 수준에서 선언 되어야 합니다. ADO 이벤트를 처리 하는 방법에 대 한 자세한 내용은 [Ado 이벤트 처리](../../../ado/guide/data/handling-ado-events.md)를 참조 하세요.

## <a name="visual-basic-examples"></a>Visual Basic 예제
 많은 Visual Basic 예제는 ADO 설명서에 포함 되어 있습니다. 자세한 내용은 [Microsoft Visual Basic의 ADO 코드 예제](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md)를 참조 하세요.

## <a name="see-also"></a>참고 항목
 Ado ( [Microsoft ADO(ActiveX Data Objects))](../../../ado/microsoft-activex-data-objects-ado.md) [를](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) 사용 하 여 ado를 사용 하는 Microsoft Visual C++ [스크립트 언어와 함께 ado 사용](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)

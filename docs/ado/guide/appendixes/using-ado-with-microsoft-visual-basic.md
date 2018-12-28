---
title: Microsoft Visual Basic 및 Visual Basic for Applications로 ADO 사용하기 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: d409f874e9fcec059c01ddef91d83d8a70fdeb47
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694181"
---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>Microsoft Visual Basic 및 Visual Basic for Applications로 ADO 사용하기
Visual Basic을 사용하든 Visual Basic for Application을 사용하든 ADO 프로젝트를 설정하고 ADO 코드를 작성하는 작업은 거의 비슷합니다. 이 항목에서는 Visual Basic 및 Visual Basic for Applications에서 ADO를 사용하는 방법 및 차이점에 대한 유의 사항을 다룹니다.

## <a name="referencing-the-ado-library"></a>ADO 라이브러리 참조하기
 자신의 프로젝트에서 ADO 라이브러리를 참조해야 합니다(만약 ADO 기능을 이용하려면).

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>Microsoft Visual Basic에서 ADO 참조하기

1.  Visual Basic에서 **프로젝트** 메뉴에서 **참조**를 클릭합니다...

2.  목록에서 **Microsoft ActiveX Data Objects x.x Library**를 선택합니다. 다음 라이브러리도 함께 선택되어 있는지 확인합니다.

    -   Visual Basic for Applications

    -   Visual Basic runtime objects and procedures

    -   Visual Basic objects and procedures

    -   OLE Automation

3.  **확인**을 클릭합니다.

 예를 들어 Microsoft Access를 사용하여 Visual Basic for Applications에서도 쉽게 ADO를 사용할 수 있습니다.

#### <a name="to-reference-ado-from-microsoft-access"></a>Microsoft Access에서 ADO 참조하기

1.  Microsoft Access에서, **데이터베이스** 창의 **모듈** 탭에서 모듈을 선택하거나 만듭니다.

2.  **도구** 메뉴에서 **참조**를 클릭합니다.

3.  목록에서 **Microsoft ActiveX Data Objects x.x Library**를 선택합니다. 다음 라이브러리도 함께 선택되어 있는지 확인합니다.

    -   Visual Basic for Applications

    -   Microsoft Access 8.0 Object Library 또는 이상

    -   Microsoft DAO 3.5 Object Library 또는 이상

4.  **확인**을 클릭합니다.

## <a name="creating-ado-objects-in-visual-basic"></a>Visual Basic에서 ADO 개체 만들기
 자동화 변수 및 해당 변수에 대한 개체의 인스턴스를 만들려면 두 가지 방법을 사용할 수 있습니다: **Dim** 혹은 **CreateObject** 문을 사용합니다.

### <a name="dim"></a>Dim 문
 한 번에 ADO 개체의 인스턴스를 만들려면 **Dim** 문과 함께 **New** 키워드를 사용합니다.

```
Dim conn As New ADODB.Connection
```

 다른 방법으로, **Dim** 문으로 선언한 다음 개체를 초기화하는 두 단계로 처리할 수도 있습니다.

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  자신의 프로젝트에서 ADO 라이브러리를 올바르게 참조했다면, **Dim** 문과 함께 `ADODB` progid를 반드시 사용할 필요는 없습니다. 그러나, 이 식별자를 사용하면 다른 라이브러리와의 이름 충돌을 확실히 방지할 수 있습니다.

> [!NOTE]
>  예를 들어, 동일한 프로젝트에서 ADO와 DAO를 모두 참조에 포함시켰다면, 다음 코드와 같이 **Recordset** 개체를 인스턴스화할 때 사용할 개체 모델을 지정하는 한정자를 반드시 포함해야 합니다.

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject 메서드
 **CreateObject** 메서드를 사용할 때에는 선언과 개체 인스턴스화 작업은 반드시 두 개의 개별 단계로 해야 합니다.

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 **CreateObject** 메서드를 이용하여 인스턴스화된 개체는 후기 바인딩 처리됩니다. 이것은 데이터 타입을 확정할 수 없으며, 그로 인해 명령줄 완성 기능이 비활성화된다는 뜻입니다. 그러나, 이렇게 처리하면 자신의 프로젝트에서 ADO 라이브러리를 참조하지 않아도 되고, (런타임 시에) 특정 버전의 개체로 인스턴스화할 수도 있습니다. 다음 예를 참고하십시오.

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 특히 ADO 버전 2.0 형식 라이브러리에 대 한 참조를 만들고 개체를 만들기도 수행할 수 있습니다.

 **CreateObject** 메서드를 사용하여 개체를 인스턴스화하는 작업은 **Dim** 문을 사용하는 것보다 일반적으로 느립니다.

## <a name="handling-events"></a>이벤트 처리
 Microsoft Visual Basic에서 ADO 이벤트를 처리하려면, **WithEvents** 키워드를 이용하여 모듈 수준의 변수를 선언해야 합니다. 이 변수는 클래스 모듈의 일부로 선언되어야 하고, 모듈 수준에서 선언되어야 합니다. ADO 이벤트를 처리하는 것에 대한 논의는 [ADO 이벤트 처리](../../../ado/guide/data/handling-ado-events.md)를 참고하십시오.

## <a name="visual-basic-examples"></a>Visual Basic 예제
 ADO 설명서에 더 많은 Visual Basic 예제가 있습니다. 자세한 내용은 [Microsoft Visual Basic의 ADO 코드 예제](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md)를 참고하십시오.

## <a name="see-also"></a>참고 항목
 [Microsoft ActiveX Data Objects(ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [Microsoft Visual C++에서 ADO 사용하기](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [스크립팅 언어에서 ADO 사용하기](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)

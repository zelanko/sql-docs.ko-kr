---
title: Microsoft Visual Basic ADO를 사용 하 여 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, Visual Basic
- Visual Basic [ADO]
ms.assetid: 9dfb6784-037d-4f9d-bb7f-b506b4498573
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: f0a27c38bde206b841829956ef3a555c5c655f8d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>Microsoft Visual Basic 및 Visual Basic ADO를 사용 하 여 응용 프로그램에 대 한
ADO 프로젝트를 설정 하 고 ADO 코드를 작성은 유사 사용할지 Visual Basic 또는 Visual Basic 응용 프로그램에 대 한 합니다. 이 항목 응용 프로그램에 대 한 Visual Basic 및 Visual Basic 모두와 함께 ADO를 사용 및 차이 인식 합니다.

## <a name="referencing-the-ado-library"></a>ADO 라이브러리 참조
 ADO 라이브러리 프로젝트에서 참조 되어야 합니다.

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>Microsoft Visual Basic에서 ADO 참조 하려면

1.  Visual basic에서에서 **프로젝트** 메뉴 선택 **참조 중...** .

2.  선택 **Microsoft ActiveX Data Objects x.x 라이브러리** 목록에서 합니다. 적어도 확인 다음 라이브러리도 선택:

    -   Visual Basic for Applications

    -   Visual Basic 런타임 개체 및 절차

    -   Visual Basic 개체 및 절차

    -   OLE Automation

3.  **확인**을 클릭합니다.

 사용할 수 있습니다 ADO 손쉽게 Visual Basic을 사용한 응용 프로그램의 경우 예를 들어 Microsoft Access를 사용 하 여.

#### <a name="to-reference-ado-from-microsoft-access"></a>Microsoft Access에서 ADO 참조 하려면

1.  Microsoft Access에서 선택 하거나에서 모듈을 만듭니다는 **모듈** 탭에 **데이터베이스** 창.

2.  에 **도구** 메뉴 선택 **참조 중...** .

3.  선택 **Microsoft ActiveX Data Objects x.x 라이브러리** 목록에서 합니다. 적어도 확인 다음 라이브러리도 선택:

    -   Visual Basic for Applications

    -   Microsoft Access 8.0 개체 라이브러리 (또는 이상)

    -   Microsoft DAO 3.5 개체 라이브러리 (또는 이상)

4.  **확인**을 클릭합니다.

## <a name="creating-ado-objects-in-visual-basic"></a>Visual Basic에서 ADO 개체 만들기
 자동화 변수 및 해당 변수에 대 한 개체의 인스턴스를 만들려면 두 가지 방법을 사용할 수 있습니다: **Dim** 또는 **CreateObject**합니다.

### <a name="dim"></a>Dim
 사용할 수는 **새로** 키워드와 **Dim** 선언 하 고 한 번에 ADO 개체의 인스턴스를 만들:

```
Dim conn As New ADODB.Connection
```

 또는 **Dim** 문을 선언과 개체 인스턴스화 두 단계로 실행할 수도 있습니다.

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  명시적으로 사용 하지 않아도 됩니다는 `ADODB` progid를 **Dim** 문, 올바르게 ADO 라이브러리 프로젝트에서 참조 하는 것으로 가정 합니다. 그러나 것을 사용 하면 됩니다 하는 것과 다른 라이브러리 이름이 충돌 합니다.

> [!NOTE]
>  예를 들어, 동일한 프로젝트에 ADO 및 DAO 모두에 대 한 참조를 포함 하는 경우를 인스턴스화할 때 사용 하는 개체 모델을 지정 하는 한정자 포함 해야 **레코드 집합** 다음 코드 에서처럼 개체:

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 와 **CreateObject** 방법, 선언 및 개체 인스턴스화 두 불연속 단계 여야 합니다.

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 사용 하 여 개체를 인스턴스화할 **CreateObject** 런타임에 바인딩되므로 강력한 형식이 아니며 및 명령줄 완성 비활성화 되었음을 의미 합니다. 그러나 ADO 라이브러리 프로젝트에서 참조할 수 있습니다 및 특정 버전의 개체를 인스턴스화할 수 있습니다. 예를 들어:

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 특히 ADO 버전 2.0 형식 라이브러리에 대 한 참조를 만들고 개체를 만드는 수행할 수 있습니다.

 사용 하 여 개체를 인스턴스화는 **CreateObject** 메서드는 일반적으로 사용 하 여 보다 느린는 **Dim** 문.

## <a name="handling-events"></a>이벤트 처리
 모듈 수준 변수를 사용 하 여 선언 해야 ADO Microsoft Visual Basic의 이벤트를 처리 하기 위해는 **WithEvents** 키워드입니다. 변수는 클래스 모듈의 일부로 선언 될 수 있으며 모듈 수준에서 선언 해야 합니다. ADO 이벤트 처리의 보다 철저 한 논의 알려면 [ADO 이벤트 처리](../../../ado/guide/data/handling-ado-events.md)합니다.

## <a name="visual-basic-examples"></a>Visual Basic 예제
 많은 Visual Basic 예제 ADO 설명서에 포함 됩니다. 자세한 내용은 참조 [ADO 코드 예제에서는 Microsoft Visual Basic](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md)합니다.

## <a name="see-also"></a>관련 항목:
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [Microsoft Visual c + +와 함께 ADO 사용](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [스크립트 언어와 함께 ADO 사용](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)

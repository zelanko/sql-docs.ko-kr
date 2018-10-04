---
title: Microsoft Visual Basic로 ADO를 사용 하 여 | Microsoft Docs
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
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>Microsoft Visual Basic 및 Visual Basic을 사용 하 여 ADO를 사용 하 여 응용 프로그램에 대 한
ADO 프로젝트를 설정 하 고 ADO 코드를 작성은 유사 사용할지 Visual Basic 또는 Visual Basic 응용 프로그램에 대 한 합니다. 이 항목에서는 Visual Basic과 Visual Basic을 사용 하 여 ADO를 사용 하 여 응용 프로그램에 대 한 주소 및 차이 정보입니다.

## <a name="referencing-the-ado-library"></a>ADO 라이브러리 참조
 ADO 라이브러리 프로젝트에서 참조 되어야 합니다.

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>Microsoft Visual Basic에서 ADO 참조

1.  Visual basic의 경우에서 **프로젝트** 메뉴에서 **참조 하는 중...** .

2.  선택 **Microsoft ActiveX Data Objects x.x 라이브러리** 목록에서. 이상 있는지 확인 하는 다음 라이브러리도 함께 선택 합니다.

    -   Visual Basic for Applications

    -   Visual Basic 런타임 개체 및 절차

    -   Visual Basic 개체 및 절차

    -   OLE Automation

3.  **확인**을 클릭합니다.

 사용할 수 있습니다 ADO 손쉽게 Visual Basic을 사용한 응용 프로그램에 대 한 예를 들어 Microsoft Access를 사용 하 여.

#### <a name="to-reference-ado-from-microsoft-access"></a>Microsoft Access에서 ADO 참조

1.  Microsoft Access에서 만들거나 선택에서 모듈을 **모듈** 탭에 **데이터베이스** 창.

2.  에 **도구** 메뉴에서 **참조 하는 중...** .

3.  선택 **Microsoft ActiveX Data Objects x.x 라이브러리** 목록에서. 이상 있는지 확인 하는 다음 라이브러리도 함께 선택 합니다.

    -   Visual Basic for Applications

    -   Microsoft Access 8.0 개체 라이브러리 (또는 이상)

    -   Microsoft DAO 3.5 개체 라이브러리 (또는 이상)

4.  **확인**을 클릭합니다.

## <a name="creating-ado-objects-in-visual-basic"></a>Visual Basic의 ADO 개체 만들기
 Automation 변수 및 해당 변수에 대 한 개체의 인스턴스를 만들려면 두 가지 방법을 사용할 수 있습니다: **Dim** 하거나 **CreateObject**합니다.

### <a name="dim"></a>Dim
 사용할 수는 **새로 만들기** 키워드를 사용 **Dim** 선언 하 고 한 번에 ADO 개체의 인스턴스를 생성 하려면:

```
Dim conn As New ADODB.Connection
```

 또는 합니다 **Dim** 문에 선언 및 개체 인스턴스화 두 단계로 실행할 수도 있습니다.

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  명시적으로 사용할 필요는 없습니다는 `ADODB` progid를 합니다 **Dim** 문, 프로젝트에서 ADO 라이브러리를 올바르게 참조 했는지 가정 합니다. 그러나 사용을 유지할 수는 없습니다 다른 라이브러리를 사용 하 여 충돌 합니다.

> [!NOTE]
>  예를 들어, 동일한 프로젝트에서 ADO 및 DAO 모두에 대 한 참조를 포함 하는 경우 인스턴스화할 때 사용 하는 개체 모델을 지정 하려면 한정자를 포함 해야 **레코드 집합** 다음 코드 에서처럼 개체:

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 사용 하 여 합니다 **CreateObject** 메서드를 선언 및 개체 인스턴스화 두 불연속 단계 여야 합니다.

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 사용 하 여 개체를 인스턴스화할 **CreateObject** 런타임에 바인딩되며, 즉 강력한 형식이 아니며 및 명령줄 완성 기능이 비활성화 됩니다. 그러나 프로젝트에서 ADO 라이브러리 참조를 건너뛸 수 있습니다 하 고 특정 버전의 개체를 인스턴스화할 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 특히 ADO 버전 2.0 형식 라이브러리에 대 한 참조를 만들고 개체를 만들기도 수행할 수 있습니다.

 사용 하 여 개체를 인스턴스화를 **CreateObject** 메서드를 사용 하 여 보다 일반적으로 느립니다 합니다 **Dim** 문.

## <a name="handling-events"></a>이벤트 처리
 모듈 수준 변수를 사용 하 여 선언 해야 Microsoft Visual Basic의 ADO 이벤트를 처리 하기 위해 합니다 **WithEvents** 키워드입니다. 변수는 클래스 모듈의 일부로 선언할 수 있으며 모듈 수준에서 선언 되어야 합니다. ADO 이벤트를 처리 하는 더 상세히 논의 참조 하세요 [ADO 이벤트 처리](../../../ado/guide/data/handling-ado-events.md)합니다.

## <a name="visual-basic-examples"></a>Visual Basic 예제
 많은 Visual Basic 예제 ADO 설명서에 포함 됩니다. 자세한 내용은 [Microsoft Visual Basic의 ADO 코드 예제](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md)합니다.

## <a name="see-also"></a>관련 항목
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [ADO를 사용 하 여 Microsoft Visual c + +를 사용 하 여](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [스크립팅 언어와 함께 ADO 사용](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)

---
title: "Fields 컬렉션 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Field object [ADO], fields collection
- Fields collection [ADO]
ms.assetid: 574cf36e-e5f5-403b-983c-749ef93c108f
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2c5d81985322b03892d17875959086078defd819
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="the-fields-collection"></a>Fields 컬렉션
**필드** 컬렉션은 ADO의 내장 컬렉션 중 하나입니다. 컬렉션은 하나의 단위로 참조할 수 있는 항목의 정렬된 된 집합. ADO 컬렉션에 대 한 자세한 내용은 참조 [The ADO 개체 모델](../../../ado/guide/data/ado-objects-and-collections.md)합니다.  
  
 **필드** 컬렉션에 포함 되어는 **필드** 에서 모든 필드 (열)에 대 한 개체는 **레코드 집합**합니다. 모든 ADO 컬렉션와 마찬가지로 **Count** 및 **항목** 속성으로 **Append** 및 **새로 고침** 메서드. 또한 **CancelUpdate**, **삭제**, **다시 동기화**, 및 **업데이트** 메서드는 다른 ADO 컬렉션에 사용할 수 없습니다.  
  
## <a name="examining-the-fields-collection"></a>Fields 컬렉션 검토  
 고려는 **필드** 샘플의 컬렉션 **레코드 집합** 이 섹션에서 소개 합니다. 샘플 **레코드 집합** SQL 문에서 파생 되었습니다  
  
```  
SELECT ProductID, ProductName, UnitPrice FROM Products WHERE CategoryID = 7  
```  
  
 따라서를 찾아야 하는 **레코드 집합 필드** 컬렉션에 세 개의 필드가 포함 되어 있습니다.  
  
```  
'BeginWalkFields  
    Dim objFields As ADODB.Fields  
    Dim intLoop As Integer  
  
    objRs.Open strSQL, strConnStr, adOpenForwardOnly, adLockReadOnly, adCmdText  
  
    Set objFields = objRs.Fields  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
    Next  
'EndWalkFields  
```  
  
 이 코드는 단순히 수가 결정 **필드** 개체에 **필드** 사용 하 여 컬렉션의 **Count** 속성 및 루프의 값을 반환 하는 컬렉션을 통해 **이름** 각 속성이 **필드** 개체입니다. 더 많은 사용할 수 있습니다 **필드** 속성 필드에 대 한 정보를 얻을 수 있습니다. 쿼리에 대 한 자세한 내용은 **필드**, 참조 [Field 개체](../../../ado/guide/data/the-field-object.md)합니다.  
  
## <a name="counting-columns"></a>계산 열  
 짐작할 수는 **Count** 의 실제 수를 반환 하는 속성 **필드** 개체에 **필드** 컬렉션입니다. 컬렉션의 멤버에 대 한 번호는 0부터 시작, 때문에 항상 코드를 작성 해야 루프는 0부터 시작 및 끝 값으로는 **Count** 속성 값-1입니다. Microsoft Visual Basic을 사용 하는 경우 확인 하지 않고 컬렉션의 멤버를 반복 하는 **Count** 속성을 사용 하 여는 **각각에 대해... 다음** 명령입니다.  
  
 경우는 **Count** 속성이 0 이면 컬렉션에는 개체가 있습니다.  
  
## <a name="getting-to-the-field"></a>필드  
 임의의 ADO 컬렉션는 **항목** 속성은 컬렉션의 기본 속성입니다. 개별 반환 **필드** 이름으로 지정 된 개체 또는 인덱스에 전달 합니다. 따라서 다음 문은 동일 샘플 **레코드 집합**:  
  
```  
objField = objRecordset.Fields.Item("ProductID")  
objField = objRecordset.Fields("ProductID")  
objField = objRecordset.Fields.Item(0)  
objField = objRecordset.Fields(0)  
```  
  
 이러한 메서드는 동일 하는 경우 가장 좋은 것은 무엇입니까? 그것은 사정 나름이에요. 인덱스를 사용 하 여 검색 한 **필드** 컬렉션 절은 더 빠르게 액세스 하기는 **필드** 문자열 조회를 수행 하지 않고 직접 합니다. 반면, 순서 **필드** 컬렉션 내에서 알 수 있어야 합니다 경우 순서 변경에 대 한 참조는 **필드의** 변경 될 때마다 인덱스가 필요 합니다. 하지만 약간 더 느려집니다 이름을 사용 하는 **필드** 의 순서에 영향을 받지 않으므로 더 융통성이 **필드** 컬렉션에 있습니다.  
  
## <a name="using-the-refresh-method"></a>Refresh 메서드를 사용 하 여  
 일부 다른 ADO 사용 하 여 컬렉션와 달리는 **새로 고침** 에서 메서드는 **필드** 컬렉션이 가시적 효과가 없습니다. 에서 변경 내용을 기본 데이터베이스 구조를 검색 하려면 하나를 사용 해야는 **Requery** 메서드, 또는 경우에는 **레코드 집합** 개체가 책갈피, 지원 하지 않습니다는 **MoveFirst**메서드 되는 명령이 공급자에 대해 다시 실행 합니다.  
  
## <a name="adding-fields-to-a-recordset"></a>레코드 집합에 필드 추가  
 **Append** 메서드는 필드를 추가 하는 데 사용 됩니다는 **레코드 집합**합니다.  
  
 사용할 수는 **Append** 을 구성 하는 메서드는 **레코드 집합** 데이터 원본에 대 한 연결을 열지 않고 프로그래밍 방식으로 합니다. 런타임 오류가 발생 합니다는 **추가** 메서드가 호출 되는 **필드** 열린 컬렉션 **레코드 집합** 또는 **레코드 집합** 여기서는 **ActiveConnection** 속성이 설정 되어 있습니다. 필드에만 추가할 수 있습니다는 **레코드 집합** 열려 있지 않으면 하 고 데이터 원본에 아직 연결 되지 않습니다. 그러나 새로 추가 된 항목에 대 한 값을 지정 하려면 **필드**, **레코드 집합** 먼저 열어야 합니다.  
  
 개발자가 일시적으로 일부 데이터를 저장 하거나 사용자 인터페이스에서 데이터 바인딩에 사용할 수 있도록 하는 서버에서 보낸 것 처럼 동작 하는 일부 데이터를 사용할 수 있는 위치를 필요한 경우가 많습니다. ADO (함께에서 [OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)) 개발자는 빈을 작성할 수 있습니다 **레코드 집합** 열 정보를 지정 하 고 호출 하 여 개체 **열**. 다음 예제에서는 세 개의 새로운 필드를 새 추가 됩니다 **레코드 집합** 개체입니다. 그런 다음 **레코드 집합** 를 열면 두 개의 새 레코드를 추가 하 고 **레코드 집합** 파일에 저장 합니다. (에 대 한 자세한 내용은 **레코드 집합** 지 속성 참조 [업데이트 및 데이터 유지](../../../ado/guide/data/updating-and-persisting-data.md).)  
  
```  
'BeginFabricate  
    Dim objRs As ADODB.Recordset  
    Set objRs = New ADODB.Recordset  
  
    With objRs.Fields  
        .Append "StudentID", adChar, 11, adFldUpdatable  
        .Append "FullName", adVarChar, 50, adFldUpdatable  
        .Append "PhoneNmbr", adVarChar, 20, adFldUpdatable  
    End With  
  
    With objRs  
        .Open  
  
        .AddNew  
        .Fields(0) = "123-45-6789"  
        .Fields(1) = "John Doe"  
        .Fields(2) = "(425) 555-5555"  
        .Update  
  
        .AddNew  
        .Fields(0) = "123-45-6780"  
        .Fields(1) = "Jane Doe"  
        .Fields(2) = "(615) 555-1212"  
        .Update  
    End With  
  
    objRs.Save App.Path & "FabriTest.adtg", adPersistADTG  
  
    objRs.Close  
'EndFabricate  
```  
  
 용도 **필드 추가** 메서드 간에 다릅니다는 **레코드 집합** 개체 및 **레코드** 개체입니다. 에 대 한 자세한 내용은 **레코드** 개체, 참조 [레코드 및 스트림](../../../ado/guide/data/records-and-streams.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [계층적 레코드 집합 구성](../../../ado/guide/data/fabricating-hierarchical-recordsets.md)


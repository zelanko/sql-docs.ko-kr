---
title: 필드 컬렉션 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Field object [ADO], fields collection
- Fields collection [ADO]
ms.assetid: 574cf36e-e5f5-403b-983c-749ef93c108f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4bd852423ed285165b4d699b391807b9a748f9b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730681"
---
# <a name="the-fields-collection"></a>필드 컬렉션
합니다 **필드** 컬렉션 ADO의 내장 컬렉션 중 하나입니다. 컬렉션은 하나의 단위로 참조할 수 있는 항목의 정렬된 된 집합입니다. ADO 컬렉션에 대 한 자세한 내용은 참조 하세요. [ADO 개체 모델](../../../ado/guide/data/ado-objects-and-collections.md)합니다.  
  
 **필드** 컬렉션에 포함을 **필드** 에서 모든 필드 (열)에 대 한 개체를 **레코드 집합**합니다. 에 모든 ADO 컬렉션과 같은 **개수** 하 고 **항목** 속성 뿐만 **추가** 및 **새로 고침** 메서드. 또한 **CancelUpdate**, **삭제**, **재 동기화**, 및 **업데이트** 다른 ADO 컬렉션에 사용할 수 없는 메서드.  
  
## <a name="examining-the-fields-collection"></a>필드 컬렉션을 검사합니다.  
 고려 합니다 **필드** 샘플의 컬렉션 **레코드 집합** 이 섹션에서 소개 합니다. 샘플 **레코드 집합** SQL 문을에서 파생 된  
  
```  
SELECT ProductID, ProductName, UnitPrice FROM Products WHERE CategoryID = 7  
```  
  
 따라서 찾아야 하는 **레코드 집합 필드** 컬렉션에는 세 개의 필드가 있습니다.  
  
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
  
 이 코드는 단순히 수가 결정 **필드** 개체를 **필드** 사용 하 여 컬렉션을 **개수** 속성과 값을 반환 하는 컬렉션을 반복 합니다 **이름을** 각각에 대 한 속성 **필드** 개체입니다. 더 많은 사용할 수 있습니다 **필드** 속성 필드에 대 한 정보를 가져오려고 합니다. 쿼리에 대 한 자세한 정보에 대 한는 **필드**를 참조 하세요 [Field 개체](../../../ado/guide/data/the-field-object.md)합니다.  
  
## <a name="counting-columns"></a>계산 열  
 예상할 수 있듯이 합니다 **개수** 속성의 실제 수를 반환 합니다. **필드** 개체를 **필드** 컬렉션입니다. 컬렉션의 멤버에 대 한 번호는 0부터 시작, 때문에 항상 0 멤버를 사용 하 여 시작 및 끝 값을 사용 하 여 루프를 코딩 해야 합니다 **개수** 에서 1 뺀 속성이 있습니다. Microsoft Visual Basic을 사용 하는 검사 하지 않고 컬렉션의 멤버를 반복 하는 경우는 **개수** 속성을 사용 하 여는 **각각에 대해... 다음** 명령입니다.  
  
 경우는 **개수** 속성이 0 이면 컬렉션에 개체가 없습니다.  
  
## <a name="getting-to-the-field"></a>필드 가져오기  
 임의의 ADO 컬렉션을 **항목** 속성은 컬렉션의 기본 속성입니다. 개별 반환 **필드** 이름으로 지정 된 개체 또는 전달 하는 인덱스입니다. 따라서 다음 문은 동일 샘플용 **레코드 집합**:  
  
```  
objField = objRecordset.Fields.Item("ProductID")  
objField = objRecordset.Fields("ProductID")  
objField = objRecordset.Fields.Item(0)  
objField = objRecordset.Fields(0)  
```  
  
 이러한 메서드에 해당 하는 경우 가장은 무엇입니까? 그것은 사정 나름이에요. 인덱스를 사용 하 여 검색을 **필드** 컬렉션에서 이므로 더 빠르게 액세스 합니다 **필드** 문자열 조회를 수행 하지 않고 직접. 반면, 순서 **필드** 컬렉션 내에서 알 수 있어야 합니다 경우 순서 변경에 대 한 참조를 **필드의** 인덱스 변경 될 때마다 해야 합니다. 조금 더 느리지만 있지만 이름을 사용 하는 **필드** 의 순서에 영향을 받지 않으므로 보다 유연 합니다 **필드** 컬렉션에서.  
  
## <a name="using-the-refresh-method"></a>Refresh 메서드를 사용 하 여  
 일부 다른 ADO 사용 하 여 컬렉션 달리 합니다 **새로 고침** 메서드를 **필드** 컬렉션이 가시적 효과가 없습니다. 변경 내용을 기본 데이터베이스 구조에서를 검색 하려면 하나를 사용 해야 합니다 **Requery** 메서드를 또는 경우에는 **레코드 집합** 개체에 책갈피를 지원 하지 않습니다는 **MoveFirst**공급자에 대해 다시 실행 하는 명령을 그러면 메서드.  
  
## <a name="adding-fields-to-a-recordset"></a>레코드 집합에 필드 추가  
 **Append** 메서드를 사용 하기 위한 필드 추가 **레코드 집합**합니다.  
  
 사용할 수는 **추가** 메서드를 작성 하는 **레코드 집합** 데이터 원본에 대 한 연결을 열지 않고 프로그래밍 방식으로. 경우 런타임 오류가 발생 합니다 **추가** 메서드를 호출 합니다 **필드** 개방적이 고 컬렉션 **레코드 집합** 또는 **레코드 집합** 여기서는 **ActiveConnection** 속성이 설정 되어 있습니다. 필드에만 추가할 수 있습니다는 **레코드 집합** 열려 있지 않으면을 데이터 원본에 아직 연결 되지 않은 합니다. 그러나 새로 추가 된 값을 지정할 **필드**의 **레코드 집합** 먼저 열어야 합니다.  
  
 개발자는 종종 사용자 인터페이스의 데이터 바인딩에 참여할 수 있도록 하는 서버에서 보낸 것 처럼 작동 하도록 몇 가지 데이터 나 일시적으로 일부 데이터를 저장할 수 있는 위치를 해야 합니다. ADO (함께에서 합니다 [OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)) 빈 빌드하려면 개발자 **레코드 집합** 열 정보를 지정 하 고 호출 하 여 개체 **엽니다**. 다음 예제에서는 세 개의 새 필드가 새 추가 됩니다 **레코드 집합** 개체입니다. 그런 다음 **레코드 집합** 를 열면 두 개의 새 레코드를 추가 및 **레코드 집합** 파일에 저장 됩니다. (에 대 한 자세한 내용은 **Recordset** 지 속성 참조 [업데이트 및 데이터 유지](../../../ado/guide/data/updating-and-persisting-data.md).)  
  
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
  
 사용 합니다 **필드 추가** 메서드 간에 다릅니다 합니다 **레코드 집합** 개체 및 **레코드** 개체. 에 대 한 자세한 내용은 합니다 **레코드** 개체를 참조 하십시오 [레코드 및 스트림](../../../ado/guide/data/records-and-streams.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [계층적 레코드 집합 구성](../../../ado/guide/data/fabricating-hierarchical-recordsets.md)

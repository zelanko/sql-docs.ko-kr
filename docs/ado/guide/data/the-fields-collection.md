---
description: 필드 컬렉션
title: Fields 컬렉션 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 580ded2e3f2539d484d2a60c85adca56ac8e3ac1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452755"
---
# <a name="the-fields-collection"></a>필드 컬렉션
**Fields** 컬렉션은 ADO의 내장 컬렉션 중 하나입니다. 컬렉션은 하나의 단위로 참조할 수 있는 정렬 된 항목 집합입니다. ADO 컬렉션에 대 한 자세한 내용은 [Ado 개체 모델](../../../ado/guide/data/ado-objects-and-collections.md)을 참조 하세요.  
  
 **Fields** 컬렉션에는 **레코드 집합**의 모든 필드 (열)에 대 한 **field** 개체가 포함 되어 있습니다. 모든 ADO 컬렉션과 마찬가지로, **추가** 및 **새로 고침** 메서드와 **개수** 및 **항목** 속성이 있습니다. 또한 다른 ADO 컬렉션에서 사용할 수 없는 **CancelUpdate**, **Delete**, **Resync**및 **Update** 메서드도 있습니다.  
  
## <a name="examining-the-fields-collection"></a>Fields 컬렉션 검사  
 이 섹션에 소개 된 예제 **레코드 집합** 의 **Fields** 컬렉션을 고려 합니다. 샘플 **레코드 집합** 은 SQL 문에서 파생 되었습니다.  
  
```  
SELECT ProductID, ProductName, UnitPrice FROM Products WHERE CategoryID = 7  
```  
  
 따라서 **레코드 집합 필드** 컬렉션에 세 개의 필드가 포함 되어 있는 것을 확인할 수 있습니다.  
  
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
  
 이 코드는 **Count** 속성을 사용 하 여 **Fields** 컬렉션의 **필드** 개체 수를 확인 하 고 컬렉션 전체를 반복 하 여 각 **필드** 개체의 **이름** 속성 값을 반환 합니다. 더 많은 **필드** 속성을 사용 하 여 필드에 대 한 정보를 가져올 수 있습니다. **필드**를 쿼리 하는 방법에 대 한 자세한 내용은 [field 개체](../../../ado/guide/data/the-field-object.md)를 참조 하세요.  
  
## <a name="counting-columns"></a>열 계산  
 짐작할 수 있듯이 **Count** 속성은 **Fields** 컬렉션에 있는 **필드** 개체의 실제 수를 반환 합니다. 컬렉션 멤버의 번호는 0으로 시작 하므로 항상 0 멤버부터 시작 하 여 **Count** 속성 값에서 1을 뺀 값으로 끝나는 루프를 코딩 해야 합니다. Microsoft Visual Basic를 사용 하 고 **Count** 속성을 확인 하지 않고 컬렉션의 멤버를 반복 하려는 경우 **for Each ...를 사용 하 여 다음** 명령입니다.  
  
 **Count** 속성이 0 이면 컬렉션에 개체가 없습니다.  
  
## <a name="getting-to-the-field"></a>필드를 가져오는 중  
 모든 ADO 컬렉션과 마찬가지로 **Item** 속성은 컬렉션의 기본 속성입니다. 전달 된 이름이 나 인덱스에 의해 지정 된 개별 **필드** 개체를 반환 합니다. 따라서 다음 문은 샘플 **레코드 집합**에 대해 동일 합니다.  
  
```  
objField = objRecordset.Fields.Item("ProductID")  
objField = objRecordset.Fields("ProductID")  
objField = objRecordset.Fields.Item(0)  
objField = objRecordset.Fields(0)  
```  
  
 이러한 방법이 가장 적합 한 것은 무엇 인가요? 경우에 따라 다릅니다. 인덱스를 사용 하 여 컬렉션에서 **필드** 를 검색 하는 것은 문자열 조회를 수행 하지 않고 **필드** 에 직접 액세스 하기 때문에 더 빠릅니다. 반면, 컬렉션 내의 **필드** 순서를 알고 있어야 하며, 순서가 변경 되는 경우 **필드의** 인덱스에 대 한 참조는 발생 될 때마다 변경 해야 합니다. **필드** 의 이름을 사용 하는 경우에는 컬렉션에 있는 **필드** 의 순서에 따라 달라 지기 때문에 더 유연 하 게 사용할 수 있습니다.  
  
## <a name="using-the-refresh-method"></a>Refresh 메서드 사용  
 다른 ADO 컬렉션과 달리 **Refresh** 메서드를 **Fields** 컬렉션에 사용 하면 아무런 효과가 없습니다. 기본 데이터베이스 구조에서 변경 내용을 검색 하려면 **Requery** 메서드를 사용 하거나, **레코드 집합** 개체가 책갈피를 지원 하지 않는 경우 ( **MoveFirst** 메서드)를 사용 하 여 공급자에 대해 명령을 다시 실행 해야 합니다.  
  
## <a name="adding-fields-to-a-recordset"></a>레코드 집합에 필드 추가  
 **Append** 메서드는 **레코드 집합**에 필드를 추가 하는 데 사용 됩니다.  
  
 **Append** 메서드를 사용 하 여 데이터 원본에 대 한 연결을 열지 않고도 프로그래밍 방식으로 **레코드 집합** 을 만들 수 있습니다. 열린 **레코드 집합** 또는 **ActiveConnection** 속성이 설정 된 **레코드 집합** 의 **Fields** 컬렉션에 대해 **Append** 메서드를 호출 하면 런타임 오류가 발생 합니다. 열려 있지 않고 데이터 원본에 아직 연결 되지 않은 **레코드 집합** 에만 필드를 추가할 수 있습니다. 그러나 새로 추가 된 **필드**의 값을 지정 하려면 먼저 **레코드 집합** 을 열어야 합니다.  
  
 개발자는 일부 데이터를 임시로 저장 하거나 일부 데이터가 서버에서 가져온 것 처럼 작동 하 여 사용자 인터페이스의 데이터 바인딩에 참여할 수 있게 하려는 경우가 종종 있습니다. ADO ( [OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)와 함께)를 사용 하면 개발자는 열 정보를 지정 하 고 **Open**을 호출 하 여 빈 **레코드 집합** 개체를 작성할 수 있습니다. 다음 예에서는 새 **레코드 집합** 개체에 3 개의 새 필드가 추가 됩니다. 그런 다음 **레코드 집합** 을 열고, 두 개의 새 레코드를 추가 하 고, **레코드 집합** 을 파일에 저장 합니다. **레코드 집합** 지 속성에 대 한 자세한 내용은 [데이터 업데이트 및 유지](../../../ado/guide/data/updating-and-persisting-data.md)를 참조 하세요.  
  
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
  
 **필드 추가** 메서드를 사용 하는 것은 **레코드 집합** 개체와 **Record** 개체 간에 다릅니다. **Record** 개체에 대 한 자세한 내용은 [레코드 및 스트림](../../../ado/guide/data/records-and-streams.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [계층적 레코드 집합 구성](../../../ado/guide/data/fabricating-hierarchical-recordsets.md)

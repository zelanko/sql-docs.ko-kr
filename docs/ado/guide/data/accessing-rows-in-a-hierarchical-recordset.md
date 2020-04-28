---
title: 계층적 레코드 집합의 행에 액세스 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e73b2ca96cc5e7eb7683b72aa19fd59a318b8596
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926351"
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>계층적 레코드 집합의 행 액세스 (예제)
다음 예에서는 계층적 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)의 행에 액세스 하는 데 필요한 단계를 보여 줍니다.

1.  **작성자 및** **은** 테이블의 **레코드 집합** 개체는 author ID로 연결 됩니다.

2.  외부 루프에는 각 저자의 성과 이름, 상태 및 식별이 표시 됩니다.

3.  각 행에 대해 추가 된 **레코드 집합** 은 [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에서 검색 되 고 *rstTitleAuthor*에 할당 됩니다.

4.  내부 루프는 추가 된 **레코드 집합**의 각 행에서 4 개의 필드를 표시 합니다.

 [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) 속성은 설명을 위해 **false** 로 설정 되므로 외부 루프의 각 반복에서 챕터 변경을 명시적으로 확인할 수 있습니다. 코드 예제를 보다 효율적으로 만들기 위해 2 단계에서 첫 번째 줄 앞의 3 단계에서 할당을 이동 하 여 할당이 한 번만 수행 되도록 할 수 있습니다. 그런 다음 [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) 속성을 **true**로 설정 하 여 *rst* 가 새 행으로 이동할 때마다 *rstTitleAuthor* 가 암시적으로 해당 챕터로 자동 변경 되도록 합니다.

## <a name="example"></a>예제

```
Sub datashape()
   Dim cnn As New ADODB.Connection
   Dim rst As New ADODB.Recordset
   Dim rstTitleAuthor As New ADODB.Recordset

   cnn.Provider = "MSDataShape"
   cnn.Open    "Data Provider=MSDASQL;" & _
               "Data Source=SRV;Integrated Security=SSPI;Database=Pubs"
' STEP 1
   rst.StayInSync = FALSE
   rst.Open    "SHAPE  {select * from authors} "  & _
               "APPEND ({select * from titleauthor} " & _
               "RELATE au_id TO au_id) AS chapTitleAuthor", _
               cnn
' STEP 2
   While Not rst.EOF
      Debug.Print    rst("au_fname"), rst("au_lname"), _
                     rst("state"), rst("au_id")
' STEP 3
      Set rstTitleAuthor = rst("chapTitleAuthor").Value
' STEP 4
      While Not rstTitleAuthor.EOF
         Debug.Print rstTitleAuthor(0), rstTitleAuthor(1), _
                     rstTitleAuthor(2), rstTitleAuthor(3)
         rstTitleAuthor.MoveNext
      Wend
      rst.MoveNext
   Wend
End Sub
```

## <a name="see-also"></a>참고 항목
 [데이터 셰이핑 개요](../../../ado/guide/data/data-shaping-overview.md) [필드 개체](../../../ado/reference/ado-api/field-object.md) [필드 컬렉션 (ado)](../../../ado/reference/ado-api/fields-collection-ado.md) [공식 셰이프 문법](../../../ado/guide/data/formal-shape-grammar.md) [OLE DB 용 Microsoft 데이터 셰이핑 서비스 (ado 서비스 공급자)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [레코드 집합 개체 (ado)](../../../ado/reference/ado-api/recordset-object-ado.md) [필요한 공급자 데이터 셰이핑](../../../ado/guide/data/required-providers-for-data-shaping.md) [셰이프 추가 절](../../../ado/guide/data/shape-append-clause.md) [셰이프 명령](../../../ado/guide/data/shape-commands-in-general.md) [Shape COMPUTE Clause](../../../ado/guide/data/shape-compute-clause.md) [Visual Basic for Applications 함수](../../../ado/guide/data/visual-basic-for-applications-functions.md)

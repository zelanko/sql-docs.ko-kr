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
manager: craigg
ms.openlocfilehash: 83b8334b4891d0b12cac59030ebf7fced871c5dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63294357"
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>계층적 레코드 집합 (예:)의 행에 액세스
다음 예제에서는 단계 액세스 행 하는 데 필요한을 계층적 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md):

1.  **레코드 집합** 에서 개체를 **작성자** 하 고 **titleauthor** 작성자 id와 관련 된 테이블

2.  외부 루프는 각 저자의 성 및 이름, 상태 및 식별을 표시합니다.

3.  추가 된 **레코드 집합** 에서 각 행이 검색에 대 한 합니다 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에 할당 *rstTitleAuthor*합니다.

4.  에 추가 된 각 행에서 4 개의 필드를 표시 하는 내부 루프 **레코드 집합**합니다.

 합니다 [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) 속성이로 설정 된 **false** 설명을 위해 볼 수 있도록 장의 변경 내용을 명시적으로 바깥쪽 루프의 각 반복 합니다. 코드 예제에서는 보다 효율적인 할당 한 번만 수행 됩니다 있도록 2 단계에서 첫 번째 줄 전에 3 단계에서 할당을 이동할 수 있습니다. 설정한 합니다 [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) 속성을 **true**되도록 *rstTitleAuthor* 자동으로 암시적으로 바뀌어 해당 장 때마다 *rst* 새 행으로 이동 합니다.

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

## <a name="see-also"></a>관련 항목
 [데이터 셰이핑 개요](../../../ado/guide/data/data-shaping-overview.md) [개체를 필드](../../../ado/reference/ado-api/field-object.md) [컬렉션 (ADO)를 필드](../../../ado/reference/ado-api/fields-collection-ado.md) [공식적인 셰이프 문법](../../../ado/guide/data/formal-shape-grammar.md) [Microsoft 데이터 셰이핑 OLE DB에 대 한 서비스 (ADO 서비스 공급자) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [데이터 셰이프에 필요한 공급자](../../../ado/guide/data/required-providers-for-data-shaping.md) [셰이프 APPEND 절](../../../ado/guide/data/shape-append-clause.md) [명령에서 셰이프 일반적인](../../../ado/guide/data/shape-commands-in-general.md) [셰이프 COMPUTE 절](../../../ado/guide/data/shape-compute-clause.md) [Visual Basic for Applications 기능](../../../ado/guide/data/visual-basic-for-applications-functions.md)

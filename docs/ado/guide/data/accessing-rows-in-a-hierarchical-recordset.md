---
title: 계층적 레코드 집합의 행에 액세스 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b1b387eaa01a3a3d71c51172becf196ec6474ea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>계층적 레코드 집합 (예:)의 행에 액세스
다음 예제에서는 단계 행 하는 데 필요한을 계층적 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md):

1.  **레코드 집합** 에서 개체는 **작성자** 및 **titleauthor** 작성자 id 관련 된 테이블

2.  외부 루프에는 각 저자의 성과 이름, 상태 및 식별 표시 됩니다.

3.  추가 된 **레코드 집합** 에서 각 행이 검색에 대 한는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에 할당 된 *rstTitleAuthor*합니다.

4.  에 추가 된 각 행에서 4 개의 필드를 표시 하는 안쪽 루프 **레코드 집합**합니다.

 [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) 속성이 **false** 설명을 위해 볼 수 있도록 장 변경 내용을 명시적으로 외부 루프의 각 반복 합니다. 코드 예제를 보다 효율적으로 만들 할당은 한 번만 수행 있도록 2 단계에서 첫 번째 줄 앞 3 단계에서 할당을 이동할 수 있습니다. 다음 설정의 [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) 속성을 **true**있도록 *rstTitleAuthor* 됩니다 암시적으로 자동으로 변경 및 해당 장 때마다 *rst* 새 행으로 이동 합니다.

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

## <a name="see-also"></a>관련 항목:
 [데이터 개요 셰이핑](../../../ado/guide/data/data-shaping-overview.md) [개체 필드](../../../ado/reference/ado-api/field-object.md) [필드 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md) [정식 문법을](../../../ado/guide/data/formal-shape-grammar.md) [Microsoft 데이터를 셰이핑 OLE DB에 대 한 서비스 (ADO 서비스 공급자) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [(ADO) 레코드 집합 개체](../../../ado/reference/ado-api/recordset-object-ado.md) [데이터 모양 지정에 필요한 공급자](../../../ado/guide/data/required-providers-for-data-shaping.md) [APPEND 절 셰이프](../../../ado/guide/data/shape-append-clause.md) [명령에서 셰이프 일반](../../../ado/guide/data/shape-commands-in-general.md) [Shape COMPUTE 절](../../../ado/guide/data/shape-compute-clause.md) [응용 프로그램 기능에 대 한 Visual Basic](../../../ado/guide/data/visual-basic-for-applications-functions.md)

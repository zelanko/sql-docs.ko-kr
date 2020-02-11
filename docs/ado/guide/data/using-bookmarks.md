---
title: 책갈피 사용 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- bookmarks [ADO]
- Recordset object [ADO]
ms.assetid: cca244e6-84f8-4394-bca9-f7a819b8f4df
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9fa2a738a3e94cd306619a318b75a2fd506972c8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923600"
---
# <a name="using-bookmarks"></a>책갈피 사용
모든 레코드를 스크롤하고 값을 비교할 필요 없이 **레코드 집합** 에서 이동한 후 특정 레코드로 직접 반환 하는 것이 유용한 경우가 많습니다. 예를 들어 **Find** 메서드를 사용 하 여 레코드를 검색 하려고 하지만 검색에서 레코드를 반환 하지 않는 경우에는 레코드 **집합**의 한쪽 끝에 자동으로 배치 됩니다. 공급자가 지 원하는 경우 사용자의 위치로 돌아갈 수 있도록 책갈피를 사용 하 여 **찾기** 방법을 사용 하기 전에 위치를 표시할 수 있습니다. 책갈피는 레코드 **집합** 개체의 레코드를 고유 하 게 식별 하는 **Variant** 형식 값입니다.  
  
 **레코드 집합 필터** 메서드와 함께 책갈피의 변형 배열을 사용 하 여 선택한 레코드 집합을 필터링 할 수도 있습니다. 이 기술에 대 한 자세한 내용은이 섹션의 뒷부분에 나오는 [레코드 집합 작업](../../../ado/guide/data/working-with-recordsets.md)항목에서 결과 필터링을 참조 하세요.  
  
 **책갈피** 속성을 사용 하 여 레코드에 대 한 책갈피를 가져오거나, 레코드 **집합** 개체의 현재 레코드를 유효한 책갈피에 의해 식별 되는 레코드로 설정할 수 있습니다. 다음 코드에서는 **bookmark** 속성을 사용 하 여 책갈피를 설정한 다음 다른 레코드로 이동한 후 책갈피가 설정 된 레코드로 돌아갑니다. **레코드 집합** 에서 책갈피를 지원 하는지 확인 하려면 **지원** 메서드를 사용 합니다.  
  
```  
'BeginBookmarkEg  
Dim varBookmark As Variant  
Dim blnCanBkmrk As Boolean  
  
objRs.Open strSQL, strConnStr, adOpenStatic, adLockOptimistic, adCmdText  
  
If objRs.RecordCount > 4 Then  
    objRs.Move 4                       ' move to the fifth record  
    blnCanBkmrk = objRs.Supports(adBookmark)  
    If blnCanBkmrk = True Then  
        varBookmark = objRs.Bookmark   ' record the bookmark  
        objRs.MoveLast                 ' move to a different record  
        objRs.Bookmark = varBookmark   ' return to the bookmarked (sixth) record  
    End If  
End If  
'EndBookmarkEg  
```  
  
 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드는 나중에 자세히 설명 합니다.  
  
 복제 된 **레코드 집합**의 경우를 제외 하 고 책갈피는 동일한 명령을 사용 하는 경우에도 생성 된 **레코드 집합** 에 대해 고유 합니다. 즉, 한 **레코드 집합** 에서 가져온 **책갈피** 를 사용 하 여 동일한 명령을 사용 하 여 연 두 번째 **레코드 집합** 의 동일한 레코드로 이동할 수 없습니다.

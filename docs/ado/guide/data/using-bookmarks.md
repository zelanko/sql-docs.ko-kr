---
title: "책갈피를 사용 하 여 | Microsoft Docs"
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
- bookmarks [ADO]
- Recordset object [ADO]
ms.assetid: cca244e6-84f8-4394-bca9-f7a819b8f4df
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0fe945bfb5a0b2460090ccc8376543364693a1de
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-bookmarks"></a>책갈피 사용
이동 하다가 특정 레코드에 직접 반환할 유용는 **레코드 집합** 모든 레코드를 스크롤하여 이동 하며 값을 비교할 필요 없이 합니다. 예를 들어, 사용 하 여 레코드를 검색 하려고 하면는 **찾을** 메서드 하지만 검색 레코드가 반환의 한쪽 끝에서 자동으로 배치 됩니다는 **레코드 집합**합니다. 위치를 표시 한 사용 하기 전에 책갈피를 사용할 수 공급자가 지 원하는, 경우는 **찾을** 메서드를 통해 위치를 반환할 수 있도록 합니다. 책갈피는는 **Variant** 의 레코드를 고유 하 게 식별 하는 값을 입력 한 **레코드 집합** 개체입니다.  
  
 책갈피와이 인수를 사용할 수도 있습니다는 **레코드 집합 필터** 메서드 선택된 된 레코드 집합에 필터를 적용 합니다. 이 방법에 대 한 자세한 참조 항목에 대 한 결과 필터링 [레코드 집합으로 작업할](../../../ado/guide/data/working-with-recordsets.md)이 섹션의 뒷부분에 나오는 합니다.  
  
 사용할 수 있습니다는 **책갈피** 레코드에 대 한 책갈피를 가져오거나 현재 레코드 설정할 속성을 **레코드 집합** 유효한 책갈피로 식별 되는 레코드에는 개체입니다. 다음 코드에서는 **책갈피** 속성 책갈피를 설정 하 고 다음 다른 레코드로 이동 후 책갈피가 표시 된 레코드를 반환 합니다. 여부를 확인 하 여 **레코드 집합** 책갈피를 사용 하 여를 지 원하는 **지원** 메서드.  
  
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
  
 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드 자세히 나중에 설명 됩니다.  
  
 경우를 제외 하 고 복제 된 **레코드 집합**, 책갈피는에 고유 하며는 **레코드 집합** 에 생성 된, 동일한 명령을 사용 하는 경우에 합니다. 즉, 사용할 수 없습니다는 **책갈피** 하나에서 가져온 **레코드 집합** 1 초 동안에서 동일한 레코드로 이동 하려면 **레코드 집합** 동일한 명령으로 연 합니다.


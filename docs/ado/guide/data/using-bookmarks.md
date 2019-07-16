---
title: 책갈피를 사용 하 여 | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923600"
---
# <a name="using-bookmarks"></a>책갈피 사용
이동 하다가 특정 레코드에 직접 반환할 유용 합니다 **레코드 집합** 모든 레코드를 스크롤하고 값을 비교 하지 않고도 합니다. 예를 들어, 사용 하 여 레코드를 검색 하려는 경우는 **찾을** 메서드이지만 검색 레코드가 반환, 양쪽 끝에 자동으로 배치 됩니다 합니다 **레코드 집합**합니다. 공급자가 지 원하는, 경우 책갈피를 사용 하기 전에 사용자의 위치를 표시 하려면 사용할 수 있습니다 합니다 **찾을** 메서드 위치로 반환할 수 있습니다. 책갈피는를 **Variant** 의 레코드를 고유 하 게 식별 하는 값을 입력 한 **레코드 집합** 개체입니다.  
  
 책갈피를 사용 하 여이 인수를 사용할 수도 있습니다는 **레코드 집합 필터** 선택한 레코드 집합을 필터링 하는 방법입니다. 이 기술에 대 한 자세한 내용은 참조 항목에서 결과 필터링 [레코드 집합으로 작업할](../../../ado/guide/data/working-with-recordsets.md)이 섹션의 뒷부분에 나오는.  
  
 사용할 수는 **책갈피** 레코드에 대 한 책갈피를 가져오거나 현재 레코드 설정 하는 속성을 **레코드 집합** 유효한 책갈피에서 식별 되는 레코드 개체. 다음 코드에서는 합니다 **책갈피** 속성을 책갈피를 설정 하 고 다른 레코드로 이동 후 책갈피가 표시 된 레코드를 반환 합니다. 여부를 확인 하 여 **레코드 집합** 책갈피를 사용 하 여 지원 합니다 **지원** 메서드.  
  
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
  
 합니다 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드는 나중에 설명 자세히입니다.  
  
 경우를 제외 하 고 복제 **레코드 집합**, 책갈피는 고유한 합니다 **레코드 집합** 에 생성 된 동일한 명령을 사용 하는 경우에 합니다. 이 사용할 수 없다는 의미는 **책갈피** 하나에서 가져온 **레코드 집합** 초에서 같은 레코드를 이동 하려면 **레코드 집합** 동일한 명령을 사용 하 여 열.

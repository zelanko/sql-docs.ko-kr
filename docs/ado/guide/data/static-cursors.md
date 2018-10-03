---
title: 정적 커서 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], static
- static cursors [ADO]
ms.assetid: cce93ace-c4ed-4c6c-940c-28a50ff2fd12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e8815522ee4f9a4221887696a23a201910d7cfad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654191"
---
# <a name="static-cursors"></a>정적 커서
정적 커서는 결과 집합 커서를 처음 연 경우 처럼 항상 표시 합니다. 구현에 따라 정적 커서는 읽기 전용 또는 읽기/쓰기 및 앞으로 및 뒤로 스크롤을 제공 합니다. 정적 커서는 멤버 자격, 순서 또는 커서가 열린 후에 결과 집합의 값에 대 한 변경 내용을 일반적으로 검색 하지 않습니다. 이렇게 하려면 필요 하지는 않지만 정적 커서는 자체 업데이트, 삭제 및 삽입을 검색할 수 있습니다.  
  
 정적 커서는 업데이트, 삭제 및 삽입 하는 다른 검색 하지 않습니다. 예를 들어 정적 커서를 행 및 다른 응용 프로그램을 가져오는 다음 해당 행을 업데이트 합니다. 응용 프로그램에는 정적 커서에서 행을 다시, 경우에 발견 하는 값을 다른 응용 프로그램에서 변경한 내용을 불구 하 고 변경 되지 않습니다. 스크롤 하는 모든 유형의 지원 되지만 공급자 수 또는 책갈피를 지원 하지 않을 수 있습니다.  
  
 응용 프로그램 데이터를 변경 하며 스크롤을 검색할 필요가 없습니다, 하는 경우 정적 커서는 것이 가장 좋습니다. 사용 하 여는 **adOpenStatic CursorTypeEnum** ado에서 정적 커서를 사용 하려는 나타냅니다.  
  
## <a name="see-also"></a>관련 항목  
 [정방향 전용 커서](../../../ado/guide/data/forward-only-cursors.md)   
 [키 집합 커서](../../../ado/guide/data/keyset-cursors.md)   
 [동적 커서](../../../ado/guide/data/dynamic-cursors.md)

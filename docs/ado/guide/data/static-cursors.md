---
description: 정적 커서
title: 정적 커서 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], static
- static cursors [ADO]
ms.assetid: cce93ace-c4ed-4c6c-940c-28a50ff2fd12
author: rothja
ms.author: jroth
ms.openlocfilehash: 65ca384d89c4afbeeb24120debfd2ead5c2716ed
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979554"
---
# <a name="static-cursors"></a>정적 커서
정적 커서는 항상 커서를 처음 열 때의 결과 집합을 표시 합니다. 구현에 따라 정적 커서는 읽기 전용 또는 읽기/쓰기 이며 앞으로 및 뒤로 스크롤을 제공 합니다. 정적 커서는 일반적으로 커서를 연 후 결과 집합의 멤버 자격, 순서 또는 값에 대 한 변경 내용을 검색 하지 않습니다. 정적 커서는 자체 업데이트, 삭제 및 삽입을 검색할 수 있지만 필수 사항은 아닙니다.  
  
 정적 커서는 다른 업데이트, 삭제 및 삽입을 검색 하지 않습니다. 예를 들어 정적 커서가 행을 페치하고 다른 애플리케이션이 해당 행을 업데이트한다고 가정합니다. 애플리케이션이 정적 커서에서 행을 다시 페치하면 다른 애플리케이션에서 변경한 내용에도 불구하고 표시되는 값은 변경되지 않습니다. 모든 스크롤 형식이 지원 되지만 공급자는 책갈피를 지원 하거나 지원 하지 않을 수 있습니다.  
  
 응용 프로그램에서 데이터 변경 내용을 검색할 필요가 없고 스크롤이 필요한 경우 정적 커서를 선택 하는 것이 가장 좋습니다. **Adopenstatic CursorTypeEnum** 를 사용 하 여 ADO에서 정적 커서를 사용 하 고 있음을 나타낼 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [앞 으로만 이동 가능한 커서](../../../ado/guide/data/forward-only-cursors.md)   
 [키 집합 커서](../../../ado/guide/data/keyset-cursors.md)   
 [동적 커서](../../../ado/guide/data/dynamic-cursors.md)

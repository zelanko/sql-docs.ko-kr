---
title: 정방향 전용 커서 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], forward-only
- forward-only cursors [ADO]
ms.assetid: 2b1e062f-3294-4a6f-8241-a17045c4df18
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a309a34d8b5a897c62de6bdceb1db2eef4d46c2
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271482"
---
# <a name="forward-only-cursors"></a>정방향 전용 커서
커서를 앞 으로만 이동 가능한 (또는 스크롤할 수 없는)를 호출 하는 일반적인 기본 커서 유형을 결과 집합 앞 으로만 이동할 수 있습니다. 정방향 전용 커서 (결과 집합에서 앞 이나 뒤로 이동 하는 기능); 스크롤을 지원 하지 않습니다. 결과 집합의 끝에 시작에서의 행 인출만 지원 합니다. 일부 정방향 전용 커서와 함께 (같은 SQL Server 커서 라이브러리와 함께), 모든 insert, update 및 delete 문을 현재 사용자 (또는 다른 사용자가 커밋하여) 행 결과 집합에 영향을 행 인출 될 때 표시 됩니다. 그러나 커서는 뒤로 스크롤할 수 없는, 행 변경 내용을 데이터베이스에 행이 인출 된 후 표시 되지 않습니다 커서를 통해.  
  
 현재 행에 대 한 데이터를 처리 한 후 정방향 전용 커서는 데이터를 저장 하는 데 사용 된 리소스를 해제 합니다. 정방향 전용 커서는 기본적으로 현재 행이 처리 될 때 모든 변경 내용이 발견 동적입니다. 된다는 제공할 수 있으며 결과 기본 테이블에 대 한 업데이트를 표시 하도록 설정 합니다.  
  
 정방향 전용 커서는 뒤로 스크롤을 지원 하지 않습니다, 하는 동안 응용 프로그램으로 커서를 닫았다가 결과 집합의 시작 부분으로 반환할 수 있습니다. 이것이 적은 양의 데이터를 사용 하는 효과적인 방법입니다. 대신 응용 프로그램 수 결과 집합을 한 번 읽고, 로컬로 데이터를 캐시 하 고 로컬 데이터 캐시를 찾습니다.  
  
 응용 프로그램은 결과 집합을 스크롤할 필요가 없으면, 정방향 전용 커서가 최소한의 오버 헤드를 사용 하 여 신속 하 게 데이터를 검색 하는 가장 좋은 방법은 있습니다. 사용 하 여는 **adOpenForwardOnly CursorTypeEnum** ado에서 정방향 전용 커서를 사용 해야 지정할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [정적 커서](../../../ado/guide/data/static-cursors.md)   
 [키 집합 커서](../../../ado/guide/data/keyset-cursors.md)   
 [동적 커서](../../../ado/guide/data/dynamic-cursors.md)

---
description: 정방향 전용 커서
title: 앞 으로만 이동 가능한 커서 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], forward-only
- forward-only cursors [ADO]
ms.assetid: 2b1e062f-3294-4a6f-8241-a17045c4df18
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ccf9d679d158b6f89ef6842b427c315078b99f6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991244"
---
# <a name="forward-only-cursors"></a>정방향 전용 커서
앞 으로만 이동 가능 하거나 스크롤할 수 없는 커서 라고 하는 일반적인 기본 커서 유형은 결과 집합을 통해서만 앞으로 이동할 수 있습니다. 앞 으로만 이동 가능한 커서는 스크롤을 지원 하지 않습니다 (결과 집합에서 앞으로 또는 뒤로 이동 하는 기능). 결과 집합의 처음부터 끝까지 행 인출만 지원 합니다. 일부 전방 전용 커서 (예: SQL Server 커서 라이브러리 사용)를 사용 하 여 결과 집합의 행에 영향을 주는 현재 사용자가 수행한 모든 삽입, 업데이트 및 삭제 문은 행이 인출 될 때 표시 됩니다. 그러나 커서는 뒤로 스크롤할 수 없기 때문에 행이 페치된 후 데이터베이스 행의 변경 내용은 대부분 커서를 통해 볼 수 없습니다.  
  
 현재 행에 대 한 데이터를 처리 한 후에는 해당 데이터를 저장 하는 데 사용 된 리소스를 앞 으로만 이동 하는 커서를 해제 합니다. 정방향 전용 커서는 기본적으로 동적이며, 이는 현재 행이 처리될 때 모든 변경 내용이 감지됨을 의미합니다. 이렇게 하면 커서가 더 빨리 열리고 결과 집합이 기본 테이블에 대한 업데이트를 표시하도록 설정할 수 있습니다.  
  
 전방 전용 커서는 역방향 스크롤을 지원 하지 않지만 커서를 닫았다가 다시 열어 결과 집합의 시작 부분으로 돌아갈 수 있습니다. 이는 소량의 데이터를 사용 하는 효과적인 방법입니다. 또는 응용 프로그램에서 결과 집합을 한 번 읽고 데이터를 로컬로 캐시 한 다음 로컬 데이터 캐시를 찾아볼 수 있습니다.  
  
 응용 프로그램에서 결과 집합을 스크롤하지 않아도 되는 경우에는 앞 으로만 이동 가능한 커서를 사용 하 여 가장 낮은 오버 헤드로 데이터를 빠르게 검색할 수 있습니다. **Adopenforwardonly CursorTypeEnum** 를 사용 하 여 ADO에서 앞 으로만 이동 가능한 커서를 사용 하도록 지정 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [정적 커서](./static-cursors.md)   
 [키 집합 커서](./keyset-cursors.md)   
 [동적 커서](./dynamic-cursors.md)
---
title: "CacheSize를 사용 하 여 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 74ec85c5907485edc5ad8dbcb6c24826fc21ccf3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-cachesize"></a>CacheSize를 사용 하 여
사용 하 여는 **CacheSize** 레코드를 공급자에서 로컬 메모리에 한 번에 가져올 수를 제어 하는 속성입니다. 예를 들어 경우는 **CacheSize** 은 10, 첫 번째 여는 **레코드 집합** 개체 공급자는 로컬 메모리에 처음 10 개의 레코드를 검색 합니다. 이동할 때는 **레코드 집합** 개체 공급자는 로컬 메모리 버퍼에서 데이터를 반환 합니다. 캐시에 있는 마지막 레코드를 지 나 이동 공급자 다음 10 개의 레코드를 캐시에에 데이터 원본에서 검색 합니다.  
  
> [!NOTE]
>  **CacheSize** 기반으로 **최대 열린 행** 공급자별 속성 (에 **속성** 의 컬렉션은 **레코드 집합** 개체). 설정할 수 없습니다. **CacheSize** 보다 큰 값으로 **최대 열린 행 수입니다.** 공급자에서 열 수 있는 행의 수를 수정 하려면 설정 **최대 열린 행**합니다.  
  
 값 **CacheSize** 의 수명 동안 조정 될 수 있습니다는 **레코드 집합** 개체가 아니라이 값을 변경만 영향을 미칩니다 캐시에 있는 레코드 수가 데이터 원본에서 발생 한 후속 검색 후 합니다. 단독 속성 값을 변경 하는 경우에 캐시의 현재 내용을 변경 되지 않습니다.  
  
 검색할 보다 더 적은 레코드 없으면 **CacheSize** 지정 공급자 나머지 레코드를 반환 하 고 오류가 발생 하지 않습니다.  
  
 A **CacheSize** 설정 0는 허용 되지 않으며 오류를 반환 합니다.  
  
 캐시에서 검색 된 레코드는 다른 사용자가 원본 데이터에 동시 변경 내용을 반영 하지 않습니다. 모든 캐시 된 데이터의 업데이트를 적용 하려면 사용 된 [다시 동기화](../../../ado/reference/ado-api/resync-method.md) 메서드.  
  
 경우 **CacheSize** 탐색 방법 1 보다 큰 값으로 설정 됩니다 ([이동](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext 및 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) 이동 하 여 삭제 될 수 있습니다 삭제 된 레코드를 가져온 후 발생 하는 경우 기록 합니다. 초기 인출 후 후속 삭제 반영 되지 않습니다 데이터 캐시에서 삭제 된 행의 데이터 값에 액세스 하려고 합니다. 그러나 설정 **CacheSize** 1에이 문제가 발생 하지 않습니다이 삭제 된 행을 가져올 수 없습니다.


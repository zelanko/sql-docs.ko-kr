---
description: CacheSize 사용
title: CacheSize 사용 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
author: rothja
ms.author: jroth
ms.openlocfilehash: 97f6dba7bf01b3236d6b8b00e6338185cf6a8d41
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979004"
---
# <a name="using-cachesize"></a>CacheSize 사용
**CacheSize** 속성을 사용 하 여 한 번에 공급자의 로컬 메모리로 검색할 레코드 수를 제어 합니다. 예를 들어 **CacheSize** 가 10 이면 먼저 **레코드 집합** 개체를 연 후 공급자는 처음 10 개의 레코드를 로컬 메모리에 검색 합니다. **레코드 집합** 개체를 이동할 때 공급자는 로컬 메모리 버퍼에서 데이터를 반환 합니다. 캐시의 마지막 레코드를 지나서 이동 하는 즉시 공급자는 데이터 원본에서 캐시로 다음 10 개의 레코드를 검색 합니다.  
  
> [!NOTE]
>  **CacheSize** 는 **레코드 집합** 개체의 **Properties** 컬렉션에 있는 **최대 Open Rows** 공급자별 속성을 기반으로 합니다. **CacheSize** 를 **열려 있는 최대 행** 보다 큰 값으로 설정할 수 없습니다. 공급자가 열 수 있는 행 수를 수정 하려면 **열려 있는 최대 행**수를 설정 합니다.  
  
 **CacheSize** 의 값은 **레코드 집합** 개체의 수명 동안 조정 될 수 있지만이 값을 변경 하면 이후 데이터 원본에서 데이터를 검색할 때 캐시에 있는 레코드 수에만 영향을 줍니다. 속성 값만 변경 해도 캐시의 현재 콘텐츠는 변경 되지 않습니다.  
  
 검색할 레코드의 개수가 **CacheSize** 에서 지정 하는 것 보다 적으면 공급자는 나머지 레코드를 반환 하 고 오류는 발생 하지 않습니다.  
  
 **CacheSize** 설정 0은 허용 되지 않으며 오류를 반환 합니다.  
  
 캐시에서 검색 된 레코드는 다른 사용자가 원본 데이터에 대해 수행한 동시 변경 내용을 반영 하지 않습니다. 모든 캐시 된 데이터를 강제로 업데이트 하려면 [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드를 사용 합니다.  
  
 **CacheSize** 가 1 보다 큰 값으로 설정 된 경우 탐색 메서드 ([Move](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext 및 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md))는 레코드가 검색 된 후 삭제가 발생 하면 삭제 된 레코드를 탐색 하 게 될 수 있습니다. 초기 인출 후에는 삭제 된 행에서 데이터 값에 액세스 하려고 할 때까지 후속 삭제가 데이터 캐시에 반영 되지 않습니다. 그러나 **CacheSize** 를 1로 설정 하면 삭제 된 행을 인출할 수 없기 때문에이 문제가 발생 하지 않습니다.

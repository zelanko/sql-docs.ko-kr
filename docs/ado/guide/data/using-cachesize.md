---
title: CacheSize 사용 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c29fb18431d1f02d82db76605a8a53752ea0357
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184901"
---
# <a name="using-cachesize"></a>CacheSize 사용
사용 된 **CacheSize** 공급자에서 로컬 메모리에 한 번에 검색할 레코드 수를 제어 하는 속성입니다. 예를 들어 경우는 **CacheSize** 가 10 이면 처음 연 후 합니다 **레코드 집합** 로컬 메모리로 처음 10 개의 레코드를 검색 하는 공급자 개체입니다. 여기저기로 이동 하면 합니다 **레코드 집합** 개체 공급자는 로컬 메모리 버퍼에서 데이터를 반환 합니다. 캐시에 있는 마지막 레코드를 통과 하는 즉시 캐시로 다음 10 개의 레코드를 데이터 원본에서 검색 공급자입니다.  
  
> [!NOTE]
>  **CacheSize** 기반으로 **최대 열린 행** 공급자별 속성 (에 **속성** 의 컬렉션을 **레코드 집합** 개체). 설정할 수 없습니다 **CacheSize** 보다 큰 값으로 **최대 열린 행 수입니다.** 설정 공급자가 열 수 있는 행의 수를 수정 하려면 **최대 열린 행**합니다.  
  
 변수의 **CacheSize** 의 수명 동안 조정할 수 있습니다 합니다 **레코드 집합** 있으 나이 값을 변경만 영향을 캐시에 있는 레코드 수가 데이터 원본에서 후속 검색 후 합니다. 단독으로 속성 값을 변경 하는 경우에 캐시의 현재 내용을 변경 되지 않습니다.  
  
 검색할 보다 적은 레코드가 없으면 **CacheSize** 공급자 나머지 레코드를 반환 하며 오류가 발생 하지 않습니다 지정 합니다.  
  
 A **CacheSize** 설정으로 0 허용 되지 않으며 오류를 반환 합니다.  
  
 캐시에서 검색 된 레코드에는 다른 사용자에 게 원본 데이터에 대 한 동시 변경 내용을 반영 하지 않습니다. 캐시 된 모든 데이터의 업데이트를 적용 하려면 사용 합니다 [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드.  
  
 하는 경우 **CacheSize** 탐색 방법 1 보다 큰 값으로 설정 됩니다 ([이동](../../../ado/reference/ado-api/move-method-ado.md)를 [MoveFirst, MoveLast, MoveNext 및 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md))를 삭제 하는 탐색 될 수 있습니다 삭제 된 레코드를 가져온 후 발생 하는 경우 기록 합니다. 초기 fetch를 후 후속 삭제 반영 되지 않습니다 데이터 캐시의 삭제 된 행의 데이터 값에 액세스 하려고 할 때 까지는 합니다. 그러나 설정 **CacheSize** 1에이 문제가 발생 하지 않습니다이 삭제 된 행을 인출할 수 없습니다.

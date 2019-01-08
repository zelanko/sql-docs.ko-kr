---
title: 잠금이란? | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], locking
- locks [ADO], about locking
ms.assetid: f8989555-28c6-4c17-9bf8-7f44a8a5c407
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 744ae9a9541b5c73d579e097f375b4141e771fce
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52501761"
---
# <a name="what-is-a-lock"></a>잠금이란?
잠금은 사용 되는 DBMS 다중 사용자 환경에서 행에 액세스를 제한 하는 프로세스입니다. 행 또는 열을 단독으로 잠긴 경우 잠금이 해제 될 때까지 잠긴된 데이터에 액세스 하려면 다른 사용자에 게 허용 되지 않습니다. 이렇게 하면 두 명의 사용자가 행의 동일한 열에 동시에 업데이트 수 없습니다.  
  
 잠금은 리소스의 관점에서 매우 비용이 많이 들 수 및 데이터 무결성을 유지 하기 위해 필요한 경우에 사용할 해야 합니다. 여기서 수백 또는 수천 명의 사용자 수 액세스 하려고 할 수 레코드를 인터넷에 연결 된 데이터베이스와 같은 초 마다-데이터베이스에서 불필요 한 잠금 발생할 수 있습니다 신속 하 게 응용 프로그램에서 성능이 저하.  
  
 어떻게 데이터 원본 및 ADO 커서 라이브러리 관리 동시성 적절 한 잠금 옵션을 선택 하 여 제어할 수 있습니다.  
  
 설정 된 **LockType** 열기 전에 속성을 **레코드 집합** 공급자 잠금 유형을 열 때 사용 하도록 지정 하려면. 개방적이 고 사용 중인 잠금 형식을 반환 하도록 속성을 읽습니다 **레코드 집합** 개체입니다.  
  
 공급자는 모든 잠금 유형을 지원 하지 않습니다. 공급자가 요청한 지원할 수 없습니다 **LockType** 설정을 대체 합니다 다른 잠금 유형입니다. 사용할 수 있는 실제 잠금 기능을 확인 하는 **레코드 집합** 개체를 사용 합니다 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드 **adUpdate** 및 **adUpdateBatch**.  
  
 **adLockPessimistic** 하는 경우 설정은 지원 되지 않습니다는 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성이 **adUseClient 합니다.** 지원 되지 않는 값을 설정 하는 경우 없음 오류가 발생 합니다. 지원 되는 가장 가까운 **LockType** 대신 사용 됩니다.  
  
 **LockType** 속성은 읽기/쓰기 때 합니다 **레코드 집합** 열려 있는 경우에 닫혀 이며 읽기 전용입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [잠금의 유형](../../../ado/guide/data/types-of-locks.md)

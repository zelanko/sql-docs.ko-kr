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
ms.openlocfilehash: c1607c9434e6c30ffd317277aadab27af96868fb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923448"
---
# <a name="what-is-a-lock"></a>잠금이란?
잠금은 DBMS에서 다중 사용자 환경에 있는 행에 대 한 액세스를 제한 하는 프로세스입니다. 행 또는 열이 단독으로 잠겨 있으면 잠금이 해제 될 때까지 다른 사용자가 잠긴 데이터에 액세스할 수 없습니다. 이렇게 하면 두 사용자가 행의 같은 열을 동시에 업데이트할 수 없습니다.  
  
 잠금은 리소스 관점에서 매우 비용이 많이 들 수 있으며 데이터 무결성을 유지 하는 데 필요한 경우에만 사용 해야 합니다. 수백 또는 수천 명의 사용자가 1 초 마다 레코드에 액세스 하려고 할 수 있는 데이터베이스에서 (예: 인터넷에 연결 된 데이터베이스와 불필요 한 잠금) 응용 프로그램의 성능이 저하 될 수 있습니다.  
  
 적절 한 잠금 옵션을 선택 하 여 데이터 원본과 ADO 커서 라이브러리가 동시성을 관리 하는 방법을 제어할 수 있습니다.  
  
 **레코드 집합** 을 열기 전에 **LockType** 속성을 설정 하 여 공급자가 열을 열 때 사용 해야 하는 잠금 유형을 지정 합니다. 열려 있는 **레코드 집합** 개체에서 사용 중인 잠금 유형을 반환 하려면 속성을 읽습니다.  
  
 공급자는 일부 잠금 유형을 지원 하지 않을 수 있습니다. 공급자는 요청한 **LockType** 설정을 지원할 수 없는 경우 다른 잠금 유형으로 대체 합니다. **레코드 집합** 개체에서 사용할 수 있는 실제 잠금 기능을 확인 하려면 **Adupdate** 및 **adupdate**에서 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드를 사용 합니다.  
  
 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성이 adUseClient로 설정 된 경우에는 **adlockpessimistic** 설정이 지원 되지 않습니다 **.** 지원 되지 않는 값이 설정 되 면 오류가 발생 하지 않습니다. 가장 가까운 지원 되는 **LockType** 가 대신 사용 됩니다.  
  
 **LockType** 속성은 **레코드 집합** 을 닫을 때 읽기/쓰기이 고, 열린 경우에는 읽기 전용입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [잠금 형식](../../../ado/guide/data/types-of-locks.md)

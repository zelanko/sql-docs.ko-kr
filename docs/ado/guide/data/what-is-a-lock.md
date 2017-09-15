---
title: "잠금을 이란? | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ADO], locking
- locks [ADO], about locking
ms.assetid: f8989555-28c6-4c17-9bf8-7f44a8a5c407
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f4975dd903c6d012976f9288b9758e1acab52f1f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="what-is-a-lock"></a>잠금을 이란?
잠금는 기준인 DBMS 다중 사용자 환경에서 한 행에 액세스를 제한 하는 프로세스입니다. 행 또는 열을 배타적으로 잠겨 잠금이 해제 될 때까지 잠긴된 데이터에 액세스 하려면 다른 사용자가 허용 되지 않습니다. 이렇게 하면 두 명의 사용자가 행의 동일한 열에 동시에 업데이트 수 없습니다.  
  
 잠금은 리소스의 관점에서 비용이 매우 많이 들 수 있습니다 및 데이터 무결성을 유지 하는 데 필요한 경우에 사용할 해야 합니다. 여기서 수백 또는 수천 명의 사용자가 수 액세스 하려고 할 수는 레코드 1 초 마다 데이터베이스에서-인터넷에 연결 된 데이터베이스와 같은-응용 프로그램의 성능이 저하 불필요 한 잠금 신속 하 게 될 수 있습니다.  
  
 어떻게 데이터 소스와 ADO 커서 라이브러리 한 동시성이 달리 관리 적절 한 잠금 옵션을 선택 하 여 제어할 수 있습니다.  
  
 설정의 **LockType** 속성 열기 전에 **레코드 집합** 를 열 때 사용 해야 하는 공급자 잠금 유형을 지정 합니다. 열린에서 사용 중인 잠금 유형을 반환 하려면 속성을 읽을 **레코드 집합** 개체입니다.  
  
 공급자는 일부 잠금 유형을 지원 하지 않습니다. 공급자가 요청 된 지원할 수 없는 **LockType** 설정, 다른 잠금 유형으로 대체 될 것입니다. 사용할 수 있는 실제 잠금 기능을 확인 하는 **레코드 집합** 개체를 가져오려면는 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드 **adUpdate** 및 **adUpdateBatch**.  
  
 **adLockPessimistic** 경우 설정을 지원 하지 않습니다는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성이 **adUseClient 합니다.** 지원 되지 않는 값을 설정 하는 경우 오류가 발생 하지 될 수 있습니다. 가장 가까운 지원 **LockType** 대신 사용 됩니다.  
  
 **LockType** 속성은 읽기/쓰기 때는 **레코드 집합** 열려 있는 경우에 닫혀 있고 이며 읽기 전용입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [잠금의 유형](../../../ado/guide/data/types-of-locks.md)

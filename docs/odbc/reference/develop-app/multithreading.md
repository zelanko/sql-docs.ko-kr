---
title: "다중 스레딩 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], thread-safe
- thread-safe drivers [ODBC]
- multithreaded applications [ODBC]
ms.assetid: cdfebdf5-12ff-4e28-8055-41f49b77f664
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9c49f5cf9e9a5082ff8fbdfcefc5b71656c61962
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="multithreading"></a>다중 스레딩
다중 스레드 운영 체제에서 드라이버는 스레드로부터 안전 하 게 보호 되어야 합니다. 즉, 둘 이상의 스레드에서 같은 핸들을 사용 하도록 응용 프로그램에 대 한 수 있어야 합니다. 드라이버 관련 되는 다음과 가능성이 드라이버를 동시에 두 개의 서로 다른 스레드에서 동일한 핸들을 사용 하려는 모든 시도 serialize 합니다.  
  
 일반적으로 응용 프로그램 비동기 처리 하는 대신 여러 스레드를 사용 합니다. 별도 스레드에서 만들고, ODBC 함수를 호출 합니다. 주 스레드에서 계속 처리 하는 응용 프로그램 합니다. 것이 아니라 지속적으로 폴링하지 비동기 함수 SQL_ATTR_ASYNC_ENABLE 문 특성을 사용할 때의 경우 처럼, 응용 프로그램 완료 새로 생성된 된 스레드를 통해 단순히 수 있습니다.  
  
 문 핸들을 그대로 사용 하 고 하나의 스레드에서 실행 하는 함수를 호출 하 여 취소할 수 **SQLCancel** 동일한 문을 사용 하 여 다른 스레드에서 처리 합니다. 드라이버의 사용을 직렬화 하지 해야 하지만 **SQLCancel** 이런 방식으로 보장은 없습니다 호출 **SQLCancel** 실제로 다른 스레드에서 실행 중인 함수를 취소 합니다.


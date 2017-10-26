---
title: "데이터에서 연결을 끊으면 원본이 나 드라이버 | Microsoft Docs"
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
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a08f5de9829ee006c51ef6a2e795b44967c43a99
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="disconnecting-from-a-data-source-or-driver"></a>데이터에서 연결을 끊으면 원본이 나 드라이버
호출 응용 프로그램 데이터 원본을 사용 하 여 완료 되 면 **SQLDisconnect**합니다. **SQLDisconnect** 연결에 할당 되는 모든 문을 해제 하 고 데이터 원본에서 드라이버 연결을 끊습니다. 트랜잭션을 진행 중인 경우 오류를 반환 합니다.  
  
 연결을 끊은 후 응용 프로그램이 호출할 수 **SQLFreeHandle** 를 연결을 해제 합니다. 응용 프로그램 프로그래밍 오류; ODBC 함수 호출에서 연결의 핸들을 사용 하려는 것이 연결을 해제 한 후 이렇게 하면 되므로 결과가 정의 되지 않은 있지만 아마도 심각한 됩니다. 때 **SQLFreeHandle** 호출 되는 드라이버 릴리스 구조는 연결에 대 한 정보를 저장 하는 데 사용 합니다.  
  
 또한 응용 프로그램 다른 데이터 원본에 연결 하거나 동일한 데이터 원본에 연결 하려면 연결을 다시 사용할 수 있습니다. 연결을 끊고, 나중에 다시 연결 하는 대신 연결 된 상태로 유지 하는 결정 해야 응용 프로그램 기록기는 각 옵션의 상대 비용을 고려 데이터 원본에 연결 하 고 연결 된 상태로 유지 연결 매체에 따라 비교적 비용이 많이 들 수 있습니다. 올바른 균형을 조절 하는 경우 응용 프로그램 에서도 가능성 및 동일한 데이터 원본에 대 한 추가 작업의 타이밍에 대 한 가정을 확인 해야 합니다.


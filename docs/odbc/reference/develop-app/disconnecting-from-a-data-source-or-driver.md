---
title: 데이터에서 연결을 끊는 중 원본 또는 드라이버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2189c0fcc65fd4192e94da140e2d55ac86826137
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62936002"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>데이터 원본 또는 드라이버 연결 끊기
호출 응용 프로그램 데이터 원본을 사용 하 여 완료 되 면 **SQLDisconnect**합니다. **SQLDisconnect** 연결에 할당 되는 모든 문을 해제 하 고 데이터 원본에서 드라이버 연결을 끊습니다. 트랜잭션이 진행에서 중이면 오류가 발생 합니다.  
  
 연결을 끊은 후 응용 프로그램이 호출할 수 있습니다 **SQLFreeHandle** 를 연결 해제 합니다. 응용 프로그램 프로그래밍 오류는 ODBC 함수 호출에서 연결의 핸들을 사용 하는 것 연결을 해제 한 후 이렇게 하면에 정의 되지 않은 있지만 아마도 심각한 결과가 발생 합니다. 때 **SQLFreeHandle** 호출 구조를 연결 하는 방법에 대 한 정보를 저장 하는 데 드라이버 릴리스 합니다.  
  
 또한 응용 프로그램 서로 다른 데이터 원본에 연결 하거나 동일한 데이터 소스에 다시 연결 하려면 연결을 다시 사용할 수 있습니다. 연결을 끊고, 나중에 다시 연결 하는 대신 연결 된 상태로 유지 하는 결정 해야 각 옵션의 상대 비용을 고려 하는 응용 프로그램 작성자 데이터 원본에 연결 및 연결 된 연결 매체에 따라 비교적 비용이 많이 들 수 있습니다. 올바른 균형을 유지 하는 경우 응용 프로그램 가능성과 동일한 데이터 원본에 대 한 추가 작업의 타이밍에 대 한 가정을 또한 확인 해야 합니다.

---
title: 데이터 원본 또는 드라이버연결 해제 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 154a571bce3a337d539216ce89c32420ab981bd8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300463"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>데이터 원본 또는 드라이버 연결 끊기
응용 프로그램이 데이터 원본을 사용하여 완료되면 **SQLDisconnect**를 호출합니다. **SQLDisconnect는** 연결에 할당된 모든 문을 해제하고 데이터 원본에서 드라이버를 연결해제합니다. 트랜잭션이 진행 중이면 오류를 반환합니다.  
  
 연결을 끊은 후 응용 프로그램은 **SQLFreeHandle을** 호출하여 연결을 해제할 수 있습니다. 연결을 해제한 후 ODBC 함수를 호출할 때 연결 핸들을 사용하는 응용 프로그램 프로그래밍 오류입니다. 이렇게 하면 정의되지 않았지만 치명적인 결과가 있을 수 있습니다. **SQLFreeHandle이** 호출되면 드라이버는 연결에 대한 정보를 저장하는 데 사용되는 구조를 해제합니다.  
  
 또한 응용 프로그램은 다른 데이터 원본에 연결하거나 동일한 데이터 원본에 다시 연결하기 위해 연결을 다시 사용할 수도 있습니다. 나중에 연결을 끊고 다시 연결하는 것과 는 달리 연결 상태를 유지하기로 결정하려면 응용 프로그램 작성자가 각 옵션의 상대적인 비용을 고려해야 합니다. 데이터 원본에 연결하고 연결된 나머지 모두 연결 매체에 따라 상대적으로 비용이 많이 들 수 있습니다. 올바른 절충을 할 때 응용 프로그램은 동일한 데이터 원본에서 추가 작업의 가능성과 타이밍에 대해서도 가정해야 합니다.

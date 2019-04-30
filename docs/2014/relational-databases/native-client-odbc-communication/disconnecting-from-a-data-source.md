---
title: 데이터 원본에서 연결 끊기 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- disconnecting [ODBC]
- ODBC applications, disconnecting
- SQLDisconnect function
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLFreeHandle function
- ODBC data sources, disconnecting
- SQL Server Native Client ODBC driver, data sources
- ODBC functions
- SQL Server Native Client ODBC driver, connections
ms.assetid: 65b0267d-b2ab-4a59-83f2-436d90cfbf79
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43ccc784d0d8759c559e705cbbb65861040f6e8a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63205682"
---
# <a name="disconnecting-from-a-data-source"></a>데이터 원본에서 연결 끊기
  호출 응용 프로그램 데이터 원본을 사용 하 여 완료 되 면 **SQLDisconnect**합니다. **SQLDisconnect** 연결에 할당 되는 모든 문을 해제 하 고 데이터 원본에서 드라이버 연결을 끊습니다. 연결을 끊은 후 응용 프로그램이 호출할 수 있습니다 [SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md) 를 연결 핸들을 해제 합니다. 를 종료 하기 전에 응용 프로그램 호출 **SQLFreeHandle** 를 환경 핸들을 해제 합니다.  
  
 연결을 끊은 후 응용 프로그램에서 할당된 연결 핸들을 다시 사용하여 다른 데이터 원본에 연결하거나 동일한 데이터 원본에 다시 연결할 수 있습니다. 연결을 끊은 후 나중에 다시 연결하는 대신 연결된 상태로 유지할지 여부를 결정하는 경우 응용 프로그램 작성기에서 각 옵션의 상대 비용을 고려해야 합니다. 데이터 원본에 연결하여 연결된 상태로 유지하는 것은 연결 매체에 따라 비교적 비용이 높을 수 있습니다. 장단점을 고려할 때 응용 프로그램은 동일한 데이터 원본에서 추가 작업이 수행될 확률과 타이밍에 대해서도 가정해야 합니다. 한 응용 프로그램에서 둘 이상의 연결을 사용해야 할 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server와의 통신 &#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  

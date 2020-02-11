---
title: 데이터 원본 또는 드라이버에서 연결을 끊는 중 | Microsoft Docs
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
ms.openlocfilehash: a01220b6a4f15ee3770b844f41e7ddc5399f5f86
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039763"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>데이터 원본 또는 드라이버 연결 끊기
응용 프로그램이 데이터 원본 사용을 마치면 **Sqldisconnect**를 호출 합니다. **Sqldisconnect** 는 연결에 할당 된 모든 문을 해제 하 고 데이터 원본에서 드라이버의 연결을 끊습니다. 트랜잭션이 진행 중인 경우 오류를 반환 합니다.  
  
 연결을 끊은 후 응용 프로그램은 **Sqlfreehandle** 을 호출 하 여 연결을 해제할 수 있습니다. 연결을 해제 한 후에는 ODBC 함수 호출에서 연결의 핸들을 사용 하는 응용 프로그램 프로그래밍 오류가 발생 합니다. 이렇게 하면 정의 되지 않았지만 심각한 결과가 발생할 수 있습니다. **Sqlfreehandle** 을 호출 하면 드라이버는 연결에 대 한 정보를 저장 하는 데 사용 되는 구조를 해제 합니다.  
  
 응용 프로그램은 다른 데이터 원본에 연결 하거나 동일한 데이터 원본에 다시 연결 하는 연결을 다시 사용할 수도 있습니다. 나중에 연결을 끊고 다시 연결 하는 것과는 반대로 연결 유지를 결정 하려면 응용 프로그램 작성자가 각 옵션의 상대적 비용을 고려해 야 합니다. 데이터 원본에 연결 하 고 연결 된 나머지는 연결 매체에 따라 상대적으로 비용이 많이 들 수 있습니다. 올바른 균형을 유지 하기 위해 응용 프로그램은 동일한 데이터 원본에 대 한 추가 작업의 가능성과 타이밍에 대 한 가정을 해야 합니다.

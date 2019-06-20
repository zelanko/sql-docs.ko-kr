---
title: 다중 스레딩 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], thread-safe
- thread-safe drivers [ODBC]
- multithreaded applications [ODBC]
ms.assetid: cdfebdf5-12ff-4e28-8055-41f49b77f664
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a16262d562ca2088f38cd863a6f44e537e65d40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63254206"
---
# <a name="multithreading"></a>다중 스레딩
다중 스레드 운영 체제에서 드라이버 스레드로부터 안전 해야 합니다. 즉, 둘 이상의 스레드에서 같은 핸들을 사용 하도록 응용 프로그램에 대 한 수 있어야 합니다. 이렇게 하는 방법을 드라이버 관련 이며 드라이버의 동시에 두 개의 다른 스레드에서 동일한 핸들을 사용 하려는 모든 시도 serialize 하는 것입니다.  
  
 일반적으로 응용 프로그램을 비동기적으로 처리 하는 대신 여러 스레드를 사용합니다. 응용 프로그램에서 ODBC 함수를 호출 하며 주 스레드에서 처리를 계속 한 다음 별도 스레드를 만듭니다 합니다. 대신 비동기 함수를 지속적으로 폴링할 SQL_ATTR_ASYNC_ENABLE 문 특성을 사용 하는 경우의 경우와 마찬가지로, 응용 프로그램 완료 새로 생성된 된 스레드를 간단히 할 수 있습니다.  
  
 문 핸들을 허용 하 고 스레드 하나에서 실행 되는 함수를 호출 하 여 취소할 수 있습니다 **SQLCancel** 동일한 문을 사용 하 여 다른 스레드에서 처리 합니다. 드라이버의 사용을 serialize 하지는 않지만 **SQLCancel** 이런 방식으로 보장이 없습니다 호출 **SQLCancel** 다른 스레드에서 실행 되는 함수를 실제로 취소 됩니다.

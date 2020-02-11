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
ms.openlocfilehash: 1eaa07ce22436bc8bfae215c0431480081ee0f06
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086347"
---
# <a name="multithreading"></a>다중 스레딩
다중 스레드 운영 체제에서 드라이버는 스레드로부터 안전 해야 합니다. 즉, 응용 프로그램에서 둘 이상의 스레드에서 동일한 핸들을 사용할 수 있어야 합니다. 이를 수행 하는 방법은 드라이버 마다 다르며, 두 개의 서로 다른 스레드에서 동일한 핸들을 동시에 사용 하려고 시도 하는 경우 드라이버에서 serialize 할 가능성이 높습니다.  
  
 응용 프로그램은 일반적으로 비동기 처리 대신 여러 스레드를 사용 합니다. 응용 프로그램은 별도의 스레드를 만들고 여기에서 ODBC 함수를 호출한 다음 주 스레드에서 처리를 계속 합니다. SQL_ATTR_ASYNC_ENABLE statement 특성을 사용 하는 경우 처럼 비동기 함수를 지속적으로 폴링하는 대신, 응용 프로그램은 단순히 새로 만든 스레드를 완료할 수 있습니다.  
  
 문 핸들을 수락 하 고 한 스레드에서 실행 되는 함수는 다른 스레드의 동일한 문 핸들을 사용 하 여 **Sqlcancel** 을 호출 하 여 취소할 수 있습니다. 이러한 방식으로 드라이버가 **sqlcancel** 사용을 직렬화 해서는 안 되지만 **sqlcancel** 을 호출 하면 다른 스레드에서 실행 되는 함수를 실제로 취소 한다는 보장이 없습니다.

---
title: 멀티스레딩 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c10d1b401ac780d24184c4c2337199e99973e916
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302420"
---
# <a name="multithreading"></a>다중 스레딩
다중 스레드 운영 체제에서 드라이버는 스레드가 안전해야 합니다. 즉, 응용 프로그램이 두 개 이상의 스레드에서 동일한 핸들을 사용할 수 있어야 합니다. 이를 달성하는 방법은 드라이버에 따라 다르며, 드라이버는 두 개의 서로 다른 스레드에서 동일한 핸들을 동시에 사용하려는 모든 시도를 직렬화할 수 있습니다.  
  
 응용 프로그램은 일반적으로 비동기 처리 대신 여러 스레드를 사용합니다. 응용 프로그램은 별도의 스레드를 만들고 ODBC 함수를 호출한 다음 주 스레드에서 처리를 계속합니다. SQL_ATTR_ASYNC_ENABLE 문 특성을 사용하는 경우와 마찬가지로 비동기 함수를 지속적으로 폴링하는 대신 응용 프로그램에서 새로 만든 스레드를 완료할 수 있습니다.  
  
 문 핸들을 수락하고 한 스레드에서 실행 중인 함수는 다른 스레드에서 동일한 명령문 핸들을 사용하는 **SQLCancel을** 호출하여 취소할 수 있습니다. 드라이버는 이러한 방식으로 **SQLCancel의** 사용을 직렬화하지 않아야 하지만 **SQLCancel를** 호출하면 실제로 다른 스레드에서 실행 중인 함수가 취소된다는 보장은 없습니다.

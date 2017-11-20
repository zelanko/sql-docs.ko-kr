---
title: "만들기 및 스레드를 종료 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7a30fbe976ac3de550f8067cca82732631f698ac
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="creating-and-terminating-threads"></a>만들기 및 스레드를 종료 합니다.
ODBC를 사용 하는 다중 스레드 응용 프로그램에서 Microsoft® C++® 런타임 라이브러리 함수를 호출 해야 **_beginthread** 및 **_endthread** (또는 **_beginthreadex** 및 **_endthreadex**)를 만들고 ODBC 드라이버 관리자를 호출 하는 스레드를 종료 합니다. 응용 프로그램 Microsoft Windows NT® 함수를 호출 하는 경우 **CreateThread** 및 **EndThread** 대신 메모리 누수 드라이버 관리자와 일부 ODBC 드라이버에 C 런타임 호출 하기 때문에 발생 합니다 함수를 호출 하 여 만든 스레드에서 작동 하지 것입니다 **CreateThread**합니다. 자세한 내용은 Microsoft Windows® 설명서를 참조 합니다.


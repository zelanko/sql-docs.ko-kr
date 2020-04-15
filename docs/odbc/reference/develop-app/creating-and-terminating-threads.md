---
title: 스레드 작성 및 종료 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3536deef604d7dbf645903e7d171a58cd9fec96a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301694"
---
# <a name="creating-and-terminating-threads"></a>스레드 생성 및 종료
ODBC를 사용하는 다중 스레드 응용 프로그램은 _beginthread **및** **_endthread(또는** **_beginthreadex** 및 **_endthreadex)** Microsoft® Visual C++® 런타임 라이브러리 함수를 호출하여 ODBC 드라이버 관리자를 호출하는 스레드를 만들고 종료해야 합니다. 응용 프로그램이 Microsoft Windows NT® 함수 **CreateThread** 및 **EndThread대신** 호출하는 경우 드라이버 관리자와 일부 ODBC 드라이버가 **CreateThread를**호출하여 만든 스레드에서 작동하지 않는 C 런타임 함수를 호출하기 때문에 메모리 누수가 발생합니다. 자세한 내용은 Microsoft Windows® 설명서를 참조하십시오.

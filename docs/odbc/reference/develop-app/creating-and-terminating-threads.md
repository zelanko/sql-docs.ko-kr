---
title: 스레드 생성 및 종료 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b97f29ad06c4ed961f3cee571b0ca7b8d9c0b774
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002087"
---
# <a name="creating-and-terminating-threads"></a>스레드 생성 및 종료
ODBC를 사용 하는 다중 스레드 응용 프로그램은 Microsoft® Visual 호출 해야 합니다 C++® 런타임 라이브러리 함수 **_beginthread** 하 고 **_endthread** (또는 **_beginthreadex**하 고 **_endthreadex**)를 만들고 ODBC 드라이버 관리자를 호출 하는 스레드를 종료 합니다. 응용 프로그램 Microsoft Windows NT® 함수를 호출 하는 경우 **CreateThread** 하 고 **EndThread** 메모리 누수 드라이버 관리자와 일부 ODBC 드라이버에는 C 런타임 호출 되기 때문에 발생 하는 함수 대신 호출 하 여 만든 스레드에서 작동 하지 것입니다 **CreateThread**합니다. 자세한 내용은 Microsoft Windows® 설명서를 참조 하십시오.

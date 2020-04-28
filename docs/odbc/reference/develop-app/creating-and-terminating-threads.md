---
title: 스레드 만들기 및 종료 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301694"
---
# <a name="creating-and-terminating-threads"></a>스레드 생성 및 종료
ODBC를 사용 하는 다중 스레드 응용 프로그램은 Microsoft® Visual C++® 런타임 라이브러리 함수 **_beginthread** , **_endthread** **또는 _beginthreadex** **)를**호출 하 여 odbc 드라이버 관리자를 호출 하는 스레드를 만들고 종료 해야 합니다. 응용 프로그램이 Microsoft Windows NT® 함수 **CreateThread** 및 **EndThread** 를 대신 호출 하는 경우 드라이버 관리자와 일부 ODBC 드라이버가 **CreateThread**를 호출 하 여 만든 스레드에서 작동 하지 않는 C 런타임 함수를 호출 하기 때문에 메모리 누수가 발생 합니다. 자세한 내용은 Microsoft Windows® 설명서를 참조 하세요.

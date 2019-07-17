---
title: '6단계: 데이터 원본에서 연결 끊기 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65cc2ae8d2c2248a733e6efa9537fd3b40bb8fd1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114118"
---
# <a name="step-6-disconnect-from-the-data-source"></a>6단계: 데이터 원본 연결 끊기
다음 그림에 나와 있는 것 처럼 데이터 원본에서 연결을 끊습니다는 최종 단계가입니다. 응용 프로그램 호출 하 여 모든 문 핸들을 해제 하는 먼저 **SQLFreeHandle**합니다. 자세한 내용은 [문 핸들 해제](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)합니다.  
  
 ![데이터 원본에서 연결 끊기 보여 줍니다](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 다음으로 사용 하 여 데이터 소스에서 응용 프로그램 연결을 끊습니다 **SQLDisconnect** 하 고 사용 하 여 연결 핸들을 해제 **SQLFreeHandle**합니다. 자세한 내용은 [데이터 원본 또는 드라이버에서 연결 끊기](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)합니다.  
  
 응용 프로그램이 사용 하 여 환경 핸들을 해제 하는 마지막으로, **SQLFreeHandle** 하 고 드라이버 관리자를 언로드합니다. 자세한 내용은 [환경 핸들 할당](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)합니다.

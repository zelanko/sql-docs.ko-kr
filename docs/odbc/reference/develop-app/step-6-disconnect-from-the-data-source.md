---
title: "6 단계: 데이터 소스에서 연결 끊기 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce3ea03a637e8edce89c83f196e4fcafd97dfdc8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="step-6-disconnect-from-the-data-source"></a>6 단계: 데이터 소스에서 연결 끊기
마지막 단계는 다음 그림에 나와 있는 것 처럼 데이터 소스에서 연결을 끊으려면입니다. 응용 프로그램 호출 하 여 모든 문 핸들을 해제 하는 첫째, **SQLFreeHandle**합니다. 자세한 내용은 참조 [문 핸들 해제](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)합니다.  
  
 ![데이터 원본에서 연결 끊기 표시](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 응용 프로그램 사용 하 여 데이터 소스에서 연결을 끊습니다는 다음으로, **SQLDisconnect** 와 연결 핸들을 해제 하 고 **SQLFreeHandle**합니다. 자세한 내용은 참조 [데이터 원본이 나 드라이버에서 연결 끊기](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)합니다.  
  
 응용 프로그램으로 환경 핸들을 해제 하는 마지막으로, **SQLFreeHandle** 를 드라이버 관리자를 지 속하거나 언로드합니다. 자세한 내용은 참조 [환경 처리할 할당](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)합니다.

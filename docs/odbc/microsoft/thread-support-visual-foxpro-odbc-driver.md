---
description: 스레드 지원(Visual FoxPro ODBC 드라이버)
title: 스레드 지원 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- thread support [ODBC]
- Visual FoxPro ODBC driver [ODBC], thread support
- FoxPro ODBC driver [ODBC], thread support
- multithreaded applications [ODBC]
ms.assetid: 0c6abbbc-012b-41aa-bded-5e7e362d015b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 013ccd1f5d202794ba6b7a44c10339dd14c08d17
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449075"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>스레드 지원(Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버는 스레드로부터 안전 합니다. 환경 핸들 (*h)*)에 대 한 액세스, 연결 핸들 (*hdbc*) 및 문 핸들 (*hstmt*)이 적절 한 세마포에 래핑되어 다른 프로세스에서 드라이버의 내부 데이터 구조에 액세스 하 고 잠재적으로 변경 하지 못하도록 합니다.  
  
 다중 스레드 응용 프로그램에서는 별도의 스레드에서 [Sqlcancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) 을 호출 하 여 *hstmt* 에서 동기적으로 실행 되는 함수를 취소할 수 있습니다.  
  
 점진적 페치를 사용 하는 경우 드라이버는 개별 스레드를 사용 하 여 데이터를 가져옵니다. 데이터 원본에 대해 점진적 페치를 사용 하려면 [ODBC Visual FoxPro 설치 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) 에서 **데이터를 백그라운드에서 페치** 확인란을 선택 하거나 연결 문자열에서 BackgroundFetch attribute 키워드를 사용 합니다. 다중 스레드 응용 프로그램에서 드라이버를 호출할 때는 백그라운드 페치를 사용 하지 마십시오. 연결 문자열 특성 키워드에 대 한 자세한 내용은 [연결 문자열 사용](../../odbc/microsoft/using-connection-strings.md)을 참조 하세요.  
  
 스레드 및 **Sqlcancel**에 대 한 자세한 내용은 *ODBC 프로그래머 참조*에서 [sqlcancel](../../odbc/reference/syntax/sqlcancel-function.md) 을 참조 하십시오.

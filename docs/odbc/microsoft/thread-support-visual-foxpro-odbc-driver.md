---
title: 스레드 지원 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- thread support [ODBC]
- Visual FoxPro ODBC driver [ODBC], thread support
- FoxPro ODBC driver [ODBC], thread support
- multithreaded applications [ODBC]
ms.assetid: 0c6abbbc-012b-41aa-bded-5e7e362d015b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71392c60f5b36e53ce1a3fcb995ff97db32a6981
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>스레드 지원 (Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버는 스레드로부터 안전 합니다. 환경 핸들에 대 한 액세스 (*때*), 연결 핸들 (*hdbc*), 및 문 핸들 (*hstmt*) 다른 프로세스를 방지 하기 위해 적절 한 세마포에 겹쳐서 표시 액세스 하 고 잠재적으로 드라이버의 내부 데이터 구조를 변경 합니다.  
  
 다중 스레드 응용 프로그램에서 동기적으로 실행 하는 함수를 취소할 수 있습니다는 *hstmt* 호출 하 여 [SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) 별도 스레드에서 합니다.  
  
 드라이버는 별도 스레드를 사용 하 여 점진적 페치를 사용 하는 경우 데이터를 가져옵니다. 데이터 원본에 대해 점진적 페치를 사용 하려면 선택은 **백그라운드에서 데이터를 인출** 확인란은 [ODBC Visual FoxPro 설정 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) BackgroundFetch 특성 키워드를 사용 하 여 연결에서 하거나 문자열입니다. 다중 스레드 응용 프로그램에서 드라이버를 호출할 때 백그라운드 가져오기를 사용 하지 마십시오. 특성에서 연결 문자열 키워드에 대 한 정보를 참조 하십시오. [연결 문자열을 사용 하 여](../../odbc/microsoft/using-connection-strings.md)합니다.  
  
 스레드에 대 한 자세한 내용은 및 **SQLCancel**, 참조 [SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) 에 *ODBC Programmer's Reference*합니다.

---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77187802bb57a832263ec2070564754e87f21345
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632926"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>스레드 지원(Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버는 스레드로부터 안전 합니다. 환경 핸들에 대 한 액세스 (*경우*), 연결 핸들 (*hdbc*), 및 문 핸들 (*hstmt*) 다른 프로세스를 방지 하기 위해 적절 한 세마포 래핑됩니다 에 액세스 하 고 잠재적으로 드라이버의 내부 데이터 구조를 변경 합니다.  
  
 다중 스레드 응용 프로그램에서 동기적으로 실행 하는 함수를 취소할 수 있습니다는 *hstmt* 호출한 [SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) 별도 스레드에서 합니다.  
  
 드라이버 점진적 페치 사용 하는 경우 데이터를 가져오기 위해 별도 스레드를 사용 합니다. 데이터 원본에 대해 점진적 페치를 사용 하려면 선택 합니다 **백그라운드에서 데이터를 인출** 확인란 합니다 [ODBC Visual FoxPro 설치 대화 상자가](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) 연결에서 BackgroundFetch 특성 키워드를 사용 문자열입니다. 다중 스레드 응용 프로그램에서 드라이버를 호출할 때 백그라운드 페치를 사용 하지 마십시오. 연결 문자열 특성 키워드에 대 한 정보를 참조 하세요 [연결 문자열을 사용 하 여](../../odbc/microsoft/using-connection-strings.md)입니다.  
  
 스레드에 대 한 자세한 내용은 및 **SQLCancel**를 참조 하세요 [SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) 에 *ODBC 프로그래머 참조*합니다.

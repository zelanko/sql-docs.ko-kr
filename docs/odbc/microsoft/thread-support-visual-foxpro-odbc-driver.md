---
title: 스레드 지원(비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
ms.openlocfilehash: 2aa19eb233525b5a65ef67fe9903814fc1163177
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303084"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>스레드 지원(Visual FoxPro ODBC 드라이버)
비주얼 FoxPro ODBC 드라이버는 스레드가 안전합니다. 환경*핸들(+1.kr),* 연결*핸들(hdbc)* 및 문*핸들(hstmt)에*대한 액세스는 다른 프로세스가 드라이버의 내부 데이터 구조에 액세스하고 잠재적으로 변경되지 않도록 적절한 세마포에 싸여 있습니다.  
  
 다중 스레드 응용 프로그램에서는 별도의 스레드에서 [SQLCancel을](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) 호출하여 *hstmt에서* 동기적으로 실행되는 함수를 취소할 수 있습니다.  
  
 드라이버는 프로그레시브 페칭을 사용할 때 별도의 스레드를 사용하여 데이터를 가져옵니다. 데이터 원본에 대해 점진적 페칭을 사용하려면 [ODBC Visual FoxPro 설치 설정 대화 상자에서](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) **백그라운드** 데이터 가져오기 확인란을 선택하거나 연결 문자열에서 BackgroundFetch 특성 키워드를 사용합니다. 다중 스레드 응용 프로그램에서 드라이버를 호출할 때 백그라운드 가져오기를 사용하지 마십시오. 연결 문자열 특성 키워드에 대한 자세한 내용은 [연결 문자열 사용을](../../odbc/microsoft/using-connection-strings.md)참조하십시오.  
  
 스레드 및 **SQLCancel에**대한 자세한 내용은 *ODBC 프로그래머 의 참조에서* [SQLCancel을](../../odbc/reference/syntax/sqlcancel-function.md) 참조하십시오.

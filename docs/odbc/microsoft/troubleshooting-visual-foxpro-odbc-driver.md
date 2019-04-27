---
title: (Visual FoxPro ODBC 드라이버) 문제 해결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI [ODBC]
- troubleshooting Visual FoxPro ODBC driver [ODBC]
- remote views [ODBC]
- multitiered views [ODBC]
- parameterized views [ODBC], Visual FoxPro ODBC driver
- fetches [ODBC], Visual FoxPro ODBC driver
- positioned updates [ODBC]
- background fetching [ODBC]
ms.assetid: fd478dd8-666a-4f0a-a2d6-b94e81cbbe4b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f0576d017068b8ab0694da798c5be458f115e56
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632609"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>문제 해결(Visual FoxPro ODBC 드라이버)
다음 섹션에서는 성능 향상 및 Visual FoxPro ODBC 드라이버를 사용 하는 동안 발생할 수 있는 문제를 해결 하는 방법을 설명 합니다.  
  
## <a name="accessing-parameterized-views"></a>매개 변수화 된 보기에 액세스  
 매개 변수가 있는 뷰와 드라이버를 사용 하 여 Visual FoxPro 데이터베이스에 액세스할 수 없습니다. 매개 변수가 있는 뷰를 뷰의 SQL의 WHERE 절을 만듭니다 **선택** 레코드를 제한 하는 문 매개 변수에 대해 제공 된 값을 사용 하 여 빌드된 WHERE 절의 조건을 충족 하는 레코드에 다운로드 합니다. 드라이버에서 보기로 전달 매개 변수를 지원 하지 않으므로에 드라이버를 사용 하 여 매개 변수가 있는 뷰를 액세스 하려고 하면 실패 합니다.  
  
 매개 변수 값을 런타임에 제공 또는 뷰를 프로그래밍 방식으로 전달할 수 있습니다.  
  
## <a name="accessing-remote-views"></a>원격 보기 액세스  
 원격 보기 드라이버를 사용 하 여 Visual FoxPro 데이터베이스에 액세스할 수 없습니다. 원격 뷰는 FoxPro 비 데이터 또는 FoxPro 및 비 FoxPro 데이터의 조합에 액세스 하는 뷰입니다. 원격 보기에 액세스 하려면 Visual FoxPro를 사용 합니다.  
  
## <a name="deleting-records"></a>레코드 삭제  
 드라이버를 사용 하 여 삭제에 대 한 레코드를 표시할 수 있지만 데이터베이스에서 레코드를 영구적으로 제거할 수 없습니다. 테이블에서 레코드를 영구적으로 제거, Visual FoxPro를 사용 합니다.  
  
## <a name="increasing-performance-using-background-fetching"></a>백그라운드 페치를 사용 하는 성능 향상  
 백그라운드 페치 드라이버의 기능을 사용 하 여 큰 인출에서 성능을 개선할 수 있습니다. 백그라운드 페치 특정 데이터 원본에서 요청한 데이터를 인출 하는 별도 스레드를 사용 합니다.  
  
 다음 방법 중 하나에서 데이터 원본에 대 한 페치 백그라운드를 사용할 수 있습니다.  
  
-   확인 합니다 **백그라운드에서 데이터를 인출** 확인란을 합니다 [ODBC Visual FoxPro 설치 대화 상자가](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)합니다.  
  
-   연결 문자열에 BackgroundFetch 특성 키워드를 사용 합니다.  
  
 연결 문자열 특성 키워드에 대 한 자세한 내용은 [연결 문자열을 사용 하 여](../../odbc/microsoft/using-connection-strings.md)입니다.  
  
## <a name="updating-multitiered-views"></a>다중 계층 뷰를 업데이트 하는 중  
 다중 계층 뷰를 기본 테이블 대신 하나 이상의 보기에서 기반 뷰입니다. 다중 계층 뷰에서 데이터를 업데이트 하면 업데이트를 한 수준 아래로 보기로 이동 하 여 최상위 뷰의 기반이 되는; 기본 테이블이 업데이트 되지 않습니다.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>저장된 프로시저에서 DDL (데이터 정의 언어)을 사용 하 여  
 CREATE TABLE 또는 ALTER TABLE과 같은 DDL Visual FoxPro 저장 프로시저를 사용할 수 없습니다.  
  
 저장된 프로시저에서 사용할 수 있는 언어에 대 한 내용은 참조 하세요 [규칙, 트리거, 기본값, 및 저장 프로시저에 대 한 지원을](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)합니다.  
  
## <a name="using-positioned-updates"></a>위치 지정된 업데이트를 사용 하 여  
 드라이버 위치 지정된 업데이트를 지원 하지 않습니다. 업데이트할 행을 식별 하는 SQL WHERE 절을 사용 합니다.  
  
## <a name="using-the-set-ansi-command"></a>SET ANSI 명령 사용  
 Visual FoxPro 개발자 인 경우에 드라이버의 경우 기본 설정인 OFF Visual FoxPro 달리 ANSI 설정에 대 한 기본 설정이 ON 임을 인식 해야 합니다. ANSI 설정에 대 한 설정에 기본값에는 일반적으로 정확한 비교를 수행 하는 다른 ODBC 데이터 원본으로 일관성 있게 동작 하도록 Visual FoxPro 데이터 원본 수 있습니다. 기본 설정을 변경할 수 있습니다. 자세한 내용은 [ANSI 설정](../../odbc/microsoft/set-ansi-command.md)합니다.

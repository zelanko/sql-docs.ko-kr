---
title: "(Visual FoxPro ODBC 드라이버) 문제 해결 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea6c45c362047d45275b6895d58faafe0250d26f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>(Visual FoxPro ODBC 드라이버) 문제 해결
다음 섹션에서는 성능을 개선 하 고 Visual FoxPro ODBC 드라이버를 사용 하는 동안 발생 하는 문제를 해결 하는 방법에 설명 합니다.  
  
## <a name="accessing-parameterized-views"></a>매개 변수화 된 보기에 액세스  
 매개 변수가 있는 뷰와 드라이버를 사용 하 여 Visual FoxPro 데이터베이스에 액세스할 수 없습니다. 매개 변수가 있는 뷰 보기의 SQL의 WHERE 절을 만듭니다 **선택** 레코드를 제한 하는 문 매개 변수에 대해 제공 된 값을 사용 하 여 작성 하는 WHERE 절 조건을 만족 하는 레코드에 다운로드 합니다. 드라이버 보기에 매개 변수 전달을 지원 하지 않으므로 드라이버를 사용 하 여 매개 변수가 있는 보기에 액세스 하는 시도가 실패 합니다.  
  
 매개 변수 값을 런타임 시 제공 또는 프로그래밍 방식으로 뷰에 전달 수 있습니다.  
  
## <a name="accessing-remote-views"></a>원격 액세스 방법 뷰  
 드라이버를 사용 하 여 Visual FoxPro 데이터베이스의 원격 보기를 액세스할 수 없습니다. 원격 뷰는 FoxPro 비 데이터 또는 FoxPro 및 비 FoxPro 데이터의 조합에 액세스 하는 뷰입니다. 보기에 액세스 하려면 원격, Visual FoxPro를 사용 합니다.  
  
## <a name="deleting-records"></a>레코드 삭제  
 드라이버를 사용 하는 삭제에 대 한 레코드를 표시할 수 있지만 데이터베이스에서 레코드를 영구적으로 제거할 수 없습니다. 레코드에서 테이블을 영구히 제거 하려면 Visual FoxPro를 사용 합니다.  
  
## <a name="increasing-performance-using-background-fetching"></a>배경 페치를 사용 하는 성능 향상  
 드라이버의 기능을 인출 하는 화면을 사용 하 여 큰 인출에서 성능을 향상 시킬 수 있습니다. 배경 인출 특정 데이터 원본에서 요청한 데이터를 인출 하는 별도 스레드를 사용 합니다.  
  
 다음 방법 중 하나에서 데이터 원본에 대 한 페치 배경을 사용할 수 있습니다.  
  
-   확인은 **백그라운드에서 데이터를 인출 하** 에서 checkbox는 [ODBC Visual FoxPro 설정 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)합니다.  
  
-   연결 문자열에 BackgroundFetch 특성 키워드를 사용 합니다.  
  
 특성에서 연결 문자열 키워드에 대 한 자세한 내용은 참조 [연결 문자열을 사용 하 여](../../odbc/microsoft/using-connection-strings.md)합니다.  
  
## <a name="updating-multitiered-views"></a>다중 계층 뷰 업데이트  
 다중 계층 뷰는 대신 기본 테이블에 하나 이상의 보기를 기반으로 하는 뷰입니다. 다중 계층 보기에서 데이터를 업데이트 하면 업데이트만 한 수준 아래로 보기로 이동 하 여 최상위 보기; 기반이 기본 테이블이 업데이트 되지 않습니다.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>저장된 프로시저에서 데이터 정의 언어 (DDL)를 사용 하 여  
 Visual FoxPro 저장 프로시저에서 DDL CREATE TABLE 또는 ALTER TABLE 등을 사용할 수 없습니다.  
  
 저장된 프로시저에서 사용할 수는 언어에 대 한 자세한 내용은 참조 하십시오. [규칙, 트리거, 기본 값 및 저장 프로시저에 대 한 지원을](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)합니다.  
  
## <a name="using-positioned-updates"></a>위치 지정된 업데이트를 사용 하 여  
 드라이버 위치 지정된 업데이트를 지원 하지 않습니다. 업데이트할 행을 식별 하는 SQL WHERE 절을 사용 합니다.  
  
## <a name="using-the-set-ansi-command"></a>SET ANSI 명령을 사용 하 여  
 Visual FoxPro 개발자 인 경우에 기본 설정인 OFF Visual FoxPro에 대 한 달리 드라이버에 대 한 ANSI 설정에 대 한 기본 설정은 ON 인지 알고 있어야 합니다. ANSI 설정에 대 한 설정에 대 한 기본값에는 일반적으로 정확한 비교를 수행 하는 다른 ODBC 데이터 소스와 일관성 있게 동작 하도록 Visual FoxPro 데이터 원본 수 있습니다. 기본 설정은 변경할 수 있습니다. 자세한 내용은 참조 [ANSI 설정](../../odbc/microsoft/set-ansi-command.md)합니다.

---
title: 문제 해결(비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70b035069c0be88d05a3aa5e17b96af991c27405
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303034"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>문제 해결(Visual FoxPro ODBC 드라이버)
다음 섹션에서는 Visual FoxPro ODBC 드라이버를 사용하는 동안 발생할 수 있는 문제를 개선하고 성능을 향상시키는 방법에 대해 설명합니다.  
  
## <a name="accessing-parameterized-views"></a>매개변수화된 뷰 에 액세스  
 드라이버를 사용하여 Visual FoxPro 데이터베이스에서 매개 변수화된 뷰에 액세스할 수 없습니다. 매개 변수화된 뷰는 매개 변수에 대해 제공된 값을 사용하여 빌드된 WHERE 절의 조건을 충족하는 레코드로 다운로드된 레코드를 제한하는 뷰의 SQL **SELECT** 문에서 WHERE 절을 만듭니다. 드라이버는 뷰에 매개 변수전달을 지원하지 않으므로 드라이버를 사용하여 매개 변수화된 뷰에 액세스하려고 시도하면 실패합니다.  
  
 매개 변수 값은 런타임에 제공되거나 프로그래밍 방식으로 뷰에 전달될 수 있습니다.  
  
## <a name="accessing-remote-views"></a>원격 보기 액세스  
 드라이버를 사용하여 Visual FoxPro 데이터베이스에서 원격 보기에 액세스할 수 없습니다. 원격 보기는 FoxPro가 아닌 데이터 또는 FoxPro 및 비 FoxPro 데이터의 조합에 액세스하는 뷰입니다. 원격 보기에 액세스하려면 Visual FoxPro를 사용합니다.  
  
## <a name="deleting-records"></a>레코드 삭제  
 드라이버를 사용하여 삭제 레코드를 표시할 수 있지만 데이터베이스에서 레코드를 영구적으로 제거할 수는 없습니다. 테이블에서 레코드를 영구적으로 제거하려면 Visual FoxPro를 사용합니다.  
  
## <a name="increasing-performance-using-background-fetching"></a>백그라운드 가져오기를 사용하여 성능 향상  
 드라이버의 백그라운드 가져오기 기능을 사용하여 큰 가져오기의 성능을 향상시킬 수 있습니다. 백그라운드 페칭은 별도의 스레드를 사용하여 특정 데이터 원본에서 요청된 데이터를 가져옵니다.  
  
 다음 방법 중 하나로 데이터 원본에 대한 백그라운드 가져오기를 사용할 수 있습니다.  
  
-   [ODBC Visual FoxPro 설치 설정 대화 상자의](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) **백그라운드** 확인란에서 가져오기 데이터를 선택합니다.  
  
-   연결 문자열에서 BackgroundFetch 특성 키워드를 사용합니다.  
  
 연결 문자열 특성 키워드에 대한 자세한 내용은 [연결 문자열 사용을](../../odbc/microsoft/using-connection-strings.md)참조하십시오.  
  
## <a name="updating-multitiered-views"></a>다계층 뷰 업데이트  
 다중 계층 뷰는 기본 테이블이 아닌 하나 이상의 뷰를 기반으로 하는 뷰입니다. 다중 계층 보기에서 데이터를 업데이트하면 업데이트가 한 수준만 내려가 최상위 뷰의 기반이 되는 뷰로 이동합니다. 기본 테이블은 업데이트되지 않습니다.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>저장 프로시저에서 데이터 정의 언어(DDL) 사용  
 Visual FoxPro 저장 프로에서 테이블 만들기 또는 테이블 변경과 같은 DDL을 사용할 수 없습니다.  
  
 저장 프로시저에서 사용할 수 있는 언어에 대한 자세한 내용은 [규칙, 트리거, 기본값 및 저장 프로시저 에 대한 지원을](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)참조하십시오.  
  
## <a name="using-positioned-updates"></a>위치 업데이트 사용  
 드라이버는 위치 업데이트를 지원하지 않습니다. SQL WHERE 절을 사용하여 업데이트할 행을 식별합니다.  
  
## <a name="using-the-set-ansi-command"></a>ANSI 설정 명령 사용  
 Visual FoxPro 개발자인 경우 VISUAL FoxPro에 대한 기본 설정과 달리 SET ANSI의 기본 설정이 드라이버에 대해 ON인지 알고 있어야 합니다. SET ANSI에 대한 기본 ON 설정을 사용하면 Visual FoxPro 데이터 원본이 일반적으로 정확한 비교를 수행하는 다른 ODBC 데이터 원본과 일관되게 행동할 수 있습니다. 기본 설정을 변경할 수 있습니다. 자세한 내용은 [ANSI 설정](../../odbc/microsoft/set-ansi-command.md)을 참조하십시오.

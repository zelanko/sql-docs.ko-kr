---
title: 문제 해결 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
ms.openlocfilehash: 4eeb6210b9bce124e16a1b4e666dee03c1d992be
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67912383"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>문제 해결(Visual FoxPro ODBC 드라이버)
다음 섹션에서는 Visual FoxPro ODBC 드라이버를 사용 하는 동안 발생할 수 있는 문제를 해결 하 고 성능을 향상 시키는 방법을 설명 합니다.  
  
## <a name="accessing-parameterized-views"></a>매개 변수가 있는 뷰 액세스  
 드라이버를 사용 하 여 Visual FoxPro 데이터베이스에서 매개 변수가 있는 보기에 액세스할 수 없습니다. 매개 변수가 있는 뷰는 뷰의 SQL **SELECT** 문에 where 절을 만듭니다 .이는 매개 변수에 제공 된 값을 사용 하 여 작성 된 where 절의 조건을 충족 하는 레코드로 다운로드 되는 레코드를 제한 하는 것입니다. 드라이버는 뷰에 매개 변수를 전달 하는 기능을 지원 하지 않으므로 드라이버를 사용 하 여 매개 변수가 있는 뷰에 액세스 하려고 하면 오류가 발생 합니다.  
  
 매개 변수 값은 런타임에 제공 될 수도 있고 뷰에 프로그래밍 방식으로 전달 될 수도 있습니다.  
  
## <a name="accessing-remote-views"></a>원격 보기 액세스  
 드라이버를 사용 하 여 Visual FoxPro 데이터베이스의 원격 보기에는 액세스할 수 없습니다. 원격 보기는 FoxPro가 아닌 데이터 또는 FoxPro와 FoxPro가 아닌 데이터의 조합에 액세스 하는 뷰입니다. 원격 뷰에 액세스 하려면 Visual FoxPro를 사용 합니다.  
  
## <a name="deleting-records"></a>레코드 삭제  
 드라이버를 사용 하 여 레코드 삭제를 표시할 수 있지만 데이터베이스에서 레코드를 영구적으로 제거할 수는 없습니다. 테이블에서 레코드를 영구적으로 제거 하려면 Visual FoxPro를 사용 합니다.  
  
## <a name="increasing-performance-using-background-fetching"></a>백그라운드 페치를 사용 하 여 성능 향상  
 드라이버의 백그라운드 인출 기능을 사용 하 여 대량 페치 시 성능을 향상 시킬 수 있습니다. 백그라운드 페치는 개별 스레드를 사용 하 여 특정 데이터 원본에서 요청 된 데이터를 인출 합니다.  
  
 다음 방법 중 하나를 사용 하 여 데이터 원본에 대 한 백그라운드 페치를 사용할 수 있습니다.  
  
-   [ODBC Visual FoxPro 설정 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)에서 **백그라운드에서 데이터 페치** 확인란을 선택 합니다.  
  
-   연결 문자열에서 BackgroundFetch attribute 키워드를 사용 합니다.  
  
 연결 문자열 특성 키워드에 대 한 자세한 내용은 [연결 문자열 사용](../../odbc/microsoft/using-connection-strings.md)을 참조 하세요.  
  
## <a name="updating-multitiered-views"></a>다중 계층 뷰 업데이트  
 다중 계층 뷰는 기본 테이블이 아닌 하나 이상의 뷰를 기반으로 하는 뷰입니다. 다중 계층 뷰에서 데이터를 업데이트 하는 경우 최상위 뷰의 기반 뷰로 업데이트가 한 수준 아래로 이동 합니다. 기본 테이블은 업데이트 되지 않습니다.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>저장 프로시저에서 DDL (데이터 정의 언어) 사용  
 CREATE TABLE 또는 ALTER TABLE과 같은 DDL은 Visual FoxPro 저장 프로시저에서 사용할 수 없습니다.  
  
 저장 프로시저에서 사용할 수 있는 언어에 대 한 자세한 내용은 [규칙, 트리거, 기본값 및 저장 프로시저에 대 한 지원](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)을 참조 하세요.  
  
## <a name="using-positioned-updates"></a>위치 지정 업데이트 사용  
 드라이버에서 위치 지정 업데이트를 지원 하지 않습니다. SQL WHERE 절을 사용 하 여 업데이트 하려는 행을 식별할 수 있습니다.  
  
## <a name="using-the-set-ansi-command"></a>SET ANSI 명령 사용  
 Visual FoxPro 개발자 인 경우에는 드라이버에 대 한 기본 설정인 SET ANSI가 ON Visual FoxPro의 기본 설정과 달리 ON으로 설정 되어 있음을 알아야 합니다. SET ANSI의 기본 설정에서는 Visual FoxPro 데이터 원본이 일반적으로 정확한 비교를 수행 하는 다른 ODBC 데이터 원본과 일관 되 게 동작할 수 있습니다. 기본 설정을 변경할 수 있습니다. 자세한 내용은 [ANSI 설정](../../odbc/microsoft/set-ansi-command.md)을 참조 하세요.

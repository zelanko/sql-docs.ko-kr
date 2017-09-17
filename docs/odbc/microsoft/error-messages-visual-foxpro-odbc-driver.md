---
title: "오류 메시지 (Visual FoxPro ODBC 드라이버) | Microsoft Docs"
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
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e561aab3359acb1f236aea38e76da33289e630ef
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>오류 메시지 (Visual FoxPro ODBC 드라이버)
오류가 발생 하면 Visual FoxPro 드라이버에서 다음 정보를 반환 합니다.  
  
-   원시 오류 번호 및 오류 메시지 텍스트  
  
-   SQLSTATE (ODBC 오류 코드) 및 오류 메시지 텍스트  
  
 호출 하 여이 오류 정보에 액세스 [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)합니다.  
  
## <a name="native-errors"></a>네이티브 오류  
 Visual FoxPro 드라이버는 데이터 원본에서 발생 하는 오류에 대 한 원시 오류 번호 및 오류 메시지 텍스트를 반환 합니다. 원시 오류 번호 목록에 대 한 참조 [Visual FoxPro ODBC 드라이버 기본 오류 메시지](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)합니다.  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE(ODBC 오류 코드)  
 검색 하 여 Visual FoxPro 드라이버에서 반환 하는 오류에 대 한 드라이버는 반환 된 원시 오류 번호를 적절 한 SQLSTATE에 매핑됩니다. Visual FoxPro 드라이버가 SQLSTATE S1000 반환 합니다. 원시 오류 번호를 매핑할 ODBC 오류 코드가 없는 경우 (일반 오류).  
  
 목록이 해당 Visual FoxPro 오류에 대 한 Visual FoxPro ODBC 드라이버에 의해 생성 된 SQLSTATE 값에 대 한 참조 [ODBC 오류 코드](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)합니다.  
  
## <a name="syntax"></a>구문  
 오류 메시지는 다음과 같은 형식에 포함:  
  
 **[** *공급 업체* **] [** *ODBC_component* **]** *error_message*  
  
 다음 표에 정의 된 대로 대괄호 ()는 접두사 오류의 출처를 식별 합니다.  
  
|데이터 원본|접두사|값|  
|-----------------|------------|-----------|  
|드라이버 관리자|[공급 업체]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC 드라이버 관리자]<br />해당 사항 없음|  
|Visual FoxPro 드라이버|공급 업체]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Visual FoxPro ODBC 드라이버]<br />해당 사항 없음|  
  
 예를 들어, Visual FoxPro ODBC 드라이버를 찾을 수 없는 파일 employee.dbf 하는 경우에 다음과 같은 오류 메시지가 반환할 수 있습니다이:  
  
 "[*Microsoft*] [*ODBC Visual FoxPro 드라이버*] 'employee.dbf' 파일이 존재 하지 않습니다"

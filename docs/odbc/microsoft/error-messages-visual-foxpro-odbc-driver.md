---
title: 오류 메시지 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b24db48d6a76c221e72944e8e5e6826cb8d5d55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127984"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>오류 메시지(Visual FoxPro ODBC 드라이버)
오류가 발생 하는 경우 Visual FoxPro 드라이버에 다음 정보를 반환 합니다.  
  
-   원시 오류 번호 및 오류 메시지 텍스트  
  
-   SQLSTATE (ODBC 오류 코드) 및 오류 메시지 텍스트  
  
 호출 하 여이 오류 정보에 액세스 [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)합니다.  
  
## <a name="native-errors"></a>원시 오류  
 Visual FoxPro 드라이버에는 데이터 원본에서 발생 하는 오류에 대 한 원시 오류 번호 및 오류 메시지 텍스트를 반환 합니다. 원시 오류 번호 목록은 참조 하세요 [Visual FoxPro ODBC 드라이버 원시 오류 메시지로](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)합니다.  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE(ODBC 오류 코드)  
 드라이버를 검색 하 여 Visual FoxPro 드라이버에서 반환 되는 오류에 대 한 적절 한 SQLSTATE 반환 된 원시 오류 번호를 매핑합니다. Visual FoxPro 드라이버 SQLSTATE S1000 반환 원시 오류 번호를 매핑할 ODBC 오류 코드에 없는 경우 (일반 오류).  
  
 해당 Visual FoxPro 오류에 대 한 Visual FoxPro ODBC 드라이버에서 생성 된 SQLSTATE 값 목록을 참조 하세요 [ODBC 오류 코드](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)합니다.  
  
## <a name="syntax"></a>구문  
 오류 메시지의 형식이:  
  
 **[** *vendor* **][** *ODBC_component* **]** *error_message*  
  
 다음 표에 정의 된 대로 대괄호 () 접두사 오류의 출처를 식별 합니다.  
  
|데이터 원본|접두사|값|  
|-----------------|------------|-----------|  
|드라이버 관리자|[vendor]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC 드라이버 관리자]<br />해당 사항 없음|  
|Visual FoxPro 드라이버|공급 업체]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Visual FoxPro ODBC 드라이버]<br />해당 사항 없음|  
  
 예를 들어, Visual FoxPro ODBC 드라이버 파일 employee.dbf 찾을 수 없습니다, 하는 경우 다음 오류 메시지가 반환할 수 있습니다.  
  
 "[*Microsoft*] [*Visual FoxPro Odbc*] 'employee.dbf' 파일이 존재 하지 않습니다"

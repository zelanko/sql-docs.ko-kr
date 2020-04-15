---
title: 오류 메시지(비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31f894e58da93fe6091dba306f8b765d14bac2cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286403"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>오류 메시지(Visual FoxPro ODBC 드라이버)
오류가 발생하면 Visual FoxPro 드라이버는 다음 정보를 반환합니다.  
  
-   네이티브 오류 번호 및 오류 메시지 텍스트  
  
-   SQLSTATE(ODBC 오류 코드) 및 오류 메시지 텍스트  
  
 [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)를 호출하여 이 오류 정보에 액세스합니다.  
  
## <a name="native-errors"></a>네이티브 오류  
 데이터 원본에서 발생하는 오류의 경우 Visual FoxPro 드라이버는 기본 오류 번호 및 오류 메시지 텍스트를 반환합니다. 네이티브 오류 번호 목록은 [Visual FoxPro ODBC 드라이버 네이티브 오류 메시지를](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)참조하십시오.  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE(ODBC 오류 코드)  
 Visual FoxPro 드라이버에서 검색되고 반환되는 오류의 경우 드라이버는 반환된 기본 오류 번호를 해당 SQLSTATE에 매핑합니다. 기본 오류 번호에 매핑할 ODBC 오류 코드가 없는 경우 Visual FoxPro 드라이버는 SQLSTATE S1000(일반 오류)을 반환합니다.  
  
 해당 Visual FoxPro 오류에 대해 Visual FoxPro ODBC 드라이버에서 생성된 SQLSTATE 값 목록은 [ODBC 오류 코드를](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)참조하십시오.  
  
## <a name="syntax"></a>구문  
 오류 메시지에는 다음과 같은 형식이 있습니다.  
  
 **【** *공급 업체* **】[** *ODBC_component* **]** *error_message*  
  
 괄호([])의 접두사는 다음 표에 정의된 오류의 원인을 식별합니다.  
  
|데이터 원본|접두사|값|  
|-----------------|------------|-----------|  
|드라이버 관리자|【벤더】<br />【ODBC_component】<br />【data_source】|[마이크로 소프트]<br />[ODBC 드라이버 매니저]<br />해당 없음|  
|비주얼 폭스프로 드라이버|공급 업체]<br />【ODBC_component】<br />【data_source】|[마이크로 소프트]<br />[ODBC 비주얼 폭스프로 드라이버]<br />해당 없음|  
  
 예를 들어 Visual FoxPro ODBC 드라이버가 파일 employee.dbf를 찾을 수 없는 경우 다음과 같은 오류 메시지가 반환될 수 있습니다.  
  
 "[*마이크로 소프트*][*ODBC 비주얼 폭스 프로 드라이버*] 파일 'employee.dbf'가 존재하지 않습니다"

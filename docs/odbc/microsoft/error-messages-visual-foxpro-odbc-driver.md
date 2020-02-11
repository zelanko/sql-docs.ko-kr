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
ms.openlocfilehash: 6072a6e317ab87118376b08790fc0fb49c495e3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67952510"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>오류 메시지(Visual FoxPro ODBC 드라이버)
오류가 발생 하면 Visual FoxPro 드라이버에서 다음 정보를 반환 합니다.  
  
-   네이티브 오류 번호 및 오류 메시지 텍스트  
  
-   SQLSTATE (ODBC 오류 코드) 및 오류 메시지 텍스트  
  
 [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)를 호출 하 여이 오류 정보에 액세스 합니다.  
  
## <a name="native-errors"></a>기본 오류  
 데이터 원본에서 오류가 발생 하는 경우 Visual FoxPro 드라이버는 원시 오류 번호와 오류 메시지 텍스트를 반환 합니다. 네이티브 오류 번호 목록은 [Visual FOXPRO ODBC 드라이버 네이티브 오류 메시지](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)를 참조 하세요.  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE(ODBC 오류 코드)  
 Visual FoxPro 드라이버에서 검색 되 고 반환 되는 오류의 경우 드라이버는 반환 된 원시 오류 번호를 적절 한 SQLSTATE에 매핑합니다. 네이티브 오류 번호에 매핑할 ODBC 오류 코드가 없으면 Visual FoxPro 드라이버가 SQLSTATE S1000 (일반 오류)를 반환 합니다.  
  
 해당 Visual foxpro 오류에 대해 Visual FoxPro ODBC 드라이버에 의해 생성 된 SQLSTATE 값 목록은 [ODBC 오류 코드](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)를 참조 하십시오.  
  
## <a name="syntax"></a>구문  
 오류 메시지의 형식은 다음과 같습니다.  
  
 **[** *공급 업체* **] [** *ODBC_component* **]** *error_message*  
  
 대괄호 ([]) 안의 접두사는 다음 표에 정의 된 대로 오류의 원인을 식별 합니다.  
  
|데이터 원본|접두사|값|  
|-----------------|------------|-----------|  
|드라이버 관리자|업체인<br />[ODBC_component]<br />[data_source]|Microsoft<br />[ODBC 드라이버 관리자]<br />해당 없음|  
|Visual FoxPro 드라이버|업체인<br />[ODBC_component]<br />[data_source]|Microsoft<br />[ODBC Visual FoxPro 드라이버]<br />해당 없음|  
  
 예를 들어, Visual FoxPro ODBC 드라이버에서 employee. .dbf 파일을 찾을 수 없는 경우 다음 오류 메시지가 반환 될 수 있습니다.  
  
 "[*Microsoft*] [*ODBC Visual FoxPro Driver*] 파일 ' employee. .dbf '가 없습니다."

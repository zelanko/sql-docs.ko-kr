---
title: 지원되는 데이터 유형(비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], data types
- FoxPro ODBC driver [ODBC], data types
- data types [ODBC], Visual FoxPro ODBC driver
ms.assetid: ab529cc6-d157-4b35-b6f9-6ffd09af098c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3fc28464a7c14f9801473cc125b0e90c50247d68
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301103"
---
# <a name="supported-data-types-visual-foxpro-odbc-driver"></a>지원되는 데이터 형식(Visual FoxPro ODBC 드라이버)
드라이버에서 지원하는 데이터 형식 목록은 ODBC API와 Microsoft 쿼리를 통해 표시됩니다.  
  
## <a name="data-types-in-c-applications"></a>C 애플리케이션의 데이터 유형  
 C 또는 C++ 응용 프로그램에서 [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) 함수를 사용하여 Visual FoxPro ODBC 드라이버에서 지원하는 데이터 형식 목록을 가져올 수 있습니다.  
  
## <a name="data-types-in-applications-using-microsoft-query"></a>Microsoft 쿼리를 사용하는 응용 프로그램의 데이터 유형  
 응용 프로그램에서 Microsoft 쿼리를 사용하여 Visual FoxPro 데이터 원본에 새 테이블을 만드는 경우 Microsoft 쿼리에 **새 테이블 정의** 대화 상자가 표시됩니다. **필드 설명**에서 **유형** 상자에는 단일 문자로 표시되는 [Visual FoxPro 필드 데이터 형식이](../../odbc/microsoft/visual-foxpro-field-data-types.md)나열됩니다.

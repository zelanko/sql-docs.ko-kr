---
title: 지원 되는 데이터 형식 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e2d23ddc5fdd00db45aee235e96f13a8cf08082a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68080779"
---
# <a name="supported-data-types-visual-foxpro-odbc-driver"></a>지원되는 데이터 형식(Visual FoxPro ODBC 드라이버)
드라이버에서 지 원하는 데이터 형식 목록은 ODBC API 및 Microsoft Query를 통해 제공 됩니다.  
  
## <a name="data-types-in-c-applications"></a>C 응용 프로그램의 데이터 형식  
 C 또는 c + + 응용 프로그램에서 [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) 함수를 사용 하 여 VISUAL FoxPro ODBC 드라이버에서 지 원하는 데이터 형식의 목록을 가져올 수 있습니다.  
  
## <a name="data-types-in-applications-using-microsoft-query"></a>Microsoft 쿼리를 사용 하는 응용 프로그램의 데이터 형식  
 응용 프로그램에서 Microsoft Query를 사용 하 여 Visual FoxPro 데이터 원본에 새 테이블을 만드는 경우 Microsoft Query는 **새 테이블 정의** 대화 상자를 표시 합니다. **필드 설명**의 **유형** 상자에는 단일 문자로 표시 되는 [Visual FoxPro 필드 데이터 형식이](../../odbc/microsoft/visual-foxpro-field-data-types.md)나열 됩니다.

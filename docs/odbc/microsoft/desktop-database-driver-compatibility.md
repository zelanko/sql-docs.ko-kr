---
title: 데스크톱 데이터베이스 드라이버 호환성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d081d53458ec59eb2ac9f05c5c1d47d6991b5010
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240356"
---
# <a name="desktop-database-driver-compatibility"></a>데스크톱 데이터베이스 드라이버 호환성
유니코드는 소프트웨어 문자 인코딩 메서드는 2 바이트의 고정된 폭으로 모든 문자를 처리 합니다. 이 메서드는 1 바이트에서 문자를 나타내므로 256 자로 제한 되는 Windows ANSI 문자 인코딩을 하는 대신 사용 됩니다. 유니코드 65,000 개 문자를 나타낼 수, 있으므로 수용 하는 것 인 문자 표현 되지 않는 다양 한 언어 ANSI 인코딩.  
  
 ODBC 3.5 (또는 이상) 드라이버 관리자는 유니코드를 지원 합니다. 이 두 가지 주요 영역에 영향을 줍니다: 함수 호출 및 문자열 데이터 형식입니다. 드라이버 관리자 맵 함수 문자열 인수 및 응용 프로그램 및 드라이버에서 필요에 따라 문자열 데이터를 유니코드를 지원 또는 ANSI 설정 둘 다이 가능 합니다.  
  
 ODBC 3.5 (또는 이상) 드라이버 관리자는 응용 프로그램을 유니코드 및 ANSI 응용 프로그램을 사용 하 여 유니코드 드라이버의 사용을 지원합니다. 또한 ANSI 응용 프로그램을 사용 하 여 ANSI 드라이버를 사용을 지원합니다. 드라이버 관리자는 ANSI 드라이버를 사용 하는 유니코드 응용 프로그램에 대 한 제한 된 유니코드에서 ANSI로 매핑을 제공 합니다. 이렇게 하면 모든 기존 ISAM 파일 형식의 지원과 3.5 Jet 데이터베이스에 대 한 액세스.  
  
 경우 ANSI 응용 프로그램은 ODBC 데스크톱 데이터베이스 드라이버 4.0을 사용 하 여 및 Microsoft Access 4.0 액세스 또는 Jet 4.0에서는 다양 한 버전에도 드라이버에서 데이터 형식으로 SQL_CHAR, SQL_VARCHAR 또는 SQL_LONGVARCHAR에 노출 하는 나중에 합니다. 이전 버전의 Jet SQL_WCHAR, SQL_WVARCHAR 및 SQL_WLONGVARCHAR 지원 하지 않습니다. 이 제한 사항은 이전 형식 Jet 4.0 데이터베이스 엔진용을 사용 하 여 사용 된 경우에도 적용 됩니다.  
  
 ODBC 사용 하 여 유니코드 문제에 관한 자세한 내용은 [유니코드](../../odbc/reference/develop-app/unicode.md) 프로그래밍 고려 사항에서입니다.

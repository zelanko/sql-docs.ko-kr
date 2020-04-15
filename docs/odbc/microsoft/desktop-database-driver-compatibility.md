---
title: 데스크톱 데이터베이스 드라이버 호환성 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89eea7ab112eaefdc73c7cbc72ee3555797c7efd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303524"
---
# <a name="desktop-database-driver-compatibility"></a>데스크톱 데이터베이스 드라이버 호환성
유니코드는 모든 문자를 2바이트의 고정 너비로 처리하는 소프트웨어 문자 인코딩 방법입니다. 이 메서드는 Windows ANSI 문자 인코딩에 대 한 대안으로 사용 됩니다., 한 바이트에서 문자를 나타내는 때문에, 256 문자로 제한 됩니다. 유니코드는 65,000자 이상을 나타낼 수 있으므로 ANSI 인코딩에 문자가 표시되지 않는 많은 언어를 수용합니다.  
  
 ODBC 3.5(이상) 드라이버 관리자는 유니코드가 활성화되어 있습니다. 이는 함수 호출과 문자열 데이터 형식의 두 가지 주요 영역에 영향을 줍니다. 드라이버 관리자는 응용 프로그램과 드라이버에서 요구하는 대로 함수 문자열 인수 및 문자열 데이터를 매핑하며, 둘 다 유니코드 지원 또는 ANSI 지원일 수 있습니다.  
  
 ODBC 3.5(이상) 드라이버 관리자는 유니코드 응용 프로그램과 ANSI 응용 프로그램을 모두 사용하여 유니코드 드라이버를 사용합니다. 또한 ANSI 응용 프로그램을 사용하여 ANSI 드라이버를 사용할 수 있습니다. 드라이버 관리자는 ANSI 드라이버로 작업하는 유니코드 응용 프로그램에 대해 제한된 유니코드-ANSI 매핑을 제공합니다. 이렇게 하면 Jet 3.5 데이터베이스에 액세스하고 모든 기존 ISAM 파일 형식을 지원할 수 있습니다.  
  
 ANSI 응용 프로그램이 ODBC 데스크톱 데이터베이스 드라이버 4.0을 사용하고 Microsoft Access 4.0 이상에 액세스하는 경우 Jet 4.0이 와이드 버전을 지원하더라도 드라이버는 데이터 형식을 SQL_CHAR, SQL_VARCHAR 또는 SQL_LONGVARCHAR 노출합니다. 이전 버전의 Jet는 SQL_WCHAR, SQL_WVARCHAR 및 SQL_WLONGVARCHAR 지원하지 않습니다. 이 제한은 Jet 4.0 데이터베이스 엔진에서 이전 형식을 사용하는 경우에도 적용됩니다.  
  
 ODBC와 관련된 유니코드 문제에 대한 자세한 내용은 프로그래밍 고려 사항의 [유니코드를](../../odbc/reference/develop-app/unicode.md) 참조하십시오.

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
ms.openlocfilehash: 31263162526b6bd2e0a116a473f09f9e2caeba94
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077279"
---
# <a name="desktop-database-driver-compatibility"></a>데스크톱 데이터베이스 드라이버 호환성
유니코드는 모든 문자를 고정 너비가 2 바이트인 것으로 처리 하는 소프트웨어 문자 인코딩의 메서드입니다. 이 메서드는 Windows ANSI 문자 인코딩에 대 한 대 안으로 사용 되며, 1 바이트의 문자를 나타내므로 256 자로 제한 됩니다. 유니코드는 65000 자를 초과 하 여 나타낼 수 있으므로, ANSI 인코딩으로 표시 되지 않는 문자를 포함 하는 많은 언어를 수용 합니다.  
  
 ODBC 3.5 이상 드라이버 관리자는 유니코드를 사용할 수 있습니다. 이는 함수 호출 및 문자열 데이터 형식과 같은 두 가지 주요 영역에 영향을 줍니다. 드라이버 관리자는 응용 프로그램 및 드라이버에서 요구 하는 함수 문자열 인수 및 문자열 데이터를 매핑합니다. 둘 다 유니코드를 사용 하도록 설정 하거나 ANSI를 사용할 수 있습니다.  
  
 ODBC 3.5 이상 드라이버 관리자는 유니코드 응용 프로그램과 ANSI 응용 프로그램 모두에서 유니코드 드라이버를 사용할 수 있도록 지원 합니다. Ansi 응용 프로그램에 ANSI 드라이버를 사용 하는 것도 지원 합니다. 드라이버 관리자는 ANSI 드라이버를 사용 하는 유니코드 응용 프로그램에 대해 제한 된 유니코드-ANSI 매핑을 제공 합니다. 이를 통해 Jet 3.5 데이터베이스 및 모든 기존 ISAM 파일 형식의 지원에 액세스할 수 있습니다.  
  
 ANSI 응용 프로그램에서 ODBC 데스크톱 데이터베이스 드라이버 4.0를 사용 하 고 Microsoft Access 4.0 이상에 액세스 하면 Jet 4.0에서 wide version을 지 원하는 경우에도 드라이버는 데이터 형식을 SQL_CHAR, SQL_VARCHAR 또는 SQL_LONGVARCHAR으로 노출 합니다. 이전 버전의 Jet는 SQL_WCHAR, SQL_WVARCHAR 및 SQL_WLONGVARCHAR를 지원 하지 않습니다. 이 제한은 Jet 4.0 데이터베이스 엔진에서 이전 형식이 사용 되는 경우에도 적용 됩니다.  
  
 ODBC의 유니코드 문제에 대 한 자세한 내용은 프로그래밍 고려 사항의 [유니코드](../../odbc/reference/develop-app/unicode.md) 를 참조 하십시오.

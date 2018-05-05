---
title: 데스크톱 데이터베이스 드라이버 호환성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5fb1e93c996b68a3110449dab797beb5c93208b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="desktop-database-driver-compatibility"></a>데스크톱 데이터베이스 드라이버 호환성
유니코드는 소프트웨어 문자 인코딩 메서드는 2 바이트의 고정된 폭을 가진 것으로 모든 문자를 처리 합니다. 이 메서드는 1 바이트의 문자를 나타내기 때문에 256 자로 제한 Windows ANSI 문자 인코딩을 하는 대신 사용 됩니다. 해당 문자가 표현 되지 않는 많은 언어를 수용 유니코드 65000 개 문자를 나타낼 수 있습니다, 때문에 ANSI 인코딩으로 합니다.  
  
 ODBC 3.5 또는 그 이상의 드라이버 관리자는 유니코드를 지원 합니다. 두 가지 주요 영역을 미치면: 함수 호출 하 고 문자열 데이터 형식입니다. 드라이버 관리자 지도 함수 문자열 인수 및 응용 프로그램 및 드라이버에서 필요에 따라 문자열 데이터를 유니코드 사용 가능 또는 ANSI 설정 중 하나는 모두 일 수 있습니다.  
  
 ODBC 3.5 또는 그 이상의 드라이버 관리자 유니코드 응용 프로그램 및 ANSI 응용 프로그램이 모두와 유니코드 드라이버의 사용을 지원 합니다. 또한 ANSI 응용 프로그램으로 ANSI 드라이버의 사용을 지원 합니다. 드라이버 관리자 ANSI 드라이버를 사용 하는 유니코드 응용 프로그램에 대 한 제한 된 유니코드에서 ANSI 매핑을 제공 합니다. 따라서 Jet 3.5 데이터베이스 및 모든 기존 ISAM 파일 형식 지원에 액세스할 수 있습니다.  
  
 ANSI 응용 프로그램이 ODBC 데스크톱 데이터베이스 드라이버 4.0을 사용 하 여 및 액세스 하는 Microsoft Access 4.0 되거나 경우 Jet 4.0에서는 다양 한 버전을 지원 하지만 드라이버에서 데이터 형식으로 SQL_CHAR, SQL_VARCHAR 또는 SQL_LONGVARCHAR에 노출 하는 나중 합니다. 이전 버전의 Jet SQL_WCHAR, SQL_WVARCHAR 및 SQL_WLONGVARCHAR 지원 하지 않습니다. 이 제한은 Jet 4.0 데이터베이스 엔진과 함께 사용 되는 이전 형식 하는 경우에도 적용 됩니다.  
  
 유니코드 ODBC 문제에 관한 자세한 내용은 참조 하십시오. [유니코드](../../odbc/reference/develop-app/unicode.md) 프로그래밍 고려 사항에서입니다.

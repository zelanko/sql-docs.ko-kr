---
description: Odbc 테스트는 odbc 드라이버 및 odbc 드라이버 관리자를 테스트 하는 데 사용할 수 있는 ODBC 사용 응용 프로그램입니다.
title: ODBC 테스트
ms.custom: ''
ms.date: 09/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC test [ODBC]
- ODBC drivers [ODBC], testing
- gtrtst32.dll
- gtrts32w.dll [ODBC]
- odbct32w.exe [ODBC]
- odbcte32.exe [ODBC]
- testing ODBC drivers [ODBC]
ms.assetid: 7f13894c-5697-436c-be3d-fe16e1a02325
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39869fe1230be75d9a76e13b8ba3938ec31ee5ee
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288248"
---
# <a name="odbc-test"></a>ODBC 테스트

## <a name="about"></a>정보

Microsoft® ODBC 테스트는 odbc 드라이버 및 odbc 드라이버 관리자를 테스트 하는 데 사용할 수 있는 ODBC 사용 응용 프로그램입니다. ODBC 테스트는 [MDAC (Microsoft Data Access Components) 2.8 소프트웨어 개발 키트](https://www.microsoft.com/download/details.aspx?id=21995)의 일부로 포함 되어 있습니다.

ODBC 3.51에는 ANSI 및 유니코드 지원 버전의 ODBC 테스트가 모두 포함 되어 있습니다. 해당 파일은 다음과 같습니다.

- `Odbcte32.exe``Gtrtst32.dll`ANSI 버전의 경우 및입니다.

- `Odbct32w.exe``Gtrts32w.dll`유니코드 버전의 경우 및입니다.

ODBC 테스트를 사용 하려면 ODBC API, C 언어 및 SQL을 이해 해야 합니다. ODBC API에 대 한 자세한 내용은 [Odbc 프로그래머 참조](../odbc/reference/odbc-programmer-s-reference.md)를 참조 하세요.

설명서의이 섹션에 이전에 포함 되었던 도움말 항목은 이제 ODBC 테스트 프로그램에 포함 되어 있습니다. `Odbcte32.exe`또는 `Odbct32w.exe` 를 열고 **도움말** 메뉴를 연 다음 **도움말 항목**을 클릭 합니다.

64 비트 Microsoft Windows 운영 체제용 64 비트 버전의 응용 프로그램은 별도의 파일 이더라도 32 비트 버전과 동일한 이름을 갖고 있습니다. 즉, ODBC 테스트 64 비트 버전의 유니코드 버전 `odbct32w.exe` 이름은입니다.

## <a name="open-source"></a>오픈 소스

ODBC 테스트는 오픈 소스입니다. 코드를 확인 하 고 ODBC 테스트의 최신 버전을 직접 작성 하려면 [Odbc 테스트에 대 한 GitHub 리포지토리](https://github.com/microsoft/ODBCTest)로 이동 합니다.

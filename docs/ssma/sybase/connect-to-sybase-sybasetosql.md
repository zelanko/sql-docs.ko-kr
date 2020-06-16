---
title: Sybase에 연결 (SybaseToSQL) | Microsoft Docs
description: SAP ase 인스턴스에 연결 하 여 Sybase 용 SSMA (SAP ASE)를 사용 하 여 마이그레이션을 시작 합니다. Sybase에 연결 대화 상자를 사용 합니다.
author: nahk-ivanov
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
ms.author: alexiva
ms.openlocfilehash: 72c6797bfc8d673069cab41002a4a93596d7e5d9
ms.sourcegitcommit: e572f1642f588b8c4c75bc9ea6adf4ccd48a353b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84779415"
---
# <a name="connect-to-sybase-sybasetosql"></a>Sybase에 연결(SybaseToSQL)

**Sybase에 연결** 대화 상자를 사용 하 여 마이그레이션하려는 Sybase 적응 서버 엔터프라이즈 (ASE) 인스턴스에 연결할 수 있습니다.

이 대화 상자에 액세스 하려면 **파일** 메뉴에서 **Sybase에 연결**을 선택 합니다. 이전에 연결한 경우이 명령은 **Sybase에 다시 연결**됩니다.

## <a name="options"></a>옵션

**공급자**  
Sybase 서버에 연결 하기 위해 컴퓨터에서 설치 된 공급자를 선택 합니다.

**모드**  
표준 또는 고급 연결 모드를 선택 합니다. 표준 모드에서는 서버 이름, 포트, 사용자 이름 및 암호에 대 한 값을 입력 하거나 선택 합니다. 고급 모드에서는 연결 문자열을 제공 합니다.

**서버 이름**  
적응 서버의 이름 또는 IP 주소를 입력 하거나 선택 합니다. 기본 서버 이름은 컴퓨터 이름과 동일 합니다. 표준 모드 옵션입니다.

**서버 포트**  
ASE에 대 한 연결에 기본 포트가 아닌 포트를 사용 하는 경우 포트 번호를 입력 합니다. 기본 포트 번호는 5000입니다. 표준 모드 옵션입니다.
  
**사용자 이름**  
ASE에 연결 하는 데 사용 되는 사용자 이름을 입력 합니다. 표준 모드 옵션입니다.

**암호**  
사용자 이름에 대한 암호를 입력합니다. 표준 모드 옵션입니다.

**연결 문자열**  
ASE에 대 한 연결에 대 한 전체 연결 문자열을 입력 합니다.

연결 문자열은 매개 변수 이름 및 값 쌍으로 구성 됩니다. 매개 변수의 이름은 사용 중인 공급자에 따라 달라 집니다.

**다양 한 공급자에 대 한 연결 매개 변수는 다음과 같습니다.**

1. **OLE DB 공급자** 에 대 한 연결 매개 변수

   |설정|Sybase 12.5 매개 변수|Sybase 15 매개 변수|
   |-----------|-------------------------|-----------------------|
   |서버 이름|서버 이름|서버|
   |포트|서버 포트 주소|포트|
   |사용자 이름|사용자 ID|사용자 ID|
   |암호|암호|암호|
   |공급자|공급자|공급자|

   Sybase ASE 12.5의 경우 연결 문자열의 예는 다음과 같습니다.

   `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`

   Sybase ASE 15의 경우 연결 문자열의 예는 다음과 같습니다.

   `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`

2. **ODBC 공급자** 에 대 한 연결 매개 변수

   |설정|Sybase 12.5/15 매개 변수|
   |-----------|-----------------------------|
   |드라이버 이름|요소|
   |서버 이름|서버|
   |사용자 이름|Uid|
   |암호|Pwd|
   |포트 번호|포트|

   Sybase ASE 12.5 또는 15의 경우 연결 문자열의 예는 다음과 같습니다.

   `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`

3. **ADO.NET Provider** 에 대 한 연결 매개 변수

   |설정|Sybase 12.5/15 매개 변수|
   |-----------|-----------------------------|
   |서버 이름|서버|
   |사용자 이름|Uid|
   |암호|Pwd|
   |포트 번호|포트|

   ADO.NET Provider에 대 한 연결 문자열의 예는 다음과 같습니다.

   `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`

   자세한 내용은 ASE 설명서를 참조 하세요.

   이 옵션은 고급 모드 옵션입니다.

## <a name="next-steps"></a>다음 단계

마이그레이션 프로세스의 다음 단계는 [SQL Server에 연결](connect-to-sql-server-sybasetosql.md)하는 것입니다.

---
title: "Sybase (SybaseToSQL)에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: fe9cf1f66a181f252e644a6e610eb102776dc27d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-sybase-sybasetosql"></a>Sybase (SybaseToSQL)에 연결
사용 하 여는 **Sybase 연결할** 마이그레이션하려는 Sybase 적응형 Server Enterprise (ASE) 인스턴스를 연결 하는 대화 상자.  
  
이 대화 상자에 액세스 하려면는 **파일** 메뉴 선택 **Sybase 연결할**합니다. 이 명령은 이전에 연결한 경우 **Sybase 다시 연결**합니다.  
  
## <a name="options"></a>옵션  
**공급자**  
Sybase 서버에 연결 하기 위한 컴퓨터에 설치 되어 있는 공급자 중 하나를 선택 합니다.  
  
**모드**  
표준 또는 고급 연결 모드 중 하나를 선택 합니다. 표준 모드에서는 입력 하거나 서버 이름, 포트, 사용자 이름 및 암호에 대 한 값을 선택 합니다. 고급 모드에서는 연결 문자열을 제공 합니다.  
  
**서버 이름**  
입력 하거나 이름 또는 적응 서버의 IP 주소를 선택 합니다. 기본 서버 이름은 컴퓨터 이름과 같습니다. 표준 모드 옵션입니다.  
  
**서버 포트**  
기본이 아닌 포트 ASE에 대 한 연결을 사용 하는 경우에 포트 번호를 입력 합니다. 기본 포트 번호는 5000입니다. 표준 모드 옵션입니다.  
  
**사용자 이름**  
ASE에 연결 하는 데 사용 되는 사용자 이름을 입력 합니다. 표준 모드 옵션입니다.  
  
**암호**  
사용자 이름에 대한 암호를 입력합니다. 표준 모드 옵션입니다.  
  
**연결 문자열**  
ASE에는 연결에 대 한 전체 연결 문자열을 입력 합니다.  
  
연결 문자열 매개 변수 이름 / 값 쌍으로 구성 됩니다. 매개 변수의 이름이 사용 되는 공급자와는 다릅니다.  
  
**다양 한 공급자에 대 한 연결 매개 변수는 다음과 같습니다.**  
  
1.  에 대 한 연결 매개 변수 **OLE DB 공급자**  
  
    |설정|Sybase 12.5 매개 변수|Sybase 15 매개 변수|  
    |-----------|-------------------------|-----------------------|  
    |서버 이름|서버 이름|Server|  
    |포트|서버 포트 주소|포트|  
    |사용자 이름|사용자 ID|사용자 ID|  
    |암호|암호|암호|  
    |공급자|공급자|공급자|  
  
    Sybase ASE 12.5에 대 한 연결 문자열의 예는 다음과 같습니다.  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    Sybase ASE 15에 대 한 연결 문자열의 예는 다음과 같습니다.  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  에 대 한 연결 매개 변수 **ODBC 공급자**  
  
    |설정|Sybase 12.5/15 매개 변수|  
    |-----------|-----------------------------|  
    |드라이버 이름|드라이버|  
    |서버 이름|Server|  
    |사용자 이름|uid|  
    |암호|Pwd|  
    |포트 번호|포트|  
  
    Sybase ASE 12.5 또는 15에 대 한 연결 문자열의 예는 다음과 같습니다.  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  에 대 한 연결 매개 변수 **ADO.NET 공급자**  
  
    |설정|Sybase 12.5/15 매개 변수|  
    |-----------|-----------------------------|  
    |서버 이름|Server|  
    |사용자 이름|uid|  
    |암호|Pwd|  
    |포트 번호|포트|  
  
    ADO.NET 공급자에 대 한 연결 문자열의 예는 다음과 같습니다.  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
자세한 내용은 ASE 설명서를 참조 합니다.  
  
고급 모드 옵션입니다.  
  


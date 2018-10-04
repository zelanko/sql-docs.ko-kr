---
title: Sybase (SybaseToSQL)에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0805246d5b88138cfa97019d1e0cd524c82456c6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738079"
---
# <a name="connect-to-sybase-sybasetosql"></a>Sybase에 연결(SybaseToSQL)
사용 된 **Sybase에 연결** 마이그레이션하려는 Sybase 적응형 Server Enterprise (ASE) 인스턴스에 연결 대화 상자.  
  
이 대화 상자에 액세스 하는 **파일** 메뉴에서 **Sybase에 연결**합니다. 이전에 연결한 경우에 명령입니다 **Sybase에 다시 연결**합니다.  
  
## <a name="options"></a>변수  
**공급자**  
Sybase 서버에 연결할 컴퓨터에 설치 된 공급자 중 하나를 선택 합니다.  
  
**모드**  
표준 또는 고급 연결 모드 중 하나를 선택 합니다. 표준 모드에서는 입력 하거나 서버 이름, 포트, 사용자 이름 및 암호에 대 한 값을 선택 합니다. 고급 모드에서 연결 문자열을 제공 합니다.  
  
**서버 이름**  
입력 하거나 이름 또는 적응 서버의 IP 주소를 선택 합니다. 기본 서버 이름은 컴퓨터 이름과 동일 합니다. 표준 모드 옵션입니다.  
  
**서버 포트**  
기본이 아닌 포트를 ASE에 대 한 연결을 사용 하는 경우에 포트 번호를 입력 합니다. 기본 포트 번호는 5000입니다. 표준 모드 옵션입니다.  
  
**사용자 이름**  
ASE에 연결 하는 데 사용 되는 사용자 이름을 입력 합니다. 표준 모드 옵션입니다.  
  
**암호**  
사용자 이름에 대한 암호를 입력합니다. 표준 모드 옵션입니다.  
  
**연결 문자열**  
ASE에는 연결에 대 한 전체 연결 문자열을 입력 합니다.  
  
연결 문자열 매개 변수 이름 / 값 쌍으로 구성 됩니다. 사용 중인 공급자를 사용 하 여 매개 변수 이름은 달라 집니다.  
  
**다양 한 공급자에 대 한 연결 매개 변수는 다음과 같습니다.**  
  
1.  연결 매개 변수를 **OLE DB Provider**  
  
    |설정|Sybase 12.5 매개 변수|Sybase 15 매개 변수|  
    |-----------|-------------------------|-----------------------|  
    |서버 이름|서버 이름|서버|  
    |포트|서버 포트 주소|포트|  
    |사용자 이름|사용자 ID|사용자 ID|  
    |암호|암호|암호|  
    |공급자|공급자|공급자|  
  
    Sybase ASE 12.5에 대 한 연결 문자열의 예는 다음과 같습니다.  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    Sybase ASE 15 일에 대 한 연결 문자열의 예는 다음과 같습니다.  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  연결 매개 변수를 **ODBC 공급자**  
  
    |설정|Sybase 12.5/15 매개 변수|  
    |-----------|-----------------------------|  
    |드라이버 이름|드라이버|  
    |서버 이름|서버|  
    |사용자 이름|uid|  
    |암호|pwd|  
    |포트 번호|포트|  
  
    Sybase ASE 12.5 또는 15의 경우 연결 문자열의 예는 다음과 같습니다.  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  연결 매개 변수를 **ADO.NET 공급자**  
  
    |설정|Sybase 12.5/15 매개 변수|  
    |-----------|-----------------------------|  
    |서버 이름|서버|  
    |사용자 이름|uid|  
    |암호|pwd|  
    |포트 번호|포트|  
  
    ADO.NET 공급자에 대 한 연결 문자열의 예는 다음과 같이.  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
자세한 내용은 ASE 설명서를 참조 하십시오.  
  
이 고급 모드 옵션입니다.  
  

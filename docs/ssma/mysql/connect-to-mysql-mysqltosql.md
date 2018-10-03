---
title: MySQL (MySQLToSQL)에 연결 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2a68b60a954e6cd89698d4e906f8272f08d6b11e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673161"
---
# <a name="connect-to-mysql-mysqltosql"></a>MySQL에 연결(MySQLToSQL)
사용 된 **MySQL에 연결** 마이그레이션하려는 MySQL 데이터베이스에 연결 대화 상자.  
  
이 대화 상자에 액세스 하는 **파일** 메뉴에서 **MySQL에 연결**합니다. 이전에 연결한 경우에 명령입니다 **MySQL에 다시 연결**합니다.  
  
## <a name="options"></a>변수  
**공급자**  
  
사용 가능한 MySQL 공급자는 MySQL 5.1 Odbc (신뢰할 수 있는)입니다.  
  
**모드**  
  
기본 모드는 표준 모드입니다. 표준 모드에서는 입력 하거나 MySQL에서 서버 이름, 서버 포트, 사용자 이름 및 암호에 대 한 값을 선택 합니다.  
  
**서버 이름**  
  
MySQL 서버 이름을 입력 합니다. 표준 모드 옵션입니다.  
  
**서버 포트**  
  
서버 포트를 입력 합니다. 기본 서버 포트 3306입니다. 표준 모드 옵션입니다.  
  
**사용자 이름**  
  
SSMA는 MySQL 데이터베이스에 연결 하는 데 사용할 수 있는 사용자 이름을 입력 합니다.  
  
**암호**  
  
사용자 이름에 대한 암호를 입력합니다.  
  
**SSL**  
  
MySQL에 안전 하 게 연결 하려는 경우 보안 소켓 레이어 (SSL)를 사용 하 여 확인 하 여 확인 합니다 **SSL** 확인란을 선택 합니다.  
  
**구성**  
  
보안 소켓 레이어 (SSL)을 통해 MySQL에 대 한 연결을 구성 하는 옵션을 제공 합니다.  
  
> [!NOTE]  
> 사용할 수 있도록 **구성**, SSL로 변경 해야 **True**합니다.  
  
"구성" 단추를 클릭 하면 대화 상자를 표시 됩니다. MySQL 데이터베이스에 대화 상자에 있는 다음 세 개의 인증서 파일의 경로를 연결 해야 하는 동안 암호화를 사용 하려면 [개인 정보 보호 향상 메일 인증서 (PEM)]를 정의 합니다.  
  
-   **SSL 인증 기관:** 신뢰 SSL Ca의 목록이 포함 된 파일의 경로 지정 합니다.  
  
-   **SSL 인증서:** 보안 연결을 설정 하는 데 SSL 인증서 파일의 이름을 지정 합니다.  
  
-   **SSL 키:** 보안 연결을 설정 하는 데 SSL 키 파일의 이름을 지정 합니다.  
  
> [!NOTE]  
> -   합니다 **확인** 필요한 정보를 제공한 경우 단추를 사용할 수 있습니다. 유효 하지 않으면 파일 경로의 모든 "확인" 단추를 사용할 수 없는 상태로 유지 됩니다.  
> -   **취소** 단추가 대화 상자를 닫습니다 및 **해제** 기본 연결 폼에서 SSL 옵션입니다.  
  

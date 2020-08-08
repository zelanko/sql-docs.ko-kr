---
title: MySQL에 연결 (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 66ec484ca6bd442f936eb852db48f34c89099d11
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935982"
---
# <a name="connect-to-mysql-mysqltosql"></a>MySQL에 연결(MySQLToSQL)
**Mysql에 연결** 대화 상자를 사용 하 여 마이그레이션하려는 mysql 데이터베이스에 연결 합니다.  
  
이 대화 상자에 액세스 하려면 **파일** 메뉴에서 **MySQL에 연결**을 선택 합니다. 이전에 연결한 경우 명령은 **MySQL에 다시 연결**됩니다.  
  
## <a name="options"></a>옵션  
**공급 기업**  
  
사용 가능한 MySQL 공급자는 MySQL ODBC 5.1 드라이버 (신뢰할 수 있음)입니다.  
  
**모드**  
  
기본 모드는 표준 모드입니다. 표준 모드에서는 MySQL, 서버 이름, 서버 포트, 사용자 이름 및 암호에 대 한 값을 입력 하거나 선택 합니다.  
  
**서버 이름**  
  
MySQL 서버 이름을 입력 합니다. 표준 모드 옵션입니다.  
  
**서버 포트**  
  
서버 포트를 입력 합니다. 기본 서버 포트는 3306입니다. 표준 모드 옵션입니다.  
  
**사용자 이름**  
  
SSMA에서 MySQL 데이터베이스에 연결 하는 데 사용할 사용자 이름을 입력 합니다.  
  
**암호**  
  
사용자 이름에 대한 암호를 입력합니다.  
  
**SSL**  
  
MySQL에 안전 하 게 연결 하려는 경우 **ssl** 확인란을 선택 하 여 Ssl (Secure Socket Layer)을 사용 합니다.  
  
**구성**  
  
SSL (Secure Socket Layer)을 통해 MySQL에 대 한 연결을 구성 하는 옵션을 제공 합니다.  
  
> [!NOTE]  
> **구성을**사용 하도록 설정 하려면 SSL을 **True**로 설정 해야 합니다.  
  
"구성" 단추를 클릭 하면 대화 상자가 나타납니다. MySQL 데이터베이스에 연결 하는 동안 암호화를 사용 하려면 대화 상자에 있는 다음 세 가지 인증서 파일의 경로를 정의 해야 [Privacy Enhanced Mail 인증서 (PEM)].  
  
-   **SSL 인증 기관:** 신뢰 SSL Ca 목록이 포함 된 파일의 경로를 지정 합니다.  
  
-   **SSL 인증서:** 보안 연결을 설정 하는 데 사용할 SSL 인증서 파일의 이름을 지정 합니다.  
  
-   **SSL 키:** 보안 연결을 설정 하는 데 사용할 SSL 키 파일의 이름을 지정 합니다.  
  
> [!NOTE]  
> -   필요한 정보가 제공 되 면 **확인** 단추를 사용할 수 있습니다. 파일 경로가 잘못 된 경우 "확인" 단추는 사용 하지 않도록 설정 된 상태로 유지 됩니다.  
> -   **취소** 단추를 클릭 하면 대화 상자가 닫히고 주 연결 양식에서 SSL 옵션이 **해제** 됩니다.  
  

---
title: MySQL (MySQLToSQL)에 연결 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2290b67ac66a1fa06d62b88390a538a3e06621ec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-mysql-mysqltosql"></a>MySQL (MySQLToSQL)에 연결
사용 하 여 **MySQL에 연결** 마이그레이션할 MySQL 데이터베이스에 연결 하는 대화 상자.  
  
이 대화 상자에 액세스 하는 **파일** 메뉴 선택 **MySQL에 연결**합니다. 이 명령은 이전에 연결한 경우 **MySQL에 다시 연결**합니다.  
  
## <a name="options"></a>옵션  
**공급자**  
  
사용 가능한 MySQL 공급자는 MySQL ODBC 5.1 드라이버 (신뢰할 수 있음).  
  
**모드**  
  
기본 모드는 표준 모드입니다. 표준 모드에서는 입력 하거나 MySQL, 서버 이름, 서버 포트, 사용자 이름 및 암호에 대 한 값을 선택 합니다.  
  
**서버 이름**  
  
MySQL 서버 이름을 입력 합니다. 표준 모드 옵션입니다.  
  
**서버 포트**  
  
서버 포트를 입력 합니다. 기본 서버 포트는 3306 합니다. 표준 모드 옵션입니다.  
  
**사용자 이름**  
  
SSMA는 MySQL 데이터베이스에 연결 하는 데 사용할 사용자 이름을 입력 합니다.  
  
**암호**  
  
사용자 이름에 대한 암호를 입력합니다.  
  
**SSL**  
  
MySQL에 안전 하 게 연결 하려는 경우를 확인 하 여 Secure Socket Layer (SSL)를 사용 하 여 **SSL** 확인란을 선택 합니다.  
  
**구성**  
  
MySQL 통해 SSL Secure Socket Layer ()에 대 한 연결을 구성 하는 옵션을 제공 합니다.  
  
> [!NOTE]  
> 사용할 수 있도록 **구성**, SSL로 설정 해야 **True**합니다.  
  
"구성" 단추를 클릭 하는 대화 상자가 나타납니다. MySQL 데이터베이스를 대화 상자에 다음 세 가지 인증서 파일에 대 한 경로에 연결 해야 하는 동안 암호화를 사용 하려면 [개인 정보 보호 향상 된 메일 인증서 (PEM)]를 정의 합니다.  
  
-   **SSL 인증 기관을:** 신뢰 SSL Ca ' 목록이 있는 파일 경로 지정 합니다.  
  
-   **SSL 인증서:** 보안 연결 구성에 사용할 SSL 인증서 파일의 이름을 지정 합니다.  
  
-   **SSL 키:** 보안 연결 구성에 사용할 SSL 키 파일의 이름을 지정 합니다.  
  
> [!NOTE]  
> -   **확인** 필요한 정보를 제공한 경우 단추를 사용할 수 있습니다. 유효 하지 않으면 파일 경로 있는 "확인" 단추가 비활성화 된 상태로 유지 됩니다.  
> -   **취소** 단추 대화 상자를 닫습니다 및 **해제** 기본 연결 폼에서 SSL 옵션입니다.  
  

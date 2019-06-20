---
title: Azure SQL DB (MySQLToSQL)에 연결 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 81623d27-25af-444f-9779-1edb8c6fb470
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 713a0ba96a2e82f10d4150b337d51f9f1774548f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63253151"
---
# <a name="connect-to-azure-sql-db-mysqltosql"></a>Azure SQL DB에 연결(MySQLToSQL)
마이그레이션하려는 SQL Azure 데이터베이스에 연결할 SQL Azure 대화 상자에 연결을 사용 합니다.  
  
이 대화 상자에 액세스 하는 **파일** 메뉴에서 **SQL Azure 연결**합니다. 이전에 연결한 경우에 명령입니다 **SQL Azure 다시 연결 합니다.**  
  
## <a name="options"></a>변수  
**서버 이름**  
  
선택 하거나 SQL Azure 연결 하기 위한 서버 이름을 입력 합니다.  
  
**데이터베이스 백업**  
  
선택, 입력 하거나 **찾아보기** 데이터베이스 이름입니다.  
  
> [!IMPORTANT]  
> MySQL 용 SSMA는 SQL Azure master 데이터베이스에 연결을 지원 하지 않습니다.  
  
**사용자 이름**  
  
SSMA가 SQL Azure 데이터베이스에 연결 하는 데 사용할 사용자 이름을 입력 합니다.  
  
**암호**  
  
사용자 이름에 대한 암호를 입력합니다.  
  
**Encrypt**  
  
SSMA는 SQL Azure 암호화 된 연결을 권장합니다.  
  
## <a name="create-azure-database"></a>Azure Database 만들기  
SQL Azure 계정에 데이터베이스가 없는 경우에 첫 번째 데이터베이스를 만들 수 있습니다.  
  
처음에 대 한 새 데이터베이스를 만들려면 다음 단계를 수행 합니다.  
  
1.  SQL Azure 대화 상자에 연결에 있는 찾아보기 단추를 클릭  
  
2.  데이터베이스가 없는 경우 다음 두 가지 메뉴 항목이 표시 됩니다.  
  
    1.  **(데이터베이스를 찾을 수 없음) ** 사용 하지 않도록 설정 하 고 항상 회색으로 표시  
  
    2.  **새 데이터베이스 만들기** SQL Azure 계정에 데이터베이스가 없는 경우에 활성화 됩니다. 이 메뉴 항목을 클릭 하면 Azure 데이터베이스 만들기 대화 상자가 데이터베이스 이름 및 크기를 사용 하 여 표시 됩니다.  
  
3.  데이터베이스 생성 시 다음 두 매개 변수를 입력으로 제공 됩니다.  
  
    1.  **데이터베이스 이름:** 데이터베이스 이름을 입력 합니다.  
  
    2.  **데이터베이스 크기:** SQL Azure 계정에 생성 해야 하는 데이터베이스 크기를 선택 합니다.  
  

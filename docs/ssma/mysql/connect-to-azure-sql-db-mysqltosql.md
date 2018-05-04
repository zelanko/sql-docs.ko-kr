---
title: Azure SQL DB (MySQLToSQL)에 연결 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
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
ms.assetid: 81623d27-25af-444f-9779-1edb8c6fb470
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a651ab897493e436df99ba797ceca2d8eef5cd2d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-azure-sql-db-mysqltosql"></a>Azure SQL DB (MySQLToSQL)에 연결
SQL Azure 대화 상자에 연결을 사용 하 여 마이그레이션할 SQL Azure 데이터베이스에 연결 합니다.  
  
이 대화 상자에 액세스 하는 **파일** 메뉴 선택 **SQL Azure에 연결**합니다. 이 명령은 이전에 연결한 경우 **SQL Azure에 다시 연결 합니다.**  
  
## <a name="options"></a>옵션  
**서버 이름**  
  
선택 하거나 SQL Azure에 연결 하기 위한 서버 이름을 입력 합니다.  
  
**데이터베이스**  
  
선택, 입력 또는 **찾아보기** 데이터베이스 이름입니다.  
  
> [!IMPORTANT]  
> MySQL 용 SSMA는 SQL Azure에서 master 데이터베이스에 연결을 지원 하지 않습니다.  
  
**사용자 이름**  
  
SSMA는 SQL Azure 데이터베이스에 연결 하는 데 사용할 사용자 이름을 입력 하십시오  
  
**암호**  
  
사용자 이름에 대한 암호를 입력합니다.  
  
**Encrypt**  
  
SSMA는 SQL Azure에 암호화 된 연결을 권장합니다.  
  
## <a name="create-azure-database"></a>Azure 데이터베이스 만들기  
SQL Azure 계정에서 데이터베이스가 없는 경우에 첫 번째 데이터베이스를 만들 수 있습니다.  
  
맨 처음에 대 한 새 데이터베이스를 만들려면 다음 단계를 수행 합니다.  
  
1.  SQL Azure 대화 상자에는 연결에 있는 찾아보기 단추를 클릭  
  
2.  데이터베이스가 없는, 다음 두 메뉴 항목이 표시 됩니다.  
  
    1.  **(데이터베이스를 찾을 수 없음)**  사용 하지 않도록 설정 되 고 항상 회색으로 표시 되는지를  
  
    2.  **새 데이터베이스 만들기** 데이터베이스가 SQL Azure 계정에 없는 경우에 활성화 되어 있습니다. 이 메뉴 항목을 클릭 하면 Azure 데이터베이스 만들기 대화 상자가 데이터베이스 이름 및 크기와 표시 됩니다.  
  
3.  데이터베이스 생성 시 다음 두 매개 변수는 입력으로 제공 됩니다.  
  
    1.  **데이터베이스 이름:** 데이터베이스 이름을 입력 합니다.  
  
    2.  **데이터베이스 크기:** SQL Azure 계정에서 만들어야 하는 데이터베이스 크기를 선택 합니다.  
  

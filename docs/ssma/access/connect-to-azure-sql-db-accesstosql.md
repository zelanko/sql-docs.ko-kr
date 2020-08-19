---
description: Azure SQL Database에 연결 (AccessToSQL)
title: Azure SQL Database에 연결 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connect to SQL Azure dialog box
ms.assetid: bf44b236-d9be-41ae-a5fd-bd73038e505f
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 15882852544113881b52f3641e0c85ec684add22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418569"
---
# <a name="connect-to-azure-sql-database-accesstosql"></a>Azure SQL Database에 연결 (AccessToSQL)
SQL Azure 연결 대화 상자를 사용 하 여 마이그레이션하려는 Azure SQL Database 데이터베이스에 연결할 수 있습니다.  
  
이 대화 상자에 액세스 하려면 **파일** 메뉴에서 **SQL Azure에 연결**을 선택 합니다. 이전에 연결한 경우 명령이 **SQL Azure에 다시 연결 됩니다.**  
  
## <a name="options"></a>옵션  
**서버 이름**  
  
SQL Azure에 연결 하기 위한 서버 이름을 선택 하거나 입력 합니다.  
  
**Database**  
  
을 선택 하 고 데이터베이스 이름을 입력 하거나 **검색** 합니다.  
  
> [!IMPORTANT]  
> Access 용 SSMA는 SQL Azure의 master 데이터베이스에 대 한 연결을 지원 하지 않습니다.  
  
**사용자 이름**  
  
SSMA에서 Azure SQL Database에 연결 하는 데 사용할 사용자 이름을 입력 합니다.  
  
**암호**  
  
사용자 이름에 대한 암호를 입력합니다.  
  
**Encrypt**  
  
SSMA는 SQL Azure에 대 한 암호화 된 연결을 권장 합니다.  
  
## <a name="create-database"></a>데이터베이스 만들기  
새 데이터베이스를 만들려면 다음 단계를 수행 합니다.  
  
1.  SQL Azure에 연결 대화 상자에 있는 찾아보기 단추를 클릭 합니다.  
  
2.  데이터베이스가 없는 경우 두 개의 메뉴 항목이 표시 됩니다.  
  
    1.  **(데이터베이스를 찾을 수 없음)** 항상 사용 하지 않도록 설정 되 고 회색으로 표시 됨  
  
    2.  항상 사용 하도록 설정 된 **새 데이터베이스를 만들어** 사용자가 새 데이터베이스를 만들 수 있도록 합니다. 이 메뉴 항목을 클릭 하면 데이터베이스 이름과 크기가 포함 된 데이터베이스 만들기 대화 상자가 표시 됩니다.  
  
3.  데이터베이스를 만들 때이 두 매개 변수는 입력으로 제공 됩니다.  
  
    1.  **데이터베이스 이름:** 데이터베이스 이름을 입력 합니다.  
  
    2.  **데이터베이스 크기:** SQL Azure 계정에서 만들어야 하는 데이터베이스 크기를 선택 합니다.  
  

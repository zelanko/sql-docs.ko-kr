---
title: "Azure SQL DB (AccessToSQL)에 연결 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Connect to SQL Azure dialog box
ms.assetid: bf44b236-d9be-41ae-a5fd-bd73038e505f
caps.latest.revision: "17"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 25d1e2190223f8f7728518701fbbf1a3590ab5f5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="connect-to-azure-sql-db-accesstosql"></a>Azure SQL DB (AccessToSQL)에 연결
SQL Azure 대화 상자에 연결을 사용 하 여 마이그레이션할 SQL Azure 데이터베이스에 연결 합니다.  
  
이 대화 상자에 액세스 하는 **파일** 메뉴 선택 **SQL Azure에 연결**합니다. 이 명령은 이전에 연결한 경우 **SQL Azure에 다시 연결 합니다.**  
  
## <a name="options"></a>옵션  
**서버 이름**  
  
선택 하거나 SQL Azure에 연결 하기 위한 서버 이름을 입력 합니다.  
  
**데이터베이스**  
  
선택, 입력 또는 **찾아보기** 데이터베이스 이름입니다.  
  
> [!IMPORTANT]  
> Access 용 SSMA는 SQL Azure에서 master 데이터베이스에 연결을 지원 하지 않습니다.  
  
**사용자 이름**  
  
SSMA는 SQL Azure 데이터베이스에 연결 하는 데 사용할 사용자 이름을 입력 하십시오  
  
**암호**  
  
사용자 이름에 대한 암호를 입력합니다.  
  
**암호화**  
  
SSMA는 SQL Azure에 암호화 된 연결을 권장합니다.  
  
## <a name="create-azure-database"></a>Azure 데이터베이스 만들기  
새 azure 데이터베이스를 만들려면 다음 단계를 수행 합니다.  
  
1.  SQL Azure 대화 상자에는 연결에 있는 찾아보기 단추를 클릭  
  
2.  데이터베이스가 없으면 두 메뉴 항목 표시  
  
    1.  **(데이터베이스를 찾을 수 없음)**  사용 하지 않도록 설정 되 고 항상 회색으로 표시 되는지를  
  
    2.  **새 데이터베이스 만들기** 항상 활성화 되어, SQL Azure 계정에서 새 azure 데이터베이스를 만들 수 있도록 합니다. 이 메뉴 항목을 클릭 하면 만들 azure 데이터베이스 대화 상자는 데이터베이스 이름 및 크기를 사용 합니다.  
  
3.  데이터베이스 생성 시이 두 매개 변수는 입력으로 제공 됩니다.  
  
    1.  **데이터베이스 이름:** 데이터베이스 이름을 입력 합니다.  
  
    2.  **데이터베이스 크기:** SQL Azure 계정에서 만들어야 하는 데이터베이스 크기를 선택 합니다.  
  

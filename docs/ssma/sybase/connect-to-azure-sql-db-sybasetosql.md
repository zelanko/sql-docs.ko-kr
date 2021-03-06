---
description: Azure SQL Database에 연결 (SybaseToSQL)
title: Azure SQL Database에 연결 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3717cce895ca602a550d47ea5c569af4c80963a0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492316"
---
# <a name="connect-to-azure-sql-database--sybasetosql"></a>Azure SQL Database에 연결 (SybaseToSQL)
Azure SQL Database 연결 대화 상자를 사용 하 여 마이그레이션하려는 Azure SQL Database 데이터베이스에 연결할 수 있습니다.  
  
이 대화 상자에 액세스 하려면 **파일** 메뉴에서 **Azure SQL Database에 연결**을 선택 합니다. 이전에 연결한 경우 명령이 **Azure SQL Database에 다시 연결 됩니다.**  
  
## <a name="options"></a>옵션  
**서버 이름**  
  
Azure SQL Database에 연결 하기 위한 서버 이름을 선택 하거나 입력 합니다.  
  
**Database**  
  
을 선택 하 고 데이터베이스 이름을 입력 하거나 **검색** 합니다.  
  
> [!IMPORTANT]  
> Sybase 용 SSMA는 Azure SQL Database의 master 데이터베이스에 대 한 연결을 지원 하지 않습니다.  
  
**사용자 이름**  
  
Azure SQL Database 데이터베이스에 연결 하는 데 사용할 사용자 이름을 입력 합니다.  
  
**암호**  
  
사용자 이름에 대한 암호를 입력합니다.  
  
**Encrypt**  
  
SSMA는 Azure SQL Database에 대 한 암호화 된 연결을 권장 합니다.  
  
## <a name="create-azure-database"></a>Azure 데이터베이스 만들기  
Azure SQL Database 계정에 데이터베이스가 없는 경우에는 첫 번째 데이터베이스를 만들 수 있습니다.  
  
처음으로 새 데이터베이스를 만들려면 다음 단계를 수행 합니다.  
  
1.  Azure SQL Database에 연결 대화 상자에 있는 찾아보기 단추를 클릭 합니다.  
  
2.  데이터베이스가 없는 경우 다음 두 가지 메뉴 항목이 표시 됩니다.  
  
    1.  **(데이터베이스를 찾을 수 없음)** 항상 사용 하지 않도록 설정 되 고 회색으로 표시 됨  
  
    2.  Azure SQL Database 계정에 데이터베이스가 없는 경우에만 사용할 수 있는 **새 데이터베이스를 만듭니다** . 이 메뉴 항목을 클릭 하면 데이터베이스 이름과 크기가 있는 Azure 데이터베이스 만들기 대화 상자가 표시 됩니다.  
  
3.  데이터베이스를 만들 때 다음 두 매개 변수를 입력으로 제공 합니다.  
  
    1.  **데이터베이스 이름:** 데이터베이스 이름을 입력 합니다.  
  
    2.  **데이터베이스 크기:** Azure SQL Database 계정에서 만들어야 하는 데이터베이스 크기를 선택 합니다.  
  

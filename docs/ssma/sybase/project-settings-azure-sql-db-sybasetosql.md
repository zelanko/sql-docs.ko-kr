---
title: "프로젝트 설정 (Azure SQL DB) (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 90b621fef119395185a79c68300faa0a800104a6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="project-settings-azure-sql-db--sybasetosql"></a>프로젝트 설정 (Azure SQL DB) (SybaseToSQL)
Azure SQL DB 프로젝트 설정에 연결 대화 상자에 추가 되 고 또한 Azure SQL DB 연결에서 하트 비트 메커니즘을 구현할 수 있게 하려면 Azure SQL DB 데이터베이스 접미사를 구성할 수 있습니다.  
  
Azure SQL DB에서 제공 되는 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자.  
  
-   프로젝트 설정 대화 상자를 사용 하 여 현재 프로젝트에 대 한 구성 옵션을 설정 합니다. Azure SQL DB 설정에 액세스 하려면는 **도구** 메뉴 선택 **프로젝트 설정**, 클릭 **일반** 선택 고 왼쪽된 창 맨 아래에 **Azure SQL DB**합니다.  
  
-   기본 프로젝트 설정 대화 상자를 사용 하 여 모든 프로젝트에 대 한 구성 옵션을 설정 합니다. Azure SQL DB 설정에 액세스 하려면는 **도구** 메뉴 선택 **DefaultProject 설정**, 클릭 **일반** 선택 고 왼쪽된 창 맨 아래에 **Azure SQL DB**합니다.  
  
## <a name="connectivity"></a>연결  
**하트 비트 간격**  
  
활성 Azure SQL DB 연결을 유지 하려면 하트 비트 메커니즘에 사용할 시간 간격을 지정 ' 분: 초 형식입니다.  
  
**기본 값**:' 4:45 '  
  
값을 지정 해야에 am: ss' 형식 (예를 들어, ' 4:45 ' 또는 ' 0:50 ').  
  
**Azure SQL DB 서버 접미사**  
  
Azure SQL DB 서버 접미사를 지정합니다.  
  
**기본 값**: 'database.windows.net'.  
  

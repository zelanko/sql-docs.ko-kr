---
title: 프로젝트 설정 (동기화) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2cd6bc01-b8e5-4312-83a4-eac66dc1d460
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 624d546309a34ad4370ab8c3eadce4324832c19f
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34779149"
---
# <a name="project-settings-synchronization-sybasetosql"></a>프로젝트 설정 (동기화) (SybaseToSQL)
동기화 페이지는 **프로젝트 설정** 대화 상자 SSMA에 테이블 및 저장된 프로시저 같은 데이터베이스 개체를 로드 하는 방식을 사용자 지정 하는 설정이 포함 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다.  
  
동일한 설정을 포함 하는 두 개의 다른 동기화 페이지에 액세스할 수 있습니다.  
  
-   모든 향후 SSMA 프로젝트에 대 한 설정을 지정 하려면는 **도구** 메뉴를 선택 **기본 프로젝트 설정**, 설정을 보거나에서 변경 하는 데 필요한는 마이그레이션 프로젝트 형식을 선택 **마이그레이션 대상 버전** 드롭 다운 한 후 선택 **동기화** 왼쪽 창의 맨 아래에 있습니다.  
  
-   에 현재 프로젝트에 대 한 설정을 지정 하려면는 **도구** 메뉴 선택 **프로젝트 설정**를 선택한 후 **동기화** 왼쪽 창의 맨 아래에 있습니다.  
  
## <a name="options"></a>변수  
**시도 횟수**  
개체를 로드할 때 SSMA를 채우는 시도할 횟수가 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 에 로드 되지 않는 개체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 현재 시도의 다시 시도 됩니다 SSMA 현재 동기화 프로세스에서 시도의 최대 수에 도달할 때까지 합니다.  
  
## <a name="synchronization-for-sql-server"></a>SQL Server에 대 한 동기화  
**로컬 및 원격 개체 변경 시 로컬 개체를 새로 고칩니다.**  
로컬 및 원격 개체를 변경 하는 경우 SSMA 해야 원격 개체 메타 데이터와 로컬 개체 메타 데이터를 대체 여부를 지정 합니다.  
선택 하는 경우 **데이터베이스에서 새로 고침**, 조건이 충족 될 때 SSMA 메타 데이터에 데이터베이스 정의 로드 됩니다.  
선택 하는 경우 **데이터베이스에 쓰기**, 조건이 충족 될 때 SSMA SSMA 메타 데이터 내용에 따라 데이터베이스의 개체를 업데이트 합니다.  
선택 하는 경우 **Skip**, SSMA 새로 고침 작업을 수행 하지 것입니다.   
기본 옵션 집합이 **를 데이터베이스에 기록 합니다.**  
  
**로컬 개체 변경 시 로컬 개체를 새로 고칩니다.**  
원격 개체 변경 되 면 SSMA 해야 원격 개체 메타 데이터와 로컬 개체 메타 데이터를 대체 여부를 지정 합니다.  
선택 하는 경우 **데이터베이스에서 새로 고침**, 조건이 충족 될 때 SSMA 메타 데이터에 데이터베이스 정의 로드 됩니다.  
선택 하는 경우 **데이터베이스에 쓰기**, 조건이 충족 될 때 SSMA SSMA 메타 데이터 내용에 따라 데이터베이스의 개체를 업데이트 합니다.  
선택 하는 경우 **Skip**, SSMA 새로 고침 작업을 수행 하지 것입니다.   
기본 옵션 집합이 **데이터베이스에 쓰기**합니다.  
  
**원격 개체 변경 시 로컬 개체를 새로 고칩니다.**  
원격 개체 변경 되 면 SSMA 해야 원격 개체 메타 데이터와 로컬 개체 메타 데이터를 대체 여부를 지정 합니다.  
선택 하는 경우 **데이터베이스에서 새로 고침**, 조건이 충족 될 때 SSMA 메타 데이터에 데이터베이스 정의 로드 됩니다.  
선택 하는 경우 **데이터베이스에 쓰기**, 조건이 충족 될 때 SSMA SSMA 메타 데이터 내용에 따라 데이터베이스의 개체를 업데이트 합니다.  
선택 하는 경우 **Skip**, SSMA 새로 고침 작업을 수행 하지 것입니다.   
기본 옵션 집합이 **데이터베이스에서 새로 고침**합니다.  
  
**로컬 개체 메타 데이터에 없을 경우 새로 고침**  
SSMA는 개체가 대상 데이터베이스에만 로컬이 아닌 경우 로컬 메타 데이터를 만들 해야 하는지 여부를 지정 합니다.  
선택 하는 경우 **데이터베이스에서 새로 고침**, SSMA는 조건이 충족 되 면 데이터베이스 옵션에서 새로 고침을 선택 합니다.  
선택 하는 경우 **데이터베이스에 쓰기**, 조건이 충족 될 때 SSMA 데이터베이스에서 개체가 삭제 됩니다.  
선택 하는 경우 **Skip**, SSMA 새로 고침 작업을 수행 하지 것입니다.   
기본 옵션 집합이 **데이터베이스에서 새로 고침**합니다.  
  

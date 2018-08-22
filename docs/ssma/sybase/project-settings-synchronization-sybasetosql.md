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
ms.openlocfilehash: fcdcfc8d113bca42a9f042e8e6196d3de55b8e7e
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40394307"
---
# <a name="project-settings-synchronization-sybasetosql"></a>프로젝트 설정(동기화)(SybaseToSQL)
[동기화] 페이지의 **프로젝트 설정** 대화 상자에는 SSMA를 테이블 및 저장된 프로시저와 같은 데이터베이스 개체를 로드 하는 방법을 사용자 지정 하는 설정이 포함 되어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다.  
  
동일한 설정을 포함 하는 두 개의 다른 동기화 페이지에 액세스할 수 있습니다.  
  
-   모든 향후 SSMA 프로젝트에 대 한 설정을 지정 하려는 경우는 **도구** 메뉴에서 **기본 프로젝트 설정**, 설정을 보거나 변경 하는 데 필요한는 마이그레이션 프로젝트 유형 선택 **마이그레이션 대상 버전** 드롭다운 목록 및 선택한 **동기화** 왼쪽 창의 맨 아래에 있습니다.  
  
-   에 현재 프로젝트에 대 한 설정을 지정 하려면 합니다 **도구** 메뉴에서 **프로젝트 설정**를 선택한 후 **동기화** 왼쪽 창의 맨 아래에.  
  
## <a name="options"></a>변수  
**시도**  
SSMA는 개체를 로드할 때 확인 해야 하는 횟수를 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 개체에 로드 되지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 현재 시도의 다시 시도 합니다 SSMA에 현재 동기화 프로세스의 최대 횟수에 도달할 때까지 합니다.  
  
## <a name="synchronization-for-sql-server"></a>SQL Server에 대 한 동기화  
**로컬 및 원격 개체 변경 시 로컬 개체를 새로 고칩니다.**  
로컬 및 원격 개체를 변경 하는 경우 SSMA 해야 원격 개체 메타 데이터를 사용 하 여 로컬 개체 메타 데이터를 대체 하는지 여부를 지정 합니다.  
선택 하는 경우 **데이터베이스에서 새로 고침**, 조건이 충족 되 면 SSMA 메타 데이터를 데이터베이스 정의 로드 됩니다.  
선택 하는 경우 **데이터베이스에 쓸**, 조건이 충족 될 때 SSMA SSMA 메타 데이터 내용에 따라 데이터베이스의 개체를 업데이트 합니다.  
선택 하는 경우 **Skip**, SSMA 새로 고침 작업을 수행 하지 것입니다.   
기본 옵션 집합은 **데이터베이스에 기록 합니다.**  
  
**로컬 개체 변경 시 로컬 개체를 새로 고칩니다.**  
원격 개체가 변경 SSMA 해야 원격 개체 메타 데이터를 사용 하 여 로컬 개체 메타 데이터를 대체 하는지 여부를 지정 합니다.  
선택 하는 경우 **데이터베이스에서 새로 고침**, 조건이 충족 되 면 SSMA 메타 데이터를 데이터베이스 정의 로드 됩니다.  
선택 하는 경우 **데이터베이스에 쓸**, 조건이 충족 될 때 SSMA SSMA 메타 데이터 내용에 따라 데이터베이스에 개체를 업데이트 합니다.  
선택 하는 경우 **Skip**, SSMA 새로 고침 작업을 수행 하지 것입니다.   
기본 옵션 집합이 **데이터베이스에 쓸**합니다.  
  
**원격 개체 변경 시 로컬 개체를 새로 고칩니다.**  
원격 개체가 변경 SSMA 해야 원격 개체 메타 데이터를 사용 하 여 로컬 개체 메타 데이터를 대체 하는지 여부를 지정 합니다.  
선택 하는 경우 **데이터베이스에서 새로 고침**, 조건이 충족 되 면 SSMA 메타 데이터를 데이터베이스 정의 로드 됩니다.  
선택 하는 경우 **데이터베이스에 쓸**, 조건이 충족 될 때 SSMA SSMA 메타 데이터 내용에 따라 데이터베이스에 개체를 업데이트 합니다.  
선택 하는 경우 **Skip**, SSMA 새로 고침 작업을 수행 하지 것입니다.   
기본 옵션 집합이 **데이터베이스에서 새로 고침**합니다.  
  
**로컬 개체 메타 데이터를 사용할 수 없는 경우 새로 고침**  
SSMA는 개체가 대상 데이터베이스에 있지만 로컬이 아닌 경우 로컬 메타 데이터를 만들 해야 하는지 여부를 지정 합니다.  
선택 하는 경우 **데이터베이스에서 새로 고침**, SSMA는 조건이 충족 되 면 데이터베이스 옵션에서 새로 고침을 선택 합니다.  
선택 하는 경우 **데이터베이스에 쓸**, 조건이 충족 되 면 SSMA 데이터베이스에서 개체가 삭제 됩니다.  
선택 하는 경우 **Skip**, SSMA 새로 고침 작업을 수행 하지 것입니다.   
기본 옵션 집합이 **데이터베이스에서 새로 고침**합니다.  
  

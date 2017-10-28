---
title: "프로젝트 설정 (개체 로드) (AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9ec1c1e8-a3e1-4e81-bf49-631f87daa209
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 84737c6b747174f993765a6d86081759cfedd4bb
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-loading-objects-accesstosql"></a>프로젝트 설정 (개체 로드) (AccessToSQL)
개체를 로드 프로젝트 설정에는 SQL Server 데이터베이스 개체와 Access 데이터베이스 개체가 동기화 되는 방식을 구성할 수 있습니다.  
  
Access 데이터베이스에서 개체를 새로 고치에 대 한 SQL Server 데이터베이스와 개체의 동기화 기본 설정을 지정 하는 기본 동작입니다. 자세한 내용은 참조 [데이터베이스 &#40;에서 새로 고침 AccessToSQL &#41;](../../ssma/access/refresh-from-database-accesstosql.md)  
  
동일한 설정을 포함 하는 두 개의 다른 동기화 페이지에 액세스할 수 있습니다.  
  
-   에 모든 향후 SSMA 프로젝트에 대 한 설정을 지정 하려면는 **도구** 메뉴에서 클릭 **DefaultProject 설정**, 클릭 하 고 **개체 로드** 왼쪽 창의 맨 아래에 있습니다.  
  
-   에 현재 프로젝트에 대 한 설정을 지정 하려면는 **도구** 메뉴에서 클릭 **프로젝트 설정**, 클릭 하 고 **개체 로드** 왼쪽 창의 맨 아래에 있습니다.  
  
## <a name="options"></a>옵션  
  
##### <a name="misc"></a>기타  
  
##### <a name="attempts"></a>시도 횟수  
SQL Server에 로드 하기 위해 수행 개체 패스의 수에 대 한 정보를 제공 합니다. SQL Server로 개체를 로드 한 패스가 여러 개에서 일반적으로 수행 됩니다. 외래 키 등의 첫 번째 단계에서 로드 하는 개체 다음에 성공적으로 로드 될 수 있습니다.  
  
기본적으로 값은 2입니다.  
  
## <a name="synchronization-for-sql-server"></a>SQL Server에 대 한 동기화  
  
##### <a name="default-action-on-local-and-remote-object-change"></a>로컬 및 원격 개체 변경에 대 한 기본 작업  
SSMA 및 데이터베이스 서버에 개체 정의가 변경 될 때 동기화 대화 상자에서 기본 설정을 지정 합니다.  
  
-   선택 하는 경우 **데이터베이스에서 새로 고침**, 조건이 충족 될 때 SSMA 메타 데이터에 데이터베이스 정의 로드 됩니다.  
  
-   선택 하는 경우 **데이터베이스에 쓰기**, 조건이 충족 될 때 SSMA SSMA 메타 데이터 내용에 따라 데이터베이스의 개체를 업데이트 합니다.  
  
-   선택 하는 경우 **Skip**, SSMA 새로 고침 작업을 수행 하지 것입니다.  
  
##### <a name="default-action-on-local-object-change"></a>로컬 개체 변경에 대 한 기본 작업  
SSMA는 개체가 변경 될 때 동기화 대화 상자에서 기본 설정을 지정 합니다.  
  
-   선택 하는 경우 **데이터베이스에서 새로 고침**, 조건이 충족 될 때 SSMA 메타 데이터에 데이터베이스 정의 로드 됩니다.  
  
-   선택 하는 경우 **데이터베이스에 쓰기**, 조건이 충족 될 때 SSMA SSMA 메타 데이터 내용에 따라 데이터베이스의 개체를 업데이트 합니다.  
  
-   선택 하는 경우 **Skip**, SSMA 새로 고침 작업을 수행 하지 것입니다.  
  
##### <a name="default-action-on-remote-object-change"></a>원격 개체 변경에 대 한 기본 작업  
데이터베이스 서버에는 개체가 변경 될 때 동기화 대화 상자에서 기본 설정을 지정 합니다.  
  
-   선택 하는 경우 **데이터베이스에서 새로 고침**, 조건이 충족 될 때 SSMA 메타 데이터에 데이터베이스 정의 로드 됩니다.  
  
-   선택 하는 경우 **데이터베이스에 쓰기**, 조건이 충족 될 때 SSMA SSMA 메타 데이터 내용에 따라 데이터베이스의 개체를 업데이트 합니다.  
  
-   선택 하는 경우 **Skip**, SSMA 새로 고침 작업을 수행 하지 것입니다.  
  
##### <a name="default-action-when-local-object-metadata-is-missing"></a>로컬 개체 메타 데이터 누락 되었을 때 기본 동작  
로컬 메타 데이터 누락 된 경우 동기화 대화 상자에서 기본 설정을 지정 합니다.  
  
-   선택 하는 경우 **데이터베이스에서 새로 고침**, SSMA는 조건이 충족 되 면 데이터베이스 옵션에서 새로 고침을 선택 합니다.  
  
-   선택 하는 경우 **데이터베이스에 쓰기**, 조건이 충족 될 때 SSMA 데이터베이스에서 개체가 삭제 됩니다.  
  
-   선택 하는 경우 **Skip**, SSMA 새로 고침 작업을 수행 하지 것입니다.  
  


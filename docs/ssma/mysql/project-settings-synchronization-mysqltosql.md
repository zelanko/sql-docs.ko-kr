---
description: 프로젝트 설정(동기화)(MySQLToSQL)
title: 프로젝트 설정 (동기화) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 42061ff7-e6e7-497b-a0d9-440b9cf5986c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3ea89bcdf9b10fb50e74228a26bfcd5cead83aca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492386"
---
# <a name="project-settings-synchronization-mysqltosql"></a>프로젝트 설정(동기화)(MySQLToSQL)
동기화 **프로젝트 설정을** 사용 하 여 MySQL 데이터베이스 개체가 SQL Server database 개체와 동기화 되는 방법을 구성할 수 있습니다.  
  
기본 작업은 MySQL 데이터베이스에서 개체를 새로 고치고 SQL Server 데이터베이스와 개체를 동기화 하기 위한 기본 설정을 지정 합니다. 자세한 내용은 [데이터베이스에서 새로 고침 &#40;MySQLToSQL&#41;](../../ssma/mysql/refresh-from-database-mysqltosql.md) 을 참조 하세요.  
  
동일한 설정을 포함 하는 두 개의 서로 다른 동기화 페이지에 액세스할 수 있습니다.  
  
-   모든 향후 SSMA 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **defaultproject settings**를 클릭 한 다음 왼쪽 창의 맨 아래에서 **동기화** 를 클릭 합니다.  
  
-   현재 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **프로젝트 설정**을 클릭 한 다음 왼쪽 창의 맨 아래에서 **동기화** 를 클릭 합니다.  
  
## <a name="options"></a>옵션  
  
##### <a name="misc"></a>기타  
  
##### <a name="attempts"></a>시도한  
개체를 SQL Server 로드 하는 데 사용 되는 패스에 대 한 정보를 제공 합니다. 개체를 SQL Server 로드 하는 것은 일반적으로 여러 패스에서 수행 됩니다. 외래 키와 같이 첫 번째 패스에서 로드에 실패 한 개체는 다음 패스에서 성공적으로 로드 될 수 있습니다.  
  
기본적으로 값은 2입니다.  
  
## <a name="synchronization-for-mysql"></a>MySQL에 대 한 동기화  
  
##### <a name="action-on-local-and-remote-object-change"></a>로컬 및 원격 개체 변경에 대 한 작업  
SSMA 및 데이터베이스 서버에서 개체 정의가 변경 되는 경우 동기화 대화 상자에서 기본 설정을 지정 합니다.  
  
-   데이터베이스에서 새로 고침을 선택 하는 경우 SSMA는 조건이 충족 될 때 메타 데이터에 데이터베이스 정의를 로드 합니다.  
  
-   건너뛰기를 선택 하면 SSMA는 새로 고침 작업을 수행 하지 않습니다.  
  
##### <a name="action-on-local-object-change"></a>로컬 개체 변경에 대 한 작업  
SSMA에서 개체가 변경 될 때 동기화 대화 상자에서 기본 설정을 지정 합니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 메타 데이터에 데이터베이스 정의를 로드 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  
##### <a name="action-on-remote-object-change"></a>원격 개체 변경에 대 한 작업  
데이터베이스 서버에서 개체가 변경 될 때 동기화 대화 상자에서 기본 설정을 지정 합니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 메타 데이터에 데이터베이스 정의를 로드 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>로컬 개체 메타 데이터가 없는 경우의 작업  
로컬 메타 데이터가 없는 경우 동기화 대화 상자에서 기본 설정을 지정 합니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 메타 데이터에 데이터베이스 정의를 로드 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  
## <a name="synchronization-for-sql-server"></a>SQL Server에 대 한 동기화  
  
##### <a name="action-on-local-and-remote-object-change"></a>로컬 및 원격 개체 변경에 대 한 작업  
SSMA 및 데이터베이스 서버에서 개체 정의가 변경 되는 경우 동기화 대화 상자에서 기본 설정을 지정 합니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 메타 데이터에 데이터베이스 정의를 로드 합니다.  
  
-   **데이터베이스에 쓰기**를 선택 하는 경우 ssma는 조건이 충족 될 때 ssma 메타 데이터 내용에 따라 데이터베이스의 개체를 업데이트 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  
##### <a name="action-on-local-object-change"></a>로컬 개체 변경에 대 한 작업  
SSMA에서 개체가 변경 될 때 동기화 대화 상자에서 기본 설정을 지정 합니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 메타 데이터에 데이터베이스 정의를 로드 합니다.  
  
-   **데이터베이스에 쓰기**를 선택 하는 경우 ssma는 조건이 충족 될 때 ssma 메타 데이터 내용에 따라 데이터베이스의 개체를 업데이트 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  
##### <a name="action-on-remote-object-change"></a>원격 개체 변경에 대 한 작업  
데이터베이스 서버에서 개체가 변경 될 때 동기화 대화 상자에서 기본 설정을 지정 합니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 메타 데이터에 데이터베이스 정의를 로드 합니다.  
  
-   **데이터베이스에 쓰기**를 선택 하는 경우 ssma는 조건이 충족 될 때 ssma 메타 데이터 내용에 따라 데이터베이스의 개체를 업데이트 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>로컬 개체 메타 데이터가 없는 경우의 작업  
로컬 메타 데이터가 없는 경우 동기화 대화 상자에서 기본 설정을 지정 합니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 데이터베이스에서 새로 고침 옵션을 선택 합니다.  
  
-   **데이터베이스에 쓰기**를 선택 하는 경우 ssma는 조건이 충족 될 때 데이터베이스에서 개체를 삭제 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  

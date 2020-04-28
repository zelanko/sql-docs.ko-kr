---
title: 프로젝트 설정 (Azure SQL DB) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Project Settings dialog box, SQL Azure
- SQL Azure settings
ms.assetid: bbb8a204-d0e4-4f0b-9709-271feb1f136e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 60140559f94cdeebea935b423fbbeef24bce7a08
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67929465"
---
# <a name="project-settings-azure-sql-db-accesstosql"></a>프로젝트 설정 (Azure SQL DB) (AccessToSQL)
SQL Azure 프로젝트 설정을 사용 하 여 연결 대화 상자에서 추가할 SQL Azure 데이터베이스 접미사를 구성 하 고 SQL Azure 연결에 하트 비트 메커니즘을 구현할 수도 있습니다.  
  
SQL Azure 창은 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자에서 사용할 수 있습니다.  
  
-   프로젝트 설정 대화 상자를 사용 하 여 현재 프로젝트에 대 한 구성 옵션을 설정할 수 있습니다. SQL Azure 설정에 액세스 하려면 **도구** 메뉴에서 **프로젝트 설정**을 선택 하 고 왼쪽 창의 맨 아래에서 **일반** 을 클릭 한 다음 **SQL Azure**을 선택 합니다.  
  
-   기본 프로젝트 설정 대화 상자를 사용 하 여 모든 프로젝트에 대 한 구성 옵션을 설정할 수 있습니다. SQL Azure 설정에 액세스 하려면 **도구** 메뉴에서 **defaultproject settings**를 선택 하 고, **마이그레이션 대상 버전** 콤보 상자에서 프로젝트 유형을 "SQL Azure"로 선택 하 여 SQL Azure 창의 설정에 액세스 하 고, 왼쪽 창의 맨 아래에서 **일반** 을 클릭 한 다음 **SQL Azure**를 선택 합니다.  
  
## <a name="options"></a>옵션  
  
## <a name="connectivity"></a>연결  
**하트 비트 간격**  
  
SQL Azure 연결을 ' 분: 초 ' 형식으로 유지 하기 위해 하트 비트 메커니즘에 사용할 시간 간격을 지정 합니다.  
  
**기본값**: ' 4:45 '  
  
값은 ' m:ss ' 형식으로 지정 해야 합니다 (예: ' 4:45 ' 또는 ' 0:50 ').  
  
**SQL Azure 서버 접미사**  
  
SQL Azure 서버 접미사를 지정 합니다.  
  
**기본값**: ' database.windows.net '.  
  

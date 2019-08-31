---
title: 프로젝트 설정 (Azure SQL DB) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 829e7b0c51cd341193944fb2f28241f48618c407
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176229"
---
# <a name="project-settings-azure-sql-db--sybasetosql"></a>프로젝트 설정(Azure SQL DB)(SybaseToSQL)
Azure SQL DB 프로젝트 설정을 사용 하 여 연결 대화 상자에 추가 될 Azure SQL DB 데이터베이스 접미사를 구성 하 고 Azure SQL DB 연결에 하트 비트 메커니즘을 구현할 수도 있습니다.  
  
Azure SQL DB 창은 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자에서 사용할 수 있습니다.  
  
-   프로젝트 설정 대화 상자를 사용 하 여 현재 프로젝트에 대 한 구성 옵션을 설정할 수 있습니다. Azure SQL DB 설정에 액세스 하려면 **도구** 메뉴에서 **프로젝트 설정**을 선택 하 고 왼쪽 창의 맨 아래에서 **일반** 을 클릭 한 다음 **Azure sql db**를 선택 합니다.  
  
-   기본 프로젝트 설정 대화 상자를 사용 하 여 모든 프로젝트에 대 한 구성 옵션을 설정할 수 있습니다. Azure SQL DB 설정에 액세스 하려면 **도구** 메뉴에서 **defaultproject settings**를 선택 하 고 왼쪽 창의 맨 아래에 있는 **일반** 을 클릭 한 다음 **Azure sql db**를 선택 합니다.  
  
## <a name="connectivity"></a>연결  
**하트 비트 간격**  
  
Azure SQL DB 연결을 ' 분: 초 ' 형식으로 유지 하기 위해 하트 비트 메커니즘에 사용할 시간 간격을 지정 합니다.  
  
**기본값**: ' 4:45 '  
  
값은 ' m:ss ' 형식으로 지정 해야 합니다 (예: ' 4:45 ' 또는 ' 0:50 ').  
  
**Azure SQL DB 서버 접미사**  
  
Azure SQL DB 서버 접미사를 지정 합니다.  
  
**기본값**: ' database.windows.net '.  
  

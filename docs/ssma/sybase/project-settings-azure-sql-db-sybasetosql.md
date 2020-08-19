---
description: 프로젝트 설정 (Azure SQL Database) (SybaseToSQL)
title: 프로젝트 설정 (Azure SQL Database) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 39a099eb243d767d18402bcd6baeb6280dbeaad4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418279"
---
# <a name="project-settings-azure-sql-database--sybasetosql"></a>프로젝트 설정 (Azure SQL Database) (SybaseToSQL)
Azure SQL Database 프로젝트 설정을 사용 하 여 연결 대화 상자에서 추가할 Azure SQL Database 데이터베이스 접미사를 구성 하 고 Azure SQL Database 연결에 하트 비트 메커니즘을 구현할 수도 있습니다.  
  
Azure SQL Database 창은 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자에서 사용할 수 있습니다.  
  
-   프로젝트 설정 대화 상자를 사용 하 여 현재 프로젝트에 대 한 구성 옵션을 설정할 수 있습니다. Azure SQL Database 설정에 액세스 하려면 **도구** 메뉴에서 **프로젝트 설정**을 선택 하 고 왼쪽 창의 맨 아래에서 **일반** 을 클릭 한 다음 **Azure SQL Database**을 선택 합니다.  
  
-   기본 프로젝트 설정 대화 상자를 사용 하 여 모든 프로젝트에 대 한 구성 옵션을 설정할 수 있습니다. Azure SQL Database 설정에 액세스 하려면 **도구** 메뉴에서 **defaultproject settings**를 선택 하 고 왼쪽 창의 맨 아래에 있는 **일반** 을 클릭 한 다음 **Azure SQL Database**을 선택 합니다.  
  
## <a name="connectivity"></a>연결  
**하트 비트 간격**  
  
Azure SQL Database 연결을 ' 분: 초 ' 형식으로 유지 하기 위해 하트 비트 메커니즘에 사용할 시간 간격을 지정 합니다.  
  
**기본값**: ' 4:45 '  
  
값은 ' m:ss ' 형식으로 지정 해야 합니다 (예: ' 4:45 ' 또는 ' 0:50 ').  
  
**Azure SQL Database 서버 접미사**  
  
Azure SQL Database 서버 접미사를 지정 합니다.  
  
**기본값**: ' database.windows.net '.  
  

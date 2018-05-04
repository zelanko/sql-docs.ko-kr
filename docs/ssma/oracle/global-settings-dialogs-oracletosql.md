---
title: 전역 설정 (대화 상자) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 43989355-cebf-4d8b-ba3d-fa8546e70230
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: v-pelars
ms.openlocfilehash: 336926af02cd8319e1a0d16250126155e7259e1e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="global-settings-dialogs--oracletosql"></a>전역 설정 (대화 상자) (OracleToSQL)
대화 상자 페이지를 사용 하는 **전역 설정** 대화 상자는 기본 사용자 작업 및 SSMA에 대 한 경고 설정을 지정 합니다.  
  
대화 상자 설정에 액세스 하려면는 **도구** 메뉴 선택 **전역 설정**, 클릭 **GUI** 선택 고 왼쪽된 창 맨 아래에 **대화 상자의**합니다.  
  
## <a name="options"></a>옵션  
**개체를 덮어쓰기 전에 경고 표시**  
SSMA는 SQL server 개체를 변환, 일부 개체는 프로젝트의 SQL Server 메타 데이터에 이미 있습니다. 이러한 개체 이미 변환 되었기 수 있습니다, 또는 개체는 대상 스키마 내에서 개체와 이름이 같은 변환 하는 것을 단순히 있을 수 있습니다.  
  
여부 SSMA 묻는 메시지가 나타납니다 덮어쓰기 중복 개체 정의 대 한 지정 하려면이 옵션을 사용 합니다.  
  
-   선택 하는 경우 **True**, SSMA 중복 개체에 도달할 때 경고 대화 상자가 표시 됩니다. 이 대화 상자에서 개별 개체 또는 모든 중복 된 개체를 덮어쓸지 아니면 모든 중복 된 개체 또는 개별 개체를 건너뛰려면를 지정할 수 있습니다.  
  
-   선택 하는 경우 **False**, **덮어쓰기 기본 동작 개체** 옵션이 기본 동작을 지정 하는 위치를 표시 합니다.  
  
**개체 덮어쓰기 기본 동작**  
선택 하는 경우이 옵션이 나타납니다 **False** 에 대 한는 **경고 개체를 덮어쓰기 전에** 옵션입니다.  
  
기본 개체 덮어쓰기 동작을 지정 하려면이 옵션을 사용 합니다.  
  
-   선택 하는 경우 **True**, SSMA 개체를 SQL Server 프로젝트 메타 데이터에 동일한 이름의 변환할 개체와 동일한 대상 스키마에 자동으로 덮어씁니다.  
  
-   선택 하는 경우 **False**, SSMA 변환 하는 동안 개체 메타 데이터를 덮어쓰지 않습니다.  
  

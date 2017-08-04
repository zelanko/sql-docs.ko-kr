---
title: "전역 설정 (대화 상자) (AccessToSQL) | Microsoft Docs"
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
ms.assetid: 6c2204f2-d49e-49ba-9c0f-f14cf07fa561
caps.latest.revision: 3
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2e86cfce8a8a963a283422ce334c8c2472b8720
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="global-settings-dialogs-accesstosql"></a>전역 설정 (대화 상자) (AccessToSQL)
대화 상자 페이지를 사용 하는 **전역 설정** 대화 상자는 기본 사용자 작업 및 SSMA에 대 한 경고 설정을 지정 합니다.  
  
대화 상자 설정에 액세스 하려면는 **도구** 메뉴 선택 **전역 설정**, 클릭 **GUI** 선택 고 왼쪽된 창 맨 아래에 **대화 상자의**합니다.  
  
## <a name="options"></a>옵션  
**마이그레이션 마법사를 다시 시작할 때 표시**  
옵션을 사용 하거나 사용 하지 않도록 설정 해야 Access 용 SSMA를 **마이그레이션 마법사** SSMA 응용 프로그램의 시작 합니다. 이 옵션은 기본적으로 **True**합니다.  
  
-   옵션 설정 된 경우 **True**, 마이그레이션 마법사 대화 상자는 표시 된 처음 Access 응용 프로그램에 대 한 SSMA를 열 때.  
  
-   옵션 설정 된 경우 **False**마이그레이션 마법사는 표시 되지 않으면 하 고 수동으로 액세스 해야 합니다는 **파일** 메뉴 필요한 경우.  
  
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
  


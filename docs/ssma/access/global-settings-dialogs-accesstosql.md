---
description: 전역 설정 (대화 상자) (AccessToSQL)
title: 전역 설정 (대화 상자) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6c2204f2-d49e-49ba-9c0f-f14cf07fa561
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 43158757be3b64cbd761e8fec8bc878dae4f68c3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423027"
---
# <a name="global-settings-dialogs-accesstosql"></a>전역 설정 (대화 상자) (AccessToSQL)
**전역 설정** 대화 상자의 대화 상자 페이지를 사용 하 여 ssma의 기본 사용자 동작 및 경고 설정을 지정할 수 있습니다.  
  
**도구** 메뉴에서 대화 상자 설정에 액세스 하려면 **전역 설정**을 선택 하 고 왼쪽 창의 맨 아래에 있는 **GUI** 를 클릭 한 다음 **대화 상자**를 선택 합니다.  
  
## <a name="options"></a>옵션  
**시작 시 마이그레이션 마법사 표시**  
Access 용 SSMA에는 SSMA 응용 프로그램 시작 시 **마이그레이션 마법사** 를 사용 하거나 사용 하지 않도록 설정할 수 있는 옵션이 있습니다. 이 옵션은 기본적으로 **True**입니다.  
  
-   이 옵션이 **True**로 설정 된 경우 Access 응용 프로그램용 ssma를 열면 마이그레이션 마법사 대화 상자가 처음에 표시 됩니다.  
  
-   옵션을 **False**로 설정 하면 마이그레이션 마법사가 표시 되지 않으므로 필요한 경우 **파일** 메뉴에서 수동으로 액세스 해야 합니다.  
  
**개체를 덮어쓰기 전에 경고**  
SSMA가 개체를 SQL Server으로 변환 하면 일부 개체가 프로젝트의 SQL Server 메타 데이터에 이미 있을 수 있습니다. 이러한 개체는 이미 변환 된 것일 수 있습니다. 또는 개체는 변환 하려는 개체와 대상 스키마 내에 동일한 이름을 가질 수 있습니다.  
  
이 옵션을 사용 하 여 SSMA에서 중복 개체 정의를 덮어쓸지 묻는 메시지를 표시할지 여부를 지정 합니다.  
  
-   **True**를 선택 하면 중복 된 개체가 나타날 때 ssma에서 경고 대화 상자를 표시 합니다. 이 대화 상자에서를 지정 하 여 개별 개체 또는 모든 중복 개체를 덮어쓰거나 개별 개체 또는 모든 중복 개체를 건너뛸 수 있습니다.  
  
-   **False**를 선택 하는 경우 기본 작업을 지정 하는 **개체 기본 동작 덮어쓰기** 옵션이 나타납니다.  
  
**개체의 기본 덮어쓰기 동작**  
이 옵션은 **개체 덮어쓰기 전 경고** 옵션에 대해 **False** 를 선택 하는 경우에 나타납니다.  
  
기본 개체 덮어쓰기 동작을 지정 하려면이 옵션을 사용 합니다.  
  
-   **True**를 선택 하면 ssma는 변환할 개체와 동일한 이름 및 대상 스키마를 가진 SQL Server 프로젝트 메타 데이터의 개체를 자동으로 덮어씁니다.  
  
-   **False**를 선택 하는 경우 ssma는 변환 중에 개체 메타 데이터를 덮어쓰지 않습니다.  
  

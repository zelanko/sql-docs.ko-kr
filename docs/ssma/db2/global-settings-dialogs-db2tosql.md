---
title: 전역 설정 (대화 상자) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 360e01bb-6347-4e2b-acda-0daa161ed33b
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: de6df03f894d43819cf9d27be3fd35a977631f29
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67989633"
---
# <a name="global-settings-dialogs-db2tosql"></a>전역 설정 (대화 상자) (DB2ToSQL)
**전역 설정** 대화 상자의 대화 상자 페이지를 사용 하 여 ssma의 기본 사용자 동작 및 경고 설정을 지정할 수 있습니다.  
  
**도구** 메뉴에서 대화 상자 설정에 액세스 하려면 **전역 설정**을 선택 하 고 왼쪽 창의 맨 아래에 있는 **GUI** 를 클릭 한 다음 **대화 상자**를 선택 합니다.  
  
## <a name="options"></a>옵션  
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
  

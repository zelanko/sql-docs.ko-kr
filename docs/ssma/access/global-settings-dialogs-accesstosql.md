---
title: 전역 설정 (대화 상자) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6c2204f2-d49e-49ba-9c0f-f14cf07fa561
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5b8ef85b9d0d997ed8aae05fc53aa685a2dcacfa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986412"
---
# <a name="global-settings-dialogs-accesstosql"></a>전역 설정 (대화 상자) (AccessToSQL)
대화 상자 페이지를 사용 합니다 **전역 설정** SSMA에 대 한 경고 설정을 확인 하 고 기본 사용자 동작을 지정 하려면 대화 상자.  
  
설정에 액세스 하는 대화에는 **도구** 메뉴에서 **전역 설정**, 클릭 **GUI** 선택 고 왼쪽된 창 맨 아래에 **대화상자**.  
  
## <a name="options"></a>변수  
**시작 시 마이그레이션 마법사를 표시 합니다.**  
SSMA for Access에 사용 하도록 설정 하거나 사용 하지 않도록 설정 하는 옵션 **마이그레이션 마법사** SSMA 응용 프로그램의 시작 합니다. 이 옵션은 기본적으로 **True**합니다.  
  
-   옵션 설정 된 경우 **True**, 마이그레이션 마법사 대화 상자가 표시 됩니다 처음 액세스 응용 프로그램에 대 한 SSMA를 열면 됩니다.  
  
-   옵션 설정 된 경우 **False**마이그레이션 마법사는 표시 되지 않습니다 하 고 수동으로 액세스 해야 합니다 **파일** 필요한 경우 메뉴.  
  
**개체를 덮어쓰기 전에 경으십시오**  
SSMA는 SQL server 개체를 변환, 일부 개체 프로젝트의 SQL Server 메타 데이터에 이미 있습니다. 이러한 개체가 이미 변환 된 수, 있거나 개체 단순히 변환 하려는 개체와 대상 스키마 내에서 동일한 이름입니다.  
  
SSMA 중복 개체 정의 덮어씁니다 묻는 해야 하는지 여부를 지정 하려면이 옵션을 사용 합니다.  
  
-   선택 하는 경우 **True**, SSMA 중복 개체를 발견할 때 경고 대화 상자가 표시 됩니다. 이 대화 상자에서 개별 개체 또는 모든 중복 개체를 덮어쓸 것인지 또는 개별 개체 또는 중복 개체를 모두 표시 하지 않으려면 값을 지정할 수 있습니다.  
  
-   선택 하는 경우 **False**의 **덮어쓰기 기본 동작 개체** 옵션이 기본 동작을 지정할 표시 됩니다.  
  
**개체 덮어쓰기 기본 동작**  
선택 하는 경우이 옵션이 나타납니다 **False** 에 대 한 합니다 **개체를 덮어쓰기 전에 경고** 옵션입니다.  
  
기본 개체 덮어쓰기 동작을 지정 하려면이 옵션을 사용 합니다.  
  
-   선택 하는 경우 **True**, SSMA 개체를 SQL Server 프로젝트 메타 데이터에서 이름이 같은 변환 될 개체와 동일한 대상 스키마에 자동으로 덮어씁니다.  
  
-   선택 하는 경우 **False**, SSMA 변환 하는 동안 개체 메타 데이터를 덮어쓰지 않습니다.  
  

---
title: 전역 설정 (대화 상자) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 43989355-cebf-4d8b-ba3d-fa8546e70230
author: Shamikg
ms.author: Shamikg
manager: v-pelars
ms.openlocfilehash: a85eb72b3c239b8be0141c445e5d4507efb438cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192345"
---
# <a name="global-settings-dialogs--oracletosql"></a>전역 설정 (대화 상자) (OracleToSQL)
대화 상자 페이지를 사용 합니다 **전역 설정** SSMA에 대 한 경고 설정을 확인 하 고 기본 사용자 동작을 지정 하려면 대화 상자.  
  
설정에 액세스 하는 대화에는 **도구** 메뉴에서 **전역 설정**, 클릭 **GUI** 선택 고 왼쪽된 창 맨 아래에 **대화상자**.  
  
## <a name="options"></a>변수  
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
  

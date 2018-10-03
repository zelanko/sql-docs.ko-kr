---
title: 프로젝트 설정 (시스템 개체 로드) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9418cb34-d869-4d24-95b3-6cb9db949bb0
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: f1497b40fbf3462228af6b0ef9ce964c7212df64
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47664247"
---
# <a name="project-settingsloading-system-objects-oracletosql"></a>프로젝트 설정(시스템 개체 로드)(OracleToSQL)
시스템 개체 로드 페이지의 **프로젝트 설정** 대화 상자는 Oracle 시스템 개체 SSMA 변환 및 로드를 지정할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
시스템 개체 로드 창에서 사용할 수는 **프로젝트 설정** 하 고 **기본 프로젝트 설정** 대화 상자:  
  
-   모든 SSMA 프로젝트에 대 한 설정을 지정 하는 **도구** 메뉴에서 **기본 프로젝트 설정**, 설정을 보거나 에서변경하는데필요한는마이그레이션프로젝트형식을선택**마이그레이션 대상 버전** 클릭 드롭다운 **일반** 클릭 한 다음 확인 하 고 왼쪽된 창 맨 아래에 **시스템 개체 로드**합니다.  
  
-   현재 프로젝트에 대 한 설정을 지정 하는 **도구** 메뉴에서 **프로젝트 설정**, 클릭 **일반** 왼쪽된 창 맨 아래에 클릭하고**시스템 개체 로드**합니다.  
  
## <a name="default-settings"></a>기본 설정  
시스템 개체를 변환 하는 시스템 리소스를 소모 및 시간이 걸립니다. 성능 향상을 위해 SSMA 다음 목록에 표시 된 것 처럼 가장 자주 사용 되는 시스템 개체만 선택 합니다.  
  
-   SYS.DBMS_OUTPUT  
  
-   SYS.DBMS_PIPE  
  
-   SYS.DBMS_UTILITY  
  
-   SYS입니다. 표준  
  
-   SYS.UTL_FILE  
  
-   SYS.DBMS_LOB  
  
-   SYS.DBMS_SQL  
  
-   SYS입니다. DBMS_SESSION  
  
Oracle 개체 추가 시스템 개체를 참조 하는 경우 해당 개체를 선택 해야 합니다. Oracle 데이터베이스 개체에 의해 참조 되는 시스템 개체를 선택 하지 않으면 SSMA 변환 오류를 보고 합니다. 누락 된 시스템 개체 인해 변환 오류가 발생할 경우이 대화 상자에서 누락 된 개체를 선택 합니다. 그런 다음 필요에 따라 변환을 반복할 수 있습니다.  
  

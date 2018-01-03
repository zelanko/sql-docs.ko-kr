---
title: "프로젝트 설정 (개체에 시스템을 로드 하는 방법) (DB2ToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9a545233-1b0a-488a-a1ec-c33aa608dcc1
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f0bf007faf72861607740d5af0f6ec418fefb71f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="project-settingsloading-system-objects-db2tosql"></a>프로젝트 설정 (개체에 시스템을 로드 하는 방법) (DB2ToSQL)
시스템 개체를 로드 페이지는 **프로젝트 설정** 대화 상자를 사용 하면 DB2 시스템 개체 SSMA 변환 및 로드 지정할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
시스템 개체를 로드에서 제공 되는 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자:  
  
-   에 모든 SSMA 프로젝트에 대 한 설정을 지정 하려면는 **도구** 메뉴 선택 **기본 프로젝트 설정**, 설정을 보거나에서 변경 하는 데 필요한는 마이그레이션 프로젝트 형식을 선택 **마이그레이션 대상 버전** 클릭 드롭다운 **일반** 클릭 한 다음 확인 하 고 왼쪽된 창 맨 아래에 **시스템 개체를 로드**합니다.  
  
-   에 현재 프로젝트에 대 한 설정을 지정 하려면는 **도구** 메뉴 선택 **프로젝트 설정**, 클릭 **일반** 클릭 한 다음 확인 하 고 왼쪽된 창 맨 아래에 **시스템 개체를 로드**합니다.  
  
## <a name="default-settings"></a>기본 설정  
시스템 개체를 변환 시스템 리소스를 소모 하며 시간이 걸립니다. 성능 향상을 위해 다음 목록에 표시 된 것 처럼 SSMA에서 가장 자주 사용 되는 시스템 개체를 선택 합니다.  
  
-   SYS입니다. DBMS_OUTPUT  
  
-   SYS입니다. DBMS_PIPE  
  
-   SYS입니다. DBMS_UTILITY  
  
-   SYS입니다. 표준  
  
-   SYS입니다. UTL_FILE  
  
-   SYS입니다. DBMS_LOB  
  
-   SYS입니다. DBMS_SQL  
  
-   SYS입니다. DBMS_SESSION  
  
DB2 개체 추가 시스템 개체를 참조 하는 경우에 해당 개체를 선택 해야 합니다. DB2 데이터베이스 개체에서 참조 되는 시스템 개체를 선택 하지 않으면 SSMA 변환 오류를 보고 합니다. 시스템 개체에 없는 경우에 발생 하는 변환 오류를 수신 하는 경우이 대화 상자에서 누락 된 개체를 선택 합니다. 그런 다음 필요에 따라 변환을 반복할 수 있습니다.  
  

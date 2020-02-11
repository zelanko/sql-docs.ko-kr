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
manager: shamikg
ms.openlocfilehash: a5e8feb6c083c787d877cbc5491c533b8a35d740
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266608"
---
# <a name="project-settingsloading-system-objects-oracletosql"></a>프로젝트 설정(시스템 개체 로드)(OracleToSQL)
**프로젝트 설정** 대화 상자의 시스템 개체 로드 페이지에서는 ssma가 변환 하 고 로드할 Oracle 시스템 개체를 지정할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
시스템 개체 로드 창은 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자에서 사용할 수 있습니다.  
  
-   모든 SSMA 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **기본 프로젝트 설정**을 선택 하 고 마이그레이션 **대상 버전** 드롭다운에서 설정 하거나 변경 해야 하는 설정에 대 한 마이그레이션 프로젝트 유형을 선택 하 고 왼쪽 창의 맨 아래에서 **일반** 을 클릭 한 다음 **시스템 개체 로드**를 클릭 합니다.  
  
-   현재 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **프로젝트 설정**을 선택 하 고 왼쪽 창의 맨 아래에서 **일반** 을 클릭 한 다음 **시스템 개체 로드**를 클릭 합니다.  
  
## <a name="default-settings"></a>기본 설정  
시스템 개체를 변환 하면 시스템 리소스가 소비 되 고 시간이 걸립니다. 성능 향상을 위해 다음 목록에 표시 된 것 처럼 SSMA는 가장 자주 사용 되는 시스템 개체만 선택 합니다.  
  
-   시스템. DBMS_OUTPUT  
  
-   시스템. DBMS_PIPE  
  
-   시스템. DBMS_UTILITY  
  
-   시스템. 비표준  
  
-   시스템. UTL_FILE  
  
-   시스템. DBMS_LOB  
  
-   시스템. DBMS_SQL  
  
-   시스템. DBMS_SESSION  
  
Oracle 개체가 추가 시스템 개체를 참조 하는 경우 해당 개체를 선택 해야 합니다. Oracle 데이터베이스 개체에서 참조 하는 시스템 개체를 선택 하지 않으면 SSMA에서 변환 오류를 보고 합니다. 누락 된 시스템 개체에 의해 발생 하는 변환 오류가 발생 하면이 대화 상자에서 누락 된 개체를 선택 합니다. 그런 다음 필요에 따라 변환을 반복할 수 있습니다.  
  

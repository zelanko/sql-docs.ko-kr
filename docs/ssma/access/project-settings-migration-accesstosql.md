---
description: 프로젝트 설정 (마이그레이션) (AccessToSQL)
title: 프로젝트 설정 (마이그레이션) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration settings
- Project Settings dialog box, Migration
ms.assetid: 4caebc9c-8680-4b99-a8fa-89c43161c95d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3163da352fa925a821287fc1447fd8b6b5e89cdb
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988499"
---
# <a name="project-settings-migration-accesstosql"></a>프로젝트 설정 (마이그레이션) (AccessToSQL)
마이그레이션 프로젝트 설정을 사용 하 여 데이터를 마이그레이션하는 방법을 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 SQL Azure 수 있습니다.  
  
마이그레이션 창은 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자에서 사용할 수 있습니다.  
  
-   **프로젝트 설정** 대화 상자를 사용 하 여 현재 프로젝트에 대 한 구성 옵션을 설정할 수 있습니다. 마이그레이션 설정에 액세스 하려면 **도구** 메뉴에서 **프로젝트 설정**을 선택 하 고 왼쪽 창에서 **일반** 을 클릭 한 다음 **마이그레이션**을 클릭 합니다.  
  
-   **기본 프로젝트 설정** 대화 상자를 사용 하 여 모든 프로젝트에 대 한 구성 옵션을 설정할 수 있습니다. 마이그레이션 설정에 액세스 하려면 **도구** 메뉴에서 **기본 프로젝트 설정**을 선택 하 고, 설정에 액세스 하려는 **마이그레이션 대상 버전** 콤보 상자의 프로젝트 형식을 선택한 후 왼쪽 창의 맨 아래에 있는 **일반** 을 클릭 하 고 **마이그레이션**을 클릭 합니다.  
  
## <a name="options"></a>옵션  
**CHECK 제약 조건**  
테이블에 데이터를 추가할 때 SSMA에서 제약 조건을 확인할 지 여부를 지정 합니다.  
  
-   **기본 모드**: False  
  
-   **낙관적 모드**: True  
  
-   **전체 모드**: False  
  
**트리거 실행**  
테이블에 데이터를 추가할 때 SSMA에서 삽입 트리거를 발생 시켜야 하는지 여부를 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **기본 모드**: False  
  
-   **낙관적 모드**: True  
  
-   **전체 모드**: False  
  
**ID 유지**  
에 데이터를 추가할 때 SSMA에서 액세스 id 값을 유지할지 여부를 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이 값이 False 이면에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] id 값을 할당 합니다.  
  
-   **기본 모드**: True  
  
-   **낙관적 모드**: True  
  
-   **전체 모드**: False  
  
**Null 유지**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 지정 된 기본값과 관계 없이 SSMA가에 데이터를 추가할 때 원본 데이터에서 null 값을 유지할지 여부를 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **기본 모드**: True  
  
-   **낙관적 모드**: False  
  
-   **전체 모드**: True  
  
**테이블 잠금**  
데이터 마이그레이션 중에 SSMA가 테이블에 데이터를 추가할 때 테이블을 잠글 것인지 여부를 지정 합니다. 값이 False 이면 SSMA에서 행 잠금을 사용 합니다.  
  
-   **기본 모드**: True  
  
-   **낙관적 모드**: True  
  
-   **전체 모드**: True  
  
**지원 되지 않는 날짜 바꾸기**  
SSMA에서 가장 이른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜/시간 날짜 (01 년 1 월 1753) 이전의 액세스 날짜를 수정 해야 하는지 여부를 지정 합니다.  
  
-   현재 날짜 값을 유지 하려면 **아무 것도 안 함**을 선택 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 datetime 열에서 01 년 1 월 1753 일 이전 날짜를 수락 하지 않습니다. 이전 날짜를 사용 하는 경우에는 datetime 값을 문자 값으로 변환 해야 합니다.  
  
-   1753 년 1 월 1 일 이전 날짜를 NULL로 변환 하려면 **바꾸기를 null로 바꾸기**를 선택 합니다.  
  
-   지원 되는 날짜를 사용 하 여 01 년 1 월 1 1753 일 이전 날짜를 바꾸려면를 **지원 되는 가장 가까운 날짜로 바꿉니다**. 이 값을 선택 하는 경우 기본적으로 가장 가까운 지원 날짜는 01 년 1 월 1753로 선택 됩니다.  
  
**Batch 크기**  
데이터 마이그레이션 중에 사용 되는 일괄 처리 크기입니다. 트랜잭션은 각 일괄 처리 후에 기록 됩니다. 기본적으로 모든 스키마에 대 한 일괄 처리 크기는 1만입니다.  
  
## <a name="see-also"></a>참고 항목  
[사용자 인터페이스 참조 (액세스)](./user-interface-reference-accesstosql.md)  

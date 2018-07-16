---
title: 서버 구성-데이터 정렬 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- collation configuration, SQL Server
- collation configuration, Setup
- collation configuration
ms.assetid: e3986870-5be4-458b-b671-5ff12a27b022
caps.latest.revision: 19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: abd57940e3caf8af66cb58fdeceebc802e877f6e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37290179"
---
# <a name="server-configuration---collation"></a>서버 구성 - 데이터 정렬
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사의 서버 구성 - 데이터 정렬 페이지에서는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 정렬하기 위해 사용하는 데이터 정렬 설정을 수정할 수 있습니다. 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치나 다른 컴퓨터의 데이터 정렬 설정과 일치하는 옵션을 선택하십시오.  
  
## <a name="options"></a>변수  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대해 사용자 지정  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬의 두 그룹을 제공 합니다: Windows 데이터 정렬 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대해 별도의 데이터 정렬 설정을 지정하거나 두 구성 요소에 대해 동일한 데이터 정렬을 지정할 수 있습니다.  
  
 기본적으로 미국 영어 시스템 로캘에 대해서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬이 선택됩니다. 지역화된 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 기본 데이터 정렬은 컴퓨터의 Windows 시스템 로캘 설정에 의해 결정됩니다.  
  
 기본 설정은 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 데이터 정렬 설정이 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 사용하는 데이터 정렬 설정과 일치해야 하는 경우 또는 다른 컴퓨터의 Windows 시스템 로캘 설정과 일치해야 하는 경우에만 변경해야 합니다.  
  
 **참고** [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 Windows 데이터 정렬만 사용합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 설치할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 과 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 간의 일관된 결과를 얻으려면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 설치하는 동안 Windows 데이터 정렬을 선택하십시오.  
  
 자세한 내용은 [설치 프로그램에서 데이터 정렬 설정](http://go.microsoft.com/fwlink/?LinkId=190977)을 참조하십시오.  
  
## <a name="best-practices"></a>최선의 구현 방법  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 사용하는 Windows 시스템 로캘 및 해당 기본 데이터 정렬 표에 대한 자세한 내용은 [설치 프로그램에서 데이터 정렬 설정](http://go.microsoft.com/fwlink/?LinkId=190977)을 참조하십시오.  
  
 가능한 경우 조직에 대해 단일 데이터 정렬을 사용하십시오. 그러면 모든 데이터베이스, 열, 식 또는 식별자에 대해 명시적으로 데이터 정렬을 지정할 필요가 없습니다. 여러 데이터 정렬과 코드 페이지 설정을 사용해야 할 경우 선행 정렬 우선 순위 규칙을 고려하도록 쿼리를 코딩하십시오. 자세한 내용은 온라인 설명서의 [선행 정렬&#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql)을 참조하세요.  
  
 다음은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 데이터 정렬을 선택할 때 고려해야 할 사항입니다.  
  
-   이진 코드 포인트 기반 정렬이 허용되는 경우 BINARY2 데이터 정렬을 선택합니다.  
  
-   데이터 형식 간 일관성 있는 비교를 원하는 경우 Windows 데이터 정렬을 선택합니다.  
  
-   언어적 정렬에 대한 지원이 중요한 경우 새로운 100수준 데이터 정렬을 사용합니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
-   데이터베이스를 업그레이드된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 마이그레이션하려는 경우에는 기존 데이터베이스 데이터 정렬과 일치하는 데이터 정렬을 선택합니다.  
  
  

---
title: '자습서: SQL Server Management Studio | Microsoft 문서'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.tutorialstart.ssms.f1
helpviewer_keywords:
- projects [SQL Server Management Studio], tutorials
- templates [SQL Server], SQL Server Management Studio
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- solutions [SQL Server Management Studio], tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.assetid: d2bade70-07cf-4d94-b5d2-88aecb538ed1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b6cd02b0679990e7781faf2195b17444cadb53e6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167313"
---
# <a name="tutorial-sql-server-management-studio"></a>자습서: SQL Server Management Studio
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 자습서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인프라 관리를 위한 통합 환경을 소개합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 구성, 모니터링 및 관리를 위한 그래픽 인터페이스를 제공합니다. 또한 데이터베이스 및 데이터 웨어하우스 등 응용 프로그램에 사용되는 데이터 계층 구성 요소를 배포, 모니터링 및 업그레이드할 수도 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 스크립트 편집 및 디버그를 위한 [!INCLUDE[tsql](../../includes/tsql-md.md)], MDX, DMX 및 XML 언어 편집기도 제공합니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서를 통해 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 정보 표시 방식과 기능을 이용하는 방법을 이해할 수 있습니다. 이 자습서는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 제외한 모든 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함된 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 전체 설치에 적용됩니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 기본 설치와 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]와 함께 제공되는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 설치의 경우 이 자습서에 설명된 것과 기능이 약간 다를 수 있습니다.  
  
 실습을 통해 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에 익숙해지는 것이 가장 좋습니다. 이 자습서에서는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 의 구성 요소를 관리하는 방법과 정기적으로 사용하는 기능을 찾는 방법을 배웁니다.  
  
 이 자습서는 다음 3개의 단원으로 이루어져 있습니다.  
  
 [1단원: SQL Server Management Studio의 기본 탐색](lesson-1-basic-navigation-in-sql-server-management-studio.md)  
 이 단원에서는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 구성 요소를 사용하는 방법, 환경 레이아웃을 다시 구성하는 방법 및 기본 레이아웃을 복원하는 방법을 배웁니다.  
  
 [2단원: Transact-SQL 작성](lesson-2-writing-transact-sql.md)  
 이 단원에서는 쿼리 편집기를 여는 방법, 코드를 관리하는 방법 및 쿼리 편집기의 다른 새로운 기능을 사용하는 방법을 배웁니다.  
  
 [3단원: 템플릿, 솔루션 및 스크립트 프로젝트 작업](lesson-3-working-with-templates-solutions-and-script-projects.md)  
 이 단원에서는 템플릿을 사용하여 솔루션 및 프로젝트에 스크립트를 구성하는 방법을 배웁니다.  
  
## <a name="requirements"></a>요구 사항  
 이 자습서는 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에는 익숙하지 않지만 데이터베이스 개념과 [!INCLUDE[tsql](../../includes/tsql-md.md)] 언어에는 익숙한 경험 있는 데이터베이스 관리자와 데이터베이스 개발자를 대상으로 합니다.  
  
 이 자습서를 사용하려면 시스템에 다음 항목이 설치되어야 합니다.  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이상 버전과 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 샘플 데이터베이스. 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다. 예제 데이터베이스를 설치하려면 [SQL Server 예제 및 예제 데이터베이스](http://sqlserversamples.codeplex.com)를 참조하세요.  
  
-   Internet Explorer 9.0 이상  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 자습서](../../relational-databases/database-engine-tutorials.md)  
  
  

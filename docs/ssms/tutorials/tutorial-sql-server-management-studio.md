---
title: "자습서: SSMS(SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 08/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.tutorialstart.ssms.f1
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
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 5aa858aff03e93db9db36b8caa710cc3a3b874ca
ms.openlocfilehash: dde887f6e0999c5ebc107a300c33981a38ec7034
ms.contentlocale: ko-kr
ms.lasthandoff: 08/31/2017

---
# <a name="tutorial-sql-server-management-studio"></a>자습서: SQL Server Management Studio
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

SSMS(SQL Server Management Studio) 자습서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인프라를 관리하기 위한 통합 환경을 소개합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 구성, 모니터링 및 관리를 위한 그래픽 인터페이스를 제공합니다. 또한 데이터베이스 등 응용 프로그램에 사용되는 데이터 계층 구성 요소를 배포, 모니터링 및 업그레이드할 수도 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 스크립트 편집 및 디버그를 위한 [!INCLUDE[tsql](../../includes/tsql-md.md)], MDX, DMX 및 XML 언어 편집기도 제공합니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
이 자습서를 통해 SSMS의 정보 표시 방식과 기능을 사용하는 방법을 이해할 수 있습니다.
  
실습을 통해 SSMS에 익숙해지는 것이 가장 좋습니다. 이 자습서에서는 SSMS의 구성 요소를 관리하는 방법과 정기적으로 사용하는 기능을 찾는 방법을 알아봅니다.  
  
이 자습서는 다음 3개의 단원으로 이루어져 있습니다.  
  
[1단원: SQL Server Management Studio의 기본 탐색](lesson-1-basic-navigation-in-sql-server-management-studio.md)  
이 단원에서는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 구성 요소를 사용하는 방법, 환경 레이아웃을 다시 구성하는 방법 및 기본 레이아웃을 복원하는 방법을 배웁니다.  
  
[2단원: Transact-SQL 작성](lesson-2-writing-transact-sql.md)  
이 단원에서는 쿼리 편집기를 여는 방법, 코드를 관리하는 방법 및 쿼리 편집기의 다른 기능을 사용하는 방법을 알아봅니다.  
  
[3단원: 템플릿, 솔루션 및 스크립트 프로젝트 작업](lesson-3-working-with-templates-solutions-and-script-projects.md)  
이 단원에서는 템플릿을 사용하여 솔루션 및 프로젝트에 스크립트를 구성하는 방법을 배웁니다.  
  
## <a name="requirements"></a>요구 사항  
이 자습서는 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에는 익숙하지 않지만 데이터베이스 개념과 [!INCLUDE[tsql](../../includes/tsql-md.md)]에는 익숙한 경험 있는 데이터베이스 관리자와 데이터베이스 개발자를 대상으로 합니다.  
  
이 자습서를 사용하려면 다음 항목이 설치되어야 합니다.  

  
-   최신 버전의 [SSMS(SQL Server Management Studio)](../download-sql-server-management-studio-ssms.md) 설치  
-   AdventureWorks 예제 데이터베이스를 포함하는 SQL Server 2016 이후 버전 AdventureWorks 예제 데이터베이스를 설치하려면 [AdventureWorks2014](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2014)를 참조하고 AdventureWorks2014(OLTP) 데이터베이스를 설치합니다.  

  
## <a name="see-also"></a>관련 항목:  
[데이터베이스 엔진 자습서](../../relational-databases/database-engine-tutorials.md)  
  
  
  



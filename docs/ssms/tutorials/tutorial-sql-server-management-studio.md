---
title: '자습서: SSMS(SQL Server Management Studio) | Microsoft Docs'
ms.custom: ''
ms.date: 08/30/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-tutorial
ms.reviewer: sstein
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Active
ms.openlocfilehash: 879326583f507b44a23955a42857fd6a8cea911b
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
---
# <a name="tutorials-for-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio) 자습서
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SSMS(SQL Server Management Studio) 자습서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인프라를 관리하기 위한 통합 환경을 소개합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 구성, 모니터링 및 관리를 위한 그래픽 인터페이스를 제공합니다. 또한 데이터베이스 등 응용 프로그램에 사용되는 데이터 계층 구성 요소를 배포, 모니터링 및 업그레이드할 수도 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 스크립트 편집 및 디버그를 위한 [!INCLUDE[tsql](../../includes/tsql-md.md)], MDX, DMX 및 XML 언어 편집기도 제공합니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  

이러한 자습서를 통해 SSMS의 정보 표시 방식과 기능을 사용하는 방법을 이해할 수 있습니다.
  
실습을 통해 SSMS에 익숙해지는 것이 가장 좋습니다. 이러한 자습서를 통해 SSMS 내에서 사용 가능한 다양한 기능을 익힐 수 있습니다.  이러한 자습서에서는 SSMS의 구성 요소를 관리하는 방법과 정기적으로 사용하는 기능을 찾는 방법을 알아봅니다.  

자습서에서 다루는 내용은 다음과 같습니다. 

  
- [자습서: SSMS를 사용하여 SQL Server 연결 및 쿼리](connect-query-sql-server.md)

    이 자습서에서는 SQL Server 인스턴스에 연결하는 방법을 알아봅니다. 또한 새 데이터베이스를 만든 다음, 쿼리하는 몇 가지 기본 T-SQL(Transact-SQL) 명령을 알아봅니다. 

- [자습서: SSMS에서 개체 스크립팅](scripting-ssms.md)

    이 자습서에서는 데이터베이스 및 쿼리를 포함하여 SSMS에서 다양한 개체를 스크립팅하는 방법을 알아봅니다. 

- [자습서: SSMS에서 템플릿 사용](templates-ssms.md)
   
    이 자습서에서는 SSMS 내에서 미리 작성된 템플릿으로 작업하는 방법을 알아봅니다. 템플릿은 다양한 데이터베이스 관리 작업을 위해 많은 Transact-SQL 코드 조각을 저장하는 잘 알려지지 않은 기능입니다. 

- [자습서: SSMS 구성](ssms-configuration.md)

    이 자습서에서는 환경 레이아웃 변경 등, SSMS 환경 구성의 기본 사항을 학습합니다. 이 자습서는 다양한 SSMS 구성 요소에 대해서도 설명합니다. 
  

- [자습서: SSMS 사용을 위한 추가 팁과 요령](ssms-tricks.md)

    이 자습서에서는 SSMS 사용을 위한 추가 팁과 요령을 알아봅니다. 자습서에는 다음이 포함되어 있습니다.
    - 텍스트 주석 처리 및 주석 처리 제거
    - 텍스트 들여쓰기
    - 개체 탐색기에서 개체 필터링
    - SQL Server 오류 로그에 액세스
    - 인스턴스 이름 찾기 
 
  
## <a name="requirements"></a>요구 사항  
이 자습서는 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에는 익숙하지 않지만 데이터베이스 개념과 [!INCLUDE[tsql](../../includes/tsql-md.md)]에는 익숙한 경험 있는 데이터베이스 관리자와 데이터베이스 개발자를 대상으로 합니다.  
  
이 자습서를 사용하려면 다음 항목이 설치되어야 합니다.  

  -   최신 버전의 [SSMS(SQL Server Management Studio)](../download-sql-server-management-studio-ssms.md) 설치  

첫 번째 섹션에서는 데이터베이스를 만드는 과정을 설명하지만 다른 샘플 데이터베이스는 여기: [AdventureWorks 샘플 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases)에서 찾을 수 있습니다. SSMS에서 데이터베이스를 복원하기 위한 지침은 여기: [데이터베이스 복원](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)에서 찾을 수 있습니다. 


  
## <a name="see-also"></a>참고 항목  
[데이터베이스 엔진 자습서](../../relational-databases/database-engine-tutorials.md)  
  
  
  


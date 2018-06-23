---
title: SQL Server 데이터베이스 엔진에 대 한 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
caps.latest.revision: 44
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4316e91e465922ca1f7c428a9f25e781837ec6e4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092246"
---
# <a name="about-the-sql-server-database-engine"></a>SQL Server 데이터베이스 엔진 정보
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소는 데이터 저장, 처리 및 보안 유지를 위한 핵심 서비스입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 기업에서 수요가 높아지고 있는 대부분의 데이터 소비형 응용 프로그램의 요구 사항을 만족시키기 위해 액세스 제어 및 빠른 트랜잭션 처리를 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 한 대의 컴퓨터에서 최대 50개의 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 지원합니다. 일반적인 만들려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 참조 [설치 마법사에서 SQL Server 2014 설치 &#40;설치&#41;](install-sql-server-from-the-installation-wizard-setup.md)합니다.  
  
 **중요** 로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사의 설치할 구성 요소 페이지에서** 데이터베이스 엔진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 선택하면 다음 기능이 설치됩니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   복제 - 선택적 구성 요소입니다.  
  
-   전체 텍스트 검색 - 선택적 구성 요소입니다.  
  
-   Data Quality Services - 선택적 구성 요소입니다.  
  
    > [!NOTE]  
    >  이 릴리스에서는 설치 중에 **Data Quality Services** 확인란을 선택해도 DQS(Data Quality Services) 서버가 설치되지 않습니다. DQS 서버를 설치하려면 추가적인 사후 설치 단계를 수행해야 합니다. 자세한 내용은 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)을 참조하세요.  
  
 일반적인 여러 사용자 시나리오에서 다음과 같은 추가 기능이 옵션으로 제공됩니다.  
  
-   Data Quality 클라이언트  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   연결 구성 요소  
  
-   프로그래밍 모델  
  
-   관리 도구  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   설명서 구성 요소  
  
> [!NOTE]  
>  기본적으로 예제 데이터베이스와 예제 코드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 일부로 설치되지 않습니다. 예제 데이터베이스와 예제 코드를 설치하려면 [CodePlex 웹 사이트](http://go.microsoft.com/fwlink/?LinkId=87843)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [버전 및 SQL Server 2014 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)   
 [고가용성 솔루션&#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [업그레이드를 SQL Server 2014 설치 마법사를 사용 하 여 &#40;설치&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
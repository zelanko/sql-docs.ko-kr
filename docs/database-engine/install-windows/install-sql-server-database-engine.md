---
title: SQL Server 데이터베이스 엔진 설치 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 968cf923f1defcf724b3a3c8a968a20c54f3e30b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67991106"
---
# <a name="install-sql-server-database-engine"></a>SQL Server 데이터베이스 엔진 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

## <a name="overview"></a>개요
[!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소는 데이터 저장, 처리 및 보안 유지를 위한 핵심 서비스입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 기업에서 수요가 높아지고 있는 대부분의 데이터 소비형 애플리케이션의 요구 사항을 만족시키기 위해 액세스 제어 및 빠른 트랜잭션 처리를 제공합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 한 대의 컴퓨터에서 최대 50개의 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 지원합니다. 표준 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치를 만들려면 [설치 마법사에서 SQL Server 설치&#40;설치 프로그램&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)를 참조하세요.  
  
>[!IMPORTANT]
>로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.  

## <a name="features"></a>기능
**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사의 설치할 구성 요소 페이지에서** 데이터베이스 엔진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 선택하면 다음 기능이 설치됩니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [SQL Server 복제](../../relational-databases/replication/sql-server-replication.md) - 선택적 구성 요소입니다.  

-   [R 및 Python을 사용하는 Machine Learning Services(데이터베이스 내)](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md) - 선택적 구성 요소입니다.

-   전체 텍스트 검색 - 선택적 구성 요소입니다.  
  
-   Data Quality Services - 선택적 구성 요소입니다.  
  
    > [!NOTE]  
    >  이 릴리스에서는 설치 중에 **Data Quality Services** 확인란을 선택해도 DQS(Data Quality Services) 서버가 설치되지 않습니다. DQS 서버를 설치하려면 추가적인 사후 설치 단계를 수행해야 합니다. 자세한 내용은 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)을 참조하세요.  
    
- [외부 데이터용 Polybase 쿼리 서비스](../../relational-databases/polybase/polybase-guide.md) - 선택적 구성 요소입니다. SQL Server 2019부터 HDFS 데이터 원본용 Java 커넥터도 사용할 수 있습니다.

  
 일반적인 여러 사용자 시나리오에서 다음과 같은 추가 기능이 옵션으로 제공됩니다.  
  
-   Data Quality 클라이언트
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]
-   연결 구성 요소
-   프로그래밍 모델
-   관리 도구
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]
-   설명서 구성 요소  
  

> [!NOTE]  
>  기본적으로 예제 데이터베이스와 예제 코드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 일부로 설치되지 않습니다. 예제 데이터베이스와 예제 코드를 설치하려면 [Microsoft SQL Server 예제](../../sample/microsoft-sql-server-samples.md)를 참조하세요. [CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843)에서 이전 예제를 참조하세요.  

  
## <a name="see-also"></a>관련 항목:  
 [버전 및 SQL Server 2017의 지원되는 기능](~/sql-server/editions-and-components-of-sql-server-2017.md)   
 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)   
 [고가용성 솔루션&#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [설치 마법사를 사용하여 SQL Server 업그레이드&#40;설치 프로그램&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  

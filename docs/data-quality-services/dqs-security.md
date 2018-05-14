---
title: DQS 보안 | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 921927f5-1b1e-452a-a79e-c691829fd826
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a10493cb997e0b361f603b5071a7c4e4b45f1464
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dqs-security"></a>DQS 보안

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] ) 보안 인프라는 SQL Server 보안 인프라를 기반으로 합니다. 데이터베이스 관리자는 사용자와 DQS 역할을 연결하여 사용자에게 사용 권한 집합을 부여합니다. 이러한 방식으로 사용자가 액세스할 수 있는 DQS 리소스와 사용자가 수행할 수 있는 기능 작업이 결정됩니다.  
  
## <a name="dqs-roles"></a>DQS 역할  
 DQS 역할은 4가지입니다. 하나는 주로 제품 설치, 데이터베이스 유지 관리 및 사용자 관리를 다루는 DBA(데이터베이스 관리자)입니다. 이 역할은 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 응용 프로그램보다는 주로 SQL Server Management Studio를 사용합니다. 서버 역할은 sysadmin입니다.  
  
 나머지 3개 역할은 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 응용 프로그램에서 작업하는 방식으로 제품을 직접 사용하는 정보 근로자, 데이터 관리자입니다. 이러한 역할은 다음과 같습니다.  
  
-   **DQS 관리자** (dqs_administrator 역할)는 제품 범위 내에서 모든 작업을 수행할 수 있습니다. DQS 관리자는 프로젝트 편집 및 실행, 기술 자료 생성 및 편집, 작업 종료, 작업 내 프로세스 중지를 수행할 수 있고 구성 및 참조 Data Services 설정을 변경할 수 있습니다. 그러나 서버를 설치하거나 새 사용자를 추가할 수는 없습니다. 이러한 작업은 데이터베이스 관리자가 수행해야 합니다.  
  
-   **DQS KB 편집자** (dqs_kb_editor 역할)는 관리를 제외한 모든 DQS 작업을 수행할 수 있습니다. KB 편집자는 프로젝트를 편집하고 실행할 수 있고, 기술 자료를 만들고 편집할 수 있습니다. 작업 모니터링 데이터를 볼 수는 있지만 특정 작업을 종료 또는 중지하거나 관리상의 임무를 수행할 수는 없습니다.  
  
-   **DQS KB 운영자** (dqs_kb_operator 역할)는 프로젝트를 편집하고 실행할 수 있습니다. DQS KB 운영자는 어떠한 유형의 기술 자료 관리도 수행할 수 없습니다. 기술 자료를 만들거나 변경할 수 없습니다. 이 운영자는 작업 모니터링 데이터를 볼 수는 있지만 특정 작업을 종료하거나 관리상의 임무를 수행할 수는 없습니다.  
  
## <a name="user-management"></a>사용자 관리  
 데이터베이스 관리자(DBA)는 SQL Server Management Studio에서 DQS 사용자를 만들어 DQS 역할에 연결합니다. DBA는 SQL 로그인을 DQS_MAIN 데이터베이스의 사용자로 추가하고 각 사용자를 DQS 역할 중 하나에 연결하는 방식으로 사용자의 사용 권한을 관리합니다. 각 역할에는 DQS_MAIN 데이터베이스의 저장 프로시저 집합에 대한 사용 권한이 부여됩니다. DQS_PROJECTS 및 DQS_STAGING_DATA 데이터베이스의 경우 이 세 가지 역할을 사용할 수 없습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|SQL Server Management Studio를 사용하여 사용자를 만들고 DQS 역할을 부여하는 방법에 대해 설명합니다.|[SSMS에서 DQS 사용자 관리](http://msdn.microsoft.com/library/955af01d-00da-4c51-9311-f3848749df54)|  
  
  

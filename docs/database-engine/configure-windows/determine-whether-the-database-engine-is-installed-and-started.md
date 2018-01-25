---
title: "데이터베이스 엔진이 설치 및 시작되었는지 확인 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server, determining if installed
- verifying Database Engine installation
- viewing Database Engine installation
- installed Database Engine verification [SQL Server]
ms.assetid: babb02e4-3521-4b75-b5df-e09205594375
caps.latest.revision: "17"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: d15c13d7a5a52616c4e6cd0c837e0979652b89f4
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="determine-whether-the-database-engine-is-installed-and-started"></a>데이터베이스 엔진이 설치 및 시작되었는지 확인
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 설치에 성공하면 파일 시스템에 파일이 설치되고 레지스트리에 항목이 생성되며 여러 가지 도구가 설치됩니다. 이 항목에서는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 설치 및 시작되었는지 여부를 확인하는 방법에 대해 설명합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### <a name="how-to-view-and-start-the-database-engine-by-using-sql-server-configuration-manager"></a>SQL Server 구성 관리자를 사용하여 데이터베이스 엔진을 보고 시작하는 방법  
  
1.  **시작**을 클릭하고 **모든 프로그램**, **Microsoft SQL Server**, **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
     **시작** 메뉴에 이러한 항목이 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 올바르게 설치되지 않은 것입니다. 설치 프로그램을 실행하여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을 설치합니다.  
  
2.  **SQL Server 구성 관리자**의 왼쪽 창에서 **SQL Server 서비스**를 클릭합니다. 오른쪽 창에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 관련된 여러 가지 서비스가 표시됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 설치되어 있으면 기본 인스턴스인 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스가 **SQL Server(MSSQLSERVER)** 로 표시되고 **이 명명된 인스턴스로 설치된 경우**\<*SQL Server(*>**instance_name**) [!INCLUDE[ssDE](../../includes/ssde-md.md)] 로 표시됩니다. 인스턴스 이름을 변경하지 않으면 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 는 **SQLEXPRESS**라는 이름의 명명된 인스턴스로 설치됩니다. 녹색 삼각형 아이콘은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 실행되고 있음을 나타냅니다. 빨간색 정사각형 아이콘은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 중지되었음을 나타냅니다.  
  
3.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 시작하려면 오른쪽 창에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 마우스 오른쪽 단추로 클릭한 다음 **시작**을 클릭합니다.  
  
> [!NOTE]  
>  설치 중에 사용자는 프로그램 파일과 데이터베이스 파일을 설치할 위치를 선택할 수 있습니다. 사용자가 기본 위치를 적용하면 파일은 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)] 및 C:\Program Files\Microsoft SQL Server\MSSQL.*x*에 설치됩니다. 여기서 *x* 는 숫자입니다.  
  
  

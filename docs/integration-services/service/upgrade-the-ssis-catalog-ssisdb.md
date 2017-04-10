---
title: "SSIS 카탈로그(SSISDB) 업그레이드 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.dbupgradewizard.f1"
ms.assetid: 170c3dc9-f5bf-4599-ae56-d24a620f23e8
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# SSIS 카탈로그(SSISDB) 업그레이드
  데이터베이스가 SQL Server 인스턴스의 최신 버전보다 오래된 상태이면 SSISDB 업그레이드 마법사를 사용하여 SSIS 카탈로그 데이터베이스인 SSISDB를 업그레이드합니다. 다음 조건 중 하나에 해당하는 경우 이 업그레이드를 수행합니다.  
  
-   이전 버전의 SQL Server에서 데이터베이스를 복원한 경우  
  
-   SQL Server 인스턴스를 업그레이드하기 전에 Always On 가용성 그룹에서 데이터베이스를 제거하지 않은 경우. 이 경우 데이터베이스가 자동으로 업그레이드되지 않습니다. 자세한 내용은 [Upgrading SSISDB in an availability group](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Upgrade)를 참조하십시오.  
  
 마법사는 로컬 서버 인스턴스의 데이터베이스만 업그레이드할 수 있습니다.  
  
## SSISDB 업그레이드 마법사를 실행하여 SSIS 카탈로그(SSISDB) 업그레이드  
  
1.  SSIS 카탈로그 데이터베이스(SSISDB)를 백업합니다.  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 로컬 서버와 **Integration Services 카탈로그**를 차례로 확장합니다.  
  
3.  **SSISDB**를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 업그레이드**를 선택하여 SSISDB 업그레이드 마법사를 시작합니다.  
  
     ![Launch the SSISDB upgrade wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-1.png "Launch the SSISDB upgrade wizard")  
  
4.  **인스턴스 선택** 페이지에서 로컬 서버의 SQL Server 인스턴스를 선택합니다.  
  
    > [!IMPORTANT]  
    >  마법사는 로컬 서버 인스턴스의 데이터베이스만 업그레이드할 수 있습니다.  
  
     마법사를 실행하기 전에 SSISDB 데이터베이스를 백업했음을 나타내는 확인란을 선택합니다.  
  
     ![Select the server in the SSISDB Upgrade Wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-2.png "Select the server in the SSISDB Upgrade Wizard")  
  
5.  **업그레이드** 를 선택하여 SSIS 카탈로그 데이터베이스를 업그레이드합니다.  
  
6.  **결과** 페이지에서 결과를 검토합니다.  
  
     ![Review the results in the SSISDB Upgrade Wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-3.png "Review the results in the SSISDB Upgrade Wizard")  
  
  
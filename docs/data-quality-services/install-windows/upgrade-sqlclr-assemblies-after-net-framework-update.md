---
title: ".NET Framework 업데이트 후 SQLCLR 어셈블리 업그레이드 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b1a008cc-7e6b-4655-a869-bd429f986400
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f234417f1e1148a0edce88df46835f63ef22625
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="upgrade-sqlclr-assemblies-after-net-framework-update"></a>.NET Framework 업데이트 후 SQLCLR 어셈블리 업그레이드
  [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS)는 Microsoft .NET Framework 4 어셈블리를 참조하는 SQLCR(SQL 공용 언어 런타임)의 컬렉션입니다. 참조되는 이러한 .NET Framework 어셈블리에 영향을 주는 .NET Framework 업데이트를 컴퓨터에 설치하면 GAC(전역 어셈블리 캐시)의 어셈블리 MVID(모듈 버전 ID)가 변경될 수 있습니다. 이렇게 되면 GAC의 참조되는 어셈블리 MVID와 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 어셈블리 MVID 간에 불일치가 발생합니다.  
  
 .NET Framework 업데이트를 위해 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 컴퓨터를 다시 시작해야 하는 경우 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 컴퓨터를 다시 시작하면 영향을 받는 SQLCLR 어셈블리가 자동으로 업그레이드되어 MVID 불일치 문제가 해결됩니다. 그러나 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 서버 컴퓨터를 다시 시작할 필요가 없는 .NET Framework 업데이트의 경우 어셈블리 MVID의 불일치로 인해 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 를 사용하여 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]에 연결하려고 할 때 오류가 발생합니다.  
  
```  
A new version of .NET was installed on this machine. In order to continue to work with DQS please run dqsinstaller.exe –upgradedlls.  
```  
  
 이 문제를 해결하려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 영향을 받는 SQLCLR 어셈블리를 업그레이드해야 합니다. DQS 데이터베이스를 다시 만드는 것을 건너뛰고 영향을 받는 어셈블리만 업그레이드하도록 **upgradedlls** 명령줄 매개 변수를 사용하여 DQSInstaller.exe를 실행하면 됩니다. 이렇게 하면 기술 자료, 데이터 품질 프로젝트 및 DQS의 다른 데이터를 유지할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
  
-   [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 컴퓨터에서 Administrators 그룹의 멤버로 로그온해야 합니다.  
  
-   Windows 사용자 계정은 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 가 설치된 SQL Server 인스턴스에서 sysadmin 고정 서버 역할의 멤버여야 합니다.  
  
### <a name="to-upgrade-sqlclr-assemblies"></a>SQLCLR 어셈블리를 업그레이드하려면  
  
1.  명령 프롬프트를 시작합니다.  
  
2.  명령 프롬프트에서 디렉터리를 DQSInstaller.exe가 있는 위치로 변경합니다. SQL Server의 기본 인스턴스를 설치한 경우 DQSInstaller.exe 파일은 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn에 있습니다.  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn  
    ```  
  
3.  명령 프롬프트에 다음 명령을 입력하고 Enter 키를 누릅니다.  
  
    ```  
    dqsinstaller.exe -upgradedlls  
    ```  
  
4.  나머지 단계는 [DQSInstaller.exe를 실행하여 Data Quality 서버 설치 완료](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#WindowsExplorer) 의 [시작 화면, 시작 메뉴 또는 Windows 탐색기에서 DQSInstaller.exe 실행](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)섹션에 설명된 2~6단계와 같습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Data Quality Services 설치](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [SQL Server 업데이트 설치 후 DQS 데이터베이스 스키마 업그레이드](../../data-quality-services/install-windows/upgrade-dqs-databases-schema-after-installing-sql-server-update.md)  
  
  

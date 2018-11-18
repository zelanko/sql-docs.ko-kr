---
title: SQL Server 업데이트 설치 후 DQS 데이터베이스 스키마 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
ms.assetid: c8f3fbae-02c4-464d-a35c-7108f48c58cb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a3743dbd355f2f6a45e3a73559a1bef93f8f2dd9
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51699741"
---
# <a name="upgrade-dqs-databases-schema-after-installing-sql-server-update"></a>SQL Server 업데이트 설치 후 DQS 데이터베이스 스키마 업그레이드

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이전에 구성한 DQS 인스턴스에 SQL Server 업데이트(패치, 핫픽스 또는 누적 업데이트)를 설치한 후에 **upgrade** 명령줄 매개 변수로 DQSInstaller.exe 파일을 실행하여 DQS 데이터베이스를 업그레이드해야 할 수 있습니다. 그렇지 않으면 Data Quality 클라이언트를 사용하여 Data Quality Server에 연결하려고 할 때 다음과 같은 오류 메시지가 나타날 수 있습니다.  
  
```  
An error occurred in the Microsoft .NET Framework while trying to load assembly id 65581.  
```  
  
 DQS 데이터베이스 스키마를 업그레이드해도 DQS 데이터베이스의 기존 데이터(기술 자료, 데이터 품질 프로젝트, DQS_STAGING_DATA 데이터베이스의 내보낸 결과)에 영향을 주지 않습니다. 그러나 스키마 업그레이드 중에 데이터 손실을 방지하기 위해 DQS 데이터베이스 스키마를 업그레이드하기 전에 DQS 데이터베이스를 백업해야 합니다. DQS 데이터베이스 백업에 대한 자세한 내용은 [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)을 참조하십시오.  
  
> [!NOTE]  
>  대부분의 경우 SQL Server를 업데이트하려면 DQS 데이터베이스 스키마로 업그레이드해야 합니다. DQS 데이터베이스 스키마로 업그레이드해야 하는 SQL Server 업데이트에 대한 자세한 내용은 [DQS 업그레이드: Data Quality Services에서 누적 업데이트 또는 핫픽스 패치 설치](https://go.microsoft.com/fwlink/?LinkID=251565)의 1.A 단계를 참조하세요.  
  
## <a name="prerequisites"></a>사전 요구 사항  
  
-   [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 컴퓨터에서 Administrators 그룹의 멤버로 로그온해야 합니다.  
  
-   Windows 사용자 계정은 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 가 설치된 SQL Server 인스턴스에서 sysadmin 고정 서버 역할의 멤버여야 합니다.  
  
### <a name="to-upgrade-dqs-databases-schema"></a>DQS 데이터베이스 스키마를 업그레이드하려면  
  
1.  스키마 업그레이드를 계속하기 전에 DQS 데이터베이스를 백업하는 것이 좋습니다. DQS 데이터베이스 백업에 대한 자세한 내용은 [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)을 참조하십시오.  
  
2.  명령 프롬프트를 시작합니다.  
  
3.  명령 프롬프트에서 디렉터리를 DQSInstaller.exe가 있는 위치로 변경합니다. SQL Server의 기본 인스턴스를 설치한 경우 DQSInstaller.exe 파일은 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn에 있습니다.  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn  
    ```  
  
4.  명령 프롬프트에 다음 명령을 입력하고 Enter 키를 누릅니다.  
  
    ```  
    dqsinstaller.exe -upgrade  
    ```  
  
5.  설치 관리자에서 계속하기 전에 DQS 데이터베이스를 백업하라는 메시지를 표시합니다. DQS 데이터베이스를 이미 백업했으면 **Y** 또는 **Yes** 를 입력하고 ENTER 키를 눌러 업그레이드를 계속하십시오.  
  
6.  DQS 데이터베이스 스키마 업그레이드에 성공하면 완료 메시지가 표시됩니다.  
  
## <a name="next-steps"></a>Next Steps  
 Data Quality 클라이언트 응용 프로그램에서 업그레이드된 Data Quality Server에 로그온합니다.  
  
 SQL Server 업데이트 설치 후 DQS 데이터베이스 스키마 업그레이드 및 관련 문제 해결 단계에 대한 자세한 내용은 [DQS 업그레이드: Data Quality Services에서 누적 업데이트 또는 핫픽스 패치 설치](https://go.microsoft.com/fwlink/?LinkID=251565)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Data Quality Services 설치](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [.NET Framework 업데이트 후 SQLCLR 어셈블리 업그레이드](../../data-quality-services/install-windows/upgrade-sqlclr-assemblies-after-net-framework-update.md)  
  
  

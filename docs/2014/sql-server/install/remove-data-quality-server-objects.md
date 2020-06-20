---
title: Data Quality 서버 개체 제거 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 1b7c6dbb-b40e-4822-9caa-608e1056af8e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 870913346a7754e54cfd007f7c2b988b9b216cc4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036661"
---
# <a name="remove-data-quality-server-objects"></a>Data Quality 서버 개체 제거
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 제거하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 있는 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 의 인스턴스를 완전히 제거해도 DQS 데이터베이스 등의 일부 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 개체는 삭제되지 않습니다. 이로 인해 사용자가 SQL Server 설치 프로그램을 사용하여 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 를 제거할 때 DQS 데이터가 삭제되지 않습니다. 제거 프로세스가 완료된 후 이러한 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 개체를 수동으로 삭제해야 합니다.  
  
> [!NOTE]
>  -   [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]를 제거하기 전에 기존의 모든 기술 자료를 .dqsb 파일로 내보내서 백업하는 것이 좋습니다. 이 파일은 나중에 모든 기술 자료를 다시 새 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 설치로 가져오는 데 사용할 수 있습니다. 모든 DQS 기술 자료를 내보내고 가져오는 작업은 명령 프롬프트에서 적합한 명령줄 매개 변수와 함께 DQSInstaller.exe를 실행해서만 수행할 수 있습니다. 자세한 내용은 [Dqsinstaller.exe를 사용하여 DQS 기술 자료 내보내기 및 가져오기](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)을(를) 참조하세요.  
> -   DQS 데이터베이스를 삭제하기 전에 데이터베이스를 보존하고 나중에 데이터를 복원하는 데 사용하려는 경우 데이터베이스를 백업하십시오. 이렇게 하는 방법은 [DQS 데이터베이스 관리](../../../2014/data-quality-services/manage-dqs-databases.md)를 참조하세요.  
  
## <a name="uninstall-data-quality-server-from-a-sql-server-instance"></a>SQL Server 인스턴스에서 Data Quality 서버 제거  
 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]만 제거하는 경우 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 제거 프로세스가 완료된 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 다음 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 개체를 수동으로 삭제해야 합니다.  
  
-   DQS_MAIN, DQS_PROJECTS 및 DQS_STAGING_DATA 데이터베이스.  
  
-   \##MS_dqs_db_owner_login## 및 ##MS_dqs_service_login## logins.  
  
-   master 데이터베이스의 DQInitDQS_MAIN 저장 프로시저  
  
 SQL Server Management Studio에서 개체를 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **삭제** 를 클릭하여 이러한 개체를 삭제할 수 있습니다.  
  
> [!IMPORTANT]  
>  명령 프롬프트에서 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 명령줄 매개 변수를 사용하여 SQL Server 인스턴스에서 `-uninstall` 를 제거하는 경우 제거 프로세스의 일부로 모든 DQS 객체가 삭제됩니다. [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]를 제거한 후 이를 수동으로 삭제할 필요가 없습니다. 명령 프롬프트에서 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 를 제거하려면 명령 프롬프트에 다음   
> `dqsinstaller.exe -uninstall`  
  
## <a name="uninstall-sql-server-instance-containing-data-quality-server"></a>Data Quality 서버를 포함하는 SQL Server 인스턴스 제거  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 포함된 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]인스턴스를 완전히 제거하는 경우 제거 프로세스가 완료된 후 컴퓨터에서 DQS_MAIN, DQS_PROJECTS 및 DQS_STAGING_DATA 데이터베이스를 수동으로 삭제해야 합니다. 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 경우 DQS_MAIN, DQS_PROJECTS 및 DQS_STAGING_DATA 데이터베이스 파일은 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA에 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server의 기존 인스턴스 제거&#40;설치 프로그램&#41;](../../../2014/sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)   
 [SQL Server 2014 제거](uninstall-sql-server.md)  
  
  

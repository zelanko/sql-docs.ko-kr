---
title: SQL Server 유틸리티에서 SQL Server 인스턴스 제거 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.utility.remove.f1
ms.assetid: ae1d126a-46d2-47bf-b339-17c743df6491
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: df13432a0b5f835690dd6371fd935198d7798b40
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783285"
---
# <a name="remove-an-instance-of-sql-server-from-the-sql-server-utility"></a>SQL Server 유틸리티에서 SQL Server 인스턴스 제거
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스를 제거하려면 다음 단계를 수행하세요. 이 절차를 수행하면 UCP 목록 뷰에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 제거되며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 데이터 컬렉션이 중지됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 제거되는 것은 아닙니다.  
  
> [!IMPORTANT]  
>  이 절차를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스를 제거하기 전에 제거할 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 SQL Server 에이전트 서비스가 실행 중인지 확인하십시오.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 유틸리티 탐색기에서 **관리되는 인스턴스**를 클릭합니다. 유틸리티 탐색기 탐색 창에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 목록 뷰를 살펴봅니다.  
  
2.  목록 뷰의 **SQL Server 인스턴스 이름** 열에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 제거할 인스턴스를 선택합니다. 제거할 인스턴스를 마우스 오른쪽 단추로 클릭하고 **Managed Instance 제거...** 를 선택합니다.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 관리자 권한이 있는 자격 증명을 지정합니다. **연결...** 을 클릭하고 **서버에 연결** 대화 상자의 정보를 확인한 다음, **연결**을 클릭합니다. **관리되는 인스턴스 제거** 대화 상자에 로그인 정보가 표시됩니다.  
  
4.  작업을 수행하려면 **확인**을 클릭합니다. 작업을 취소하려면 **취소**를 클릭합니다.  
  
## <a name="manually-remove-a-managed-instance-of-sql-server-from-a-sql-server-utility"></a>SQL Server 유틸리티에서 수동으로 SQL Server의 관리되는 인스턴스 제거  
 이 절차를 수행하면 UCP 목록 뷰에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 제거되며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 데이터 컬렉션이 중지됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 제거되는 것은 아닙니다.  
  
 PowerShell을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스를 제거하려면 다음 단계를 수행하세요. 이 스크립트는 다음 작업을 수행합니다.  
  
-   서버 인스턴스 이름으로 UCP를 얻습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스를 제거합니다.  
  
```powershell
# Get Ucp connection  
$UcpServerInstanceName = "ComputerName\InstanceName";  
$UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server $UcpServerInstanceName;  
$UcpConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
$Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($UcpConnection);  
  
# Now remove the ManagedInstance from the SQL Server Utility  
$ServerInstanceName = "ComputerName\InstanceName";  
$Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server $ServerInstanceName;  
$InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
$ManagedInstance = $Utility.ManagedInstances[$ServerInstanceName];  
$ManagedInstance.Remove($InstanceConnection);  
```  
  
에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]저장 된 것과 동일 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게 인스턴스 이름을 참조 하는 것이 중요 합니다. 대/소문자를 구분하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서는 @@SERVERNAME으로 반환되는 것과 동일하게 대/소문자를 지정해야 합니다. 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스의 인스턴스 이름을 얻으려면 관리되는 인스턴스에서 이 쿼리를 실행합니다.  
  
```sql
select @@SERVERNAME AS instance_name  
```  
  
 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스가 UCP에서 완전하게 제거됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 데이터를 다음번 새로 고치면 목록 뷰에 해당 인스턴스가 표시되지 않습니다. 이 상태는 SSMS 사용자 인터페이스를 통해 관리되는 인스턴스 제거 작업을 성공적으로 수행한 것과 동일합니다.  
  
## <a name="see-also"></a>참고 항목  
 [유틸리티 탐색기를 사용하여 SQL Server 유틸리티 관리](use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [SQL Server 유틸리티 문제 해결](../../database-engine/troubleshoot-the-sql-server-utility.md)  

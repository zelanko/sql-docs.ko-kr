---
title: 가장 및 연결에 대 한 자격 증명 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- authentication [CLR integration]
- user impersonation [CLR integration]
- credentials [CLR integration]
- database objects [CLR integration], security
ms.assetid: 293dce7d-1db2-4657-992f-8c583d6e9ebb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 50069ad5b96914d98f3d08e795467c2693fabe87
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874019"
---
# <a name="impersonation-and-credentials-for-connections"></a>연결에 대한 가장 및 자격 증명
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR(공용 언어 런타임) 통합에서 Windows 인증 사용은 복잡하지만 SQL Server 인증을 사용하는 것보다 더 안전합니다. Windows 인증을 사용하는 경우 다음 사항을 고려하십시오.  
  
 기본적으로 Windows에 연결하는 SQL Server 프로세스는 SQL Server Windows 서비스 계정의 보안 컨텍스트를 얻습니다. 그러나 CLR 함수를 프록시 ID에 매핑하여 해당 아웃바운드 연결이 Windows 서비스 계정과는 다른 보안 컨텍스트를 사용하도록 할 수 있습니다.  
  
 경우에 따라 서비스 계정으로 실행하는 대신 `SqlContext.WindowsIdentity` 속성을 사용하여 호출자를 가장할 수도 있습니다. `WindowsIdentity` 인스턴스는 호출 코드를 호출한 클라이언트의 ID를 나타내며, 클라이언트에서 Windows 인증을 사용한 경우에만 사용할 수 있습니다. `WindowsIdentity` 인스턴스를 얻은 후 `Impersonate`를 호출하여 스레드의 보안 토큰을 변경한 다음 클라이언트 대신 ADO.NET 연결을 열 수 있습니다.  
  
 SQLContext.WindowsIdentity.Impersonate를 호출한 후에 로컬 데이터에 액세스할 수 없습니다 및 시스템 데이터에 액세스할 수 없습니다. 데이터에 액세스 하려면 다시 WindowsImpersonationContext.Undo 호출 해야 합니다.  
  
 다음 예에서는 `SqlContext.WindowsIdentity` 속성을 사용하여 호출자를 가장하는 방법을 보여 줍니다.  
  
 Visual C#  
  
```  
WindowsIdentity clientId = null;  
WindowsImpersonationContext impersonatedUser = null;  
  
clientId = SqlContext.WindowsIdentity;  
  
// This outer try block is used to protect from   
// exception filter attacks which would prevent  
// the inner finally block from executing and   
// resetting the impersonation.  
try  
{  
   try  
   {  
      impersonatedUser = clientId.Impersonate();  
      if (impersonatedUser != null)  
         return GetFileDetails(directoryPath);  
         else return null;  
   }  
   finally  
   {  
      if (impersonatedUser != null)  
         impersonatedUser.Undo();  
   }  
}  
catch  
{  
   throw;  
}  
```  
  
> [!NOTE]  
>  가장의 동작 변경 내용에 대 한 정보를 참조 하세요 [SQL Server 2014 데이터베이스 엔진 기능의 주요 변경 내용](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)합니다.  
  
 또한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows ID 값을 받은 경우 기본적으로 해당 인스턴스를 다른 컴퓨터에 전파할 수 없습니다. Windows 보안 인프라에서 기본적으로 이 작업이 제한됩니다. 하지만 신뢰할 수 있는 여러 컴퓨터에 Windows ID를 전파할 수 있는 "위임"이라는 메커니즘이 있습니다. 자세한 내용은 TechNet 문서에서는 위임에 대 한 "[Kerberos 프로토콜 전환 및 제한 된 위임](https://go.microsoft.com/fwlink/?LinkId=50419)"입니다.  
  
## <a name="see-also"></a>관련 항목  
 [SqlContext 개체](../../clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  

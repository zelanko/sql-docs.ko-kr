---
title: 연결에 대한 가장 및 자격 증명 | 마이크로 소프트 문서
description: SQL Server CLR 통합에서 SqlContext.WindowsIdentity 속성을 사용하여 Windows 인증에서 호출자를 가장할 수 있습니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 382185c036055bb9ea689f551c256a26ee83b0b4
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81485342"
---
# <a name="impersonation-and-credentials-for-connections"></a>연결에 대한 가장 및 자격 증명
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR(공용 언어 런타임) 통합에서 Windows 인증 사용은 복잡하지만 SQL Server 인증을 사용하는 것보다 더 안전합니다. Windows 인증을 사용하는 경우 다음 사항을 고려하십시오.  
  
 기본적으로 Windows에 연결하는 SQL Server 프로세스는 SQL Server Windows 서비스 계정의 보안 컨텍스트를 얻습니다. 그러나 CLR 함수를 프록시 ID에 매핑하여 해당 아웃바운드 연결이 Windows 서비스 계정과는 다른 보안 컨텍스트를 사용하도록 할 수 있습니다.  
  
 경우에 따라 서비스 계정으로 실행 하는 대신 **SqlContext.WindowsIdentity** 속성을 사용 하 여 호출자 가장을 할 수 있습니다. **WindowsIdentity** 인스턴스는 호출 코드를 호출한 클라이언트의 ID를 나타내며 클라이언트가 Windows 인증을 사용한 경우에만 사용할 수 있습니다. **WindowsIdentity** 인스턴스를 얻은 후 **사칭을** 호출하여 스레드의 보안 토큰을 변경한 다음 클라이언트를 대신하여 ADO.NET 연결을 열 수 있습니다.  
  
 SQLContext.WindowsIdentity.Impersonate를 호출한 후에는 로컬 데이터에 액세스할 수 없으며 시스템 데이터에 액세스할 수 없습니다. 데이터에 다시 액세스하려면 Windows사칭컨텍스트.Undo를 호출해야 합니다.  
  
 다음 예제에서는 **SqlContext.WindowsIdentity** 속성을 사용하여 호출자 가장하는 방법을 보여 주며 있습니다.  
  
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
>  가장의 동작 변경 사항에 대한 자세한 내용은 [SQL Server 2016의 데이터베이스 엔진 기능에 대한 주요 변경 내용을](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)참조하십시오.  
  
 또한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows ID 값을 받은 경우 기본적으로 해당 인스턴스를 다른 컴퓨터에 전파할 수 없습니다. Windows 보안 인프라에서 기본적으로 이 작업이 제한됩니다. 하지만 신뢰할 수 있는 여러 컴퓨터에 Windows ID를 전파할 수 있는 "위임"이라는 메커니즘이 있습니다. TechNet 문서에서 위임에 대해 자세히 알아볼[Kerberos Protocol Transition and Constrained Delegation](https://go.microsoft.com/fwlink/?LinkId=50419)수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SqlContext 개체](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  

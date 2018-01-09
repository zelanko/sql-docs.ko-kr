---
title: "가장 및 연결에 대 한 자격 증명 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b3c4495b75f9464eb0e8211eeea6529264053c61
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="impersonation-and-credentials-for-connections"></a>연결에 대한 가장 및 자격 증명
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Windows 인증을 사용 하 여 공용 언어 런타임 (CLR) 통합은 복잡 하지만 SQL Server 인증을 사용 하 여 보다 더 안전 합니다. Windows 인증을 사용하는 경우 다음 사항을 고려하십시오.  
  
 기본적으로 Windows에 연결하는 SQL Server 프로세스는 SQL Server Windows 서비스 계정의 보안 컨텍스트를 얻습니다. 그러나 CLR 함수를 프록시 ID에 매핑하여 해당 아웃바운드 연결이 Windows 서비스 계정과는 다른 보안 컨텍스트를 사용하도록 할 수 있습니다.  
  
 사용 하 여 호출자를 가장 하려는 경우에 따라는 **SqlContext.WindowsIdentity** 서비스 계정으로 실행 하는 대신 속성입니다. **WindowsIdentity** 인스턴스 호출 코드를 호출 하는 클라이언트는 Windows 인증을 사용 하는 경우에 클라이언트의 id를 나타냅니다. 가져온 후의 **WindowsIdentity** 인스턴스를 호출할 수 있습니다 **Impersonate** 를 스레드의 보안 토큰을 변경한 다음 클라이언트 대신 ADO.NET 연결을 엽니다.  
  
 SQLContext.WindowsIdentity.Impersonate를 호출한 후에 로컬 데이터에 액세스할 수 없습니다 및 시스템 데이터에 액세스할 수 없습니다. 데이터에 액세스 하려면 다시 WindowsImpersonationContext.Undo 호출 해야 합니다.  
  
 사용 하 여 호출자를 가장 하는 방법을 보여 주는 다음 예제는 **SqlContext.WindowsIdentity** 속성입니다.  
  
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
>  가장의 동작 변경에 대 한 정보를 참조 하십시오. [SQL Server 2016 데이터베이스 엔진 기능의 주요 변경 내용](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)합니다.  
  
 또한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows ID 값을 받은 경우 기본적으로 해당 인스턴스를 다른 컴퓨터에 전파할 수 없습니다. Windows 보안 인프라에서 기본적으로 이 작업이 제한됩니다. 하지만 신뢰할 수 있는 여러 컴퓨터에 Windows ID를 전파할 수 있는 "위임"이라는 메커니즘이 있습니다. TechNet 문서에 위임에 대 한 자세히 알아볼 수 있습니다 "[Kerberos 프로토콜 전환 및 제한 위임](http://go.microsoft.com/fwlink/?LinkId=50419)"입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SqlContext 개체](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  

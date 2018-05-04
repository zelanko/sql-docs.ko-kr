---
title: 파일 및 버전 번호 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, versions
- components [SMO]
- files [SMO], components
- SMO [SQL Server], versions
- versions [SMO]
ms.assetid: 510907b6-e7a9-41bd-b892-d6d99a5118e1
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b4833d716821b64a890815e2fa650caf6c665d46
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="files-and-version-numbers"></a>파일 및 버전 번호
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  모든 필수 SQL Server 관리 개체 (SMO) 구성 요소가 Microsoft.SqlServer.SqlManagementObjects NuGet 패키지에 포함 합니다. SMO는 몇 개의 관리되는 어셈블리에 구현됩니다. 클라이언트나 서버에서 SMO 응용 프로그램을 개발할 수 있습니다.  

>>[!Important]
SMO 어셈블리의 파일 버전이 주으로 표시 됩니다. **0**합니다. Build.Revision 합니다. 하지만 포함 된 어셈블리 버전은 주 버전. **100**합니다. Build.Revision 합니다. 이 작업은 하나에 대 한 업데이트에 영향을 주지는 기타 모든 하므로 별도 각 응용 프로그램에서 사용 되는 SMO의 버전을 유지 하려면 수행 됩니다.
>>
>>이 때문에 수행 해야 **하지** 이러한 버전의 어셈블리를 전역 어셈블리 캐시 (GAC)에 설치 합니다. 이렇게 다른 응용 프로그램을 같은 발생할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio를 중단 하도록 합니다. 
  
|파일|Description|  
|-----------|-----------------|  
|Microsoft.SqlServer.ConnectionInfo.dll|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결 지원을 포함합니다.|  
|Microsoft.SqlServer.ServiceBrokerEnum.dll|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker 프로그래밍 지원을 포함합니다. 이 파일은 Service Broker에 액세스하는 프로그램에만 필요합니다.|  
|Microsoft.SqlServer.Smo.dll|SMO 클래스를 대부분 포함합니다.|  
|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|SMO 클래스 지원을 포함합니다.|  
|Microsoft.SqlServer.WmiEnum.dll|WMI(Windows Management Instrumentation) 공급자 클래스를 포함합니다. 이 파일은 WMI 공급자 클래스를 사용하는 프로그램에만 필요합니다.|  
|Microsoft.SqlServer.RegSvrEnum.dll|등록된 서버 클래스를 포함합니다. 이 파일은 등록된 서버 클래스를 사용하는 프로그램에만 필요합니다.|  
  
  

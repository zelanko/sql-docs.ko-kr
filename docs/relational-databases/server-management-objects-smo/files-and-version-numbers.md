---
title: 파일 및 버전 번호 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, versions
- components [SMO]
- files [SMO], components
- SMO [SQL Server], versions
- versions [SMO]
ms.assetid: 510907b6-e7a9-41bd-b892-d6d99a5118e1
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7936eaf327f9df3cb0f3d8545d7bf557ef1471ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098044"
---
# <a name="files-and-version-numbers"></a>파일 및 버전 번호
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  모든 SQL Server 관리 개체 (SMO) 구성 요소가 Microsoft.SqlServer.SqlManagementObjects NuGet 패키지에 포함 해야 합니다. SMO는 몇 개의 관리되는 어셈블리에 구현됩니다. 클라이언트나 서버에서 SMO 애플리케이션을 개발할 수 있습니다.  

> > [!Important]
> > SMO 어셈블리의 파일 버전은 중요로 표시 됩니다. **0**합니다. Build.Revision 합니다. 하지만 포함 된 어셈블리 버전은 주 버전. **100**합니다. Build.Revision 합니다. 이렇게 하나에 대 한 업데이트에 영향을 주지 다른 되므로 각 응용 프로그램에 사용 되는 SMO의 버전을 별도로 유지 하 합니다.
> > 
> > 이 때문에 수행 해야 합니다 **되지** 이러한 버전의 어셈블리를 전역 어셈블리 캐시 (GAC)에 설치 합니다. 이렇게 인해 다른 응용 프로그램과 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio에서 중단 합니다. 
  
|파일|설명|  
|-----------|-----------------|  
|Microsoft.SqlServer.ConnectionInfo.dll|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결 지원을 포함합니다.|  
|Microsoft.SqlServer.ServiceBrokerEnum.dll|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker 프로그래밍 지원을 포함합니다. 이 파일은 Service Broker에 액세스하는 프로그램에만 필요합니다.|  
|Microsoft.SqlServer.Smo.dll|SMO 클래스를 대부분 포함합니다.|  
|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|SMO 클래스 지원을 포함합니다.|  
|Microsoft.SqlServer.WmiEnum.dll|WMI(Windows Management Instrumentation) 공급자 클래스를 포함합니다. 이 파일은 WMI 공급자 클래스를 사용하는 프로그램에만 필요합니다.|  
|Microsoft.SqlServer.RegSvrEnum.dll|등록된 서버 클래스를 포함합니다. 이 파일은 등록된 서버 클래스를 사용하는 프로그램에만 필요합니다.|  
  
  

---
title: 파일 및 버전 번호 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: f1a7286f15af28f97e488b8b40fd745a0d320108
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84997142"
---
# <a name="files-and-version-numbers"></a>파일 및 버전 번호
  필요한 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMO (Management Objects) 구성 요소는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 또는 서버 인스턴스의 일부로 설치 됩니다. SMO는 몇 개의 관리되는 어셈블리에 구현됩니다. 클라이언트나 서버에서 SMO 애플리케이션을 개발할 수 있습니다.  
  
|디렉터리|파일|Description|  
|---------------|----------|-----------------|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.ConnectionInfo.dll|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결 지원을 포함합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.ServiceBrokerEnum.dll|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker 프로그래밍 지원을 포함합니다. 이 파일은 Service Broker에 액세스하는 프로그램에만 필요합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.Smo.dll|SMO 클래스를 대부분 포함합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|SMO 클래스 지원을 포함합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.WmiEnum.dll|WMI(Windows Management Instrumentation) 공급자 클래스를 포함합니다. 이 파일은 WMI 공급자 클래스를 사용하는 프로그램에만 필요합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.RegSvrEnum.dll|등록된 서버 클래스를 포함합니다. 이 파일은 등록된 서버 클래스를 사용하는 프로그램에만 필요합니다.|  
  
  

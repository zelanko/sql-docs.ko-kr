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
manager: craigg
ms.openlocfilehash: 0a1b0b28afbb83028af8d71644af08ca660a0b36
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62753415"
---
# <a name="files-and-version-numbers"></a>파일 및 버전 번호
  필요한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모든 SMO (Management Objects) 구성 요소는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 또는 서버 인스턴스의 일부로 설치 됩니다. SMO는 몇 개의 관리되는 어셈블리에 구현됩니다. 클라이언트나 서버에서 SMO 애플리케이션을 개발할 수 있습니다.  
  
|디렉터리|파일|Description|  
|---------------|----------|-----------------|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.ConnectionInfo.dll|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결 지원을 포함합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.ServiceBrokerEnum.dll|
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker 프로그래밍 지원을 포함합니다. 이 파일은 Service Broker에 액세스하는 프로그램에만 필요합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.Smo.dll|SMO 클래스를 대부분 포함합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|SMO 클래스 지원을 포함합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.WmiEnum.dll|WMI(Windows Management Instrumentation) 공급자 클래스를 포함합니다. 이 파일은 WMI 공급자 클래스를 사용하는 프로그램에만 필요합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.RegSvrEnum.dll|등록된 서버 클래스를 포함합니다. 이 파일은 등록된 서버 클래스를 사용하는 프로그램에만 필요합니다.|  
  
  

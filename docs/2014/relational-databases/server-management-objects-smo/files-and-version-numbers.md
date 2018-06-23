---
title: 파일 및 버전 번호 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, versions
- components [SMO]
- files [SMO], components
- SMO [SQL Server], versions
- versions [SMO]
ms.assetid: 510907b6-e7a9-41bd-b892-d6d99a5118e1
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 63602af6a7d798086c3e41d3796b20a2f71d6950
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186721"
---
# <a name="files-and-version-numbers"></a>파일 및 버전 번호
  필요한 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의의 일환으로 Management Objects (SMO) 구성 요소가 설치 되어 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 또는 서버입니다. SMO는 몇 개의 관리되는 어셈블리에 구현됩니다. 클라이언트나 서버에서 SMO 응용 프로그램을 개발할 수 있습니다.  
  
|디렉터리|파일|Description|  
|---------------|----------|-----------------|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.ConnectionInfo.dll|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결 지원을 포함합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.ServiceBrokerEnum.dll|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker 프로그래밍 지원을 포함합니다. 이 파일은 Service Broker에 액세스하는 프로그램에만 필요합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.Smo.dll|SMO 클래스를 대부분 포함합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|SMO 클래스 지원을 포함합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.WmiEnum.dll|WMI(Windows Management Instrumentation) 공급자 클래스를 포함합니다. 이 파일은 WMI 공급자 클래스를 사용하는 프로그램에만 필요합니다.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.RegSvrEnum.dll|등록된 서버 클래스를 포함합니다. 이 파일은 등록된 서버 클래스를 사용하는 프로그램에만 필요합니다.|  
  
  
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6d682ca3d6768da16d43c3c09471a6c722561dd3
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008627"
---
# <a name="files-and-version-numbers"></a>파일 및 버전 번호
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  필요한 모든 SMO (SQL Server Management Object) 구성 요소가 Microsoft Sql Server Server NuGet 패키지에 포함 되어 있습니다. SMO는 몇 개의 관리되는 어셈블리에 구현됩니다. 클라이언트나 서버에서 SMO 애플리케이션을 개발할 수 있습니다.  

> > [!Important]
> > SMO 어셈블리의 파일 버전은 Major로 표시 됩니다. **0**. 빌드. 수정 버전. 그러나 포함 된 어셈블리 버전은 중요 합니다. **100**. 빌드. 수정 버전. 이 작업은 각 응용 프로그램에서 사용 되는 SMO의 버전을 분리 하 여 다른 항목에 대 한 업데이트가 다른 모든 항목에 영향을 주지 않도록 합니다.
> > 
> > 따라서 이러한 버전의 어셈블리를 GAC (전역 어셈블리 캐시) **에 설치 하면 안 됩니다** . 이렇게 하면 Management Studio 같은 다른 응용 프로그램이 중단 될 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 
  
|파일|Description|  
|-----------|-----------------|  
|Microsoft.SqlServer.ConnectionInfo.dll|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결 지원을 포함합니다.|  
|Microsoft.SqlServer.ServiceBrokerEnum.dll|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker 프로그래밍 지원을 포함합니다. 이 파일은 Service Broker에 액세스하는 프로그램에만 필요합니다.|  
|Microsoft.SqlServer.Smo.dll|SMO 클래스를 대부분 포함합니다.|  
|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|SMO 클래스 지원을 포함합니다.|  
|Microsoft.SqlServer.WmiEnum.dll|WMI(Windows Management Instrumentation) 공급자 클래스를 포함합니다. 이 파일은 WMI 공급자 클래스를 사용하는 프로그램에만 필요합니다.|  
|Microsoft.SqlServer.RegSvrEnum.dll|등록된 서버 클래스를 포함합니다. 이 파일은 등록된 서버 클래스를 사용하는 프로그램에만 필요합니다.|  
  
  

---
title: 데이터 처리 확장 프로그램 개요 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], about extensions
ms.assetid: 1d652605-9313-4c75-98b4-ba4dcbbb222d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 283d810adec697ce2a78f60358a2c00e33be5cb3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48092912"
---
# <a name="data-processing-extensions-overview"></a>데이터 처리 확장 프로그램 개요
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 데이터 처리 확장 프로그램을 통해 데이터 원본에 연결하고 데이터를 검색할 수 있습니다. 이 프로그램은 데이터 원본과 데이터 집합을 연결하는 역할도 합니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 데이터 공급자 인터페이스의 하위 집합을 본떠서 만든 것입니다.  
  
 다음 표에서는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에 포함된 데이터 처리 확장 프로그램을 나열합니다.  
  
|데이터 처리 확장 프로그램|Description|  
|-------------------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 데이터 처리 확장 프로그램|.NET Framework Data Provider for SQL Server를 사용하여 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]에 연결하고 데이터를 검색합니다.|  
|OLE DB용 데이터 처리 확장 프로그램|.NET Framework Data Provider for OLE DB를 사용합니다. 이 확장 프로그램을 사용하여 보고서 서버에서 OLE DB 공급자를 가진 데이터 원본을 쿼리할 수 있습니다.|  
|Oracle용 데이터 처리 확장 프로그램|.NET Framework Data Provider for Oracle을 사용합니다. 이 확장 프로그램을 사용하여 보고서 서버에서 Oracle 클라이언트 연결 소프트웨어를 통해 Oracle 데이터 원본에 액세스할 수 있습니다.|  
|ODBC용 데이터 처리 확장 프로그램|.NET Framework Data Provider for ODBC를 사용합니다. 이 확장 프로그램을 사용하여 보고서 서버에서 ODBC 드라이버가 있는 임의의 데이터베이스의 데이터에 액세스할 수 있습니다.|  
  
 [!INCLUDE[ssRS](../../../includes/ssrs.md)] 데이터 처리 API를 사용하여 사용자 지정 데이터 처리를 보고서 서버에 추가할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]의 데이터 공급자를 기본적으로 지원합니다. 이미 완전한 데이터 공급자를 구현한 경우에는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램을 구현할 필요가 없습니다. 하지만 보안 연결 자격 증명이나 서버 쪽 집계와 같은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 2005 특정 기능을 포함시키려면 데이터 공급자 확장을 고려해야 합니다.  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에 포함된 각 데이터 처리 확장 프로그램에서는 공통된 인터페이스 집합을 사용합니다. 이로 인해 모든 확장 프로그램에서 비슷한 기능이 구현됩니다.  
  
 고유의 데이터 원본에 맞는 데이터 처리 확장 프로그램을 개발하거나, 인터페이스를 사용하여 공통 데이터베이스 인프라에 데이터 처리 층을 하나 더 추가할 수 있습니다. 사용자 지정 데이터 처리 확장 프로그램을 배포하여 조직의 기존 보고서 서버에 완벽한 데이터 통합을 구현할 수 있습니다. 뿐만 아니라 소비자에게 제공하는 사용자 지정 보고 제품군의 일부로 사용할 수도 있습니다.  
  
 ![데이터 처리 확장 프로그램 아키텍처](../../media/bk-dataprocess-extensions.gif "데이터 처리 확장 프로그램 아키텍처")  
Reporting Services 데이터 처리 확장 프로그램 아키텍처  
  
 사용자 지정 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램을 구현하면 다음과 같은 이점이 있습니다.  
  
-   데이터 액세스 아키텍처가 단순해지므로 유지 관리가 더 편리하고 성능이 향상됩니다.  
  
-   확장 프로그램 특정 기능을 소비자에게 직접 제공할 수 있습니다.  
  
-   소비자에게 제공되는 특정 인터페이스를 통해 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 내에서 데이터 원본에 액세스할 수 있습니다.  
  
## <a name="data-extension-process-flow"></a>데이터 확장 프로세스 흐름  
 사용자 지정 데이터 확장 프로그램을 개발하기 전에 보고서 서버에서 데이터 확장 프로그램을 사용하여 어떻게 데이터를 처리하는지 이해해야 합니다. 또한 보고서 서버에서 호출되는 생성자와 메서드에 대해서도 잘 알고 있어야 합니다.  
  
 ![데이터 처리 확장 프로그램의 프로세스 흐름](../../media/bk-ext-01.gif "데이터 처리 확장 프로그램의 프로세스 흐름")  
보고서 서버에서 호출되는 데이터 확장 프로그램의 단계별 프로세스 흐름  
  
 이 그림은 다음과 같은 이벤트 시퀀스를 나타냅니다.  
  
1.  보고서 서버에서 연결 개체를 만들고 보고서와 연관된 연결 문자열 및 자격 증명을 전달합니다.  
  
2.  보고서의 명령 텍스트를 사용하여 명령 개체가 생성됩니다. 이 프로세스에서 데이터 처리 확장 프로그램에는 명령 텍스트의 구문을 분석하고 명령에 대한 매개 변수를 만드는 코드가 포함될 수 있습니다.  
  
3.  명령 개체와 매개 변수가 처리되면 데이터 판독기가 생성되어 결과 집합이 반환되고 보고서 서버에서 보고서 데이터를 보고서 레이아웃과 연결할 수 있습니다.  
  
## <a name="developer-requirements"></a>개발자 요구 사항  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램을 개발하려면 다음이 필요합니다.  
  
-   보고서 디자이너 또는 보고서 서버가 설치된 배포 컴퓨터가 있어야 합니다.  
  
-   [!INCLUDE[vsprvsext](../../../includes/vsprvsext-md.md)] 이상 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK(소프트웨어 개발 키트)가 설치된 개발 컴퓨터가 있어야 합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 기능을 자세히 알고 있어야 합니다.  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 아키텍처, [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 데이터 공급자, ADO.NET 데이터 집합 개체 및 공통 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 인터페이스에 대해 자세히 알고 있어야 합니다.  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET과 같은 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 언어에 대한 개발 경험이 있어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 확장 프로그램](../reporting-services-extensions.md)   
 [Reporting Services 확장 라이브러리](../reporting-services-extension-library.md)  
  
  

---
title: Analysis Services 연결에 사용 되는 데이터 공급자 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7703bda267a7b646bf6ccbbfee98c7401599f3a0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="client-libraries-data-providers-used-for-analysis-services-connections"></a>Analysis Services 연결에 사용 되는 클라이언트 라이브러리 (데이터 공급자)
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services에서는 세 가지 클라이언트 라이브러리 라고도 **데이터 공급자**, 서버 및 도구 및 클라이언트 응용 프로그램에서 데이터 액세스에 대 한 합니다. 도구에는 SSMS와 SSDT 및 Power BI Desktop 및 Excel 이러한 라이브러리를 사용 하 여 Analysis Services에 연결 하는 같은 응용 프로그램 같은입니다. 그중에서 ADOMD.NET 및 AMO Analysis Services Management Objects (), 클라이언트 라이브러리는 관리 되는 클라이언트 라이브러리입니다. Analysis Services OLE DB 공급자 (MSOLAP DLL)는 네이티브 클라이언트 라이브러리입니다. 클라이언트 라이브러리는 SQL Server Analysis Services와 Azure Analysis Services에 대해 동일합니다.
  
##  <a name="bkmk_downloadsite"></a> 최신 버전을 가져올 위치  
 클라이언트 컴퓨터에 설치 된 버전의 데이터를 제공 하는 서버의 주 버전을 일치 해야 합니다. 서버 설치가 네트워크에서 워크스테이션에 설치된 데이터 공급자보다 최신인 경우 최신 라이브러리를 설치해야 할 수 있습니다.  

해당 SQL 버전;에 해당 하는 이전 SQL Server 기능 팩에 포함 하는 클라이언트 라이브러리 그러나 최신 하지 못할 수 있습니다. Azure Analysis Services에 연결 하면 이후 버전 필요할 수 있습니다. 모든 버전은 이전 버전과 호환 됩니다.

최신 정보를 얻을, 참조 [Azure Analysis Services에 연결 하기 위한 클라이언트 라이브러리](https://docs.microsoft.com/azure/analysis-services/analysis-services-data-providers)합니다. 
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services에 연결](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  

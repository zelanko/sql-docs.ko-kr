---
title: "연결을 설정 하는 동안 오류가 발생 했습니다. | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 1b951da1-f62d-43d2-b40b-270a4a9ab92c
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 226842eb86c8eb7d5981407c805e18495dfb2579
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection"></a>연결을 설정 하는 동안 오류가 발생 했습니다.
  이 오류는 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 이 설치되어 있지 않은 서버에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터를 쿼리하면 발생합니다. 또한 SQL Server Analysis Services([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 서비스가 중지되었거나 이전 버전에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터를 보려는 경우에도 발생합니다.  
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|적용 대상|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|제품 버전|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|원인|데이터 연결이 실패했습니다.|  
|메시지 텍스트|외부 데이터 원본에 대한 연결을 설정하는 동안 오류가 발생했습니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 연결을 새로 고치지 못했습니다.|  
  
## <a name="explanation"></a>설명  
 SharePoint에 게시된 Excel 통합 문서에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터를 쿼리할 때 SharePoint 환경에 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버가 없거나 SQL Server Analysis Services([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 서비스가 중지된 경우 Excel Services가 이 오류를 반환합니다.  
  
 쿼리 엔진을 사용할 수 없을 때 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터를 필터링하거나 조각을 생성하면 이 오류가 발생합니다.  
  
## <a name="user-action"></a>사용자 동작  
 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을 설치하거나 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 이 설치된 SharePoint 환경으로 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서를 이동합니다. 자세한 내용은 [SharePoint 2010용 Power Pivot 설치](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)를 참조하세요.  
  
 소프트웨어가 설치되어 있는 경우 SQL Server Analysis Services([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 인스턴스가 실행되고 있는지 확인합니다. 중앙 관리에서 **서버의 서비스 관리** 를 확인합니다. 또한 관리 도구에서 서비스 콘솔 응용 프로그램을 확인합니다.  
  
 SQL Server 2008 R2 버전의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel에서 만든 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서의 경우 SQL Server 2008 R2 버전의 Analysis Services OLE DB 공급자를 설치해야 합니다. 이 오류는 공급자를 설치했지만 Microsoft.AnalysisServices.ChannelTransport.dll 파일을 등록하지 않은 경우 발생합니다. 파일 등록에 대한 자세한 내용은 [SharePoint 서버에서 Analysis Services OLE DB 공급자 설치](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [Windows 인증을 사용 하는 데이터 연결 및 사용자 자격 증명을 위임할 수 없습니다. 다음과 같은 연결을 새로 고치지 못했습니다: 파워 피벗 데이터](../../analysis-services/power-pivot-sharepoint/the-data-connection-user-could-not-be-delegated.md)  
  
  

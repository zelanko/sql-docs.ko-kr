---
title: "데이터 처리 확장 프로그램 배포 | Microsoft Docs"
ms.custom: 
ms.date: 03/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: e5c0b5a9-1386-47cb-aade-96653ecfaa54
caps.latest.revision: 34
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d312cdf2c5588c8dc12ff000fe4163d7f562ea7f
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="deploying-a-data-processing-extension"></a>데이터 처리 확장 프로그램 배포
  작성 하 고 컴파일된 프로그램 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램에는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 라이브러리, 보고서 디자이너 및 보고서 서버에서 검색할 수 있도록 해야 합니다. 이 작업은 확장 프로그램을 적절한 디렉터리에 복사하고 해당하는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 파일에 항목을 추가하여 간단히 수행할 수 있습니다.  
  
## <a name="configuration-file-extension-element"></a>구성 파일 확장 프로그램 요소  
 보고서 서버 또는 보고서 디자이너에 배포 하는 데이터 처리 확장 프로그램으로 입력 해야 **확장** 구성 파일에 있는 요소입니다. 이러한 파일은 보고서 서버의 경우 RSReportServer.config이고, 보고서 디자이너의 경우 RSReportDesigner.config입니다.  
  
 다음 표에서 설명에 대 한 특성은 **확장** 데이터 처리 확장 프로그램에 대 한 요소입니다.  
  
|Attribute|Description|  
|---------------|-----------------|  
|**이름**|확장 프로그램에 대한 고유한 이름입니다(예: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 처리 확장 프로그램의 경우 "SQL" 또는 OLE DB 데이터 처리 확장 프로그램의 경우 "OLEDB"). **Name** 특성의 최대 길이는 255자입니다. 이름은 구성 파일의 **Extension** 요소에 있는 모든 항목 중에서 고유해야 합니다.|  
|**형식**|정규화된 네임스페이스와 어셈블리 이름을 포함하는 쉼표로 구분된 목록입니다.|  
|**Visible**|값이 **false** 는 데이터 처리 확장 프로그램은 표시 되지 않음을 사용자 인터페이스에 나타냅니다. 이 특성이 포함되지 않을 경우 기본값은 **true**입니다.|  
  
 RSReportServer.config 또는 RSReportDesigner.config 파일에 대 한 자세한 내용은 참조 [Reporting Services Configuration Files](../../../reporting-services/report-server/reporting-services-configuration-files.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[방법: 보고서 서버에 데이터 처리 확장 프로그램 배포](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-a-report-server.md)|데이터 처리 확장 프로그램을 보고서 서버에 배포하는 방법을 설명합니다.|  
|[방법: 보고서 디자이너에 데이터 처리 확장 프로그램 배포](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md)|데이터 처리 확장 프로그램을 보고서 디자이너에 배포하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [데이터 처리 확장 프로그램 구현](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 확장 프로그램 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

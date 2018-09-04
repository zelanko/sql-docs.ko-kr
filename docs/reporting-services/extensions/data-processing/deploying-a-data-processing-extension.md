---
title: 데이터 처리 확장 프로그램 배포 | Microsoft Docs
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.suite: pro-bi
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: e5c0b5a9-1386-47cb-aade-96653ecfaa54
author: markingmyname
ms.author: maghan
ms.openlocfilehash: df6542f3e5035e4aae3d603c8068e37abc78f6d1
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43272572"
---
# <a name="deploying-a-data-processing-extension"></a>데이터 처리 확장 프로그램 배포
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램을 작성하고 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 라이브러리에 컴파일한 후에는 보고서 서버 및 보고서 디자이너에서 이를 찾을 수 있도록 해야 합니다. 이 작업은 확장 프로그램을 적절한 디렉터리에 복사하고 해당하는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 파일에 항목을 추가하여 간단히 수행할 수 있습니다.  
  
## <a name="configuration-file-extension-element"></a>구성 파일 확장 프로그램 요소  
 보고서 서버나 보고서 디자이너에 배포하는 데이터 처리 확장 프로그램은 구성 파일에 **Extension** 요소로 입력해야 합니다. 이러한 파일은 보고서 서버의 경우 RSReportServer.config이고, 보고서 디자이너의 경우 RSReportDesigner.config입니다.  
  
 다음 표는 데이터 처리 확장 프로그램에 대한 **Extension** 요소의 특성을 설명합니다.  
  
|attribute|설명|  
|---------------|-----------------|  
|**이름**|확장 프로그램에 대한 고유한 이름입니다(예: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 처리 확장 프로그램의 경우 "SQL" 또는 OLE DB 데이터 처리 확장 프로그램의 경우 "OLEDB"). **Name** 특성의 최대 길이는 255자입니다. 이름은 구성 파일의 **Extension** 요소에 있는 모든 항목 중에서 고유해야 합니다.|  
|**형식**|정규화된 네임스페이스와 어셈블리 이름을 포함하는 쉼표로 구분된 목록입니다.|  
|**Visible**|**false** 값은 데이터 처리 확장 프로그램이 사용자 인터페이스에 표시되지 않음을 나타냅니다. 이 특성이 포함되지 않을 경우 기본값은 **true**입니다.|  
  
 RSReportServer.config 또는 RSReportDesigner.config 파일에 대한 자세한 내용은 [Reporting Services 구성 파일](../../../reporting-services/report-server/reporting-services-configuration-files.md)을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|-----------|-----------------|  
|[방법: 보고서 서버에 데이터 처리 확장 프로그램 배포](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-a-report-server.md)|데이터 처리 확장 프로그램을 보고서 서버에 배포하는 방법을 설명합니다.|  
|[방법: 보고서 디자이너에 데이터 처리 확장 프로그램 배포](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md)|데이터 처리 확장 프로그램을 보고서 디자이너에 배포하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [데이터 처리 확장 프로그램 구현](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 확장 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

---
title: "데이터 처리 확장 프로그램 코드 디버깅 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- debugging data processing extensions [Reporting Services]
- troubleshooting [Reporting Services], data processing extensions
- data processing extensions [Reporting Services], debugging
ms.assetid: e963e205-9ae0-446d-97df-028a1d2727d9
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 0b7ee42be2f3d54fc8fb19ab48b3b603e29669e2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/12/2017

---
# <a name="debugging-data-processing-extension-code"></a>데이터 처리 확장 프로그램 코드 디버깅
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 수 있는 몇 가지 디버깅 도구는 데이터 처리 확장 프로그램 코드를 분석 하 고 오류를 찾는 제공 합니다. 작업하기 가장 좋은 도구는 수행하려는 작업에 따라 달라집니다. 이 예에서는 [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]를 사용합니다.  
  
#### <a name="to-debug-your-data-processing-extension-code"></a>데이터 처리 확장 프로그램 코드를 디버깅하려면  
  
1.  [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]를 시작하고 데이터 처리 확장 프로그램 프로젝트를 엽니다.  
  
2.  프로젝트를 빌드하고 데이터 처리 확장 프로그램 어셈블리 및 해당하는 .pdb 파일을 보고서 디자이너에 배포합니다. 배포에 대 한 자세한 내용은 참조 [하는 방법: 보고서 디자이너에 데이터 처리 확장 프로그램 배포](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md)합니다.  
  
3.  데이터 처리 확장 프로그램 코드를 별도의 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 창에 열어 둔 상태로 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]에서 새 보고서 프로젝트를 엽니다.  
  
4.  데이터 처리 확장 프로그램 프로젝트를 포함하는 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 창으로 이동하고 코드에서 중단점을 설정합니다.  
  
5.  데이터 처리 확장 프로그램 프로젝트 창을 활성화 한 상태로, 클릭 **프로세스에 연결** 에 **디버그** 메뉴.  
  
     **프로세스에 연결** 대화 상자가 열립니다.  
  
6.  프로세스 목록에서 보고서 프로젝트에 해당 하는 devenv.exe 프로세스를 선택 하 고 클릭 **연결**합니다.  
  
7.  보고서 데이터 원본을 사용 하 여 정의 된 **보고서 데이터** 보고서 프로젝트의 탭 합니다. 대개 일반 쿼리 디자이너를 사용하여 사용자 지정 데이터 원본에 대해 쿼리를 실행합니다. 그러면 디버거가 호출되고 중단점에 해당하는 코드가 실행됩니다.  
  
8.  F11 키를 사용하여 코드를 단계별로 실행합니다. [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]를 사용하여 디버깅하는 방법은 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 설명서를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 처리 확장 프로그램 배포](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [데이터 처리 확장 프로그램 구현](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 확장 프로그램 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

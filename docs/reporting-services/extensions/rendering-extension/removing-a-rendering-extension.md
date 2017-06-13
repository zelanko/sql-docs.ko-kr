---
title: "렌더링 확장 프로그램 제거 | Microsoft Docs"
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
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
caps.latest.revision: 38
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 58e9d46c17b300cda365e8b42d6442e00ffab0b9
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="removing-a-rendering-extension"></a>렌더링 확장 프로그램 제거
  제거 하는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 렌더링 확장 프로그램을 제거 하면는 **확장** 요소에 있는 rsreportserver.config 파일에서 렌더링 확장 프로그램에 대 한 **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\< 인스턴스 이름 > services\reportserver** 폴더입니다. 보고서 서버 뿐만 아니라 보고서 디자이너에 대 한 항목을 만든 경우 제거는 **확장** 에서 요소는 [RSReportDesigner 구성 파일](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md) 도 합니다. 구성 정보를 제거한 후에는 구성 요소에서 렌더링 확장 프로그램을 사용할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services 구성 파일](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [렌더링 확장 프로그램 구현](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [렌더링 확장 프로그램 개요](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [IRenderingExtension 인터페이스 구현](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [확장에 대 한 보안 고려 사항](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [렌더링 확장 프로그램 배포](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  

---
title: "사용자 지정 보고서 항목 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- extending Reporting Services
- Reporting Services, extending
- custom report items
ms.assetid: 64dcaf2c-1af5-4937-8ff7-98f1ec3b367e
caps.latest.revision: "22"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d50b011363826860678b6b7c503d2ecea01a89cb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="custom-report-items"></a>사용자 지정 보고서 항목
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 엔터프라이즈 보고서 작성 및 게시, 보안 및 구독 관리, 포괄적 API를 통한 보고 기능 확장 등을 위한 풍부한 도구 집합을 제공합니다. 보고서는 RDL(Report Definition Language)이라는 XML 기반 언어를 사용하여 정의됩니다. RDL은 보고서의 레이아웃, 쿼리 정보 및 항목 형식을 설명하는 지침을 제공합니다. 사용자 지정 보고서 항목을 작성하여 RDL을 확장할 수 있습니다. 사용자 지정 보고서 항목은 런타임에 보고서 처리기에서 호출하는 런타임 구성 요소와 사용자 지정 보고서 항목을 보고서 디자이너에서 사용할 수 있도록 하는 디자인 타임 구성 요소로 구성됩니다.  
  
 완전히 구현된 사용자 지정 보고서 항목 예는 [SQL Server Reporting Services 제품 예제](http://go.microsoft.com/fwlink/?LinkId=177889)를 참조하세요.  
  
## <a name="custom-report-item-scenarios"></a>사용자 지정 보고서 항목 시나리오  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 응용 프로그램에 통합해야 하는 개발자는 기본적으로 RDL에서 지원되지 않는 기능이 필요할 수 있습니다. 이러한 기능에는 맵 컨트롤, 가로 목록, 열 목록, 피벗 재설정 가능 행렬 등이 포함됩니다. 응용 프로그램으로 런타임 사용자 지정 보고서 항목 구성 요소를 개발하고 배포하여 필요한 기능을 제공할 수 있습니다.  
  
 기본적으로 지원되지 않는 기능을 제공하는 것 외에도 일부 개발자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 이미 포함되어 있는 컨트롤의 다른 버전으로 기존 기능을 확장해야 할 수도 있습니다. 이 시나리오에서는 개발자가 런타임 구성 요소, 디자인 타임 구성 요소 및 디자인 타임 보고서 항목 변환 구성 요소의 세 가지 구성 요소를 제공할 수 있습니다. 이 중 디자인 타임 보고서 항목 변환 구성 요소는 요청 시 기존 보고서 항목을 사용자 지정 보고서 항목으로 변환합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [사용자 지정 보고서 항목 아키텍처](../../reporting-services/custom-report-items/custom-report-item-architecture.md)  
 사용자 지정 보고서 항목을 구성하는 구성 요소를 설명합니다.  
  
 [사용자 지정 보고서 항목 구현 요구 사항](../../reporting-services/custom-report-items/custom-report-item-implementation-requirements.md)  
 사용자 지정 보고서 항목을 만들기 위한 선행 조건을 설명합니다.  
  
 [사용자 지정 보고서 항목 런타임 구성 요소 만들기](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)  
 사용자 지정 보고서 항목 런타임 구성 요소를 만드는 방법을 설명합니다.  
  
 [사용자 지정 보고서 항목 디자인 타임 구성 요소 만들기](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)  
 사용자 지정 보고서 항목 디자인 타임 구성 요소를 만드는 방법을 설명합니다.  
  
 [방법: 사용자 지정 보고서 항목 배포](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
 사용자 지정 보고서 항목을 배포하는 방법을 설명합니다.  
  
 [사용자 지정 보고서 항목 클래스 라이브러리](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
 **Microsoft.ReportDesigner** 네임스페이스의 사용자 지정 보고서 항목 인프라 클래스 및 관리되는 래퍼 클래스를 설명합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [기술 참조&#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  

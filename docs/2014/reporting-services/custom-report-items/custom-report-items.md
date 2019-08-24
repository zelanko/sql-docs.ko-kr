---
title: 사용자 지정 보고서 항목 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- extending Reporting Services
- Reporting Services, extending
- custom report items
ms.assetid: 64dcaf2c-1af5-4937-8ff7-98f1ec3b367e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 39860a2b147a2db392219552ebfd18cbbf7b7992
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63264779"
---
# <a name="custom-report-items"></a>사용자 지정 보고서 항목
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 엔터프라이즈 보고서 작성 및 게시, 보안 및 구독 관리, 포괄적 API를 통한 보고 기능 확장 등을 위한 풍부한 도구 집합을 제공합니다. 보고서는 RDL(Report Definition Language)이라는 XML 기반 언어를 사용하여 정의됩니다. RDL은 보고서의 레이아웃, 쿼리 정보 및 항목 형식을 설명하는 지침을 제공합니다. 사용자 지정 보고서 항목을 작성하여 RDL을 확장할 수 있습니다. 사용자 지정 보고서 항목은 런타임에 보고서 처리기에서 호출하는 런타임 구성 요소와 사용자 지정 보고서 항목을 보고서 디자이너에서 사용할 수 있도록 하는 디자인 타임 구성 요소로 구성됩니다.  
  
 완전히 구현된 사용자 지정 보고서 항목 예는 [SQL Server Reporting Services 제품 예제](https://go.microsoft.com/fwlink/?LinkId=177889)를 참조하세요.  
  
## <a name="custom-report-item-scenarios"></a>사용자 지정 보고서 항목 시나리오  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 애플리케이션에 통합해야 하는 개발자는 기본적으로 RDL에서 지원되지 않는 기능이 필요할 수 있습니다. 이러한 기능에는 맵 컨트롤, 가로 목록, 열 목록, 피벗 재설정 가능 행렬 등이 포함됩니다. 애플리케이션으로 런타임 사용자 지정 보고서 항목 구성 요소를 개발하고 배포하여 필요한 기능을 제공할 수 있습니다.  
  
 기본적으로 지원되지 않는 기능을 제공하는 것 외에도 일부 개발자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 이미 포함되어 있는 컨트롤의 다른 버전으로 기존 기능을 확장해야 할 수도 있습니다. 이 시나리오에서는 개발자가 런타임 구성 요소, 디자인 타임 구성 요소 및 디자인 타임 보고서 항목 변환 구성 요소의 세 가지 구성 요소를 제공할 수 있습니다. 이 중 디자인 타임 보고서 항목 변환 구성 요소는 요청 시 기존 보고서 항목을 사용자 지정 보고서 항목으로 변환합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [사용자 지정 보고서 항목 아키텍처](custom-report-item-architecture.md)  
 사용자 지정 보고서 항목을 구성하는 구성 요소를 설명합니다.  
  
 [사용자 지정 보고서 항목 구현 요구 사항](custom-report-item-implementation-requirements.md)  
 사용자 지정 보고서 항목을 만들기 위한 선행 조건을 설명합니다.  
  
 [사용자 지정 보고서 항목 런타임 구성 요소 만들기](creating-a-custom-report-item-run-time-component.md)  
 사용자 지정 보고서 항목 런타임 구성 요소를 만드는 방법을 설명합니다.  
  
 [사용자 지정 보고서 항목 디자인 타임 구성 요소 만들기](creating-a-custom-report-item-design-time-component.md)  
 사용자 지정 보고서 항목 디자인 타임 구성 요소를 만드는 방법을 설명합니다.  
  
 [방법: 사용자 지정 보고서 항목 배포](how-to-deploy-a-custom-report-item.md)  
 사용자 지정 보고서 항목을 배포하는 방법을 설명합니다.  
  
 [사용자 지정 보고서 항목 클래스 라이브러리](custom-report-item-class-libraries.md)  
 `Microsoft.ReportDesigner` 네임스페이스의 사용자 지정 보고서 항목 인프라 클래스 및 관리되는 래퍼 클래스를 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [기술 참조&#40;SSRS&#41;](../technical-reference-ssrs.md)  
  
  

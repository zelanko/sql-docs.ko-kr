---
title: Reporting Services 확장 프로그램 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SQL Server Reporting Services, extending
- extensions [Reporting Services], about extensions
- SSIS, extending
- Reporting Services, extending
- extensions [Reporting Services]
ms.assetid: 2bf17ae4-2292-4a58-a1f0-56e99abd9b69
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b671200dce3b5be1e01e40b09ff285563c4d4f6b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62985771"
---
# <a name="reporting-services-extensions"></a>Reporting Services 확장 프로그램
  확장성을 위해 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 모듈식 아키텍처를 디자인했습니다. 다양한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소에서 사용되는 확장 프로그램을 쉽게 개발, 설치 및 관리할 수 있도록 관리 코드 API를 사용할 수 있습니다. 를 사용 하 여 개인 또는 공유 어셈블리를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 만들고 진화 하 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 비즈니스 요구에 맞게 새 기능을 추가할 수 있습니다.  
  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 고유한 확장성 아키텍처를 통해 개발자는 제품 및 해당 구성 요소의 특정 기능을 확장할 수 있습니다. 현재 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 데이터 처리 기능을 확장할 수 있도록 폭넓은 지원이 제공됩니다. 데이터 처리 API에는 개발자가 추가 데이터 처리를 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]에 구축하는 데 사용할 수 있는 친숙한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 공급자 구문 및 규칙이 포함됩니다. 이러한 데이터 처리 확장 프로그램은 보고서 서버와 보고서 디자이너 모두에 기능을 추가하여 사용자 지정 데이터가 보고서에 완벽하게 통합되도록 합니다.  
  
 지원되는 다른 확장 프로그램은 배달 확장 프로그램입니다. 배달 API는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 아키텍처와 완벽하게 통합되어 보고서 알림을 사용자에게 보낼 때 다양한 배달 메커니즘을 사용할 수 있습니다. 보고서 서버를 확장하여 사용자에게 사용자 지정 배달을 제공할 수 있으며 보고서 관리자의 구독 관리 페이지를 확장하여 사용자 지정 배달 확장 프로그램을 사용하는 구독이 가능하도록 할 수 있습니다.  
  
 또 다른 보고서 서버 확장 프로그램인 RDCE(Report Definition Customization Extension)에서는 보고서 정의가 처리 엔진에 전달되기 전에 보고서 정의를 동적으로 사용자 지정할 수 있습니다. 사용자나 언어 등의 요소를 기준으로 보고서를 사용자 지정할 수 있습니다. 예를 들어, 관리자나 부서원과 같이 다양한 사용자가 보는 뷰를 서로 다르게 구현하거나 프랑스어 또는 아랍어로 렌더링될 때 레이아웃이 서로 다르도록 보고서를 사용자 지정할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [확장에 대한 보안 고려 사항](security-considerations-for-extensions.md)  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 확장 프로그램 개발 및 배포와 관련된 보안 문제를 설명합니다.  
  
 [데이터 처리 확장 프로그램 구현](data-processing/implementing-a-data-processing-extension.md)  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 대한 데이터 처리 확장 프로그램을 구현하기 위한 요구 사항 및 단계를 설명합니다.  
  
 [배달 확장 프로그램 구현](delivery-extension/implementing-a-delivery-extension.md)  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 대한 배달 확장 프로그램을 구현하기 위한 요구 사항 및 단계를 설명합니다.  
  
 [렌더링 확장 프로그램 구현](rendering-extension/implementing-a-rendering-extension.md)  
 렌더링 확장 프로그램 개발에 대한 소개가 포함되어 있습니다.  
  
 [보안 확장 프로그램 구현](security-extension/implementing-a-security-extension.md)  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보안 확장 프로그램을 구현하기 위한 요구 사항 및 단계를 설명합니다.  
  
 [Reporting Services 확장 라이브러리](reporting-services-extension-library.md)  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 확장성 기능용 확장 API 라이브러리에 대한 프로그래밍 참조가 포함되어 있습니다.  
  
  

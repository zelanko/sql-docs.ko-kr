---
title: 물리적 아키텍처 (Analysis Services-데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- server architecture [Analysis Services]
- architecture [Analysis Services]
ms.assetid: 25eeecf0-6e85-4527-b94d-5503d27edaed
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 88c46b152935b805195b2d04b3dfcc5843e94577
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="physical-architecture-analysis-services---data-mining"></a>물리적 아키텍처(Analysis Services - 데이터 마이닝)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버와 클라이언트 구성 요소를 사용 하 여 비즈니스 인텔리전스 응용 프로그램에 대 한 데이터 마이닝 기능을 제공 합니다.  
  
-   서버 구성 요소는 Microsoft Windows 서비스로 구현됩니다. 동일한 컴퓨터에서 각각 별개의 Windows 서비스 인스턴스로 구현된 여러 개의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 유지할 수 있습니다.  
  
-   클라이언트는 웹 서비스로 노출되어 명령을 실행하고 응답을 수신하는 SOAP 기반 프로토콜인 공용 표준 XMLA(XML for Analysis)를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 와 통신합니다. 또한 XMLA를 통해 클라이언트 개체 모델이 제공되며 이는 ADOMD.NET과 같은 관리 공급자나 네이티브 OLE DB 공급자 중 하나를 사용하여 액세스할 수 있습니다.  
  
-   쿼리 명령은 데이터 마이닝 지향 업계 표준 쿼리 언어인 DMX(Data Mining Extensions)를 사용하여 실행할 수 있습니다. 또한 ASSL(Analysis Services Scripting Language)을 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 개체를 관리할 수도 있습니다.  
  
## <a name="architectural-diagram"></a>아키텍처 다이어그램  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스는 독립 실행형 서비스로 실행되며 서비스와의 통신은 HTTP 또는 TCP를 사용하는 XMLA(XML for Analysis)를 통해 이루어집니다.  
  
 AMO는 사용자 응용 프로그램과 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 관리 개체에 대한 액세스를 제공하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 사이의 계층입니다. AMO는 클라이언트 응용 프로그램에서 명령을 가져와서 이 명령을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 XMLA 메시지로 변환하는 클래스 라이브러리이며, 명령을 실행하는 메서드 멤버 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체에 대한 데이터를 포함하는 속성 멤버와 함께 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 개체를 최종 사용자에게 클래스로 표시합니다.  
  
 다음 그림은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 내의 서비스 및 이 인스턴스와 상호 작용하는 사용자 구성 요소를 비롯한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 요소 아키텍처를 보여 줍니다.  
  
 또한 HTTP 또는 TCP를 사용하는 XMLA(XML for Analysis) 수신기를 통해서만 이 인스턴스에 액세스할 수 있음을 보여 줍니다.  
  
> [!WARNING]  
>  DSO는 더 이상 사용되지 않습니다. 솔루션을 개발할 때 DSO를 사용해서는 안 됩니다.  
  
 ![Analysis Services 시스템 아키텍처 다이어그램](../../analysis-services/data-mining/media/analysisservicessystemarchitecture.gif "Analysis Services 시스템 아키텍처 다이어그램")  
  
## <a name="server-configuration"></a>서버 구성  
 하나의 서버 인스턴스는 각각 클라이언트 요청에 응답하고 개체를 처리하는 고유의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스 인스턴스가 있는 여러 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 지원할 수 있습니다.  
  
 테이블 형식 모델과 데이터 마이닝 및/또는 다차원 모델을 사용하려면 별도의 인스턴스를 설치해야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 테이블 형식 모드(xVelocity 메모리 내 분석 엔진(VertiPaq) 저장소 엔진 사용)로 실행되는 인스턴스와 기존 OLAP, MOLAP 또는 ROLAP 구성 중 하나로 실행되는 인스턴스의 단계별 설치를 지원합니다. 자세한 내용은 [Analysis Services 인스턴스의 서버 모드 확인](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)을 참조하세요.  
  
 클라이언트와 Analysis Services 서버 간의 모든 통신은 플랫폼 독립적, 언어 독립적인 프로토콜인 XMLA를 사용합니다. 클라이언트의 요청이 수신되면 Analysis Services는 이 요청이 OLAP과 관련된 것인지 또는 데이터 마이닝과 관련된 것인지 판단하고 이 판단에 따라 요청을 라우팅합니다. 자세한 내용은 [OLAP 엔진 서버 구성 요소](../../analysis-services/multidimensional-models/olap-physical/olap-engine-server-components.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [논리적 아키텍처 & #40; Analysis Services-데이터 마이닝 & #41;](../../analysis-services/data-mining/logical-architecture-analysis-services-data-mining.md)  
  
  

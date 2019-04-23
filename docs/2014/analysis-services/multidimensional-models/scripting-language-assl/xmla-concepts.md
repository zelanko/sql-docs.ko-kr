---
title: XMLA 개념 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XMLA, concepts
ms.assetid: 816183a7-d2f7-4e14-8e5b-2a4c1798fbc1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0da9467d293c0081309accd99fb46d7589fb4b8b
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158119"
---
# <a name="xmla-concepts"></a>XMLA 개념
  XMLA(XML for Analysis) 개방형 표준에서는 World Wide Web에 있는 데이터 원본에 대한 데이터 액세스를 지원합니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] XMLA 1.1 사양에 따라 XMLA를 구현합니다.  
  
 XMLA(XML for Analysis)는 웹에 있는 표준 다차원 데이터 원본에 대한 범용 데이터 액세스를 위해 특별히 설계된 SOAP(Simple Object Access Protocol) 기반 XML 프로토콜입니다. XMLA도 하지 않아도 구성 요소 개체 모델 (COM)를 노출 하는 클라이언트 구성 요소를 배포 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 인터페이스입니다. XMLA는 서버와의 왕복에 시간과 리소스가 많이 소모되며 데이터 원본에 대한 상태 저장 연결에 따라 서버의 사용자 연결이 제한되는 인터넷 환경에서 최적화됩니다.  
  
 XMLA는 용 네이티브 프로토콜로 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 인스턴스와 클라이언트 응용 프로그램 간의 모든 상호 작용에 사용 되는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 XML for Analysis 1.1을 완벽하게 지원하고 메타데이터 관리, 세션 관리 및 잠금 기능을 지원하는 확장을 제공합니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 인스턴스와 통신할 때 AMO(Analysis Management Objects)와 ADOMD.NET 모두 XMLA 프로토콜을 사용합니다.  
  
## <a name="handling-xmla-communications"></a>XMLA 통신 처리  
 XMLA 개방형 표준에서는 일반적으로 액세스 가능한 두 가지 메서드인 `Discover` 및 `Execute`를 설명합니다. 이러한 메서드는 XML에서 지원되는 느슨하게 연결된 클라이언트 및 서버 아키텍처를 사용하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 인스턴스에서 들어오고 나가는 정보를 처리합니다.  
  
 `Discover` 메서드는 웹 서비스에서 정보와 메타데이터를 가져옵니다. 이 정보에는 사용할 수 있는 데이터 원본 목록과 데이터 원본 공급자에 대한 정보가 포함될 수 있습니다. 속성에서는 데이터 원본에서 가져온 데이터를 정의하고 구체화합니다. `Discover` 메서드는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스의 데이터 원본에서 클라이언트 응용 프로그램에 필요한 많은 유형의 정보를 정의하는 일반적인 메서드입니다. 속성과 제네릭 인터페이스에서 확장성을 제공하므로 클라이언트 응용 프로그램에서 기존 기능을 다시 작성할 필요가 없습니다.  
  
 응용 프로그램에서 `Execute` 메서드를 사용하여 XMLA 데이터 원본에 대한 공급자 관련 명령을 실행할 수 있습니다.  
  
 XMLA 프로토콜은 웹 응용 프로그램에 최적화되어 있지만 LAN 지향 응용 프로그램에도 사용할 수 있습니다. 다음 응용 프로그램은이 XML 기반 API에서 활용할 수 있습니다.  
  
-   클라이언트와 서버 간 유연한 기술이 필요한 클라이언트/서버 응용 프로그램  
  
-   여러 운영 체제를 대상으로 하는 클라이언트/서버 응용 프로그램  
  
-   서버 용량을 늘리기 위해 중요한 상태가 필요하지 않는 클라이언트  
  
## <a name="xmla-and-the-unified-dimensional-model"></a>XMLA 및 UDM(Unified Dimensional Model)  
 XMLA는 UDM(Unified Dimensional Model) 방법론을 채택한 비즈니스 인텔리전스 응용 프로그램에 사용되는 프로토콜입니다.  
  
  

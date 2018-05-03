---
title: 서비스 공급자 및 구성 요소 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e83cbfa4be055e5949b7ae15c9280a396b914950
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="service-providers-and-components"></a>서비스 공급자 및 구성 요소
서비스 공급자는 데이터 저장소에서 기본적으로 지원 되지 않는 확장된 인터페이스를 구현 하 여 데이터 공급자의 기능을 확장 하는 구성 요소입니다.  
  
 범용 데이터 액세스를 제공는 *구성 요소 아키텍처* 기능이 적은 저장소 위에 데이터베이스 기능 또는 "서비스"의 불연속 집합을 구현 하려면 특수 구성 요소를 허용 하는 합니다. 따라서 모든 응용 프로그램 수 있는 공통 구현을 제공 서비스 구성 요소 확장 된 기능의 자체 구현을 제공 하도록 각 데이터 저장소 또는 일반 응용 프로그램에서 내부적으로 데이터베이스 기능을 구현 하는 대신 모든 데이터 저장소에 액세스할 때 사용 합니다. 일부 기능은 데이터 저장소와 일반 구성 요소를 통해 일부 여 고유 하 게 구현 됩니다 팩트는 응용 프로그램에 투명 합니다.  
  
 와 같은 커서 엔진 예를 들어 [OLE DB에 대 한 커서 서비스](http://msdn.microsoft.com/en-us/57638feb-4ecd-4051-becb-8f828d21cf44)을 스크롤할 수 있는 데이터를 생성 하는 순차적 정방향 전용 데이터 저장소에서 데이터를 사용할 수 있는 서비스 구성 요소입니다. ADO에서 일반적으로 사용 하는 다른 서비스 공급자가 포함 된 [Microsoft OLE DB 지 속성 공급자 (ADO 서비스 공급자)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) (에 대 한 데이터 파일에 저장)를는 [OLE DB (ADO 서비스 공급자)에 대 한 Microsoft Data Shaping Service ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (에 대 한 계층적 **레코드 집합**), 및 [Microsoft OLE DB Remoting Provider (ADO 서비스 공급자)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) (원격 컴퓨터에서 데이터 공급자 호출용).  
  
 서비스 및 데이터 공급자에 대 한 자세한 내용은 참조 [부록 a: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)합니다.

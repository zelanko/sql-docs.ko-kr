---
title: 서비스 공급자 및 구성 요소 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9bebbf4c89a04474cbf2d0c88704603cb4c3fef3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700382"
---
# <a name="service-providers-and-components"></a>서비스 공급자 및 구성 요소
서비스 공급자는 데이터 저장소에서 기본적으로 지원 되지 않는 확장된 인터페이스를 구현 하 여 데이터 공급자의 기능을 확장 하는 구성 요소입니다.  
  
 범용 데이터 액세스를 제공 된 *구성 요소 아키텍처* 는 특수 한 구성 요소를 허용 데이터베이스 기능 또는 "서비스"의 불연속 집합을 구현 하려면 기능이 적은 저장소를 기반으로 합니다. 따라서 모든 응용 프로그램 수 있는 일반적인 구현을 제공 서비스 구성 요소 확장 기능의 자체 구현을 제공 하도록 각 데이터 저장소 또는 일반 응용 프로그램에서 내부적으로 데이터베이스 기능을 구현 하는 대신 모든 데이터 저장소에 액세스할 때 사용 합니다. 일부 기능은가 구현 하는 고유 하 게 데이터 저장소와 일반 구성 요소를 통해 일부 팩트는 응용 프로그램에 투명 합니다.  
  
 와 같은 커서 엔진 예를 들어 [OLE DB에 대 한 커서 서비스](https://msdn.microsoft.com/57638feb-4ecd-4051-becb-8f828d21cf44)를 스크롤할 수 있는 데이터를 생성 하도록 순차, 정방향 전용 데이터 저장소에서 데이터를 사용할 수 있는 서비스 구성 요소입니다. ADO에서 일반적으로 사용 하는 다른 서비스 공급자를 포함 합니다 [Microsoft OLE DB 지 속성 공급자 (ADO 서비스 공급자)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) (에 대 한 데이터를 저장 하는 파일)에 [OLE DB (ADO 서비스 공급자)에 대 한 Microsoft Data Shaping Service ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (에 대 한 계층적 **레코드 집합**), 및 [Microsoft OLE DB 원격 공급자 (ADO 서비스 공급자)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) (에 대 한 원격 컴퓨터에서 데이터 공급자를 호출).  
  
 서비스 및 데이터 공급자에 대 한 자세한 내용은 참조 하세요. [부록 a: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)합니다.

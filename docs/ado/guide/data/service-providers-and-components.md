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
ms.openlocfilehash: a78db07f5ba445c54108558b2ff222bd217c2bbe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924241"
---
# <a name="service-providers-and-components"></a>서비스 공급자 및 구성 요소
서비스 공급자는 데이터 저장소에서 기본적으로 지원 하지 않는 확장 된 인터페이스를 구현 하 여 데이터 공급자의 기능을 확장 하는 구성 요소입니다.  
  
 유니버설 데이터 액세스는 개별 구성 요소에서 개별 데이터베이스 기능 집합을 구현할 수 있도록 하는 *구성 요소 아키텍처* 를 제공 합니다. 따라서 각 데이터 저장소에서 확장 된 기능의 자체 구현을 제공 하거나 일반 응용 프로그램을 통해 내부적으로 데이터베이스 기능을 구현 하도록 하는 대신 서비스 구성 요소는 응용 프로그램에서 사용할 수 있는 일반적인 구현을 제공 합니다. 데이터 저장소에 액세스할 때 사용 합니다. 일부 기능은 데이터 저장소에 의해 기본적으로 구현 되 고 일부는 제네릭 구성 요소가 응용 프로그램에 투명 하 게 구현 된다는 사실입니다.  
  
 예를 들어 [OLE DB에 대 한 커서 서비스](https://msdn.microsoft.com/57638feb-4ecd-4051-becb-8f828d21cf44)와 같은 커서 엔진은 순차적이 고 앞 으로만 이동 가능한 데이터 저장소의 데이터를 사용 하 여 스크롤 가능한 데이터를 생성할 수 있는 서비스 구성 요소입니다. ADO에서 자주 사용 하는 기타 서비스 공급자에는 [microsoft OLE DB 지 속성 공급자 (Ado 서비스 공급자)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) (파일에 데이터를 저장 하는 경우), [OLE DB (ado 서비스 공급자) 용 Microsoft 데이터 셰이핑 서비스 (ado 서비스 공급자)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (계층적 **레코드 집합**) 및 [Microsoft OLE DB Remoting 공급자 (ado 서비스 공급자)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) (원격 컴퓨터에서 데이터 공급자를 호출 하는 경우)가 포함 됩니다.  
  
 서비스 및 데이터 공급자에 대 한 자세한 내용은 [부록 a: providers](../../../ado/guide/appendixes/appendix-a-providers.md)를 참조 하십시오.

---
title: OLE DB 공급자 (ADO) | Microsoft Docs
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
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 926e5abc1c65db152c5ca5927c5acd2c932d6b90
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700530"
---
# <a name="ole-db-providers-ado"></a>OLE DB 공급자(ADO)
OLE DB 균일 한 액세스를 사용 하 여 응용 프로그램을 다양 한 소스에 저장 된 데이터를 제공 하는 COM 인터페이스 집합을 정의 합니다. 이 방법을 통해 데이터 원본을 지 원하는 DBMS 기능은 데이터 원본에 적절 한 인터페이스를 통해 데이터를 공유할 수 있습니다. 기본적으로 OLE DB의 고성능 아키텍처는 유연 하 고 구성 요소 기반 서비스 모델의 용도 기준으로 합니다. OLE DB에는 응용 프로그램과 데이터 간의 중간 계층의 수를 지정된 대신 하는 데 필요한 만큼의 구성에는 특정 태스크를 수행 하는 때에 필요 합니다.  
  
 예를 들어 사용자가 쿼리를 실행 하는 것으로 가정 합니다. 다음과 같은 시나리오를 고려해 보세요.  
  
-   데이터가 있는 현재 존재 하는 ODBC 드라이버는 있지만 네이티브 OLE DB 공급자는 관계형 데이터베이스에 있습니다. 그런 다음 적절 한 ODBC 드라이버를 로드 하는 ODBC 용 OLE DB 공급자에 게 ADO를 사용 하는 응용 프로그램입니다. 드라이버가 dbms의 데이터를 검색 하는 SQL 문을 전달 합니다.  
  
-   데이터는 네이티브 OLE DB 공급자가 Microsoft SQL Server에 상주 합니다. ADO를 사용 하 여 Microsoft SQL Server 용 OLE DB 공급자에 직접 연결 하는 응용 프로그램입니다. 없는 매개자는 필요 합니다.  
  
-   데이터에는 OLE DB 공급자는 SQL 쿼리를 처리 하기 위한 엔진으로 노출 하지 않습니다는 Microsoft Exchange Server에 상주 합니다. 응용 프로그램이 ADO를 사용 하 여 Microsoft Exchange 용 OLE DB 공급자에 게 및 쿼리 처리에 OLE DB 쿼리 프로세서 구성 요소를 호출 합니다.  
  
-   데이터는 문서 형식의 Microsoft NTFS 파일 시스템에 상주합니다. Microsoft 인덱싱 서비스에 대해 효율적인 콘텐츠 검색을 사용 하도록 설정 하려면 파일 시스템에 콘텐츠 및 문서 속성을 인덱싱하는 네이티브 OLE DB 공급자를 사용 하 여 데이터 액세스 됩니다.  
  
 위의 모든 예제에서 응용 프로그램 데이터를 쿼리할 수 있습니다. 최소한의 구성 요소를 사용 하 여 사용자의 요구 사항이 충족 됩니다. 각각의 경우에서 필요한 경우에 사용 되는 추가 구성 요소 및 필수 구성 요소 호출 됩니다. OLE DB를 사용할 때 재사용 가능한와 공유할 수 있는 구성 요소의이 요청 시 로드 높은 성능에 크게 기여 합니다.  
  
 공급자 두 범주로 나누어집니다: 서비스를 제공 하 고 데이터를 제공 합니다. 자체 데이터를 소유 하 고 응용 프로그램에 테이블 형식으로 제공 하는 데이터 공급자입니다. 서비스 공급자는 서비스를 캡슐화 생성 하 고 데이터를 사용 하 여 ADO 응용 프로그램의 기능을 확대 합니다. 서비스 공급자를 다른 서비스 공급자 또는 구성 요소와 함께 작동 해야 하는 서비스 구성 요소를 추가로 정의할 수도 있습니다.  
  
 ADO 제공 일관 된 다양 한 OLE DB 공급자에 게 더 높은 수준 인터페이스입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [데이터 공급자](../../../ado/guide/data/data-providers.md)  
  
-   [서비스 공급자 및 구성 요소](../../../ado/guide/data/service-providers-and-components.md)

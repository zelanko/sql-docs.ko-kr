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
ms.openlocfilehash: 7e86375639d875f5cfec21705af47c005afd901e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924753"
---
# <a name="ole-db-providers-ado"></a>OLE DB 공급자(ADO)
OLE DB은 다양 한 정보 소스에 저장 된 데이터에 대 한 일관 된 액세스를 제공 하는 응용 프로그램을 제공 하는 COM 인터페이스 집합을 정의 합니다. 이 접근 방식을 사용 하면 데이터 원본에서 데이터 원본에 적합 한 DBMS 기능을 지 원하는 인터페이스를 통해 데이터를 공유할 수 있습니다. 기본적으로 OLE DB의 고성능 아키텍처는 유연 하 고 구성 요소 기반 서비스 모델을 사용 하는 것을 기반으로 합니다. 응용 프로그램과 데이터 사이에 지정 된 수의 중간 계층을 포함 하는 대신 OLE DB에는 특정 작업을 수행 하는 데 필요한 만큼의 구성 요소만 필요 합니다.  
  
 예를 들어 사용자가 쿼리를 실행 하려고 한다고 가정 합니다. 다음과 같은 시나리오를 고려해 보세요.  
  
-   데이터는 현재 ODBC 드라이버는 있지만 네이티브 OLE DB 공급자는 없는 관계형 데이터베이스에 있습니다. 응용 프로그램은 ADO를 사용 하 여 ODBC 용 OLE DB 공급자와 통신 하 여 적절 한 ODBC 드라이버를 로드 합니다. 드라이버는 SQL 문을 DBMS에 전달 하 여 데이터를 검색 합니다.  
  
-   데이터는 네이티브 OLE DB 공급자가 있는 Microsoft SQL Server에 있습니다. 응용 프로그램은 ADO를 사용 하 여 Microsoft SQL Server에 대 한 OLE DB 공급자와 직접 통신 합니다. 중개자가 필요 하지 않습니다.  
  
-   데이터는 Microsoft Exchange Server에 있으며,이는 OLE DB 공급자가 있지만 SQL 쿼리를 처리 하는 엔진을 노출 하지 않습니다. 응용 프로그램은 ADO를 사용 하 여 Microsoft Exchange 용 OLE DB 공급자와 통신 하 고 OLE DB 쿼리 프로세서 구성 요소를 호출 하 여 쿼리를 처리 합니다.  
  
-   데이터는 문서 형식으로 Microsoft NTFS 파일 시스템에 상주 합니다. Microsoft 인덱싱 서비스를 통해 네이티브 OLE DB 공급자를 사용 하 여 데이터에 액세스 합니다. 그러면 파일 시스템의 문서 내용과 속성을 인덱싱하고 효율적인 콘텐츠 검색을 사용할 수 있습니다.  
  
 위의 모든 예제에서 응용 프로그램은 데이터를 쿼리할 수 있습니다. 최소한의 구성 요소를 사용 하 여 사용자의 요구 사항을 충족 해야 합니다. 각 경우에 필요한 경우에만 추가 구성 요소가 사용 되며, 필요한 구성 요소만 호출 됩니다. 재사용 가능 하 고 공유할 수 있는 구성 요소를 로드 하면 OLE DB를 사용할 때 성능이 크게 향상 됩니다.  
  
 공급자는 데이터 및 서비스 제공 서비스를 제공 하는 두 가지 범주로 나뉩니다. 데이터 공급자는 자체 데이터를 소유 하 고 응용 프로그램에 테이블 형식으로 제공 합니다. 서비스 공급자는 데이터를 생성 및 사용 하 여 서비스를 캡슐화 하 고 ADO 응용 프로그램의 기능을 확대 합니다. 서비스 공급자는 다른 서비스 공급자나 구성 요소와 함께 작동 해야 하는 서비스 구성 요소로 추가로 정의할 수도 있습니다.  
  
 ADO는 다양 한 OLE DB 공급자에 게 보다 일관 되 고 높은 수준의 인터페이스를 제공 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [데이터 공급자](../../../ado/guide/data/data-providers.md)  
  
-   [서비스 공급자 및 구성 요소](../../../ado/guide/data/service-providers-and-components.md)

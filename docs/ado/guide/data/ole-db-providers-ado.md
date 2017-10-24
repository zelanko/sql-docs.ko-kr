---
title: "OLE DB 공급자 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ef1c85f55928c266fb88f1639d5ccd53450fe59
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="ole-db-providers-ado"></a>OLE DB 공급자 (ADO)
OLE DB는 다양 한 소스에 저장 된 데이터에 일관 되 게 액세스 응용 프로그램에 제공 되는 COM 인터페이스의 집합을 정의 합니다. 이 방법을 통해 데이터 원본을 지 원하는 데이터 원본에 적합 한 DBMS 기능 인터페이스를 통해 데이터를 공유할 수 있습니다. 기본적으로 OLE DB의 성능 우선 아키텍처는 유연 하 고 구성 요소 기반 서비스 모델의 용도 기반으로 합니다. 지정 된 수의 데이터와 응용 프로그램 간에 중간 계층 대신 OLE DB에는 특정 작업을 수행 하는 데 필요한 만큼의 구성 하는 때에 필요 합니다.  
  
 예를 들어 사용자가 쿼리를 실행 하는 것으로 가정 합니다. 다음과 같은 시나리오를 고려해 보세요.  
  
-   데이터가 있는 현재 존재 하는 ODBC 드라이버는 하지만 네이티브 OLE DB 공급자는 관계형 데이터베이스에 있는: 응용 프로그램 ADO를 사용 하 여 다음 적절 한 ODBC 드라이버를 로드 하는 ODBC 용 OLE DB Provider와 통신할 수 있습니다. 드라이버는 DBMS의 데이터를 검색 하는 SQL 문을 전달 합니다.  
  
-   멤버의 데이터에 네이티브 OLE DB 공급자는 Microsoft SQL Server: Microsoft SQL Server 용 OLE DB Provider에 직접 연결 하는 응용 프로그램 ADO를 사용 합니다. 없음 매개자는 필요 합니다.  
  
-   OLE DB 공급자는 하지만 쿼리를 처리 하 SQL 엔진을 노출 하지 않습니다는 대 한 Microsoft Exchange Server의 데이터가 있는: 응용 프로그램 ADO를 사용 하 여 Microsoft Exchange 용 OLE DB 공급자에 게 문의 하 고 OLE DB 쿼리 프로세서를 호출 쿼리를 처리 하는 구성 요소입니다.  
  
-   문서 형식의 Microsoft NTFS 파일 시스템에 데이터가 있는: Microsoft 인덱싱 서비스에서 콘텐츠 및 문서 속성을 효율적으로 콘텐츠를 사용 하도록 설정 하려면 파일 시스템에 인덱스를 통해 네이티브 OLE DB 공급자를 사용 하 여 데이터 액세스 검색 합니다.  
  
 위의 모든 예제 응용 프로그램 데이터를 쿼리할 수 있습니다. 최소 구성 요소 수와 사용자의 요구를 충족 됩니다. 각각의 경우에서, 필요한 경우에 사용 되는 추가 구성 요소 및 필수 구성 요소 호출 됩니다. 이 요청 시 로드 재사용 가능한 및 공유할 수 있는 구성 요소는 OLE DB에서 사용 되는 경우에 크게 고성능에 기여 합니다.  
  
 공급자 두 범주로 나누어집니다: 데이터 및 서비스를 제공 하는 것을 제공 하는 것입니다. 데이터 공급자는 자체 데이터를 소유 하 고 응용 프로그램에 테이블 형식으로 제공 합니다. 서비스 공급자는 서비스를 캡슐화 생성 하 고 데이터를 사용 하 여 ADO 응용 프로그램의 기능을 확대 합니다. 서비스 공급자 다른 서비스 공급자 또는 구성 요소와 함께에서 작동 해야 하는 서비스 구성 요소로 추가 정의할 수도 있습니다.  
  
 ADO는 일관 된 제공 다양 한 OLE DB 공급자에 고급 인터페이스입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [데이터 공급자](../../../ado/guide/data/data-providers.md)  
  
-   [서비스 공급자 및 구성 요소](../../../ado/guide/data/service-providers-and-components.md)


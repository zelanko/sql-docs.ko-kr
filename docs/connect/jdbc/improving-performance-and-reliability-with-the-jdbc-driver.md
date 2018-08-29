---
title: JDBC Driver로 성능 및 안정성 개선 | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e1592499-b87b-45ee-bab8-beaba8fde841
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9108ab6ac330086acab16a73550d5fcab5d3970
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42783896"
---
# <a name="improving-performance-and-reliability-with-the-jdbc-driver"></a>JDBC 드라이버로 성능 및 안정성 개선

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

응용 프로그램 개발에서 모든 응용 프로그램에 공통적인 한 가지 측면은 성능 및 안정성을 개선하는 데 필요한 상수입니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 이러한 목적을 이루기 위한 다양한 기술을 갖추고 있습니다.  
  
이 섹션의 항목에서는 JDBC 드라이버 사용 시 응용 프로그램 성능 및 안정성을 향상시킬 수 있는 다양한 기술에 대해 설명합니다.  

## <a name="in-this-section"></a>섹션 내용

|항목|설명|  
|-----------|-----------------|  
|[사용하지 않을 때 개체 닫기](../../connect/jdbc/closing-objects-when-not-in-use.md)|JDBC 드라이버 개체가 더 이상 필요하지 않을 때 개체를 닫는 일의 중요성에 대해 설명합니다.|  
|[트랜잭션 크기 관리](../../connect/jdbc/managing-transaction-size.md)|트랜잭션 성능을 개선하는 기법을 설명합니다.|  
|[문 및 결과 집합 사용](../../connect/jdbc/working-with-statements-and-result-sets.md)|문 또는 결과 집합 개체를 사용 하는 경우 성능 향상을 위한 기술을 설명 합니다.|  
|[적응 버퍼링 사용](../../connect/jdbc/using-adaptive-buffering.md)|서버 커서 오버헤드 없이 모든 종류의 큰 값 데이터를 검색할 수 있도록 설계된 선택 버퍼링 기능에 대해 설명합니다.|  
|[스파스 열](../../connect/jdbc/sparse-columns.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스파스 열에 대한 JDBC Driver의 지원을 설명합니다.|  
|[JDBC 드라이버에 대한 준비된 문 메타데이터 캐싱](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)|준비 된 문 쿼리를 사용 하 여 성능 향상을 위한 기술을 설명 합니다.|
|[일괄 처리 삽입 작업에 대량 복사 API 사용](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)|일괄 처리 삽입 작업 및 그 이점에 대 한 대량 복사 API를 사용 하도록 설정 하는 방법에 설명 합니다.|

## <a name="see-also"></a>관련 항목:

[JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
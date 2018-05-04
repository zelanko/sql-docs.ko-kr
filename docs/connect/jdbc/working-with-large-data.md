---
title: 큰 데이터 작업 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5b93569f-eceb-4f05-b49c-067564cd3c85
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a1c7813018753ae525a3931ca2938e32e288c90e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-large-data"></a>큰 데이터 작업
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  JDBC 드라이버에서는 서버 커서 오버헤드 없이 모든 종류의 큰 값 데이터를 검색할 수 있는 선택 버퍼링이 지원됩니다. 선택 버퍼링을 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 에서 문 실행 결과 검색 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 응용 프로그램에서 필요할 때 보다는 한 번에 모두 있습니다. 또한 응용 프로그램에서 더 이상 액세스할 수 없는 결과를 즉시 삭제합니다.  
  
 에 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] JDBC 드라이버 버전 1.2에서 버퍼링 모드를 "**전체**" 기본적으로 합니다. 응용 프로그램 "responseBuffering" 연결 속성 설정 하지 않은 경우 "**적응**" 또는 연결 속성에서 사용 하 여는 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 의 메서드는 [ SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 개체, 서버에서 한 번에 전체 결과 읽도록 드라이버 지원 합니다. 선택 버퍼링 동작을 얻으려면 응용 프로그램 "responseBuffering" 연결 속성을 설정 해야 했습니다 "**적응**" 명시적으로 합니다.  
  
 **적응** 값이 기본 버퍼링 모드 이며 JDBC 드라이버는 필요할 때 최소 가능한 데이터를 버퍼링 합니다. 선택 버퍼링 사용에 대 한 자세한 내용은 참조 [선택 버퍼링 사용 하 여](../../connect/jdbc/using-adaptive-buffering.md)합니다.  
  
 이 섹션의 항목에서 큰 값 데이터를 검색 하는 데 사용할 수 있는 다양 한 방법에 설명 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[대규모 데이터 읽기 샘플](../../connect/jdbc/reading-large-data-sample.md)|SQL 문을 사용하여 큰 값 데이터를 검색하는 방법에 대해 설명합니다.|  
|[저장 프로시저에서 대규모 데이터 읽기 샘플](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md)|큰 CallableStatement OUT 매개 변수 값을 검색하는 방법에 대해 설명합니다.|  
|[대규모 데이터 업데이트 샘플](../../connect/jdbc/updating-large-data-sample.md)|데이터베이스에서 큰 값 데이터를 업데이트하는 방법에 대해 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [샘플 JDBC 드라이버 응용 프로그램](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  

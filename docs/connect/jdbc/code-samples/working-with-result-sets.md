---
title: With Result Sets | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4fc4b1c6-3075-4ad7-9244-865d9ede7ae6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1802a6a51773ce552bcd4fcc45745a29e2405db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32828238"
---
# <a name="working-with-result-sets"></a>결과 집합 사용
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  에 포함 된 데이터로 작업 하는 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터베이스에서 데이터 조작 방법 중 하나가 결과 집합을 사용 하는 합니다. [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 결과의 사용을 통해 설정 지원은 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다. SQLServerResultSet 개체를 사용 하 여 SQL 문이나 저장된 프로시저에서 반환 된 데이터를 검색할 필요에 따라 데이터를 업데이트 한 한 후 데이터베이스에 다시 보관할 수 있습니다.  
  
 또한 SQLServerResultSet 개체는 기본 데이터베이스의 변경 내용에 따라 중요도 수준을 다양 하 게 설정할 행의 데이터 탐색, 가져오기 또는 설정에 포함 된 데이터에 대 한 메서드를 제공 합니다.  
  
> [!NOTE]  
>  변경 내용에 따른 중요도 포함 하 여 결과 집합에 대 한 자세한 내용은 참조 [JDBC 드라이버로 결과 집합 관리](../../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)합니다.  
  
 이 섹션의 항목에 포함 된 데이터를 조작 하는 결과 집합을 사용할 수 있는 다양 한 방법을 설명는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터베이스입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[결과 집합 데이터 검색 샘플](../../../connect/jdbc/retrieving-result-set-data-sample.md)|결과 집합에서 데이터 검색을 사용 하는 방법에 설명 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터베이스를 표시 합니다.|  
|[결과 집합 데이터 샘플 수정](../../../connect/jdbc/modifying-result-set-data-sample.md)|결과 집합을 삽입, 검색 및 수정에 대 한 데이터를 사용 하는 방법에 설명 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터베이스입니다.|  
|[결과 집합 데이터 캐싱 샘플](../../../connect/jdbc/caching-result-set-data-sample.md)|많은 양의 데이터를 검색할에 결과 집합을 사용 하는 방법에 설명는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터베이스를 클라이언트에서 해당 데이터가 캐시 되는 방식을 제어 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [샘플 JDBC 드라이버 응용 프로그램](../../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  

---
title: SQLServerDataSourceObjectFactory 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b616632b-5987-470d-b36c-b22fa9213145
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ecec8f58587d6a57468f8078e1f680675bede77
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32845818"
---
# <a name="sqlserverdatasourceobjectfactory-class"></a>SQLServerDataSourceObjectFactory 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JNDI(Java Naming and Directory Interface)의 데이터 원본을 구체화하기 위한 개체 팩터리를 나타냅니다.  
  
 **패키지에 대 한** com.microsoft.sqlserver.jdbc  
  
 **확장:** java.lang.Object  
  
 **구현:** javax.naming.spi.ObjectFactory  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerDataSourceObjectFactory  
```  
  
## <a name="remarks"></a>주의  
 모든 데이터 원본 클래스는 이 메서드를 상속합니다. 참조 가능한 인터페이스에 대 한 지원의 일환으로 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 는 ObjectFactory를 구현 하는이 클래스를 노출 합니다. Java 응용 프로그램 서버 getReference를 호출 하는 데이터 원본 클래스에 하 고이 내부적으로 클래스 이름을 해당 클래스 팩터리로 사용 하는 참조 방식 개체를 만듭니다.  
  
 SQLServerDataSourceObjectFactory 개체와 호출의 인스턴스를 만들고 참조 개체가 역참조 해야 하는 Java 응용 프로그램 서버에 있는 경우는 [getObjectInstance](../../../connect/jdbc/reference/getobjectinstance-method-sqlserverdatasourceobjectfactory.md) 참조 개체에 전달 하는 메서드 데이터 원본 인스턴스를 검색 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSourceObjectFactory 멤버](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

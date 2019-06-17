---
title: SQLServerDataSourceObjectFactory 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b616632b-5987-470d-b36c-b22fa9213145
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6314bf3fe9f0d5773ed1084858ea1691418528af
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66784357"
---
# <a name="sqlserverdatasourceobjectfactory-class"></a>SQLServerDataSourceObjectFactory 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JNDI(Java Naming and Directory Interface)의 데이터 원본을 구체화하기 위한 개체 팩터리를 나타냅니다.  
  
 **패키지:** com.microsoft.sqlserver.jdbc  
  
 **확장:** java.lang.Object  
  
 **구현:** javax.naming.spi.ObjectFactory  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerDataSourceObjectFactory  
```  
  
## <a name="remarks"></a>Remarks  
 모든 데이터 원본 클래스는 이 메서드를 상속합니다. 참조 가능한 인터페이스에 대한 지원의 일부로 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 ObjectFactory를 구현하는 이 클래스를 노출합니다. Java 애플리케이션 서버에서는 데이터 원본 클래스에 대해 getReference를 호출하고, 내부적으로 클래스 이름을 해당 클래스 팩터리로 사용하는 Reference 개체를 만듭니다.  
  
 SQLServerDataSourceObjectFactory 개체 호출의 인스턴스를 만들고 Java 응용 프로그램 서버에 대 한 참조 개체를 역참조 하는 경우는 [getObjectInstance](../../../connect/jdbc/reference/getobjectinstance-method-sqlserverdatasourceobjectfactory.md) 에 대 한 참조 개체를 전달 하는 메서드 데이터 원본 인스턴스를 검색 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSourceObjectFactory 멤버](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

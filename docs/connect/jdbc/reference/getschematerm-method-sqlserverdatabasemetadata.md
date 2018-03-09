---
title: "getSchemaTerm 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDatabaseMetaData.getSchemaTerm
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 3e4a400f-0859-4ac3-983e-c25633b33683
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 50df53f6f7eae8c825a9420aaf24288081e413f5
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getschematerm-method-sqlserverdatabasemetadata"></a>getSchemaTerm 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스에서 "스키마"에 사용하는 기본 용어를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getSchemaTerm()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 기본 용어가 들어 있는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getSchemaTerm 메서드는 java.sql.DatabaseMetaData 인터페이스의 getSchemaTerm 메서드에 의해 지정 됩니다.  
  
 사용 하는 경우는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터베이스를이 메서드는 "스키마"를 기본 용어로 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

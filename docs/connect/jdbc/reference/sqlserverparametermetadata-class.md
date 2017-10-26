---
title: "SQLServerParameterMetaData 클래스 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 546290e0-9411-4a2b-aa36-61251e70e9cf
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 836d6d90405e42df25a9bffb025a6113268560c8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverparametermetadata-class"></a>SQLServerParameterMetaData 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  준비된 문 매개 변수의 메타데이터를 나타냅니다.  
  
 **패키지에 대 한** com.microsoft.sqlserver.jdbc  
  
 **확장:** java.lang.Object  
  
 **구현:** java.sql.ParameterMetaData  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerParameterMetaData  
```  
  
## <a name="remarks"></a>주의  
 매개 변수 메타데이터를 검색하려면 준비된 문을 SET FMT ONLY를 사용하여 실행합니다. 호출 가능한 문에서는 sp_sproc_columns를 호출하여 프로시저 매개 변수의 이름과 메타데이터를 검색합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerParameterMetaData 멤버](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  


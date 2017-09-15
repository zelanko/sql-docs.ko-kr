---
title: "getTime 메서드 (java.lang.String, java.util.Calendar) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.getTime (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3d4c67c2-a3c8-4a26-a159-89c5d63fda0b
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eaa53198cb3a96725f3304a7bb8fa88c67df73b1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="gettime-method-javalangstring-javautilcalendar"></a>getTime 메서드(java.lang.String, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 Java 프로그래밍 언어에서 지정된 된 일정 개체를 사용 하 여 매개 변수 이름 지정의 java.sql.Time 개체로 지정된 된 매개 변수의 값을 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Time getTime(java.lang.String sCol,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
 *cal*  
  
 일정 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 시간 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getTime 메서드는 java.sql.CallableStatement 인터페이스의 getTime 메서드에 의해 지정 됩니다.  
  
 "Getter 메서드 변환" 이라는 차트 참조 [데이터 형식 변환 이해](../../../connect/jdbc/understanding-data-type-conversions.md) 된을 확인할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터 형식은이 방법으로 검색할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getTime 메서드 &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

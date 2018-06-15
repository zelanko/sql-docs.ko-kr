---
title: getTime 메서드 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTime (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ca0a3b29-30d1-4d20-bc8d-d3d9ed19ff50
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea3d8a2bb7c3b261f62197307eced014727c2a34
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32839228"
---
# <a name="gettime-method-javalangstring"></a>getTime 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 이름이 지정된 경우 지정된 매개 변수의 값을 검색하여 Java 프로그래밍 언어의 java.sql.Time 개체로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Time getTime(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 시간 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getTime 메서드는 java.sql.CallableStatement 인터페이스의 getTime 메서드에 의해 지정 됩니다.  
  
 "Getter 메서드 변환" 이라는 차트 참조 [데이터 형식 변환 이해](../../../connect/jdbc/understanding-data-type-conversions.md) 된을 확인할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터 형식은이 방법으로 검색할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getTime 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

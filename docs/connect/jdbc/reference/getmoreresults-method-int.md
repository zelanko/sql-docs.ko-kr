---
title: "getMoreResults 메서드 (int) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.getMoreResults (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6419e5a8-8b3a-4d5b-8226-95865c52c723
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0daf7ce3684ce376ea228adcc9e4b2c0d32f831b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getmoreresults-method-int"></a>getMoreResults 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 항목의 다음 결과로 이동 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체와 현재 열려 있는 모든 결과와 거래 고 지정 된 모드의 지침에 따라 개체를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final boolean getMoreResults(int mode)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *모드*  
  
 **int** 현재 열려 있는 결과 집합 개체를 처리 하는 방법을 나타내는 합니다. 다음 상수 중 하나여야 합니다.  
  
 CLOSE_CURRENT_RESULT  
  
 KEEP_CURRENT_RESULT(JDBC 드라이버에서는 지원되지 않음)  
  
 CLOSE_ALL_RESULTS  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 경우 반환 된 결과 결과 집합입니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getMoreResults 메서드는 java.sql.Statement 인터페이스의 getMoreResults 메서드에 의해 지정 됩니다.  
  
 지정 된 대로 동작 하는 getMoreResults 메서드 결과 검색 하기 전에 호출 하는 경우는 *모드* 인수와 다음 결과로 이동 합니다.  
  
> [!NOTE]  
>  JDBC 드라이버에서는 KEEP_CURRENT_RESULT 상수의 사용을 지원하지 않습니다. 이 상수를 사용하면 예외가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getMoreResults 메서드 &#40; SQLServerStatement &#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  


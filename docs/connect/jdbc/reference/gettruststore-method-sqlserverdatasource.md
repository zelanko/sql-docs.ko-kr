---
title: "getTrustStore 메서드 (SQLServerDataSource) | Microsoft Docs"
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
- getTrustStore Method (SQLServerDataSource)
apilocation:
- getTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 8f5850e4-8627-49a8-ba0e-b1f4014322a5
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e23a59adeb94be0f7cacebdc40fb442c3c69f9ae
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="gettruststore-method-sqlserverdatasource"></a>getTrustStore 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  인증서 trustStore 파일의 경로(파일 이름 포함)를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getTrustStore()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 설정 된 경우 인증서 trustStore 파일 또는 null로 경로 (파일 이름 포함)를 포함 하 합니다.  
  
## <a name="remarks"></a>주의  
 TrustStore 속성이 설정 하지 않으면는 [getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md) 메서드가 null을 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

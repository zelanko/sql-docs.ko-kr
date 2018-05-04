---
title: getTrustStore 메서드 (SQLServerDataSource) | Microsoft Docs
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
- getTrustStore Method (SQLServerDataSource)
apilocation:
- getTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 8f5850e4-8627-49a8-ba0e-b1f4014322a5
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 523ae02799c14c2b55d1bd6144758952930cf190
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
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
  
  

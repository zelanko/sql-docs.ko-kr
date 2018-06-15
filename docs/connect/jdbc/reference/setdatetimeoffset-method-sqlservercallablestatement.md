---
title: setDateTimeOffset 메서드 (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9383e14d-c83e-43c5-980c-50a3e0bedc31
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bb5ed787351a9159f9eb839575743a4137cdafea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32841618"
---
# <a name="setdatetimeoffset-method-sqlservercallablestatement"></a>setDateTimeOffset 메서드(SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 메서드는에서 추가 된 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0.  
  
 에 지정 된 열의 값을 설정 하는 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setDateTimeOffset(String sCol, microsoft.sql.DateTimeOffset t)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 열 이름입니다.  
  
 *t*  
  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 검색할 수 있습니다는 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 값과 [SQLServerCallableStatement.getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)합니다.  
  
 [setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlserverpreparedstatement.md) 열의 서 수를 사용 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

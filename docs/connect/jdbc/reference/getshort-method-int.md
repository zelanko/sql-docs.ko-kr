---
description: getShort 메서드(int)
title: getShort 메서드(int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getShort (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cd9773c1-b598-4adb-aaf6-0c0f589cbef5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b3a2b821a05f51a39cce4bf6b6458ccfe3c0e64
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434565"
---
# <a name="getshort-method-int"></a>getShort 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 인덱스가 지정된 경우 지정된 매개 변수의 값을 Java 프로그래밍 언어의 **short**로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public short getShort(int index)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *index*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 **short** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getShort 메서드는 java.sql.CallableStatement 인터페이스의 getShort 메서드에 의해 지정됩니다.  
  
 이 메서드는 **smallint**, **tinyint** 및 **bit**와 같이 정수 값을 안전하게 반환할 수 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식에서만 지원됩니다. 다른 데이터 형식에 이 메서드를 사용하면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getShort 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

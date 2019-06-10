---
title: getBytes 메서드(SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b6e88cea-54b3-4d18-a9af-db54abf19f45
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: eb7fe193d1b854ca3d551b065825e8705cd92cb8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66804002"
---
# <a name="getbytes-method-sqlservercallablestatement"></a>getBytes 메서드(SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수의 값을 검색하여 바이트 배열로 반환합니다.  
  
## <a name="overload-list"></a>오버로드 목록  
  
|속성|설명|  
|----------|-----------------|  
|[getBytes(int)](../../../connect/jdbc/reference/getbytes-method-int.md)|매개 변수 인덱스가 지정된 경우 지정된 매개 변수의 값을 검색하여 바이트 값의 배열로 반환합니다.|  
|[getBytes(java.lang.String)](../../../connect/jdbc/reference/getbytes-method-java-lang-string.md)|매개 변수 이름이 지정된 경우 지정된 매개 변수의 값을 검색하여 바이트 값의 배열로 반환합니다.|  
  
## <a name="remarks"></a>Remarks  
 이전 버전의 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 SQLServerCallableStatement.getBytes를 사용하여 바이트 배열과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식 **date**, **time**, **datetime2** 또는 **datetimeoffset** 간에 값을 변환할 수 있었습니다. 이제 이 메서드와 이러한 데이터 형식을 함께 사용하면 변환이 지원되지 않음을 나타내는 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

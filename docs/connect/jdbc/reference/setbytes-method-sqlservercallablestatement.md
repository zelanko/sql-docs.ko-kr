---
title: setBytes 메서드(SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f264f1a6-ee35-4eaf-81d8-ecf99f03b35d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4cb75f7d7e0ed77872e384d6e981a8fe8cae4410
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80929153"
---
# <a name="setbytes-method-sqlservercallablestatement"></a>setBytes 메서드(SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 **byte** 값의 배열로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setBytes(java.lang.String sCol,  
                     byte[] b)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
 *b*  
  
 **byte** 값의 배열입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이전 버전의 드라이버에서는 SQLServerCallableStatement.setBytes를 사용하여 바이트 배열과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식 **date**, **time**, **datetime2** 또는 **datetimeoffset** 간에 값을 변환할 수 있었습니다. 이제 이 메서드와 이러한 데이터 형식을 함께 사용하면 변환이 지원되지 않음을 나타내는 예외가 발생합니다.  
  
 이 setBytes 메서드는 java.sql.CallableStatement 인터페이스의 setBytes 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

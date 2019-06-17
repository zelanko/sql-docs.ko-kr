---
title: getPrecision 메서드 (SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getPrecision
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8bd79484-bab6-423b-978f-d7ec7132ebeb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4f7959476f092389f22f2d7720927907b8f59d69
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66771349"
---
# <a name="getprecision-method-sqlserverparametermetadata"></a>getPrecision 메서드(SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수의 자릿수를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getPrecision(int param)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *param*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 지정된 매개 변수의 전체 자릿수를 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getPrecision 메서드는 java.sql.ParameterMetaData 인터페이스의 getPrecision 메서드에 의해 지정 됩니다.  
  
 숫자 형식의 경우 이 메서드는 자릿수를 가져옵니다. 문자 형식의 경우에는 최대 길이(문자 수)를 가져옵니다. 이진 형식의 경우에는 최대 길이(바이트)를 가져옵니다. 자릿수를 알 수 없으면 이 메서드는 "0"을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerParameterMetaData 메서드](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 멤버](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 클래스](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  

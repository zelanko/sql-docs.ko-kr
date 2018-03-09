---
title: "setNCharacterStream 메서드 판독기 개체-int | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7732746b-eda5-469e-8567-e8546c4d81cd
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a06f22774bfedf22f02d4daf3cb613aeac64db51
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="setncharacterstream-method-int-javaioreader"></a>setNCharacterStream 메서드(int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 된 Reader 개체를 지정된 된 매개 변수를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setNCharacterStream(int parameterIndex,  
                                                 java.io.Reader value)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 **int** 매개 변수 인덱스를 나타내는입니다.  
  
 *value*  
  
 매개 변수 값을 포함 하는 판독기 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setNCharacterStream 메서드는 java.sql.PreparedStatement 인터페이스의 setNCharacterStream 메서드에 의해 지정 됩니다.  
  
 에 대 한이 메서드를 사용 해야 **NCHAR**, **NVARCHAR**, **NTEXT**, 및 **XML** 데이터 형식입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setNCharacterStream 메서드 &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  

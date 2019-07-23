---
title: setNCharacterStream 메서드를 판독기 개체로-int | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7732746b-eda5-469e-8567-e8546c4d81cd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 01e501bbe9ae68b35c4e9b8373b0dfe1f55d9f6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973904"
---
# <a name="setncharacterstream-method-int-javaioreader"></a>setNCharacterStream 메서드(int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 Reader 개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setNCharacterStream(int parameterIndex,  
                                                 java.io.Reader value)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
 *value*  
  
 매개 변수 값이 들어 있는 Reader 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setNCharacterStream 메서드는 Java.sql.preparedstatement 인터페이스의 setNCharacterStream 메서드에 의해 지정 됩니다.  
  
 이 메서드는 **NCHAR**, **NVARCHAR**, **NTEXT**및 **XML** 데이터 형식에 사용 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [setNCharacterStream 메서드 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  

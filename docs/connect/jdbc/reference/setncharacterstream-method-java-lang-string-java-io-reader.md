---
title: setNCharacterStream 메서드 판독기 개체를 문자열 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fd19fbb8-a878-4d98-a584-e4969d649844
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 361193c9f85034da5a40c6dac6d1865a77c34612
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800469"
---
# <a name="setncharacterstream-method-javalangstring-javaioreader"></a>setNCharacterStream 메서드(java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 Reader 개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setNCharacterStream(java.lang.String parameterName,  
                       java.io.Reader value)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 매개 변수 이름을 나타내는 **문자열**입니다.  
  
 *value*  
  
 판독기 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setNCharacterStream 메서드는 java.sql.CallableStatement 인터페이스의 setNCharacterStream 메서드에 의해 지정 됩니다.  
  
 에 대 한이 메서드를 사용할지 **NCHAR**, **NVARCHAR**를 **NTEXT**, 및 **XML** 데이터 형식입니다.  
  
## <a name="see-also"></a>참고 항목  
 [setNCharacterStream 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  

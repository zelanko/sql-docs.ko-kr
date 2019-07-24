---
title: setNCharacterStream 메서드를 판독기 개체로-문자열 | Microsoft Docs
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
ms.openlocfilehash: 34eb40d6c36f5c1586ac690de5e9fc354c8fd1f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973864"
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
 이 setNCharacterStream 메서드는 setNCharacterStream 메서드를 통해 지정 됩니다.  
  
 이 메서드는 **NCHAR**, **NVARCHAR**, **NTEXT**및 **XML** 데이터 형식에 사용 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [setNCharacterStream 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  

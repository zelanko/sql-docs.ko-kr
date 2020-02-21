---
title: Reader 개체에 대한 setNCharacterStream 메서드 - long | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: af9a1ba8-7980-43fa-88e5-14f6cc5e897c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 73bd7fe7d3da0745f66e0a6d883d7024a318c95f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67973890"
---
# <a name="setncharacterstream-method-javalangstring-javaioreader-long"></a>setNCharacterStream 메서드(java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 문자 길이의 지정된 Reader 개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setNCharacterStream(java.lang.String parameterName,  
                     java.io.Reader value,  
                     long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 매개 변수 이름을 나타내는 **문자열**입니다.  
  
 *value*  
  
 Reader 개체입니다.  
  
 *length*  
  
 스트림의 문자 수를 나타내는 **long**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setNCharacterStream 메서드는 java.sql.CallableStatement 인터페이스의 setNCharacterStream 메서드에 의해 지정됩니다.  
  
 이 메서드는 **NCHAR**, **NVARCHAR**, **NTEXT**및 **XML** 데이터 형식에 사용해야 합니다.  
  
 스트림의 길이가 *length* 매개 변수에 지정된 길이와 다르면 행이 업데이트되거나 삽입될 때 JDBC 드라이버에서 예외가 발생합니다.  
  
 스트림의 길이를 알 수 없으면 *length* 매개 변수는 드라이버에서 스트림의 길이에 상관없이 스트림을 허용해야 함을 나타내는 -1로 설정될 수 있습니다. sqljdbc4.jar을 사용하면 애플리케이션에서 길이를 알 수 없는 스트림에서 열을 업데이트하려고 할 때 JDBC 4.0 메서드 [setNCharacterStream 메서드 &#40;java.lang.String, java.io.Reader&#41;](../../../connect/jdbc/reference/setncharacterstream-method-java-lang-string-java-io-reader.md)를 사용하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
 [setNCharacterStream 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  

---
title: setNClob 메서드(java.lang.String, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c1b95ee7-7e82-418f-8f30-948589086f63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5d94c56b057c5909ec4d092ad8814258c5eab3e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923294"
---
# <a name="setnclob-method-javalangstring-javaioreader-long"></a>setNClob 메서드(java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 문자 길이의 지정된 Reader 개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setNClob(java.lang.String parameterName,  
              java.io.Reader reader,  
              long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
 *reader*  
  
 Reader 개체입니다.  
  
 *length*  
  
 스트림의 문자 수를 나타내는 **long**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 메서드는 **NCHAR**, **NVARCHAR**, **NTEXT**및 **XML** 매개 변수 데이터 형식에 사용해야 합니다.  
  
 이 setNClob 메서드는 java.sql.CallableStatement 인터페이스의 setNClob 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [setNClob 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  

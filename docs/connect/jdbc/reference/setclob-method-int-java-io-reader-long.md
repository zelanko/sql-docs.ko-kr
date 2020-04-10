---
title: setClob 메서드(int, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 157882dd-1a96-4501-a895-46e88a49266e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 373af12cda9700eeab6912baf21c12015c1a82d3
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927153"
---
# <a name="setclob-method-int-javaioreader-long"></a>setClob 메서드(int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 문자 길이의 지정된 Reader 개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setClob(int parameterIndex,  
                          java.io.Reader reader,  
                          long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
 *reader*  
  
 Reader 개체입니다.  
  
 *length*  
  
 매개 변수 값의 문자 수를 나타내는 **long**입니다.  
  
## <a name="remarks"></a>설명  
 이 setClob 메서드는 java.sql.PreparedStatement 인터페이스의 setClob 메서드에 의해 지정됩니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>참고 항목  
 [setClob 메서드&#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setclob-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  

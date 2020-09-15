---
description: setCharacterStream 메서드(int, java.io.Reader)
title: setCharacterStream 메서드(int, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8d4e1f7-14fc-4590-af98-1eda30d2ca6d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2cd2b09810329bc79f74616fc964eb18c2efd803
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432325"
---
# <a name="setcharacterstream-method-int-javaioreader"></a>setCharacterStream 메서드(int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 java.io.Reader 개체로 설정합니다.  
  
> [!NOTE]
>  이 기능은 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 버전 2.0에 새로 도입된 기능입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setCharacterStream(int parameterIndex,  
                              java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 매개 변수 번호를 나타내는 **int**입니다.  
  
 *reader*  
  
 유니코드 데이터가 들어 있는 java.io.Reader 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setCharacterStream 메서드는 Java.sql.PreparedStatement 인터페이스의 setCharacterStream 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [setCharacterStream 메서드&#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  

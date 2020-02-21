---
title: getSendStringParametersAsUnicode 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3836d0ab-c3fb-41ff-bb89-10389594ae51
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df27a5368dfea7f417fb84e2ebe38a8987165aec
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67979975"
---
# <a name="getsendstringparametersasunicode-method-sqlserverdatasource"></a>getSendStringParametersAsUnicode 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  문자열 매개 변수를 서버에 유니코드 형식으로 보낼 수 있는지 여부를 나타내는 **boolean** 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getSendStringParametersAsUnicode()  
```  
  
## <a name="return-value"></a>Return Value  
 문자열 매개 변수를 서버에 유니코드 형식으로 보낼 수 있으면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>설명  
 sendStringParametersAsUnicode 속성이 기본값인 **true**로 설정되어 있으면 문자열 매개 변수가 서버에 유니코드 형식으로 보내집니다. sendStringParametersAsUnicode 속성이 **false**로 설정되어 있으면 문자열 매개 변수가 서버에 유니코드 형식이 아닌 ASCII/MBCS 형식으로 보내집니다. sendStringParametersAsUnicode 속성이 설정되어 있지 않으면 getSendStringParametersAsUnicode는 기본값인 **true**를 반환합니다.  
  
 sendStringParametersAsUnicode 연결 속성에 대한 자세한 내용은 [연결 속성 설정](../../../connect/jdbc/setting-the-connection-properties.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

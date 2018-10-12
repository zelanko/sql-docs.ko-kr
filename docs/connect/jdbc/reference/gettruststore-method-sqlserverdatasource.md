---
title: getTrustStore 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getTrustStore Method (SQLServerDataSource)
apilocation:
- getTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 8f5850e4-8627-49a8-ba0e-b1f4014322a5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 561148cb1492457c4528bd1fdbf60e66233c6b6e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47708871"
---
# <a name="gettruststore-method-sqlserverdatasource"></a>getTrustStore 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  인증서 trustStore 파일의 경로(파일 이름 포함)를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getTrustStore()  
```  
  
## <a name="return-value"></a>반환 값  
 인증서 trustStore 파일의 경로(파일 이름 포함) 또는 값이 설정되지 않은 경우 null이 포함되어 있는 **문자열**입니다.  
  
## <a name="remarks"></a>Remarks  
 trustStore 속성이 설정되어 있지 않으면 [getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md) 메서드는 null을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

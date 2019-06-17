---
title: getResponseBuffering 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getResponseBuffering()
apilocation:
- SQLServerDataSource.getResponseBuffering()
apitype: Assembly
ms.assetid: 19585a93-88a4-415e-a20e-12ba58cddeaa
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7ea9552ff9a9bf8d0a591f35670ca7147c67e18d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801363"
---
# <a name="getresponsebuffering-method-sqlserverdatasource"></a>getResponseBuffering 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체에 대한 응답 버퍼링 모드를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 소문자를 포함 하는 **전체** 하거나 **적응**합니다.  
  
## <a name="remarks"></a>Remarks  
 **full** 값은 런타임에 서버의 전체 결과를 읽도록 지정합니다.  
  
 **adaptive** 값은 필요할 때 가능한 최소한의 데이터를 버퍼링하도록 지정합니다. **adaptive** 값은 기본 버퍼링 모드입니다.  
  
 응답 버퍼링 모드를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [를 사용 하 여 선택 버퍼링](../../../connect/jdbc/using-adaptive-buffering.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [setResponseBuffering 메서드(SQLServerDataSource)](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)   
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

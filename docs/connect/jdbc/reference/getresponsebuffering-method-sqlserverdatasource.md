---
title: "getResponseBuffering 메서드 (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDataSource.getResponseBuffering()
apilocation: SQLServerDataSource.getResponseBuffering()
apitype: Assembly
ms.assetid: 19585a93-88a4-415e-a20e-12ba58cddeaa
caps.latest.revision: "27"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b11609d9b29bbd76a65c3db3dff12a94d4d96767
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getresponsebuffering-method-sqlserverdatasource"></a>getResponseBuffering 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  응답 버퍼링 모드를이 대 한 반환 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 포함 하는 소문자 **전체** 또는 **적응**합니다.  
  
## <a name="remarks"></a>주의  
 **전체** 값 런타임 시 서버에서 전체 결과 읽도록 지정 합니다.  
  
 **적응** 값 필요할 때 최소 가능한 데이터를 버퍼링 하도록 지정 합니다. **적응** 값이 기본 버퍼링 모드입니다.  
  
 응답 버퍼링 모드를 사용 하는 방법에 대 한 자세한 내용은 참조 [선택 버퍼링 사용 하 여](../../../connect/jdbc/using-adaptive-buffering.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setResponseBuffering 메서드 &#40; SQLServerDataSource &#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)   
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

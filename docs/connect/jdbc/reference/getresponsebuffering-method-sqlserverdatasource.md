---
title: getResponseBuffering 메서드(SQLServerDataSource) | Microsoft Docs
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
ms.openlocfilehash: 4b3e53579b8c95cce0585e9614152053f39cafa8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980428"
---
# <a name="getresponsebuffering-method-sqlserverdatasource"></a>getResponseBuffering 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체에 대한 응답 버퍼링 모드를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>Return Value  
 소문자 **full** 또는 **adaptive**가 들어 있는 **문자열**입니다.  
  
## <a name="remarks"></a>설명  
 **full** 값은 런타임에 서버의 전체 결과를 읽도록 지정합니다.  
  
 **adaptive** 값은 필요할 때 가능한 최소한의 데이터를 버퍼링하도록 지정합니다. **adaptive** 값은 기본 버퍼링 모드입니다.  
  
 응답 버퍼링 모드 사용에 대한 자세한 내용은 [적응 버퍼링 사용](../../../connect/jdbc/using-adaptive-buffering.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [setResponseBuffering 메서드(SQLServerDataSource)](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)   
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

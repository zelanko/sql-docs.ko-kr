---
title: "setResponseBuffering 메서드 (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: c9e43ff2-8117-4dca-982d-83c863d0c8e1
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 88cfa89a30461ba3013c7b227651d5d0292c77b2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setresponsebuffering-method-sqlserverdatasource"></a>setResponseBuffering 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  응답 버퍼링이 사용 하 여 만든 연결에 대 한 모드를 설정 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *value*  
  
 A **문자열** 버퍼링 및 스트리밍 모드가 들어 있는입니다. 유효한 모드는 다음과 같은 대/소문자 구분 문자열 중 하나일 수 있습니다: **전체** 또는 **적응**합니다.  
  
## <a name="remarks"></a>주의  
 **전체** 값 런타임 시 서버에서 전체 결과 읽도록 지정 합니다.  
  
 **적응** 값 필요할 때 최소 가능한 데이터를 버퍼링 하도록 지정 합니다. **적응** 값이 기본 버퍼링 모드입니다.  
  
 응답 버퍼링 모드를 사용 하는 방법에 대 한 자세한 내용은 참조 [선택 버퍼링 사용 하 여](../../../connect/jdbc/using-adaptive-buffering.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
